# Chapter 11: Systems

## Core Idea
A system is more than the sum of its parts. The architecture and design of a system should separate concerns, enable independence, and be testable and maintainable.

## Frameworks Introduced
- **Separate Constructing a System from Using It**: The startup process (construction) should be separate from the runtime logic
  - When to use: When designing any application or system
  - How: Move all construction logic (factories, dependency injection setup) to a separate Main or initializer
- **Factories**: Encapsulate object creation logic
  - When to use: When object creation is complex or involves conditionals
  - How: Use Abstract Factory or Factory Method patterns to create objects without specifying concrete classes
- **Dependency Injection**: Dependencies should be provided to a class rather than created by the class
  - When to use: When a class depends on other objects or services
  - How: Pass dependencies through constructors, setters, or interfaces; use a DI framework if needed
- **Scaling Up**: Systems should be designed to scale horizontally and vertically
  - When to use: When anticipating growth in users, data, or complexity
  - How: Separate cross-cutting concerns, use concurrency wisely, and design for partitioning
- **Cross-Cutting Concerns**: Aspects of a system that affect multiple modules (logging, security, transactions)
  - When to use: When you have concerns that cut across the natural divisions of your system
  - How: Use Aspect-Oriented Programming (AOP) or similar techniques to modularize these concerns
- **Java Proxies**: Dynamic proxies that implement interfaces and delegate to handlers
  - When to use: When you need to intercept method calls for logging, timing, or other concerns
  - How: Use java.lang.reflect.Proxy to create proxy instances at runtime
- **Pure Java AOP Frameworks**: Frameworks that provide AOP capabilities without special compilers
  - When to use: When you want AOP but cannot use AspectJ or need pure Java solutions
  - How: Use frameworks like Spring AOP or JBoss AOP
- **AspectJ Aspects**: A mature AOP language and compiler
  - When to use: When you need powerful AOP capabilities
  - How: Write aspects in AspectJ and compile with the AspectJ compiler
- **Test Drive the System Architecture**: Architecture should evolve through testing, not just upfront design
  - When to use: When designing or refactoring a system
  - How: Write tests that exercise architectural decisions and use them to guide design
- **Optimize Decision Making**: Good architecture supports rapid, informed decision-making
  - When to use: When making architectural choices
  - How: Ensure that architectural documents are clear, concise, and focused on trade-offs
- **Use Standards Wisely, When They Add Demonstratable Value**: Adopt standards only when they provide clear benefits
  - When to use: When considering industry or technology standards
  - How: Evaluate standards based on concrete benefits to your specific context, not just popularity
- **Systems Need Domain-Specific Languages**: DSLs can express domain concepts more clearly than general-purpose code
  - When to use: When you have repetitive patterns or complex domain logic
  - How: Create small, focused languages that solve specific problems in your domain

## Key Concepts
- **Separation of Main**: Distinguishing system startup (construction) from runtime logic
- **Factories**: Objects that create other objects
- **Dependency Injection (DI)**: Providing dependencies from outside
- **Inversion of Control (IoC)**: A principle where control flow is inverted compared to traditional procedural programming
- **Cross-Cutting Concerns**: Concerns that affect multiple modules (logging, security, etc.)
- **Aspect-Oriented Programming (AOP)**: Separating cross-cutting concerns from main business logic
- **Proxies**: Objects that act as intermediaries for other objects
- **Domain-Specific Languages (DSLs)**: Languages tailored to a specific application domain
- **Test-Driven Architecture**: Using tests to guide and validate architectural decisions

## Mental Models
- Think of a system like a city: construction (building factories, power plants) is separate from using it (driving cars, living in houses)
- Think of factories as real-world factories that produce products on demand
- Think of dependency injection as getting your tools provided to you rather than having to make or find them yourself
- Think of cross-cutting concerns like utilities (electricity, water) that run throughout a building
- Think of AOP as hiring specialists to handle utilities so builders can focus on the building itself
- Think of proxies as representatives or agents who act on your behalf
- Think of DSLs as specialized jargon that makes communication more efficient in a specific field

## Anti-patterns
- **Mixing construction and use**: Doing complex setup in the middle of application logic
- **Manual dependency management**: Having classes create their own dependencies with `new` statements
- **Ignoring cross-cutting concerns**: Letting logging, security, etc. scatter throughout the codebase
- **Overusing AOP**: Using aspects for things that could be simpler solutions
- **Ignoring scalability**: Building systems that work for small loads but fail under growth
- **Adopting standards blindly**: Using standards just because they're popular, not because they help
- **Over-engineering DSLs**: Creating complex languages for simple problems
- **Not testing architecture**: Assuming architectural decisions are correct without validation

## Worked Example
The author shows how to improve a system that mixes construction and use:
Before:
```java
public class Service {
    private Repository repository;
    
    public Service() {
        this.repository = new Repository(new DatabaseConnection("url", "user", "pass"));
    }
    
    public void serve() {
        // ... use repository
    }
}
```
After separating construction and using dependency injection:
```java
public interface Repository {
    void save(Object obj);
    Object find(Long id);
}

public class Service {
    private Repository repository;
    
    public Service(Repository repository) {
        this.repository = repository;
    }
    
    public void serve() {
        // ... use repository
    }
}
// Construction happens elsewhere (in Main or a factory)
public class Main {
    public static void main(String[] args) {
        Repository repository = new Repository(
                new DatabaseConnection("url", "user", "pass"));
        Service service = new Service(repository);
        service.serve();
    }
}
```
Then further improving by using a DI framework or factory to manage the construction of complex object graphs.

## Key Takeaways
1. Separate system construction (startup) from system use (runtime logic)
2. Use factories to encapsulate complex object creation
3. Apply dependency injection to decouple classes from their dependencies
4. Address cross-cutting concerns with AOP or similar techniques
5. Design systems to scale from the beginning
6. Test-drive your system architecture to validate decisions
7. Use standards only when they provide demonstrable value
8. Consider domain-specific languages for repetitive domain patterns
9. Remember that good architecture supports change and decision-making

## Connects To
- **Ch 1**: Good systems are built from clean code principles
- **Ch 3**: Functions within systems should be small and focused
- **Ch 5**: Proper formatting makes system code readable
- **Ch 6**: Objects in systems should properly encapsulate data
- **Ch 7**: Error handling in systems should be clean and separate
- **Ch 8**: System boundaries with third-party code should be protected
- **Ch 9**: Systems should be easily unit-testable
- **Ch 10**: Classes in systems should follow SRP and have high cohesion
- **Ch 12**: Emergent design principles apply to system architecture
- **Ch 13**: Concurrency considerations are part of scaling systems
- **Ch 14**: Successive refinement applies to evolving systems
- **Ch 15**: Understanding frameworks helps in using them properly
- **Ch 16**: Refactoring techniques apply to system code
- **Ch 17**: Heuristics and smells guide system improvements