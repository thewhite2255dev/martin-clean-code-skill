---
name: martin-clean-code
description: 'Knowledge base from "Clean Code: A Handbook of Agile Software Craftsmanship" by Robert C. Martin. Use when applying Martin''s frameworks for writing clean, professional code, studying agile software craftsmanship, or referencing its principles and practices.'
---

<!-- argument-hint: [topic, framework name, or chapter number] -->

# Clean Code: A Handbook of Agile Software Craftsmanship
**Author**: Robert C. Martin | **Pages**: ~450 | **Chapters**: 17 | **Generated**: 2026-08-19

## How to Use This Skill

- **Without arguments** — load core frameworks for reference
- **With a topic** — ask about `naming`, `functions`, `comments`, `formatting`, `objects`, `error handling`, `boundaries`, `testing`, `classes`, `systems`, `emergence`, `concurrency`, or another indexed topic; I find and read the relevant chapter
- **With chapter** — ask for `ch03`; I load that specific chapter
- **Browse** — ask "what chapters do you have?" to see the full index

When you ask about a topic not covered in Core Frameworks below, I will read
the relevant chapter file before answering.

---

## Core Frameworks & Mental Models

### The Boy Scout Rule
Leave the campground cleaner than you found it.
- **When to use**: Every time you check in code
- **How**: Make one small improvement each time—rename a variable for clarity, extract a small function, remove a comment, or simplify a complex expression

### The Primal Conundrum
Developers feel pressure to make messes to meet deadlines, but this actually slows them down.
- **When to use**: When feeling pressured to cut corners on code quality
- **How**: Remember that the only way to go fast is to keep code clean at all times—messy code slows you down instantly

### Intention-Revealing Names
Names should reveal intent, not just type or encoding.
- **When to use**: Naming any variable, function, class, or module
- **How**: Choose names that answer why it exists, what it does, and how it is used. If you need a comment to explain the name, it doesn't reveal its intent

### Small Functions
Functions should be barely larger than a few lines.
- **When to use**: When writing any function
- **How**: Keep functions under 20 lines, preferably much shorter; if a function grows beyond that, look for ways to split it

### Do One Thing
A function should do one thing, do it well, and do it only.
- **When to use**: When designing or refactoring a function
- **How**: Verify that every statement in the function is at the same level of abstraction and directly related to the stated purpose; if you can extract another function with a meaningful name, it's doing more than one thing

### One Level of Abstraction per Function
Statements within a function should all be at the same level of abstraction.
- **When to use**: When writing or reviewing a function
- **How**: Mixing levels of abstraction is confusing; ensure that all steps in a function are either all high-level concepts or all low-level details

### Stepdown Rule
Code should read like a top-down narrative, where each function leads to the next at a lower level of abstraction.
- **When to use**: When organizing functions within a module or class
- **How**: After reading the top-level function, each subsequent function should be encountered at decreasing levels of abstraction, like reading a newspaper article

### Use Exceptions Rather Than Return Codes
Exceptions clean up error handling by separating error detection from error handling.
- **When to use**: Whenever you encounter an error condition
- **How**: Throw exceptions instead of returning error codes; this allows the calling code to handle errors in one place

### Write Your Try-Catch-Finally Statement First
Start with the structure for handling errors, then fill in the try block.
- **When to use**: When writing code that could throw exceptions
- **How**: Begin with try-catch-finally, then add the code that might fail in the try block

### Law of Demeter
A module should not know about the innards of the objects it manipulates.
- **When to use**: When writing code that interacts with objects
- **How**: Talk to friends, not strangers—only call methods on: the object itself, objects passed as parameters, objects you create, your direct component objects

### Data/Object Anti-Symmetry
Objects hide data and expose functions; data structures expose data and have no significant functions.
- **When to use**: When deciding whether to use an object or a data structure
- **How**: Choose objects when you want to add new data types easily; choose data structures when you want to add new functions easily

### The Three Laws of TDD
1. You may not write production code until you have written a failing unit test.
2. You may not write more of a unit test than is sufficient to fail; and failing is not compiling.
3. You may not write more production code than is sufficient to pass the one failing unit test.
- **When to use**: When practicing Test-Driven Development
- **How**: Follow the red-green-refactor cycle strictly

### Classes Should Be Small!
Classes should be smaller than small.
- **When to use**: When designing or refactoring a class
- **How**: If a class grows beyond a certain size, look for ways to split it

### Single Responsibility Principle (SRP)
A class should have one, and only one, reason to change.
- **When to use**: When designing or evaluating a class
- **How**: Identify all the reasons a class might change; if there's more than one, consider splitting it

### Separate Constructing a System from Using It
Separate the startup process (construction) from the runtime logic.
- **When to use**: When designing any application or system
- **How**: Move all construction logic (factories, dependency injection setup) to a separate Main or initializer

### Dependency Injection
Dependencies should be provided to a class rather than created by the class.
- **When to use**: When a class depends on other objects or services
- **How**: Pass dependencies through constructors, setters, or interfaces; use a DI framework if needed

### Emergent Design
Design that emerges from practice rather than being fully specified upfront.
- **Core Principle**: Let the right design emerge from test-driven development and continuous improvement through the application of simple design rules
- **Simple Design Rules**:
  1. **Runs All the Tests**: The system must be testable and all tests must pass
  2. **No Duplication**: Eliminate duplication in all forms
  3. **Expressive**: Code should be clear and expressive
  4. **Minimal Classes and Methods**: Keep the number of classes and methods to a minimum

