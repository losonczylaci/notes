[TOC]



# Stephen Cleary

[msd blog](https://msdn.microsoft.com/hu-hu/magazine/mt149362?author=stephen+cleary)

## Async/Await

* Always use `Task ` or `Task<T` as return type for async methods 
* only exception the **event handlers**

### Exception handling

* in case of  `Task` or `Task<T>` return type the exception is captured by the the Task object 

* in case of `async void` function the exception will be raised in the `Synchronization Context` where the particular function has been called

  *example:*

```c#
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



### Task completion  



# Tim Corney 

## Async/await

[Youtube](https://www.youtube.com/watch?v=2moh18sh5p4&t=1966s) C# Async / Await - Make your app more responsive and faster with asynchronous programming 

**An example application to download websites and showing the benefit of async programing (and parallelism)**

### Turning sync code into async - [13:12]

* do not return `void` for async method - *except event handler*
* non-async method can be invoked asynchronously by creating a new a Task

```c#
DataModel result = await Task.Run( () => DownloadWebsite("www.google.com"))
```

* in order to invoke a method in an async way we are allowed change event handler to an `async` function

### Running tasks in parallel - [23:54]

at the moment of the appending new task to the list execution is started in the below example
`Task.WhenAll()` method is waits for all the completion and continues the with the  remaining code

```c#
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

## Advanced Async
[Youtube](https://www.youtube.com/watch?v=ZTKGRJy5P2M&t=322s) - C# Advanced Async - Getting progress reports, cancelling tasks, and more

**Continuning the first project by adding progress bar and cancellation token**

### IProgress - [13:09]

* Just pass `IProgress<T>` as a parameter to the async function and call the `.Report(T value)`

* outside of the async method just create an `System.Progress<T>` instance and subscribe to its `ProgressChanged` event - in the event handler we can update the UI

### Cancellation Token - [26:00]
* `CancellationTokenSource cts` is needed  to be defined globally
* `cts.Token` needs to be passed to the async method
* `cts.ThrowIfCancellationRequested()` in order to throw an exception in the called async methof
* the called async function needs to be wrapped by a `try - catch` block as essentiallly an exception will be thrown
* `cts.Cancell()` should be called -  maybe by a button click - to request the cancellation

### Cancallation Token for parallel task [36:00]
* It seems cancellation cannot be implemented in case a conventional foreach is used for parallelism... **will see**
* RunDownloadParallelSync.... dude DUFAK?
* instead of foreach `Parallel.ForEach<T>( list, () => {})`



**Notice the difference! **

Both async functions run parallel, but:

* in 1st case the all the sub-task must finish in order finish the execution
* in the 2nd if the very first task finishes it will allow us to do something else 
  *e.g. cancel tasks, report progress, check which task was finished first... etc.*

![1543796546965](.\img\1543796546965.png)

![1543796509371](.\img\1543796509371.png)