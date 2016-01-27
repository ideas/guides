# Node.js Style Guide

Node.js version: 5.3.x.

## Table of Contents

  - [References](#references)
  - [Objects](#objects)
  - [Arrays](#arrays)
  - [Strings](#strings)
  - [Functions](#functions)
  - [Arrow Functions](#arrow-functions)
  - [Constructors](#constructors)
  - [Promises](#promises)
  - [Iterators](#iterators)
  - [Properties](#properties)
  - [Variables](#variables)
  - [Comparison Operators and Equality](#comparison-operators-and-equality)
  - [Blocks](#blocks)
  - [Comments](#comments)
  - [Whitespace](#whitespace)
  - [Commas](#commas)
  - [Semicolons](#semicolons)
  - [Type Casting & Coercion](#type-casting--coercion)
  - [Naming Conventions](#naming-conventions)
  - [Accessors](#accessors)
  - [Testing](#testing)

## References

  - Use `const` for all of your references; avoid using `var`. This ensures that you can't reassign your references, which can lead to bugs and difficult to comprehend code.

  - If you must reassign references, use `let` instead of `var`. `let` is block-scoped rather than function-scoped like `var`.

## Objects

  - Use the literal syntax for object creation.

    ```javascript
    const item = {};
    ```

  - Use computed property names when creating objects with dynamic property names. They allow you to define all the properties of an object in one place.

  - Use object method shorthand.

    ```javascript
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  - Use property value shorthand. It is shorter to write and descriptive.

    ```javascript
    const value = 1;

    const atom = {
      value,
    };
    ```

  - Group your shorthand properties at the beginning of your object declaration. It's easier to tell which properties are using the shorthand.

## Arrays

  - Use the literal syntax for array creation.

    ```javascript
    const items = [];
    ```

  - Use `Array#push` instead of direct assignment to add items to an array.

  - Use array spreads `...` to copy arrays.

  - To convert an array-like object to an array, use `Array#from`.

## Strings

  - Use single quotes `''` for strings.

  - Strings that cause the line to go over 100 characters should be written across multiple lines using string concatenation.

  - When programmatically building up strings, use template strings instead of concatenation. Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

    ```javascript
    $message = `Welcome back, ${name}!`;
    ```

  - Never use `eval()` on a string, it opens too many vulnerabilities.

## Functions

  - Use function declarations instead of function expressions. Function declarations are named, so they're easier to identify in call stacks. Also, the whole body of a function declaration is hoisted, whereas only the reference of a function expression is hoisted. This rule makes it possible to always use Arrow Functions in place of function expressions.

    ```javascript
    function foo() {
      // ...
    }
    ```

  - Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead.

    ```javascript
    let test;
    if (true) {
      test = () => {
        console.log('Hello');
      };
    }
    ```

  - Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

  - Never use the `Function` constructor to create a new function. Creating a function in this way evaluates a string similarly to `eval()`, which opens vulnerabilities.

  - Never mutate parameters. Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

  - Never reassign parameters. Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

## Arrow Functions

  - When you must use function expressions (as when passing an anonymous function), use arrow function notation. It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

    ```javascript
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  - If the function body consists of a single expression, use the implicit return. Otherwise use a `return` statement.

    ```javascript
    [1, 2, 3].map((number) => `A string containing the ${number}.`);
    ```

  - In case the expression spans over multiple lines, wrap it in parentheses for better readability. It shows clearly where the function starts and ends.

    ```js
    [1, 2, 3].map((number) => (
      `As time went by, the string containing the ${number} became much ` +
      'longer. So we needed to break it over multiple lines.'
    ));
    ```
  - Place 1 space before and after `=>`.

    ```js
    [1, 2, 3].map((x) => x * x);
    ```

## Constructors

  - Always use `class`. Avoid manipulating `prototype` directly.

    ```javascript
    class Queue {
      constructor(contents) {
        this._queue = contents || [];
      }

      pop() {
        const value = this._queue[0];
        this._queue.splice(0, 1);
        return value;
      }
    }
    ```

  - Use `extends` for inheritance. It is a built-in way to inherit prototype functionality without breaking `instanceof`.

    ```javascript
    class PeekableQueue extends Queue {
      peek() {
        return this._queue[0];
      }
    }
    ```

  - Methods can return `this` to help with method chaining.

  - It's okay to write a custom `toString()` method, just make sure it works successfully and causes no side effects.

## Promises

  - Build you interfaces using Promises. Instead of asking to provide a callback to your function, return a Promise.

  - Always use the native Promise implementation.

  - Don't define rejection handlers as the second argument for `then` calls, always use an extra `catch`.

    ```js
    const promise = execute();
    promise
      .then((data) => {
        // success
      })
      .catch((err) => {
        // error
      });
    ```

  - Flatten Promise chains.

## Iterators

  - Don't use iterators. Prefer JavaScript's higher-order functions like `map()` and `reduce()` instead of loops like `for-of`. This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side-effects.

## Properties

  - Use dot notation when accessing properties.

    ```javascript
    const value = atom.value;
    ```

  - Use subscript notation `[]` when accessing properties with a variable.

## Variables

  - Always use `const` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace.

  - Use one `const` declaration per variable. It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs.

  - Group all your `const`s and then group all your `let`s. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

## Comparison Operators and Equality

  - Use `===` and `!==` over `==` and `!=`.

  - Use shortcuts.

    ```javascript
    if (name) {
      // ...
    }

    if (items.length) {
      // ...
    }
    ```

## Blocks

  - Use braces with all multi-line blocks.

    ```javascript
    if (test) return false;

    if (test) {
      return false;
    }
    ```

  - If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your
    `if` block's closing brace.

    ```javascript
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

## Comments

  - Use `/** ... */` for multi-line comments. Include a description, specify types and values for all parameters and return values.

  - Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it's on the first line of a block.

    ```javascript
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;
    }
    ```

## Whitespace

  - Use soft tabs set to 2 spaces.

    ```javascript
    function() {
    ∙∙const name;
    }
    ```

  - Place 1 space before the leading brace.

    ```javascript
    function test() {
      console.log('test');
    }
    ```

  - Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space before the argument list in function calls and declarations.

    ```javascript
    if (test) {
      console.log('test');
    }

    function test() {
      console.log('test');
    }
    ```

  - Set off operators with spaces.

    ```javascript
    const x = y + 5;
    ```

  - End files with a single newline character.

  - Use indentation when making long method chains. Use a leading dot, which emphasizes that the line is a method call, not a new statement.

  - Leave a blank line after blocks and before the next statement.

    ```javascript
    const obj = {
      foo() {
      },

      bar() {
      }
    };

    return obj;
    ```

  - Do not pad your blocks with blank lines.

    ```javascript
    function bar() {
      console.log(foo);
    }
    ```

  - Do not add spaces inside parentheses.

    ```javascript
    if (foo) {
      console.log(foo);
    }
    ```

  - Do not add spaces inside brackets.

    ```javascript
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  - Add spaces inside curly braces.

    ```javascript
    const foo = { bar: 'test' };
    ```

  - Avoid having lines of code that are longer than 100 characters (including whitespace). This ensures readability and maintainability.

## Commas

  - Don't use leading commas.

  - Don't use trailing commas.

## Semicolons

  - Use semicolons.

    ```javascript
    (() => {
      const name = 'Dana Scully';
      return name;
    })();
    ```

## Type Casting & Coercion

  - Perform type coercion at the beginning of the statement.

  - Strings:

    ```javascript
    const value = String(input);
    ```

  - Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings.

    ```javascript
    const value = Number(input);
    const value = parseInt(input, 10);
    ```

  - Booleans:

    ```javascript
    const value = Boolean(input);
    const value = !!input;
    ```

## Naming Conventions

  - Avoid single letter names (except in loops). Be descriptive with your naming.

  - Use camelCase when naming objects, functions, and instances.

    ```javascript
    const thisIsMyObject = {};

    function thisIsMyFunction() {
      // ...
    }
    ```

  - Use PascalCase when naming constructors, classes, and imported modules.

    ```javascript
    const Fs = require('fs');

    class User {
      constructor(options) {
        this.name = options.name;
      }
    }
    ```

  - Use a leading underscore `_` when naming private properties.

    ```javascript
    this._name = 'Dana Scully';
    ```

  - Don't save references to `this`. Use arrow functions or `Function#bind`.

    ```javascript
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

## Accessors

  - Accessor functions for properties are not required.

  - If you do make accessor functions use `getValue()` and `setValue(value)`.

    ```javascript
    user.getAge();
    user.setAge(27);
    ```

  - If the property is a `boolean`, use `isValue()` or `hasValue()`.

    ```javascript
    if (!user.hasAge()) {
      return false;
    }
    ```

  - It's okay to create `get()` and `set()` functions, but be consistent.

    ```javascript
    class User {
      constructor(options) {
        const name = options.name || 'n/a';
        this.set('name', name);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

## Testing

  - Use tests with 100% code coverage.
