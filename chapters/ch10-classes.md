# Chapter 10: Classes

## Core Idea
Classes should be small, have a single responsibility, and be organized for change. The goal is to create classes that are easy to understand, modify, and maintain.

## Frameworks Introduced
- **Class Organization**: Start with public variables, then private variables, then public functions, then private functions
  - When to use: When organizing the contents of a class
  - How: Group similar concepts together and follow a logical order
- **Encapsulation**: Keep variables and utility functions private unless they need to be public
  - When to use: When designing class interfaces
  - How: Hide implementation details and expose only what is necessary
- **Classes Should Be Small!**: Classes should be smaller than small
  - When to use: When designing or refactoring a class
  - How: If a class grows beyond a certain size, look for ways to split it
- **The Single Responsibility Principle (SRP)**: A class should have one, and only one, reason to change
  - When to use: When designing or evaluating a class
  - How: Identify all the reasons a class might change; if there's more than one, consider splitting it
- **Cohesion**: Classes should have high cohesion—methods and variables should be closely related
  - When to use: When evaluating class design
  - How: The higher the cohesion, the better; methods and variables should belong together
- **Maintaining Cohesion Results in Many Small Classes**: Applying SRP and cohesion naturally leads to smaller, more focused classes
  - When to use: When refactoring large classes
  - How: Split classes along responsibility boundaries to increase cohesion
- **Organizing for Change**: Organize classes to minimize the impact of changes
  - When to use: When designing systems that will evolve over time
  - How: Isolate areas likely to change from areas that should remain stable
- **Isolating from Change**: Use interfaces and abstractions to protect code from changes
  - When to use: When anticipating changes in requirements or implementations
  - How: Depend on abstractions rather than concrete implementations

## Key Concepts
- **Class Organization**: The order and grouping of elements within a class
- **Encapsulation**: Hiding internal details and exposing only necessary interfaces
- **Single Responsibility Principle**: One reason to change per class
- **Cohesion**: How closely related the responsibilities of a class are
- **Change Isolation**: Protecting stable code from volatile code
- **Interfaces**: Contracts that define what a class does without specifying how
- **Abstraction**: Hiding complexity behind simple interfaces

## Mental Models
- Think of classes as tools in a toolbox—each should be designed for a specific job
- Think of SRP as giving each class a single job description
- Think of cohesion as how well the tools in a toolbox belong together
- Think of change isolation as building firewalls between different parts of a system
- Think of interfaces as electrical outlets—you don't need to know how the power works, just what plug fits

## Anti-patterns
- **God Classes**: Classes that know too much or do too much
- **Low Cohesion**: Classes with unrelated responsibilities stuffed together
- **Violating SRP**: Classes that have multiple reasons to change
- **Poor Encapsulation**: Exposing internal details that should be hidden
- **Random Organization**: No logical order to class contents
- **Tight Coupling**: Classes that are too dependent on specific implementations
- **Fear of Small Classes**: Believing that many small classes are worse than few large ones

## Worked Example
The author shows how to improve a large, poorly organized class:
Before:
```java
public class SuperDashboard extends JFrame implements MetadataUser {
    public String lastAccessedProfile;
    public List<Subview> subviews = new ArrayList<>();
    public Color background = Color.LIGHT_GRAY;
    public boolean changed = false;
    public int numberOfOpenDirtyFiles = 0;
    // ... many more public variables
    public synchronized void setIsNew(boolean isNew) throws Exception {
        // ... complex method
    }
    // ... many more methods mixing concerns
}
```
After applying SRP and proper organization:
```java
public class SuperDashboard extends JFrame implements MetadataUser {
    // Public variables (if any)
    private String lastAccessedProfile;
    private List<Subview> subviews = new ArrayList<>();
    private Color background = Color.LIGHT_GRAY;
    private boolean changed = false;
    // ... other private variables
    
    // Public methods
    public synchronized void setIsNew(boolean isNew) throws Exception {
        // ... simplified method delegating to other objects
    }
    // ... other public methods
    
    // Private utility methods
    private void updateSubviews() {
        // ... private helper method
    }
    // ... other private methods
}
```
Then further splitting responsibilities into smaller classes like `MetadataUser`, `ChangeTracker`, `SubviewManager`, etc.

## Key Takeaways
1. Classes should be small—aim for fewer responsibilities, not fewer lines
2. Apply the Single Responsibility Principle—one reason to change per class
3. Strive for high cohesion—keep related responsibilities together
4. Organize class contents logically (variables first, then functions)
5. Encapsulate properly—hide implementation details
6. Design for change—isolate volatile code from stable code
7. Remember that maintaining cohesion naturally leads to many small classes
8. Use interfaces and abstractions to protect against changes

## Connects To
- **Ch 1**: Small, focused classes are part of writing clean code
- **Ch 2**: Classes with intention-revealing names are easier to understand
- **Ch 3**: Classes should contain small, focused functions
- **Ch 4**: Well-designed classes need fewer comments to be understood
- **Ch 5**: Properly formatted classes are more readable
- **Ch 6**: Classes should properly encapsulate data and objects
- **Ch 7**: Classes should handle errors cleanly and separately
- **Ch 8**: Class boundaries with third-party code should be protected
- **Ch 9**: Classes should be easily unit-testable
- **Ch 11**: Classes are the building blocks of larger systems