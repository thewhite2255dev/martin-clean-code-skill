## Intention-Revealing Names
**When to use**: Naming any variable, function, class, or module
**How**: Choose names that answer why it exists, what it does, and how it is used
**Trade-offs**: Longer names take more space but save time in understanding; avoiding disinformation requires domain knowledge

## Small Functions
**When to use**: Writing any function
**How**: Keep functions under 20 lines, preferably much shorter; split when they grow beyond that
**Trade-offs**: More functions mean more jumping between definitions, but each function is easier to understand

## One Thing Functions
**When to use**: Designing or refactoring a function
**How**: Verify every statement is at the same abstraction level and directly related to the purpose; extract if you can make another meaningful function
**Trade-offs**: May create more functions, but each has a clear, single responsibility

## One Level of Abstraction per Function
**When to use**: Writing or reviewing a function
**How**: Ensure all statements in a function are at the same level of abstraction; mix high-level concepts with high-level concepts, low-level with low-level
**Trade-offs**: Requires careful thought about what constitutes a level of abstraction, but makes code much easier to follow

## Stepdown Rule
**When to use**: Organizing functions within a module or class
**How**: After reading the top-level function, each subsequent function should be encountered at decreasing levels of abstraction
**Trade-offs**: Requires thoughtful ordering, but creates a natural reading flow like a newspaper article

## Use Exceptions Rather Than Return Codes
**When to use**: Whenever you encounter an error condition
**How**: Throw exceptions instead of returning error codes; allows calling code to handle errors in one place
**Trade-offs**: Exceptions can have performance overhead, but they clean up error handling significantly

## Write Your Try-Catch-Finally Statement First
**When to use**: Writing code that could throw exceptions
**How**: Begin with try-catch-finally, then add the code that might fail in the try block
**Trade-offs**: Might feel unnatural at first, but leads to more robust error handling

## Use Unchecked Exceptions
**When to use**: When you want to avoid forcing callers to declare or catch exceptions
**How**: Use exceptions that inherit from RuntimeException rather than checked exceptions
**Trade-offs**: Callers might miss handling errors they should deal with, but reduces boilerplate

## Provide Context with Exceptions
**When to use**: When throwing or logging exceptions
**How**: Include enough information (operation being attempted, failed values) to determine the source and cause
**Trade-offs**: Makes exceptions more verbose, but invaluable for debugging

## Don't Return Null
**When to use**: Never—avoid returning null from methods
**How**: Throw exceptions or return special case objects instead
**Trade-offs**: Might require creating special case objects, but prevents NullPointerExceptions

## Don't Pass Null
**When to use**: Never—avoid passing null as a parameter
**How**: Validate inputs early and throw IllegalArgumentException for null parameters
**Trade-offs**: Requires upfront validation, but prevents confusing null-related bugs

## Separate Constructing a System from Using It
**When to use**: When designing any application or system
**How**: Move all construction logic (factories, dependency injection setup) to a separate Main or initializer
**Trade-offs**: Slightly more complex startup, but much cleaner separation of concerns

## Factories
**When to use**: When object creation is complex or involves conditionals
**How**: Use Abstract Factory or Factory Method patterns to create objects without specifying concrete classes
**Trade-offs**: Adds indirection, but encapsulates creation logic and allows flexibility

## Dependency Injection
**When to use**: When a class depends on other objects or services
**How**: Pass dependencies through constructors, setters, or interfaces; use a DI framework if needed
**Trade-offs**: Requires more upfront design, but creates loosely coupled, testable code

## Learning Tests
**When to use**: When integrating a new third-party package
**How**: Write tests that call the third-party code to understand its behavior and limitations
**Trade-offs**: Takes time to write tests, but protects you from changes in third-party code

## Using Code That Does Not Yet Exist
**When to use**: When we know what we want but don't want to be constrained by existing interfaces
**How**: Write code against the interface we wish we had, then write adapters to convert to third-party interfaces
**Trade-offs**: Requires writing adapter code, but protects your code from third-party changes

## Clean Boundaries
**When to use**: Whenever integrating external code
**How**: Use adapters, facades, or wrappers to translate between our ideal interface and the third-party implementation
**Trade-offs**: Adds some indirection, but keeps your code clean at the edges

## The Three Laws of TDD
**When to use**: When practicing Test-Driven Development
**How**: 1) No production code without a failing test, 2) No more test than enough to fail, 3) No more production code than enough to pass the one failing test
**Trade-offs**: Slows initial coding, but leads to better design and fewer defects

## Keeping Tests Clean
**When to use**: When writing or maintaining test code
**How**: Apply the same clean code principles to test code as to production code
**Trade-offs**: Requires discipline, but tests remain maintainable and valuable

## One Assert per Test
**When to use**: When writing individual test cases
**How**: Split tests that verify multiple things into separate tests
**Trade-offs**: Creates more test methods, but each test has a clear, singular purpose

## Single Concept per Test
**When to use**: When designing test cases
**How**: Ensure each test has a clear, singular purpose
**Trade-offs**: Requires thoughtful test design, but makes failures easy to diagnose

## F.I.R.S.T.
**When to use**: Evaluating unit tests
**How**: Ensure tests are Fast, Independent, Repeatable, Self-Validating, and Timely
**Trade-offs**: May require refactoring slow or dependent tests, but creates a valuable test suite

## Classes Should Be Small!
**When to use**: When designing or refactoring a class
**How**: If a class grows beyond a certain size, look for ways to split it
**Trade-offs**: Might create more classes, but each is easier to understand and maintain

## Single Responsibility Principle (SRP)
**When to use**: When designing or evaluating a class
**How**: Identify all the reasons a class might change; if there's more than one, consider splitting it
**Trade-offs**: Might create more classes, but each has a clear, single responsibility

