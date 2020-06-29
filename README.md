# TypeScript Coding Guidelines

## Whitespace
![Whitespace guidelines](https://raw.githubusercontent.com/javascript-tutorial/en.javascript.info/master/1-js/03-code-quality/02-coding-style/code-style.svg)

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
- If you must reassign references, use `let` instead of `var`.
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
- Use single quotes `''` for strings.
  > This keeps things consistent and allows you use new lines and interpolation within the same format.
  ```typescript
  // bad
  const name: string = "Capt. Janeway";

  // bad - template literals should contain interpolation or newlines
  const name: string = `Capt. Janeway`;

  // good
  const name: string = 'Capt. Janeway';
  ```
- Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.
  > Broken strings are painful to work with and make code less searchable.
  ```typescript
  // bad
  const errorMessage: string = 'This is a super long error that was thrown because \
  of Batman. When you stop to think about how Batman had anything to do \
  with this, you would get nowhere \
  fast.';

  // bad
  const errorMessage: string = 'This is a super long error that was thrown because ' +
    'of Batman. When you stop to think about how Batman had anything to do ' +
    'with this, you would get nowhere fast.';

  // good
  const errorMessage: string = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
  ```
- When programmatically building up strings, use template strings instead of concatenation.
  > Template strings give you a readable, concise syntax with proper newlines and string interpolation features.
  ```typescript
  // bad
  function sayHi(name: string): string {
    return 'How are you, ' + name + '?';
  }

  // bad
  function sayHi(name: string): string {
    return ['How are you, ', name, '?'].join();
  }

  // bad
  function sayHi(name: string): string {
    return `How are you, ${ name }?`;
  }

  // good
  function sayHi(name: string): string {
    return `How are you, ${name}?`;
  }
  ```
- Never use `eval()` on a string, it opens too many vulnerabilities.
- Do not unnecessarily escape characters in strings.
  > Backslashes harm readability, thus they should only be present when necessary.
  ```typescript
  // bad
  const foo: string = '\'this\' \i\s \"quoted\"';

  // good
  const foo: string = '\'this\' is "quoted"';
  const foo: string = `my name is '${name}'`;
  ```

## Arrays
- Annotate arrays as `foos: Foo[]` instead of `foos: Array<Foo>`.

## Functions
- Use named function expressions instead of function declarations.
   > Function declarations are hoisted, which means that it’s easy - too easy - to reference the function before it is defined in the file. This harms readability and maintainability. If you find that a function’s definition is large or complex enough that it is interfering with understanding the rest of the file, then perhaps it’s time to extract it to its own module! Don’t forget to name the expression - anonymous functions can make it harder to locate the problem in an Error's call stack.
   ```typescript
  // bad
  function foo(): void {
    // ...
  }

  // bad
  const foo = (): void => {
    // ...
  };

  // good
  const foo = function bar(): void {
    // ...
  };
  ```
- Use arrow functions over anonymous functions.
  ```typescript
  // bad
  const foo = function(): void => {
    // ...
  };

  // good
  const foo = (): void => {
    // ...
  };
  ```
- Wrap immediately invoked function expressions in parentheses.
  > An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.
  ```typescript
  // immediately-invoked function expression (IIFE)
  ((): void {
    console.log('Welcome to the Internet. Please follow me.');
  }());
  ```
- Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.

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
- Use 2 spaces per indentation.
