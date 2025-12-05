## The Throwable Hierarchy
![[Throwable|500]]
## Exceptions
- Exceptions report **exceptional conditions** : unusual, strange, unexpected
- These conditions deserve exceptional treatment
### Some Methods Throw Exceptions
```java
public boolean addAll(int index, Colllection<? excends E> c)
```
> Inserts all of the elements in the specified collection into this list, starting at the specified position. 

***Throws***
- `IndexOutOfBoundsException` - if the index is out of range `(index < 0 || index > size())`
- `NullPointerException` - if the specified collection is `null`
### How to Deal with Exceptions
- To **throw an exception** : 
	- `throw new Throwable(message)`
 ```java
 if (age < 0) {
	 throw new IllegalArgumentException("Age cannot be negative");
 }
 ```
- To **catch an exception** and deal with it :
```java
	try {
		// statement that may throw an exception
	} catch (Throwable parrameter) {
		// statement that will be executed
		// instead of crashing the program
	}
```
- To  say a method isn't going to deal with exceptions (or may throw its own):
	- `accessModifier returnType methodName(parameters) throws Throwable { ... }`
```java
	public int readNumber(String path) throws IOException { ... }
```

### Why Use Exceptions
- Less programmer time spent on handling errors
- Cleaner program structure
	- Isolates exceptional situations rather than sprinkling them through the code.
- Separation of concerns
	- Pay local attention to the algorithm being implemented and global attention to errors that are raised.
### Cascading Catches
```java
try { ...  
} catch (ExSubA e) {  
	// We do this if an ExSubA is thrown.  
} catch (ExSup e) {  
	// We do this if any ExSup that is not an ExSubA is thrown.  
} catch (ExSubB e) {  
	// We never do this, even if an ExSubB is thrown.  
} finally {  
	// We always do this, even if no exception is thrown.  
} 
```
- `finally` clause is **always executed**, whether an exception was thrown or not, and whether or not the thrown exception was caught.
	- Example : Close open files as a clean-up step
### Useful Methods
- Constructors : `Throwable()`, `Throwable(String message)`

| Method              | What it returns                    | When to use                  |
| ------------------- | ---------------------------------- | ---------------------------- |
| `getMessage()`      | Only the message string            | Simple error message to user |
| `printStackTrace()` | Prints full stack trace to console | Debugging during development |
| `getStackTrace()`   | Array of stack trace elements      | Custom logging or processing |
### Checked vs. Unchecked Exceptions
**Checked Exceptions**
- A method **must** include `throws ExceptionClassName` in its declaration
- The compiler will check to make sure that the exception is caught by the method that calls it, or the method that calls that method, ...
- Examples : `IOException`, `SQLException`, `FileNotFoundException`
**Unchecked Exceptions**
- It is not required to declare or catch an exception
- Compiler does not force handing exceptions
- Represents the **programming errors**.
- Examples : `NullPointerException`, `ArrayIndexOutOfBoundsException`, all subclasses of `RuntimeException`
- They should be **fixed** in code, not "handled."

> You are not required to handle `RuntimeException` or `Error`.
- `RuntimeException` is *unchecked*, so the compiler does not force handling, but you _may_ handle it when appropriate.
- `Error` represents serious JVM failures and generally **should not** be handled at all.
### Extending Exceptions
```java
class MyException extends Exception {...}  

class MyClass {  
	public void m() throws MyException { ...  
		if (...) throw new MyException("oops!"); ...  
	}  
}  
```
- A method `m()` that throws your own exception `MyException`, a subclass of `Exception`.
```java
class MyClass {  
	public static class MyException extends Exception {...}  
	
	public void m() throws MyException { ...  
		if (...) throw new MyException("oops!"); ...  
	}  
}
```
- This is the alternative way of creating your own exception `MyException`.

