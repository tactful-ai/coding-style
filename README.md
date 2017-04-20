# TypeScript Coding Guidelines

## References
- Use `const` for all of your references; avoid using `var`.
  > This ensures that you can't reassign your references, which can lead to bugs and difficult to comprehend code.
  ```typescript
  // bad
  var a: number = 1;
  var b: number = 2;

  // good
  const a: number = 1;
  const b: number = 2;
  ```
- If you must reassign references, use let instead of var.
  > `let` is block-scoped rather than function-scoped like `var`.
  ```typescript
  // bad
  var count: number = 1;
  if (true) {
    count += 1;
  }

  // good, use the let.
  let count: number = 1;
  if (true) {
    count += 1;
  }
  ```

## Strings
- Use template literals ` `` ` for all strings.
  > This keeps things consistent and allows you use new lines and interpolation within the same format.
  ```typescript
  // bad
  const name: string = "Capt. Janeway";
  const name: string = 'Capt. Janeway';

  // good
  const name: string = `Capt. Janeway`;
  ```
- Never use `eval()` on a string, it opens too many vulnerabilities.

## Names
- Use PascalCase for type names.
- Do not use "I" as a prefix for interface names.
- Use PascalCase for enum values.
- Use camelCase for function names.
- Use camelCase for property names and local variables.
- Do not use "_" as a prefix for private properties.
- Use whole words in names when possible.

## Types
- Do not export types/functions unless you need to share it across multiple components.
- Do not introduce new types/values to the global namespace.
- Shared types should be defined in 'types.ts'.
- Within a file, type definitions should come first.

## null and undefined
- Use undefined, do not use null.

## General Assumptions
- Consider objects like Nodes, Symbols, etc. as immutable outside the component that created them. Do not change them.
- Consider arrays as immutable by default after creation.

## Classes
- For consistency, do not use classes in the core compiler pipeline. Use function closures instead.

## Flags
- More than 2 related Boolean properties on a type should be turned into a flag.

## Comments
- Use JSDoc style comments for functions, interfaces, enums, and classes.
  ```typescript
  /**
   * Log a message in red
   * @param text {string} - the text to log
   */
  export const error = (text: string) => {
      console.log();
      console.log(`  ${chalk['black']['bgRed']['bold'](' ! ')} ${chalk['red'](text)}`);
  };
  ```

## Strings
- Use backticks for strings, not just template literals.
  ```typescript
  `string text`

  `string text line 1
   string text line 2`

  `string text ${expression} string text`
  ```

## Style
- Use arrow functions over anonymous function expressions.
- Always surround arrow function parameters with parentheses. 
  - For example, `x => x + x` is wrong but the following are correct:
    ```typescript
    (x) => x + x
    (x,y) => x + y
    <T>(x: T, y: T) => x === y
    ```
- Always surround loop and conditional bodies with curly braces.
- Open curly braces always go on the same line as whatever necessitates them.
- Parenthesized constructs should have no surrounding whitespace.
- A single space follows commas, colons, and semicolons in those constructs. For example:
  ```typescript
  for (var i = 0, n = str.length; i < 10; i++) { }
  if (x < 10) { }
  function f(x: number, y: string): void { }
  ```
- Use a single declaration per variable statement. For example:
  ```typescript 
  var x = 1; 
  var y = 2;
  // instead of
  var x = 1, 
      y = 2;
  ```
- `else` goes on a separate line from the closing curly brace.
- Use 4 spaces per indentation.
