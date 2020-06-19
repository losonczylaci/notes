# async

\[TOC\]

## Stephen Cleary

[Msdn blog](https://msdn.microsoft.com/hu-hu/magazine/mt149362?author=stephen+cleary)

### Async/Await

* Always use `Task` or `Task<T` as return type for async methods 
* only exception the **event handlers**

**Exception handling**

* in case of `Task` or `Task<T>` return type the exception is captured by the the Task object
* in case of `async void` function the exception will be raised in the `Synchronization Context` where the particular function has been called

  _example:_

```text
  async void ThrowExceptionAsync() {
      throw new InvalidOperationException();
  }
  void AsyncVoidException_CannotBeCaughtByCatch() {
      try {
          ThrowExceptionAsync();
      } catch {
          throw; //the exception is never caught here
      }
  }
```

These exception can be observed by `AppDomain.UnhandledException` but using this is not recommended for regular exception handling

```text
private async void button1_Click(object sender, EventArgs e) {
  await Button1ClickAsync();
}
public async Task Button1ClickAsync() {
  await Task.Delay(1000); // Do asynchronous work.
}
```

**!** It is a good practice to minimize the code into a function in the event handler. This way the event can be unit-tested

_"To summarize this first guideline, you should prefer async Task to async void. Async Task methods enable easier error-handling, composability and testability. The exception to this guideline is asynchronous event handlers, which must return void. This exception includes methods that are logically event handlers even if they’re not literally event handlers \(for example, `ICommand.Execute` implementations\)."_

#### Async All the Way

* shouldn't mix sync and async program without considering the consequences
* in particular, avoid calling`.Result` or `.Await()` because it could case deadlock really easily in GUI applications

```text
public static class DeadlockDemo {
  private static async Task DelayAsync() {
    await Task.Delay(1000);
  }
  // This method causes a deadlock when called in a GUI or ASP.NET context.
  public static void Test()  {
    var delayTask = DelayAsync(); // Start the delay.
    delayTask.Wait(); // Wait for the delay to complete.
  }
}
```

> above example work fine in a Console deadlocks in case of call from GUI

**Explanation:**

* async function is called
* `.Wait()` blocks the code and tries to wait until async is finished \(it is in use\)
* after async function is finished it tries to return to the calling context \(GUI context - _SynchronizationContext_ \), but it is already blocked

**Exception handling**

* every task stores a list of exceptions
* in case async code in synchronously blocked in the try catch the thrown exception will be wrapped in an `AggregateException`

**Non-fully async function**

```text
public static async Task TestNotFullyAsync() {
    await Task.Yield();
    Thread.Sleep(5000);
}
```

> above function will start the execution asynchronously, but once it is done it will continue with the remaining code and it will block current thread/context

**Summary**

| To Do This … | Instead of This … | Use This |
| :--- | :--- | :--- |
| Retrieve the result of a background task | Task.Wait or Task.Result | await |
| Wait for any task to complete | Task.WaitAny | await Task.WhenAny |
| Retrieve the results of multiple tasks | Task.WaitAll | await Task.WhenAll |
| Wait a period of time | Thread.Sleep | await Task.Delay |

#### Configure Context

```text
await Task.Delay(1000).ConfigureAwait(continueOnCapturedContext: false);
//or
await Task.Delay(1000).ConfigureAwait(false);
```

> enables a small amount of parallelism, meaning the started task not necessarily should return to the caller thread/context.

* **Performance improvement**
* Aside performance, it can **avoid deadlocks**. -&gt; this technique could help to gradually convert to your synchronous program to async
* **but, do not use** if GUI manipulation take place after awaited function

  for example

```text
private async void button1_Click(object sender, EventArgs e) {
  button1.Enabled = false;
  try {
    await Task.Delay(1000); // Can't use ConfigureAwait here ...
  }
  finally {

    button1.Enabled = true; // Because we need the context here.
  }
}
```

* Each async function **has its own context**, so if an async method calls another one **their contexts are independent**

```text
private async Task HandleClickAsync() {
  await Task.Delay(1000).ConfigureAwait(false); // Can use ConfigureAwait here.
}

private async void button1_Click(object sender, EventArgs e) {
  btn1.Enabled = false;
  try {
    await HandleClickAsync(); // Can't use ConfigureAwait here.
  }
  finally {
    btn1.Enabled = true; // We are back on the original context for this method.
  }
}
```

==Still not clear== In case you can use `ConfigureContext` at some point it is recommended to use it after every `await` from that point.... If you can use ConfigureAwait at some point within a method, then I recommend you use it for every await in that method after that point. Recall that the context is captured only if an incomplete Task is awaited; if the Task is already complete, then the context isn’t captured. Some tasks might complete faster than expected in different hardware and network situations, and you need to graciously handle a returned task that completes before it’s awaited. Figure 6 shows a modified example.

```text
async Task MyMethodAsync()
{
    // Code here runs in the original context.
  await Task.FromResult(1); //original context
    // Code here runs in the original context.
  await Task.FromResult(1).ConfigureAwait(false);
    // Code here runs in the original context.
  int delay = (new Random()).Next(2); // Delay is either 0 or 1
  await Task.Delay(delay).ConfigureAwait(false);
    // Code here might or might not run in the original context.
    // The same is true when you await any Task
    // that might complete very quickly.
}
```

**Summary**

You should use `Configure­Await` when possible. Context-free code has better performance for GUI applications and is a useful technique for avoiding deadlocks when working with a partially async codebase. The exceptions to this guideline are methods that require the context.

#### Know your tools

| Problem | Solution |
| :--- | :--- |
| Create a task to execute code | `Task.Run` or `TaskFactory.StartNew` \(_not_ the Task constructor or Task.Start\) |
| Create a task wrapper for an operation or event | `TaskFactory.FromAsync` or `TaskCompletionSource<T>` |
| Support cancellation | `CancellationTokenSource` and `CancellationToken` |
| Report progress | `IProgress<T>` and `Progress<T>` |
| Handle streams of data | TPL Dataflow or Reactive Extensions |
| Synchronize access to a shared resource | SemaphoreSlim |
| Asynchronously initialize a resource | AsyncLazy |
| Async-ready producer/consumer structures | TPL Dataflow or AsyncCollection |

## Tim Corney

### Async/await

[Youtube](https://www.youtube.com/watch?v=2moh18sh5p4&t=1966s) C\# Async / Await - Make your app more responsive and faster with asynchronous programming

**An example application to download websites and showing the benefit of async programing \(and parallelism\)**

#### Turning sync code into async - \[13:12\]

* do not return `void` for async method - _except event handler_
* non-async method can be invoked asynchronously by creating a new a Task

```text
DataModel result = await Task.Run( () => DownloadWebsite("www.google.com"))
```

* in order to invoke a method in an async way we are allowed change event handler to an `async` function

#### Running tasks in parallel - \[23:54\]

at the moment of the appending new task to the list execution is started in the below example `Task.WhenAll()` method is waits for all the completion and continues the with the remaining code

```text
private async Task RunDownloadParallelAsync() {
  var websites = PrepData();
  var tasks = new List<Task<DataModel>>();
  foreach(string site in websites) {
    tasks.Add(Task.Run(() => DownloadWebsite(site)));
  }
  var results = await Task.WhenAll(tasks);
  foreach(var item in results) {
    Report(item);
  }
}
```

### Advanced Async

[Youtube](https://www.youtube.com/watch?v=ZTKGRJy5P2M&t=322s) - C\# Advanced Async - Getting progress reports, cancelling tasks, and more

**Continuning the first project by adding progress bar and cancellation token**

#### IProgress - \[13:09\]

* Just pass `IProgress<T>` as a parameter to the async function and call the `.Report(T value)`
* outside of the async method just create an `System.Progress<T>` instance and subscribe to its `ProgressChanged` event - in the event handler we can update the UI

#### Cancellation Token - \[26:00\]

* `CancellationTokenSource cts` is needed  to be defined globally
* `cts.Token` needs to be passed to the async method
* `cts.ThrowIfCancellationRequested()` in order to throw an exception in the called async methof
* the called async function needs to be wrapped by a `try - catch` block as essentiallly an exception will be thrown
* `cts.Cancell()` should be called -  maybe by a button click - to request the cancellation

#### Cancallation Token for parallel task \[36:00\]

* It seems cancellation cannot be implemented in case a conventional foreach is used for parallelism... **will see**
* RunDownloadParallelSync.... dude DUFAK?
* instead of foreach `Parallel.ForEach<T>( list, () => {})`

**Notice the difference!** 

Both async functions run parallel, but:

* in 1st case the all the sub-task must finish in order finish the execution
* in the 2nd if the very first task finishes it will allow us to do something else 

  _e.g. cancel tasks, report progress, check which task was finished first... etc._

![1543796546965](https://github.com/losonczylaci/notes/tree/d5f768b02e44a8b7691088d1d9a2649424dbafef/csharp/img/1543796546965.png)

![1543796509371](https://github.com/losonczylaci/notes/tree/d5f768b02e44a8b7691088d1d9a2649424dbafef/csharp/img/1543796509371.png)

## On .Net

[Youtube video](https://www.youtube.com/watch?v=My2gAv5Vrkk&t=497s) - Brandon Minnick - async/await best practices

### Async/Await

This is how compiled `async` and `await` code looks like:

![](https://github.com/losonczylaci/notes/tree/d5f768b02e44a8b7691088d1d9a2649424dbafef/csharp/img/compiledAsyncAwait1.png)

![](https://github.com/losonczylaci/notes/tree/d5f768b02e44a8b7691088d1d9a2649424dbafef/csharp/img/compiledAsyncAwait2.png)

* This is basically a state-machine implemented by `IAsyncStatemachine`.
* notice the try-catch blocks, exception within this class will be re-thrown for the caller

### Refactoring

#### Fire and forget in the constructor

problem:

```text
Task.Run(async () => await ExecuteRefreshCommand());
```

solution: executing `RefreshCommand` instead

#### .Wait\(\) in the RefreshCommand

If we want to run the async code synchronously we should use the `.GetAwaiter.GetResult` formula instead because in the case the thrown exception will be unwrapped.

#### Performance boost by .ConfigureAwait\(\)

In the example the RefershCommand does nothing in the UI thread after invoking the Command. By calling `ConfigureAwait(false)` basically tells the sw to do not switch back to the caller thread after finishing the async task, keep continue. **This trick saves time/effort needed by the context switch.**

#### Returning a Task instead

Returning `Task` instead of awaiting it sometimes could boost the performance as well, but be careful. If you return the task then you should handle the exception at the point it is awaited.

**If your function call is in a try-catch or using block you have to await your function at that point**

