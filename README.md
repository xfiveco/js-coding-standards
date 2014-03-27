JavaScript Coding Standards
===================

JavaScript Coding Standards you must conform to when writing JS in XHTMLized projects.

## Table of contents

- [Indentation](#indentation)
- [Line endings](#line-endings)
- [Naming conventions](#naming-conventions)
- [Control structures](#control-structures)
- [Comments](#comments)
- [Splitting functionality](#splitting-functionality)
- [Code refactoring](#code-refactoring)
- [Performance optimization](#performance-optimization)
- [License](#license)

## Indentation

Use soft tabs with two spaces. Drop anything that breaks a line and indent one full level:

```js	
SomeObject
  .myMethod().chain1()
  .chain2().chain3();
 
SomeObject.myMethod({
  some: value,
  another: value
});
 
var myList = [
  "some",
  "another"
];
 
NameSpace.Indents.A.Lot.SomeObject
  .chainMethod(foo)
  .chainMethodWithALongName(
  	bar,
  	someReallyLongVariable
  )
  .chainMethod({
  	foo: bar,
  	another: [
      'set',
      'of',
      'values'
  	]
  })
  .chainMethod([
  	foo,
  	bar,
  	value
  ]);
```

## Line endings

Format files with \n as the line ending (Unix line endings). Do not use \r\n (Windows line endings) or \r (Apple OS's).

## Naming conventions

When you're starting a new project, please use the following naming conventions:

- **camelCase** for all variables, methods, and functions (never underscore-separated)
- **UpperCamelCase** for all constructor functions and namespace objects
- **UPPERCASE_UNDERSCORE_SEPARATED** for constants.
- jQuery collections should be prefixed with $: `var $items = $('.some-selector');`

When working with existing project it is important to recognize and follow the same naming pattern. No matter what conventions are followed, all names should be **descriptive**, identifying what the data variable holds or what the function does.

### Why are naming conventions important?

Consistency in naming conventions helps a lot when you need to work with someone else's code or revisit your own after some time. If we all use the same naming pattern, it is easier for person asked to do modifications to recognize "what's what", to reuse solutions created for other projects and to keep code quality when many people are working together.

Code without any set standard is much harder to read and work with. Let's prove this by way of example. Here's a code snippet, one of which is readable and easy to understand (Sample B), the other of which is not (Sample A).

#### Sample A - Wrong naming
```js
function toggle() {
  var tabs = $(this).closest('.tabs'),
  	d_cont = tabs.siblings('.drawers'),
  	li = tabs.children('ul'),
  	o = tabs.hasClass('open'),
  	h = 0, oh, tH;
  
  if (o) {
  	li.height('');
  	oh = d_cont.data('oh');
  	d_cont.height(oh);
  }
  else {
  	li.children().each(function () {
  	  h += $(this).outerHeight();
  	});
  	li.height(h);
  	oh = d_cont.height();
  	tH = tabs.outerHeight(true);
  	d_cont
      .data('oh', oh)
      .height(Math.max(oh, h - tH));
  }
  
  tabs.toggleClass('open', !o);
};
```

#### Sample B - Proper naming
```js
function toggleDropdown() {
  var $tabs = $(this).closest('.tabs'),
  	$drawersContainer = $tabs.siblings('.drawers'),
  	$list = $tabs.children('ul'),
  	isOpen = $tabs.hasClass('open'),
  	h = 0, oldH, tabsH;
  
  if (isOpen) {
  	$list.height('');
  	oldH = $drawersContainer.data('oldH');
  	$drawersContainer.height(oldH);
  }
  else {
  	$list.children().each(function () {
  	  h += $(this).outerHeight();
  	});
  	$list.height(h);
  	oldH = $drawersContainer.height();
  	tabsH = $tabs.outerHeight(true);
  	$drawersContainer
  	  .data('oldH', oldH)
  	  .height(Math.max(oldH, h - tabsH));
    }
  
  $tabs.toggleClass('open', !isOpen);
};
```

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

### Why are comments important?

Documenting functions, methods, settings and parameters is helpful, but it's not enough. In many cases it's even more important to explain the logic that the code executes. Moreover, writing explanatory comments first and the code itself later will help you organize your thoughts better, resulting in less time wasted writing and debugging.

#### Sample C - Proper commenting
```js
/**
 * Helper function to open or close drawers dropdown.
 *
 * @this {HTMLElement} Drawer tab.
 */
function toggleDropdown () {
  var $tabs = $(this).closest('.tabs'),
  	$drawersContainer = $tabs.siblings('.drawers'),
  	$list = $tabs.children('ul'),
  	isOpen = $tabs.hasClass('open'),
  	h = 0, oldH, tabsH;
  
  if (isOpen) {
  	// Reset heights
  	$list.height('');
  	oldH = $drawersContainer.data('oldH');
  	$drawersContainer.height(oldH);
  }
  else {
  	// Set list height to the sum of children heights
  	$list.children().each(function () {
  	  h += $(this).outerHeight();
  	});
  	$list.height(h);
  	// Remember old container height
  	oldH = $drawersContainer.height();
  	// Ensure drawer container has same or bigger height
  	// so that whole dropdown would be visible
  	tabsH = $tabs.outerHeight(true);
  	$drawersContainer
      .data('oldH', oldH)
      .height(Math.max(oldH, h - tabsH));
    }
  
  $tabs.toggleClass('open', !isOpen);
};
```

## Splitting functionality

When writing a code try to modularize it as much as possible by creating methods/functions (a convention set in the default main.js). If a project has more JavaScript functionality, add namespaces or even separate it into different files.

#### Sample D - Proper file organization
```js
var App = {
  /**
   * Init Function
   */
  init: function() {
  	App.myFeature1();
  	App.myFeature2();
  },
  
  /**
   * App feature 1
   */
  myFeature1: function() {
  	// statements
  },
  
  /**
   * Feature 2
   */
  myFeature2: function() {
  	// statements	   
  }
}
```

#### Sample E - Proper file organization

```js
var App = {
 
  /**
   * Init Function
   */
  init: function() {
  	App.Feature1.init();
  	App.Feature2.init();
  },
  
  /**
   * App feature 1
   */
  Feature1: {
  	init: function() {
      App.Feature1.prepareStructure();
      $('.selector')
      	.on('click', App.Feature1.handleClick)
      	.on('keyup', App.Feature1.handleKeyup);
  	},
  
  	/**
  	 * Some prep feature 1 work
  	 */
  	prepareStructure: function() {
      // statements
  	},
  
    /**
     * Does something on click
     */
  	handleClick: function() {
      // statements
  	},
  
  	/**
  	 * Does something on keyup
  	 */
  	handleKeyup: function() {
      // statements
  	}
  },
  
  /**
   * Feature 2
   */
  Feature2: {
  	// statements
  }
}
```

### Why is splitting functionality to functions important?

Separating functionalities makes your code easier to debug and maintain. If a bug is reported it will be much easier to localize when you can just focus on one section of the logic and ignore (or even temporary turn off) other modules. In addition, when writing in a modular style you will probably automatically stop to write code that depends on so many things to actually work.

Do you know the scenario? You've implemented the tabs on a page - and they work great. You also implemented popups - and they work great too. But now the Client sends "a small modification" to the designs. And now you must have tabs in the popups as well. Will they work out-of-the-box or will you need to modify quite a bit of code to get it done? With modular-based code, in the best case scenario, you probably won't need to do anything or write a one-line initializer. In the worst case scenario, you at least have all functionality code in one place and don't need to re-read a lot of the code to find places to modify.

## Code refactoring

Try to adhere to the [DRY principles](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself). Copy-pasting code results in very hard maintenance, bigger file sizes and overall debugging nightmare. If two blocks of code look similar, see if they cannot be parametrized and written only once. If handling some events is almost the same, then extract common logic to the separate method/function and call it inside event handlers. If there are some "magic numbers" in your code - try to move them into constants with names that actually will tell the reader what it is.

Don't be afraid to use delete key. If some code is no longer needed, simply remove it from the file. If you found a great solution on the web, look through it to see if you need everything that's in there. And make sure you understand, at least general terms, what is it doing and why it is doing it this way. This will help you to avoid conflicts and working around something that could be easily changed.

### Why is code refactoring important?

You may think that you project is small, has a well-defined set of functionalities and will never change. And usually you're right. But when that exception comes and you've written code that can handle only that specific set of requirements, it will hurt you. Or, the developer that is tasked with making modifications will want to hurt you. All because you've hardcoded some heights eight times throughout the file, assumed that no one will ever want to have two slider sections on the same page, or assumed that tiles will always be directly on a page, never dynamically loaded.

## Performance optimization

There are many great performace tips out there, both for jQuery and pure JavaScript. Some of them are:

- http://jonraasch.com/blog/10-advanced-jquery-performance-tuning-tips-from-paul-irish
- http://24ways.org/2011/your-jquery-now-with-less-suck/
- http://www.joezimjs.com/javascript/3-simple-things-to-make-your-jquery-code-awesome/

One of the simplest, and at the same time, improving code quality, is jQuery collection caching. When you have some root element that you will be selecting all other needed elements from - keep it in variable instead of selecting it over and over. Searching the DOM is costly, especially in slightly older browsers. So this:

```js
var $container = $('.my-root'),
  $list = $container.find('.my-list'),
  $items = $container.find('.my-items');
```

is better than:

```js
var $list = $('.my-root .my-list'),
  $items = $('.my-root .my-items');
```

Not to mention the number of places that will need to be updated if it turns out that `.my-root` needs to be called `.my-unique-root` because the other name conflicted with something.

### Why is performance optimization important?

You may think that performance doesn't matter in small projects. But that's not true. Aside from the matter of code readability, it also forces you to think in a way that will become natural as time passes by. So that when bigger project happens, or when the old one suddenly grows, all good practices are already there and there's no need to suddenly make a big rewrite of everything to make site faster and more responsive to the user actions.

## License

[![](http://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
