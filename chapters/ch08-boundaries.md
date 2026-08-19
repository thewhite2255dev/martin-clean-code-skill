# Chapter 8: Boundaries

## Core Idea
When we use third-party code, we want to protect our investment in our code from changes in that third-party code. We want to call third-party code in a way that doesn't force us to change large amounts of our code when they change theirs.

## Frameworks Introduced
- **Using Third-Party Code**: Protect our code from changes in third-party packages
  - When to use: Integrating external libraries or frameworks
  - How: Learn the third-party code, but don't let it invade our codebase; use our own interfaces or adapters
- **Exploring and Learning Boundaries**: Write tests to explore and learn third-party code
  - When to use: When integrating a new third-party package
  - How: Write tests that call the third-party code to understand its behavior and limitations
- **Learning Tests Are Better Than Free**: Learning tests are an investment that pays dividends
  - When to use: When learning or integrating third-party code
  - How: Write tests that verify your understanding of the third-party code; these tests protect you from changes
- **Using Code That Does Not Yet Exist**: Define our ideal interface before implementing or using third-party code
  - When to use: When we know what we want but don't want to be constrained by existing interfaces
  - How: Write code against the interface we wish we had, then write adapters to convert to third-party interfaces
- **Clean Boundaries**: Keep our code clean at the edges where it interacts with third-party code
  - When to use: Whenever integrating external code
  - How: Use adapters, facades, or wrappers to translate between our ideal interface and the third-party implementation

## Key Concepts
- **Third-Party Code**: External libraries or frameworks we don't control
- **Learning Tests**: Tests we write to explore and understand third-party behavior
- **Adapter Pattern**: Converting one interface to another that clients expect
- **Facade Pattern**: Providing a simplified interface to a complex system
- **Dependency Injection**: Passing dependencies rather than having objects create them
- **Interface Segregation**: Creating small, focused interfaces rather than large, general ones

## Mental Models
- Think of third-party code as a foreign country—we want to visit and learn from it, but not immigrate
- Think of learning tests as an insurance policy against changes in third-party code
- Think of our ideal interface as the doorway to our code—we control what comes in and goes out
- Think of adapters as translators that allow two different systems to communicate

## Anti-patterns
- **Letting third-party code invade**: Using third-party classes directly throughout our codebase
- **Not writing learning tests**: Assuming we understand third-party code without verifying
- **Ignoring version updates**: Failing to prepare for changes in third-party packages
- **Creating tight coupling**: Making our code dependent on specific third-party implementations
- **Wasting time on poor wrappers**: Creating adapters that don't actually simplify or protect

## Worked Example
The author shows how to protect code from a third-party bounding box utility:
Before (direct use throughout code):
```java
public class Shape {
    public void draw() {
        Boundary boundingBox = Boundary.Geometry.create()
            .addPoint(0, 0)
            .addPoint(5, 5)
            .rectangle();
        // ... use boundingBox directly in drawing code
    }
}
```
After (using an adapter to protect our code):
```java
public interface Boundary {
    Point getUpperLeft();
    Point getLowerRight();
    // ... other methods we need
}

public class MapShape {
    private Shape shape;
    private Boundary boundary;
    
    public MapShape(Shape shape, Boundary boundary) {
        this.shape = shape;
        this.boundary = boundary;
    }
    
    public void draw() {
        // Use our clean Boundary interface
        Point ul = boundary.getUpperLeft();
        Point lr = boundary.getLowerRight();
        // ... drawing code using our interface
    }
}
// Adapter for third-party Boundary implementation
public class BoundaryAdapter implements Boundary {
    private thirdParty.Boundary realBoundary;
    
    public BoundaryAdapter(thirdParty.Boundary realBoundary) {
        this.realBoundary = realBoundary;
    }
    
    public Point getUpperLeft() {
        return new Point(realBoundary.getUpperLeftX(), realBoundary.getUpperLeftY());
    }
    
    public Point getLowerRight() {
        return new Point(realBoundary.getLowerRightX(), realBoundary.getLowerRightY());
    }
}
```

## Key Takeaways
1. Write learning tests to explore and understand third-party code
2. Keep our code clean at boundaries by using adapters or facades
3. Don't let third-party code invade our codebase—protect our investment
4. Define the interface we wish we had, then adapt to whatever we actually have
5. Learning tests are an investment that protects us from third-party changes
6. Use dependency injection to maintain flexibility at boundaries
7. Prefer small, focused interfaces over large, general ones
8. Remember that our code should control the boundary, not be controlled by it

## Connects To
- **Ch 1**: Clean boundaries are part of writing professional, maintainable code
- **Ch 3**: Functions at boundaries should be small and focused
- **Ch 5**: Proper formatting makes boundary code readable
- **Ch 6**: Objects at boundaries should properly encapsulate data
- **Ch 7**: Error handling at boundaries should be clean and separate
- **Ch 9**: Unit tests for third-party code should be learning tests
- **Ch 10**: Class design at boundaries should follow SOLID principles