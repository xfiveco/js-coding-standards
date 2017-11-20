JavaScript Coding Standards
===================

JavaScript Coding Standards you must conform to when writing JS in Xfive projects.

## Table of contents
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Code style](#code-style)
- [Line endings](#line-endings)
- [Variables](#variables)
- [Comments](#comments)
- [Modules/dependencies](#modulesdependencies)
- [Code structure](#code-structure)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Code style

Use `eslint-config-chisel` or `eslint-config-airbnb` with `eslint-config-prettier`. This setup allows for automatic code formatting with [Prettier](https://github.com/prettier/prettier) so you don't need to worry about the small details.

## Line endings

Format files with \n as the line ending (Unix line endings). Do not use \r\n (Windows line endings) or \r (Apple OS's).

## Variables

When you're starting a new project, use the following naming conventions:

- Prefer [block scoping](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block) with let and const.
- Use `const` to assign a variable unless you’re certain you’re going to reassign it later.
- In general, use **camelCase** to name variables. Of course, there can be exceptions like sometimes you have_to_use underscores to access a value from JSON and can’t do much about it. Or there’s a third party code which imposes certain naming conventions.
- Start class names (constructors) with a **BigLetter**.
- Use **UPPERCASE_WITH_UNDERSCORES** to name constants. You can define constants in JS with assigning a [primitive value](https://developer.mozilla.org/pl/docs/Glossary/Primitive) with `const`.

  Following examples have one thing in common: they can’t be reassigned nor mutated. This makes them constants.

  ```js
  const MARGIN_TOP = 2;
  const DEBUG_MODE = false;
  const API_URL = 'http://my-api.com';
  ```

- Avoid UPPERCASE_NAMING for mutable values like arrays or object literals.

  Following examples aren’t constants as they can be easily updated. This is why using uppercase naming is misleading when used with them.

  ```js
  const MY_ARR = [1, 2, 3];
  MY_ARR.splice(0);
  console.log(MY_ARR);
  // prints []
  // Holy moly the array is now empty!

  ```

  ```
  const MY_OBJECT = { a: 'something important' };
  delete MY_OBJECT.a;
  console.log(MY_OBJECT);
  // prints {}
  // Empty!
  ```
- jQuery objects should be prefixed with $: `const $items = $('.some-selector');`

When working with existing project it is important to recognize and follow the same naming pattern. No matter what conventions are followed, all names should be **descriptive**, identifying what the data variable holds or what the function does.

## Comments

**Avoid obvious comments.** They bring _no value_ and make the code _harder to maintain_. Comment only exceptions and code which doesn’t seem to be clear to understand. The latter can be hard to identify. It’s the code _you_ have written  after all so it’s more obvious to you. Don’t hesitate to ask your peers or developers you consider more experienced to take a look at your code!

## Modules/dependencies

- Use [import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) to split your code into components.
- Make sure you import _just what you need_ and not the whole library. Here's [Lodash example](https://stackoverflow.com/a/35251059). It can vary depending on the package you want to use (sometimes can be even impossible!). In general, verify if your JS bundle size isn't suspiciously big.
- Use [Yarn](https://yarnpkg.com/lang/en/) to install packages. Not only it's fast but also creates a lockfile which make much easier to setup the project for other developers.

## Code structure
- Prefer to use a class syntax over object literals when structuring your code.

  ```js
  // You can do it like this
    const app = {
      init() {
        this.doSomething();
      },

      doSomething() {
        console.log('Bam!');
      }
    };

    // But the class is more suitable for the job!
    class App {
      constructor() {
        this.doSomething();
      }

      doSomething() {
        console.log('Oh boy a class!');
      }
    }
  ```

- When writing a code try to modularize it as much as possible by creating methods/functions. If a project has more JavaScript functionality, add namespaces or separate it into different files (modules).

## License

[![](http://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
