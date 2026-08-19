# Chapter 9: Unit Tests

## Core Idea
Unit tests are code too, and they should be as clean, readable, and maintainable as production code. Clean tests follow specific principles that make them effective and valuable.

## Frameworks Introduced
- **The Three Laws of TDD**:
  1. You may not write production code until you have written a failing unit test.
  2. You may not write more of a unit test than is sufficient to fail; and failing is not compiling.
  3. You may not write more production code than is sufficient to pass the one failing unit test.
  - When to use: When practicing Test-Driven Development
  - How: Follow the red-green-refactor cycle strictly
- **Keeping Tests Clean**: Tests should be as clean as production code
  - When to use: When writing or maintaining test code
  - How: Apply the same clean code principles to test code as to production code
- **Clean Tests**: Tests that are readable, maintainable, and focused
  - When to use: When designing test suites
  - How: Use domain-specific testing language, avoid duplication, keep tests focused
- **One Assert per Test**: Each test should verify one concept or behavior
  - When to use: When writing individual test cases
  - How: Split tests that verify multiple things into separate tests
- **Single Concept per Test**: Each test should test exactly one thing
  - When to use: When designing test cases
  - How: Ensure each test has a clear, singular purpose
- **F.I.R.S.T.**: Principles for good unit tests
  - **Fast**: Tests should run quickly
  - **Independent**: Tests should not depend on each other
  - **Repeatable**: Tests should pass/fail consistently in any environment
  - **Self-Validating**: Tests should have a clear boolean output (pass/fail)
  - **Timely**: Tests should be written just before the production code

## Key Concepts
- **Tests Enable the -ilities**: Tests make code maintainable, extensible, and flexible
- **Domain-Specific Testing Language**: Using helper methods/functions to create expressive tests
- **A Dual Standard**: Different standards for production code vs. test code (but both should be clean)
- **F.I.R.S.T.**: Acronym for qualities of good unit tests
- **Behavior Verification**: Testing what code does, not how it does it
- **State Verification**: Testing the state of objects after operations

## Mental Models
- Think of tests as executable specifications that document how code should behave
- Think of the Three Laws as a disciplined approach to ensuring test coverage
- Think of clean tests as documentation that stays in sync with the code
- Think of F.I.R.S.T. as the qualities that make tests valuable over time

## Anti-patterns
- **Slow tests**: Tests that take too long to run, discouraging frequent execution
- **Interdependent tests**: Tests that rely on the state left by other tests
- **Non-repeatable tests**: Tests that pass or fail depending on external factors
- **Tests with unclear output**: Tests that require interpretation to determine pass/fail
- **Tests written after the fact**: Tests that don't guide design or catch issues early
- **Tests with multiple asserts**: Tests that verify multiple things, making failures hard to diagnose
- **Tests that test too much**: Tests that verify multiple behaviors or concepts
- **Duplication in test code**: Repeating the same setup or verification code across tests
- **Obscure test names**: Names that don't clearly indicate what is being tested

## Worked Example
The author shows how to improve a test:
Before:
```java
@Test
public void testPageCraetion() throws Exception {
    WikiPage root = addPage("root", PageData.makeEmpty());
    WikiPage pageOne = addPage("PageOne", root, PageData.makeEmpty());
    WikiPage pageTwo = addPage("PageTwo", root, PageData.makeEmpty());
    
    assertEquals(2, root.getChildren().size());
    assertTrue(root.hasChild("PageOne"));
    assertTrue(root.hasChild("PageTwo"));
}
```
After:
```java
@Test
public void rootPageHasTwoChildrenAfterAddingTwoPages() throws Exception {
    WikiPage root = makeRoot("root");
    WikiPagePageOne = makePage("PageOne");
    WikiPage pageTwo = makePage("PageTwo");
    
    addPageTo(root, pageOne);
    addPageTo(root, pageTwo);
    
    assertRootHasTwoChildren(root);
    assertRootHasChildNamed(root, "PageOne");
    assertRootHasChildNamed(root, "PageTwo");
}
```
With helper methods that create a domain-specific testing language.

## Key Takeaways
1. Follow the Three Laws of TDD rigorously
2. Keep test code as clean as production code
3. Write tests that are Fast, Independent, Repeatable, Self-Validating, and Timely (F.I.R.S.T.)
4. Each test should verify exactly one concept or behavior
5. Use domain-specific testing language to make tests expressive and readable
6. Tests should enable the -ilities (maintainability, extensibility, flexibility)
7. Write tests before production code to guide design
8. Treat test code with the same respect as production code

## Connects To
- **Ch 1**: Clean tests are part of writing professional, maintainable code
- **Ch 3**: Test functions should be small and focused
- **Ch 4**: Test code should not need excessive comments to be understood
- **Ch 5**: Proper formatting makes test code readable
- **Ch 6**: Test objects should properly encapsulate data
- **Ch 7**: Test error handling should be clean and separate
- **Ch 8**: Test boundaries with third-party code should be protected