## Cohesion
**When to use**: When evaluating class design
**How**: The higher the cohesion, the better; methods and variables should belong together
**Trade-offs**: Requires refactoring to increase cohesion, but results in more maintainable classes

## Organizing for Change
**When to use**: When designing systems that will evolve over time
**How**: Isolate areas likely to change from areas that should remain stable
**Trade-offs**: Requires upfront architectural thinking, but pays dividends when changes occur

## Isolating from Change
**When to use**: When anticipating changes in requirements or implementations
**How**: Depend on abstractions rather than concrete implementations
**Trade-offs**: Requires interfaces and abstraction skills, but protects code from volatility

## Simple Design Rule 1: Runs All the Tests
**When to use**: As the foundation of any design effort
**How**: Write tests first (TDD) and ensure all pass before considering design complete
**Trade-offs**: Requires writing tests first, but ensures design actually works

## Simple Design Rule 2: No Duplication
**When to use**: Throughout development and refactoring
**How**: Look for duplicated code, logic, structure, or thought and eliminate it
**Trade-offs**: Takes time to find and eliminate duplication, but reduces bugs and maintenance cost

## Simple Design Rule 3: Expressive
**When to use**: When naming variables, functions, classes, etc.
**How**: Choose names that clearly express intent and make code read like well-written prose
**Trade-offs**: Might require longer names, but code becomes self-documenting

## Simple Design Rule 4: Minimal Classes and Methods
**When to use**: When refactoring to eliminate duplication and increase expressiveness
**How**: After eliminating duplication and making code expressive, see if you can reduce class and method count
**Trade-offs**: Might require merging functionality, but results in simpler design

## Law of Demeter
**When to use**: When writing code that interacts with objects
**How**: Talk to friends, not strangers—only call methods on: the object itself, objects passed as parameters, objects you create, your direct component objects
**Trade-offs**: Might require writing wrapper methods, but reduces coupling and increases encapsulation

## Tell, Don't Ask
**When to use**: When interacting with objects
**How**: Instead of asking an object for data and then acting on it, tell the object what you want done
**Trade-offs**: Requires thinking about behavior rather than data, but leads to better encapsulation

## Data/Object Anti-Symmetry
**When to use**: When deciding whether to use an object or a data structure
**How**: Choose objects when you want to add new data types easily; choose data structures when you want to add new functions easily
**Trade-offs**: Requires understanding the trade-off, but leads to appropriate choices

## DTOs (Data Transfer Objects)
**When to use**: When you need to move data between different parts of an application
**How**: Use public variables with no encapsulation—these are pure data structures for transfer only
**Trade-offs**: Breaks encapsulation intentionally, but appropriate for data transfer layers

## Command Query Separation (CQS)
**When to use**: Designing functions or methods
**How**: Functions should either perform an action (command) or return data (query), but not both
**Trade-offs**: Might require splitting functions, but makes intent clearer and reduces side effects

## Error Handling Is One Thing
**When to use**: When writing functions that handle errors
**How**: Functions that handle errors should do nothing else—no logging, no recovery, just error handling
**Trade-offs**: Might require more functions, but each has a clear, single responsibility

## Special Case Pattern
**When to use**: When you have frequent special cases that could be handled with exceptions
**How**: Return objects that handle the special case transparently instead of throwing exceptions
**Trade-offs**: Requires creating special case objects, but makes normal flow cleaner

## Null Object Pattern
**When to use**: When you want to eliminate null checks
**How**: Use an object that does nothing but eliminates the need for null checks
**Trade-offs**: Requires creating null object classes, but simplifies calling code

## Factory Method Pattern
**When to use**: When a class can't anticipate the class of objects it must create
**How**: Define an interface for creating an object, but let subclasses decide which class to instantiate
**Trade-offs**: Creates subclassing dependency, but provides flexibility in object creation

## Abstract Factory Pattern
**When to use**: When creating families of related or dependent objects without specifying their concrete classes
**How**: Provide an interface for creating families of related objects without specifying their concrete classes
**Trade-offs**: More complex than Factory Method, but handles families of objects

## Adapter Pattern
**When to use**: When you need to use an existing class, but its interface doesn't match the one you need
**How**: Convert the interface of a class into another interface clients expect
**Trade-offs**: Adds indirection and complexity, but enables reuse of existing classes

## Facade Pattern
**When to use**: When you need to provide a simplified interface to a complex subsystem
**How**: Provide a unified interface to a set of interfaces in a subsystem
**Trade-offs**: Might hide flexibility, but simplifies usage of complex systems

## Proxy Pattern
**When to use**: When you need to provide a surrogate or placeholder for another object to control access to it
**How**: Provide a surrogate or placeholder for another object
**Trade-offs**: Adds indirection, but enables lazy loading, access control, logging, etc.

## Observer Pattern
**When to use**: When an object (subject) needs to notify other objects (observers) about changes in its state
**How**: Define a one-to-many dependency between objects
**Trade-offs**: Can lead to memory leaks if not managed properly, but enables loose coupling

## Strategy Pattern
**When to use**: When you need to define a family of algorithms, encapsulate each one, and make them interchangeable
**How**: Define a family of algorithms, encapsulate each one, and make them interchangeable
**Trade-offs**: Increases number of objects, but enables algorithm selection at runtime

## Template Method Pattern
**When to use**: When you need to define the skeleton of an algorithm in an operation, deferring some steps to subclasses
**How**: Define the skeleton of an algorithm in an operation, deferring some steps to subclasses
**Trade-offs**: Inverts control structure, but enables code reuse through inheritance