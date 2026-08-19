# Chapter 12: Emergence

## Core Idea
Clean code emerges from applying simple design rules through disciplined refactoring, not from big upfront design. The goal is to let the right design emerge from test-driven development and continuous improvement.

## Frameworks Introduced
- **Simple Design Rule 1: Runs All the Tests**: The system must be testable and all tests must pass
  - When to use: As the foundation of any design effort
  - How: Write tests first (TDD) and ensure all pass before considering design complete
- **Simple Design Rule 2: No Duplication**: Eliminate duplication in all forms
  - When to use: Throughout development and refactoring
  - How: Look for duplicated code, logic, structure, or thought and eliminate it
- **Simple Design Rule 3: Expressive**: Code should be clear and expressive
  - When to use: When naming variables, functions, classes, etc.
  - How: Choose names that clearly express intent and make code read like well-written prose
- **Simple Design Rule 4: Minimal Classes and Methods**: Keep the number of classes and methods to a minimum
  - When to use: When refactoring to eliminate duplication and increase expressiveness
  - How: After eliminating duplication and making code expressive, see if you can reduce class and method count

## Key Concepts
- **Emergent Design**: Design that emerges from practice rather than being fully specified upfront
- **Test-Driven Development (TDD)**: Writing tests before production code to guide design
- **Refactoring**: Improving the design of existing code without changing its behavior
- **Duplication**: Repeated code, logic, structure, or thought that should be eliminated
- **Expressiveness**: Code that clearly communicates its intent
- **Minimalism**: Keeping the design as simple as possible while still being correct

## Mental Models
- Think of design as a sculpture that emerges from chipping away at a block of stone
- Think of tests as the scaffolding that supports and guides the emergence of design
- Think of duplication as waste that obscures the true design underneath
- Think of expressiveness as the clarity that allows others to understand and build upon your work
- Think of minimalism as Occam's Razor applied to code design

## Anti-patterns
- **Big Upfront Design (BUFD)**: Spending too much time designing before writing any code
- **Ignoring Tests**: Writing code without tests or letting tests fail
- **Tolerating Duplication**: Accepting duplicated code as inevitable or acceptable
- **Prioritizing Cleverness Over Clarity**: Writing code that is hard to understand but "smart"
- **Over-Designing**: Creating more classes or methods than necessary
- **Ignoring Expressiveness**: Focusing on mechanics rather than clarity of intent
- **Refactoring Without Tests**: Making changes without the safety net of tests

## Worked Example
The author shows how a design emerges through TDD and refactoring:
1. Start with a failing test for a simple requirement
2. Write the simplest code that could possibly pass
3. Refactor to eliminate duplication (e.g., extracting a common function)
4. Refactor to increase expressiveness (e.g., renaming for clarity)
5. Refactor to minimize classes and methods (e.g., combining related functionality)
6. Repeat with the next test, letting the design emerge incrementally

For example, when building a money conversion system:
- First test: 5 CHF * 2 = 10 CHF → simple multiplication function
- Second test: 10 EUR * 2 = 20 EUR → notice duplication in multiplication logic
- Refactor: Extract multiplication into a shared function
- Third test: 5 CHF + 5 CHF = 10 CHF → need addition function
- Fourth test: 5 CHF + 5 CHF = 10 CHF and 5 USD + 5 USD = 10 USD → notice duplication in addition logic
- Refactor: Extract addition into a shared function
- Fifth test: 5 CHF + 10 EUR = ? (needs conversion) → realize need for Currency class
- Continue refactoring to eliminate duplication and increase expressiveness
- Eventually emerge with a clean Money and Currency design that handles all cases

## Key Takeaways
1. Let design emerge from TDD and refactoring rather than trying to get it right upfront
2. Make sure all tests pass—this is the foundation of good design
3. Relentlessly eliminate duplication in all its forms
4. Strive for expressiveness—code should clearly communicate its intent
5. Continuously seek minimalism—reducing unnecessary classes and methods
6. Apply the simple design rules in order: tests pass → no duplication → expressive → minimal
7. Remember that emergent design requires discipline and practice
8. The best designs are simple, not complex

## Connects To
- **Ch 1**: Emergent design is how clean code actually gets written in practice
- **Ch 3**: Functions should emerge as small and focused through TDD/refactoring
- **Ch 4**: Comments should not be needed as expressive code emerges
- **Ch 5**: Formatting should support, not hinder, emergent design
- **Ch 7**: Error handling should emerge as clean and separate through TDD
- **Ch 9**: Unit tests are the foundation that enables emergent design
- **Ch 10**: Classes should emerge as small and focused with single responsibility
- **Ch 11**: System architecture should emerge through test-driven development
- **Ch 13**: Concurrency concerns should be addressed through test-driven emergence
- **Ch 14**: Successive refinement is how clean code emerges over time
- **Ch 15**: Understanding frameworks helps in using them properly in emergent design
- **Ch 16**: Refactoring techniques are essential for emergent design
- **Ch 17**: Heuristics and smells guide the emergence of clean code