# Clean Code Cheatsheet

## Decision Rules

### When to split a function
- If it does more than one thing (can extract another meaningful function)
- If it has more than 2-3 levels of indentation
- If it's longer than 20 lines (prefer much shorter)
- If it mixes levels of abstraction
- If it uses flag arguments

### When to split a class
- If it has more than one reason to change (SRP)
- If it's trying to do too many things
- If its methods don't share much data (low cohesion)
- If it has many unrelated instance variables
- If it's difficult to test due to too many dependencies

### When to use comments
- Legal notices (copyright, authorship)
- Informative comments about constants or algorithms
- Explanation of intent (why, not what)
- Clarification of obscure parameters or return values
- Warnings about consequences
- TODO items (temporary!)
- Amplification of importance
- Javadocs for public APIs

### When NOT to use comments
- To explain bad code (refactor instead)
- When the code is already clear
- Redundant information
- Misleading or outdated information
- Journal comments (use version control)
- Noise comments ("end of loop")
- Position markers (use meaningful names)
- Closing brace comments (use proper indentation)
- Attributions and bylines
- HTML comments
- Nonlocal information
- Too much historical detail
- Inobvious connections
- Function headers
- Javadocs on non-public code

### When to use exceptions vs return codes
- Always prefer exceptions for error conditions
- Exceptions separate error handling from normal flow
- Return codes clutter interfaces and force immediate handling
- Use unchecked exceptions when callers can't recover
- Use checked exceptions only when you want to force handling

### When to avoid null
- Never return null from methods
- Never pass null as a parameter
- Use special case objects or throw exceptions instead
- Null creates work for callers and leads to NullPointerExceptions

### When to apply the Law of Demeter
- When calling methods on objects returned from other method calls
- When you find yourself writing trains like `obj.getA().getB().getC()`
- When your code knows too much about object internals
- When you want to reduce coupling between classes

### When to use factories
- When object creation is complex
- When creation involves conditionals
- When you want to hide concrete classes
- When you need to create families of related objects

### When to use dependency injection
- When a class depends on other objects/services
- When you want to make code testable
- When dependencies might change
- When you want to decouple implementation from interface

### When to write learning tests
- When integrating third-party code
- When you want to understand behavior
- When you want protection from third-party changes
- When exploring unfamiliar APIs

### When to separate construction from use
- Always! Construction logic should be separate from runtime logic
- Move factory/DI setup to Main or initializer
- Makes runtime code cleaner and more focused

## Thresholds & Defaults

### Function Size
- Aim for: 4-7 lines (ideal)
- Acceptable: up to 20 lines
- Too long: over 20 lines (refactor)
- Extreme: over 50 lines (definitely split)

### Function Parameters
- Best: niladic (0 args)
- Good: monadic (1 arg)
- Acceptable: dyadic (2 args)
- Avoid: triadic (3 args) - justify why needed
- Never: polyadic (4+ args) - use argument objects

### Class Size
- Small: < 100 lines
- Medium: 100-200 lines
- Large: > 200 lines (consider splitting)
- Extreme: > 500 lines (definitely split)

### Indentation Levels
- Ideal: 1-2 levels
- Acceptable: 3 levels
- Warning: 4 levels
- Danger: 5+ levels (refactor immediately)

### Line Length
- Ideal: 80-120 characters
- Maximum: 150 characters
- Teams should agree on a standard and stick to it

### Comments Ratio
- Ideal: < 10% of lines
- Acceptable: 10-20%
- Warning: > 20% (indicates unclear code)
- Danger: > 30% (code needs serious refactoring)

### Test Coverage
- Unit tests: aim for 80%+ coverage
- Critical paths: 100% coverage
- Property-based testing for complex logic
- Mutation testing to test test quality

## Trade-off Matrices

### Naming Approaches
| Approach | Clarity | Length | Searchability | Pronunciation | Best For |
|----------|---------|--------|---------------|---------------|----------|
| Full descriptive | High | Long | Excellent | Good | Public APIs, complex domains |
| Domain abbreviations | Medium | Medium | Good | Good | Internal code, well-known domains |
| Single letters | Low | Short | Poor | Poor | Loop indices, mathematical formulas |
| Encoded (Hungarian) | Low/Med | Medium | Fair | Poor | Legacy systems only |
| Numbered (var1, var2) | Low | Short | Fair | Good | Never use |

### Error Handling Strategies
| Strategy | Safety | Clarity | Performance | Caller Burden | Best For |
|----------|--------|---------|-------------|---------------|----------|
| Exceptions | High | High | Medium | Low/High* | Most application code |
| Return Codes | Medium | Low | High | High | Systems programming, embedded |
| Null Returns | Low | Medium | High | Low | Rare cases, prefer Optional |
| Logging Only | Low | Low | Medium | None | Debugging, not production |
| Assertions | Med/Low | High | High | None | Internal invariants |

*Higher burden if unhandled interferes with business logic