---

## Chapter Index

| # | Title | Key Frameworks |
|---|-------|----------------|
| [ch01](chapters/ch01-clean-code.md) | Clean Code | Boy Scout Rule, Primal Conundrum, Code-Sense, Care |
| [ch02](chapters/ch02-meaningful-names.md) | Meaningful Names | Intention-Revealing Names, Avoid Disinformation, Make Meaningful Distinctions, Use Searchable Names |
| [ch03](chapters/ch03-functions.md) | Functions | Small!, Do One Thing, One Level of Abstraction per Function, Stepdown Rule, Command Query Separation |
| [ch04](chapters/ch04-comments.md) | Comments | Good Comments, Bad Comments, Explanation of Intent, Clarification, Warning of Consequences |
| [ch05](chapters/ch05-formatting.md) | Formatting | Newspaper Metaphor, Vertical Openness, Vertical Density, Horizontal Formatting, Indentation, Dummy Scopes |
| [ch06](chapters/ch06-objects-data-structures.md) | Objects and Data Structures | Data Abstraction, Data/Object Anti-Symmetry, Law of Demeter, Train Wrecks, Hybrids, Data Transfer Objects, Active Record |
| [ch07](chapters/ch07-error-handling.md) | Error Handling | Use Exceptions, Write Try-Catch-Finally First, Unchecked Exceptions, Provide Context, Define Exception Classes, Don't Return/Pass Null |
| [ch08](chapters/ch08-boundaries.md) | Boundaries | Using Third-Party Code, Learning Tests, Using Code That Does Not Yet Exist, Clean Boundaries |
| [ch09](chapters/ch09-unit-tests.md) | Unit Tests | Three Laws of TDD, Keeping Tests Clean, Clean Tests, One Assert per Test, Single Concept per Test, F.I.R.S.T. |
| [ch10](chapters/ch10-classes.md) | Classes | Class Organization, Encapsulation, Classes Should Be Small!, Single Responsibility Principle, Cohesion, Organizing for Change |
| [ch11](chapters/ch11-systems.md) | Systems | Separate Constructing from Using, Factories, Dependency Injection, Dependency Injection, Scaling Up, Cross-Cutting Concerns, Java Proxies, AOP, AspectJ, Test Drive Architecture |
| [ch12](chapters/ch12-emergence.md) | Emergence | Emergent Design, Simple Design Rules (Tests Pass, No Duplication, Expressive, Minimal) |
| [ch13](chapters/ch13-concurrency.md) | Concurrency | Why Concurrency?, Myths, Challenges, Concurrency Defense Principles, Know Your Library/Execution Models, Beware Dependencies, Keep Synchronized Sections Small, Shut-Down Code, Testing Threaded Code |
| [ch14](chapters/ch14-successive-refinement.md) | Successive Refinement | *(Content extracted)* |
| [ch15](chapters/ch15-junit-internals.md) | JUnit Internals | *(Content extracted)* |
| [ch16](chapters/ch16-refactoring-serialdate.md) | Refactoring SerialDate | *(Content extracted)* |
| [ch17](chapters/ch17-smells-heuristics.md) | Smells and Heuristics | *(Content extracted)* |

## Topic Index

- **Abstraction** → ch6, ch10, ch11
- **Active Record** → ch6
- **Aspect-Oriented Programming (AOP)** → ch11
- **Boy Scout Rule** → ch1
- **Care** → ch1
- **Cohesion** → ch10
- **Command Query Separation** → ch3
- **Comments** → ch4
- **Concurrency** → ch13
- **Data Abstraction** → ch6
- **Data Structure** → ch6
- **Dependency Injection** → ch6, ch11
- **Encapsulation** → ch6, ch10
- **Emergent Design** → ch12
- **Error Handling** → ch7
- **Expressiveness** → ch12
- **Factory** → ch11
- **Formatting** → ch5
- **Functions** → ch3
- **Getters/Setters** → ch6
- **Heuristics** → ch17
- **Hungarian Notation** → ch2
- **Interfaces** → ch10, ch11
- **Law of Demeter** → ch6
- **Learning Tests** → ch8
- **Meaningful Names** → ch2
- **Minimal Classes and Methods** → ch12
- **Null Object** → ch7
- **Object** → ch6
- **One Assert per Test** → ch9
- **One Level of Abstraction per Function** → ch3
- **Output Arguments** → ch3, ch7
- **Primal Conundrum** → ch1
- **Refactoring** → ch12, ch16
- **Returns** → ch3, ch7
- **Single Responsibility Principle (SRP)** → ch10, ch12
- **Stepdown Rule** → ch3
- **Structured Programming** → ch3
- **Systems** → ch11
- **Test-Driven Development (TDD)** → ch9, ch12
- **Thread-Safe Collections** → ch13
- **Train Wrecks** → ch6
- **Variables** → ch2, ch3

## Supporting Files

- [glossary.md](glossary.md) — all key terms with definitions
- [patterns.md](patterns.md) — all techniques and design patterns
- [cheatsheet.md](cheatsheet.md) — quick reference tables and decision guides

---

## Scope & Limits

This skill covers the book content only. For hands-on implementation in your codebase,
combine with project-specific tools. For topics beyond this book, check related skills
or ask the agent directly.