# Chapter 3: Functions

## Core Idea
Functions should be small, do one thing, and do it well. They should have a single responsibility, be easy to read, and follow the stepdown rule where the code reads like a top-down narrative.

## Frameworks Introduced
- **Small!**: Functions should be barely larger than a few lines
  - When to use: When writing any function
  - How: Keep functions under 20 lines, preferably much shorter; if a function grows beyond that, look for ways to split it
- **Do One Thing**: A function should do one thing, do it well, and do it only
  - When to use: When designing or refactoring a function
  - How: Verify that every statement in the function is at the same level of abstraction and directly related to the stated purpose; if you can extract another function with a meaningful name, it's doing more than one thing
- **One Level of Abstraction per Function**: Statements within a function should all be at the same level of abstraction
  - When to use: When writing or reviewing a function
  - How: Mixing levels of abstraction is confusing; ensure that all steps in a function are either all high-level concepts or all low-level details
- **Stepdown Rule**: Code should read like a top-down narrative, where each function leads to the next at a lower level of abstraction
  - When to use: When organizing functions within a module or class
  - How: After reading the top-level function, each subsequent function should be encountered at decreasing levels of abstraction, like reading a newspaper article

## Key Concepts
- **Blocks and Indenting**: Proper indentation and block structure make code readable
- **Sections within Functions**: Logical groupings within a function that should be extracted into their own functions
- **Switch Statements**: Often indicate doing more than one thing; should be avoided or hidden behind abstractions
- **Function Arguments**: Ideally zero (niladic), then one (monadic), then two (dyadic); three (triadic) should be avoided where possible
- **Flag Arguments**: Boolean arguments that indicate the function does more than one thing
- **Output Arguments**: Arguments that are modified by the function; should be avoided as they are confusing
- **Command Query Separation**: Functions should either perform an action (command) or return data (query), but not both
- **Error Handling Is One Thing**: Functions that handle errors should do nothing else
- **Don't Repeat Yourself (DRY)**: Duplication is the primary enemy of clean code
- **Structured Programming**: The ability to break down complex problems into smaller, manageable pieces

## Mental Models
- Think of functions as paragraphs in an essay—each should cover one topic and lead naturally to the next
- Think of function arguments as inputs to a machine—the fewer the inputs, the simpler the machine
- Think of switching on a type as a smell that suggests polymorphism would be better
- Think of output arguments as confusing because they violate the usual input→output flow

## Anti-patterns
- **Functions that are too long**: Violate the small! principle and become difficult to understand
- **Functions that do multiple things**: Violate the "do one thing" principle and lead to confusion
- **Using flag arguments**: Indicates the function does more than one thing; should be split into separate functions
- **Using output arguments**: Confusing and unnatural; prefer returning multiple values or exceptions
- **Mixing levels of abstraction**: Makes code difficult to follow as readers must constantly shift mental gears
- **Ignoring the stepdown rule**: Code becomes difficult to read as it jumps between levels of abstraction

## Worked Example
The author shows how to improve a function that does multiple things:
Before:
```java
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
    if (isTestPage(pageData))
        return renderPageWithSetupsAndTeardowns(pageData, isSuite);
    else
        return renderPageWithSetupsAndTeardowns(pageData, false);
}
```
After extracting the duplicated logic and clarifying intent:
```java
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
    if (isTestPage(pageData))
        return renderTestPage(pageData);
    else
        return renderNonTestPage(pageData);
}
```
Then further extracting the common setup and teardown logic into separate functions.

## Key Takeaways
1. Functions should be small—aim for under 20 lines, preferably much shorter
2. Functions should do one thing—verify by checking if you can extract another function with a meaningful name
3. Keep all statements in a function at the same level of abstraction
4. Follow the stepdown rule—code should read like a top-down narrative
5. Prefer fewer arguments (niladic > monadic > dyadic > triadic); avoid flag and output arguments
6. Separate command from query functions—functions should either do something or answer something, not both
7. Error handling should be done in functions that do nothing else

## Connects To
- **Ch 1**: Functions that do one thing well embody the core idea of clean code
- **Ch 2**: Functions with intention-revealing names are easier to understand and use
- **Ch 4**: Comments should not be needed to explain what a function does if it's well-named and small
- **Ch 6**: Functions that operate on objects and data structures should be small and focused