### Coupling Reduction Techniques
| Technique | Encapsulation | Flexibility | Complexity | Performance | Best For |
|-----------|---------------|-------------|------------|-------------|----------|
| Interfaces | High | High | Low | Very Low | Public contracts, DI |
| Abstract Classes | Medium | Medium | Low | Low | Shared implementation |
| Inheritance Templates | Low | Low | Medium | Very Low | Framework extensions |
| Delegation/Composition | High | High | Medium | Very Low | Most cases |
| Global Variables | None | None | None | Very Low | Never use |
| Singletons | Low | Low | Low | Very Limited | Rare coordination cases |
| Service Locator | Medium | Medium | Low | Low | Legacy code migration |

### Collections & Data Structures
| Structure | Read Access | Insert/Delete | Search | Memory | Best For |
|-----------|-------------|---------------|--------|--------|----------|
| Array/List | O(1) | O(n) | O(n) | Low | Sequential access, small data |
| Linked List | O(n) | O(1)* | O(n) | Low | Frequent middle inserts/deletes |
| Hash Map | O(1) | O(1) | O(1) | Medium | Key-value lookups, caching |
| Tree Set/Map | O(log n) | O(log n) | O(log n) | Medium | Sorted data, ranges |
| Stack/Queue | Specific | O(1) | O(n) | Low | LIFO/FIFO processing |
| Concurrent Versions | Thread-safe | Thread-safe | Thread-safe | Higher | Multi-threaded scenarios |

*Actual insertion point matters for linked lists

## Tells & Smells

### Code Smells Requiring Immediate Attention
- **Long Functions**: >20 lines, especially with nested loops/conditionals
- **Large Classes**: >200 lines, especially with many instance variables
- **Primitive Obsession**: Using primitives for domain concepts (String for phone numbers)
- **Switch Statements**: Often indicate missing polymorphism
- **Temporary Fields**: Instance variables used only in certain conditions
- **Refused Bequest**: Subclasses not using inherited methods or fields
- **Alternative Classes with Different Interfaces**: Similar functionality, different method names
- **Data Clumps**: Same 3-4 variables always appearing together
- **Shotgun Surgery**: One change requiring edits in many classes
- **Feature Envy**: Method more interested in another class's data than its own
- **Inappropriate Intimacy**: Classes knowing too much about each other's internals
- **Message Chains**: Trains like `a.getB().getC().getD()`
- **Middle Man**: Classes that just delegate to another class
- **Insider Trading**: Classes accessing private members of others
- **Large Hierarchies**: Inheritance trees deeper than 5-6 levels
- **Speculative Generality**: Building features "just in case" they're needed
- **Comments**: Especially those explaining what the code does

### Test Smells
- **Slow Tests**: Tests taking >100ms to run
- **Interdependent Tests**: Tests that depend on order or state from others
- **Brittle Tests**: Tests breaking from unrelated changes
- **Tests with Magic Numbers**: Unexplained literals in assertions
- **Duplicate Test Code**: Same setup/verification copied across tests
- **Tests with Multiple Asserts**: Verifying more than one thing per test
- **Poor Test Names**: Not indicating what's being tested
- **Lack of Assertions**: Tests that don't actually verify anything
- **Overuse of Mocks**: Mocking everything instead of using real/fake objects
- **Conditional Test Logic**: If statements in tests

### Design Smells
- **Rigidity**: Changes affect too many other parts
- **Fragility**: Changes cause unexpected breakage
- **Immobility**: Hard to reuse in other contexts
- **Viscosity**: Easy ways are hard, hard ways are easy
- **Needless Complexity**: Over-engineered solutions
- **Needless Repetition**: Duplication that should be eliminated
- **Opacity**: Hard to understand what's happening
- **Silence**: Missing comments where they would help
- **Violation of Standard Conventions**: Not following team/project standards

## Quick Reference

### The Boy Scout Rule
"Leave the campground cleaner than you found it."
- Every check-in should improve the code
- One small improvement: rename, extract, simplify, clarify
- Cumulative effect prevents code rot

### The Primal Conundrum
"The only way to go fast is to keep the code clean at all times."
- Messy code slows you down immediately
- "Moving fast" by making messes is an illusion
- Professionalism means caring for your code

### Code-Sense
"The disciplined ability to recognize good vs. bad code and know how to transform bad code into clean code."
- Developed through practice and study
- Enables behavior-preserving transformations
- Essential for sustainable development

### Functions Should
- Be small (4-7 lines ideal)
- Do one thing only
- Have one level of abstraction
- Follow the stepdown rule
- Have descriptive, intention-revealing names
- Have few arguments (niladic > monadic > dyadic)
- Have no side effects (unless that's the purpose)
- Either be commands or queries, not both

### Classes Should
- Be small (aim for <100 lines)
- Have one reason to change (SRP)
- Have high cohesion (methods/data belong together)
- Be encapsulated (hide implementation details)
- Be organized for change (isolate volatile code)
- Have intention-revealing names
- Follow composition over inheritance where appropriate

### Comments Should
- Explain intent, not repeat code
- Clarify complex algorithms
- Warn about consequences
- Document public APIs
- Be maintained with the code (or removed)
- Never be used to explain bad code (refactor instead)

### Tests Should
- Be fast, independent, repeatable, self-validating, timely (F.I.R.S.T.)
- Test one concept per test
- Have one assert per test (usually)
- Be as clean as production code
- Be written before the code (TDD)
- Enable the -ilities (maintainability, flexibility, etc.)