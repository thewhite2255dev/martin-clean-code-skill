# Chapter 7: Error Handling

## Core Idea
Error handling is important, but if it obscures logic, it's wrong. The goal is to write error handling code that is clean, readable, and maintains the flow of the main program logic.

## Frameworks Introduced
- **Use Exceptions Rather Than Return Codes**: Exceptions clean up error handling by separating error detection from error handling
  - When to use: Whenever you encounter an error condition
  - How: Throw exceptions instead of returning error codes; this allows the calling code to handle errors in one place
- **Write Your Try-Catch-Finally Statement First**: Start with the structure for handling errors, then fill in the try block
  - When to use: When writing code that could throw exceptions
  - How: Begin with try-catch-finally, then add the code that might fail in the try block
- **Use Unchecked Exceptions**: Prefer runtime exceptions over checked exceptions when possible
  - When to use: When you want to avoid forcing callers to declare or catch exceptions
  - How: Use exceptions that inherit from RuntimeException rather than checked exceptions
- **Provide Context with Exceptions**: Include relevant information in exceptions to help diagnose problems
  - When to use: When throwing or logging exceptions
  - How: Include enough information (like operation being attempted, failed values) to determine the source and cause
- **Define Exception Classes in Terms of a Caller's Needs**: Create specific exception types that help callers respond appropriately
  - When to use: When different error conditions require different responses
  - How: Create specific exception types like `NoSuchAccountException` rather than generic ones
- **Define the Normal Flow**: Use patterns like Special Case Pattern or Null Object to reduce exception handling
  - When to use: When you have frequent special cases that could be handled with exceptions
  - How: Return objects that handle the special case transparently instead of throwing exceptions
- **Don't Return Null**: Returning null creates work for callers and leads to NullPointerExceptions
  - When to use: Never—avoid returning null from methods
  - How: Throw exceptions or return special case objects instead
- **Don't Pass Null**: Passing null is often a mistake that leads to confusion
  - When to use: Never—avoid passing null as a parameter
  - How: Validate inputs early and throw IllegalArgumentException for null parameters

## Key Concepts
- **Checked vs Unchecked Exceptions**: Checked exceptions must be declared/caught; unchecked (runtime) exceptions don't
- **Exception Context**: Information that helps diagnose why an exception occurred
- **Special Case Pattern**: Returning objects that handle special cases instead of throwing exceptions
- **Null Object**: An object that does nothing but eliminates null checks
- **Dependency Injection**: Passing dependencies rather than having objects create them (mentioned in Dependency Magnet)
- **Error.java Dependency Magnet**: A class that accumulates error handling dependencies and should be avoided

## Mental Models
- Think of exceptions as a way to separate error detection (where something goes wrong) from error handling (how to respond)
- Think of try-catch-finally as setting up safety nets before doing dangerous work
- Think of unchecked exceptions as allowing errors to propagate until someone wants to handle them
- Think of null as a landmine that explodes when touched—better to avoid it entirely
- Think of special case objects as polite ways to say "this doesn't apply here" instead of throwing an error

## Anti-patterns
- **Using return codes**: Clutters interfaces and forces callers to check for errors immediately
- **Ignoring exceptions**: Swallowing exceptions without logging or handling them
- **Throwing generic exceptions**: Losing specific information about what went wrong
- **Returning null**: Creating work for callers and leading to NullPointerExceptions
- **Passing null**: Creating confusion and potential runtime errors
- **Overusing checked exceptions**: Forcing callers to deal with exceptions they can't recover from
- **Creating dependency magnets**: Classes that accumulate error handling concerns
- **Losing context**: Throwing exceptions without enough information to diagnose problems

## Worked Example
The author shows how to improve error handling:
Before:
```java
public class DeviceController {
    public void sendShutDown() {
        try {
            tryToShutDown();
        } catch (DeviceShutDownError e) {
            logger.log(e);
        } catch (DeviceManagerError e) {
            logger.log(e);
        }
    }
}
```
After:
```java
public class DeviceController {
    private DeviceShutDownListener listener;
    
    public void sendShutDown() {
        try {
            tryToShutDown();
        } catch (DeviceShutDownError e) {
            listener.handleShutDownError(e);
        }
    }
}
```
Then further improving by separating concerns:
```java
public interface DeviceShutDownListener {
    void handleShutDownError(Exception e);
}

public class DeviceController {
    private DeviceShutDownListener listener;
    
    public void sendShutDown() {
        try {
            tryToShutDown();
        } catch (DeviceShutDownError e) {
            listener.handleShutDownError(e);
        }
    }
}
```

## Key Takeaways
1. Use exceptions rather than return codes for cleaner error handling
2. Start with try-catch-finally when writing code that could fail
3. Prefer unchecked exceptions when you don't need to force callers to handle them
4. Always provide context in exceptions to help with debugging
5. Define specific exception types that help callers respond appropriately
6. Avoid returning null—throw exceptions or use special case patterns instead
7. Avoid passing null—validate inputs early
8. Don't let error handling obscure the main logic—keep it separate
9. Use dependency injection to avoid creating dependency magnets like Error.java

## Connects To
- **Ch 1**: Proper error handling is part of writing clean, professional code
- **Ch 3**: Functions that handle errors should do one thing (handle errors)
- **Ch 6**: Objects should encapsulate error handling concerns properly
- **Ch 8**: Boundaries between layers often involve translating exceptions appropriately