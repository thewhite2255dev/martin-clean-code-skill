# Chapter 6: Objects and Data Structures

## Core Idea
Objects hide their data behind abstractions and expose functions that operate on that data. Data structures expose their data and have no meaningful functions. The choice between them depends on whether you want to easily add new data types or new functions.

## Frameworks Introduced
- **Data Abstraction**: Hide implementation details behind clean interfaces
  - When to use: When you want to allow implementation changes without affecting users
  - How: Expose only what is necessary through well-chosen functions that manipulate internal data
- **Data/Object Anti-Symmetry**: Objects hide data and expose functions; data structures expose data and have no significant functions
  - When to use: When deciding whether to use an object or a data structure
  - How: Choose objects when you want to add new data types easily; choose data structures when you want to add new functions easily
- **The Law of Demeter**: A module should not know about the innards of the objects it manipulates
  - When to use: When writing code that interacts with objects
  - How: Talk to friends, not strangers—only call methods on:
    - The object itself
    - Objects passed as parameters
    - Objects you create
    - Your direct component objects
- **Train Wrecks**: Chains of method calls like `getObj().getThing().getData()` that violate the Law of Demeter
  - When to use: Never—these indicate poor encapsulation
  - How: Break the chain by telling the object what you want instead of asking for its internals
- **Hybrids**: Structures that mix object and data structure characteristics, leading to the worst of both worlds
  - When to use: Never—these create confusing interfaces
  - How: Choose either pure objects or pure data structures, not both
- **Hiding Structure**: Objects should not expose their internal structure through getters/setters
  - When to use: When designing object interfaces
  - How: Avoid getters and setters that expose internal data; instead, provide meaningful operations
- **Data Transfer Objects (DTOs)**: Simple structures used to transfer data between layers or systems
  - When to use: When you need to move data between different parts of an application
  - How: Use public variables with no encapsulation—these are pure data structures for transfer only
- **Active Record**: A special form of DTO that includes navigation methods like save and find
  - When to use: When you need a data structure with database awareness
  - How: Mixes data transfer with database operations—use with caution as it can create hybrids

## Key Concepts
- **Data Abstraction**: Exposing operations on data while hiding the data itself
- **Data Structure**: A container for data with minimal or no behavior
- **Object**: An entity that encapsulates data and provides methods to operate on that data
- **Law of Demeter**: Principle of least knowledge—don't talk to strangers
- **Train Wrecks**: Method chains that violate encapsulation principles
- **Hybrids**: Confusing mixtures of objects and data structures
- **DTOs**: Pure data structures for transferring data between layers
- **Active Record**: Data structures with persistence methods

## Mental Models
- Think of objects as capsules—you interact with them through their exposed surface, not their interior
- Think of data structures as containers—you can see and access everything inside directly
- Think of the Law of Demeter as only talking to your immediate friends, not friends of friends
- Think of train wrecks as asking someone for their friend's friend's address instead of asking them to deliver a message

## Anti-patterns
- **Exposing data through getters/setters**: Violates encapsulation by exposing internal structure
- **Train wrecks**: Long chains of method calls like `customer.getAddress().getStreet().getNumber()`
- **Hybrid structures**: Trying to be both an object and a data structure
- **Inappropriate use of DTOs**: Using them when real objects with behavior would be better
- **Active Record abuse**: Making every data structure an active record, leading to complexity
- **Violating data/object anti-symmetry**: Not choosing clearly between the two approaches

## Worked Example
The author shows how to improve a poorly designed object:
Before:
```java
public class Point {
    public double x;
    public double y;
    
    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
}
```
After applying proper encapsulation:
```java
public class Point {
    private double x;
    private double y;
    
    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double getX() { return x; }
    public double getY() { return y; }
    public void setX(double x) { this.x = x; }
    public void setY(double y) { this.y = y; }
    
    public double distanceTo(Point other) {
        return Math.sqrt(Math.pow(other.x - x, 2) + Math.pow(other.y - y, 2));
    }
}
```
Then further improving by removing getters/setters and focusing on behavior:
```java
public class Point {
    private final double x;
    private final double y;
    
    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double distanceFrom(Point other) {
        return Math.sqrt(Math.pow(other.x - x, 2) + Math.pow(other.y - y, 2));
    }
}
```

## Key Takeaways
1. Choose objects when you want to add new data types easily; choose data structures when you want to add new functions easily
2. Respect the Law of Demeter—don't talk to strangers
3. Avoid train wrecks by telling objects what you want instead of asking for their internals
4. Stay away from hybrids—choose either pure objects or pure data structures
5. Use DTOs purely for data transfer between layers, never for encapsulation
6. Hide data structure details behind meaningful object interfaces
7. Prefer immutability when possible—it simplifies reasoning about objects
8. Focus on what objects do, not what they contain

## Connects To
- **Ch 1**: Proper encapsulation is part of writing clean code
- **Ch 3**: Functions that operate on objects should be small and focused
- **Ch 7**: Proper error handling is part of good object design
- **Ch 8**: Boundaries between layers often involve DTOs for data transfer