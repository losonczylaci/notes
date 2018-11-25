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

