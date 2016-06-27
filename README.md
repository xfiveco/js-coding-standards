JavaScript Coding Standards
===================

JavaScript Coding Standards you must conform to when writing JS in Xfive projects.

## Table of contents

- [Indentation](#indentation)
- [Line endings](#line-endings)
- [Naming conventions](#naming-conventions)
- [Control structures](#control-structures)
- [Comments](#comments)
- [Splitting functionality](#splitting-functionality)
- [License](#license)

## Indentation

Use soft tabs with 2 spaces for code indentation.

Use indentation consistently to enhance the readability of the code.

## Line endings

Format files with \n as the line ending (Unix line endings). Do not use \r\n (Windows line endings) or \r (Apple OS's).

## Naming conventions

When you're starting a new project, please use the following naming conventions:

- **camelCase** for all variables, methods, and functions (never underscore-separated)
- **UpperCamelCase** for all constructor functions and namespace objects
- **UPPERCASE_UNDERSCORE_SEPARATED** for constants.
- jQuery collections should be prefixed with $: `var $items = $('.some-selector');`

When working with existing project it is important to recognize and follow the same naming pattern. No matter what conventions are followed, all names should be **descriptive**, identifying what the data variable holds or what the function does.

## Control structures

Use the following format when writing control structures:

### if

```js
if (condition1 || condition2) {
  action1();
}
else if (condition3 && condition4) {
  action2();
}
else {
  defaultAction();
}
```

### switch

```js
switch (condition) {
  case 1:
  	action1();
  	break;
  
  case 2:
  	action2();
  	break;
  
  default:
  	defaultAction();
}
```

### try

```js
try {
  // Statements...
}
catch (variable) {
  // Error handling...
}
finally {
  // Statements...
}

```

## Comments

Inline documentation for source files should follow the [JSDoc](http://en.wikipedia.org/wiki/JSDoc) formatting conventions. In addition, please use comments to explain the logic behind more tricky parts of code.

## Splitting functionality

When writing a code try to modularize it as much as possible by creating methods/functions. If a project has more JavaScript functionality, add namespaces or even separate it into different files.

## License

[![](http://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
