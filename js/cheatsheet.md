# JavaScript Curriculum Cheat Sheet 🚀

This is a quick-reference guide covering the core concepts and syntax from all six stages of your JavaScript learning journey.

## Stage 1: The Building Blocks

- **Variables**: Use `let` for values that change and `const` for values that stay the same.
- **Data Types**: Primitive types include Strings (text), Numbers (math), and Booleans (true/false).
- **Template Literals**: Use backticks (`` ` ``) and `${variable}` to inject values into text.
- **Operators**: `+`, `-`, `*`, `/`, `%` (remainder).
- **Comparison**: `===`, `!==`, `>`, `<`, `>=`, `<=`.

## Stage 2: Logic & Loops

- **Conditionals**: Use `if`, `else if`, and `else` to control the flow of your program.
- **Equality**: Use `===` to check if two values are exactly equal.
- **Logical Operators**: `&&` (AND), `||` (OR), and `!` (NOT) help combine multiple conditions.
- **Loops**:
  - `for` loops repeat code a specific number of times.
  - `while` loops repeat as long as a condition is true.

## Stage 3: Functions & Scope

- **Declaration**: Use `function name(parameter) { ... }` to create reusable blocks of code.
- **Returns**: The `return` keyword hands data back to whatever called the function.
- **Arrow Functions**: Shorter syntax: `const name = (param) => { ... }`. _(Remember: removing `{}` implicitly returns the value; keeping `{}` requires an explicit `return`!)_
- **Scope**: Variables declared inside a block (`{ ... }`) cannot be seen outside that block. Avoid **variable shadowing** (naming a local variable the same as a global variable).

## Stage 4: Arrays & Objects (React Foundations)

- **Arrays**: Lists of data created with `[]`. They start at index `0`.
- **Push/Pop**: Use `.push()` to add to the end and `.pop()` to remove from the end.
- **Objects**: Data stored in key-value pairs using `{}`. Access data with `object.key`.
- **Array Methods**:
  - `.forEach()`: Runs code for every item.
  - `.map()`: Creates a **new** array with transformed items.
  - `.filter()`: Creates a **new** array containing only items that pass a test.
- **Power Tools**:
  - **Destructuring**: Pull properties out of an object or array into variables.
  - **Spread Operator**: Use `...` to copy or combine arrays and objects.

## Stage 5: The DOM

- **Selecting**: Find elements using `document.getElementById()` or `document.querySelector()`.
- **Events**: Use `element.addEventListener('event', () => { ... })` to respond to user actions.
- **Styles & Classes**: Modify elements via `.style.property` or `.classList.add/remove/toggle()`.
- **Custom Data Attributes**: Store extra metadata in HTML using `data-*` and access it in JS using `element.dataset.*`.
- **Creating**: Generate new elements with `document.createElement()` and add them with `.appendChild()`.

## Stage 6: Modern Asynchronous JS

- **Timing**: Use `setTimeout()` to delay code execution.
- **Promises**: Objects representing a task that will finish in the future (Pending, Fulfilled, or Rejected).
- **Fetch API**: Request data from external servers using `fetch('url')`.
- **Async/Await**: Use `async` before a function and `await` inside it to handle promises like synchronous code.
