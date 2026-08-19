# Chapter 4: Comments

## Core Idea
Comments are not a substitute for clean code. They are often a sign that the code itself needs improvement. The best comments are those that explain intent, clarify complex algorithms, or warn about consequences—not those that explain what the code does.

## Frameworks Introduced
- **Good Comments**: Comments that add value beyond what the code expresses
  - When to use: When the code itself cannot clearly express certain information
  - How: Use for legal comments, informative comments, explanation of intent, clarification, warnings of consequences, TODO comments, amplification, and Javadocs in public APIs
- **Bad Comments**: Comments that clutter code, mislead, or indicate poor code quality
  - When to use: Never—these indicate the code needs refactoring
  - How: Eliminate mumbling, redundant comments, misleading comments, mandated comments, journal comments, noise comments, scary noise, position markers, closing brace comments, attributions/bylines, commented-out code, HTML comments, nonlocal information, too much information, inobvious connections, function headers, and Javadocs in nonpublic code

## Key Concepts
- **Legal Comments**: Copyright notices, author information, etc.
- **Informative Comments**: Provide basic information about constants or complex algorithms
- **Explanation of Intent**: Explain why something is done, not what is done
- **Clarification**: Help readers understand obscure arguments or return values
- **Warning of Consequences**: Alert other programmers to potential problems
- **TODO Comments**: Mark things that need to be done (but should be temporary)
- **Amplification**: Emphasize the importance of something that might seem insignificant
- **Javadocs in Public APIs**: Documentation for public interfaces
- **Mumbling**: Incomplete thoughts or half-sentences in comments
- **Redundant Comments**: Comments that repeat what the code already says clearly
- **Misleading Comments**: Comments that lie or are outdated
- **Mandated Comments**: Comments required by foolish process rather than need
- **Journal Comments**: Logs of changes that should be in version control
- **Noise Comments**: Comments that add no value (like "// end of loop")
- **Scary Noise**: Comments with excessive punctuation or all caps
- **Commented-Out Code**: Dead code that clutters the file
- **Nonlocal Information**: Information not related to the code it's near
- **Too Much Information**: Historical details or personal anecdotes
- **Inobvious Connection**: Comments whose relationship to nearby code is unclear
- **Function Headers**: Comments that repeat function signature information
- **Position Markers**: Comments used to mark positions in code (use meaningful names instead)
- **Closing Brace Comments**: Comments that mark which function a brace belongs to (use proper indentation instead)

## Mental Models
- Think of comments as a necessary evil—use them sparingly and only when the code cannot express something clearly
- Think of each comment as a smell that indicates an opportunity to improve the code
- Think of the ideal state as code that is so clear it needs few or no comments

## Anti-patterns
- **Using comments to explain bad code**: Instead of writing clear code, using comments to explain what confusing code does
- **Commented-out code**: Leaving dead code in the file instead of deleting it
- **Redundant documentation**: Comments that repeat information already expressed in the code
- **Misleading comments**: Comments that are outdated or incorrect
- **Javadoc on non-public code**: Wasting effort documenting code that isn't part of the public API
- **Using comments as TODO lists**: Leaving temporary comments in the code permanently

## Worked Example
The author shows how to improve code that relies on comments:
Before:
```java
// Check if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && 
    (employee.age > 65))
```
After:
```java
if (employee.isEligibleForFullBenefits())
```
The improved version eliminates the need for a comment by extracting the logic into a well-named function that expresses intent.

## Key Takeaways
1. Comments are not a substitute for clean code—use them only when necessary
2. Good comments explain intent, clarify complex algorithms, or warn about consequences
3. Bad comments clutter code, mislead, or indicate poor code quality that needs refactoring
4. The goal is code so clear it needs few or no comments
5. When you feel compelled to write a comment, first try to refactor the code to make it self-explanatory
6. Delete commented-out code instead of leaving it in the file
7. Use version control systems for tracking changes instead of journal comments in code
8. Javadocs should only be used for public APIs, not internal code

## Connects To
- **Ch 1**: Comments should not be needed to explain what clean code does
- **Ch 2**: Intention-revealing names reduce the need for explanatory comments
- **Ch 3**: Small functions that do one thing are self-documenting
- **Ch 5**: Proper formatting makes code readable without excessive comments