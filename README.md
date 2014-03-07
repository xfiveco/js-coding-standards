JavaScript Coding Standards
===================

JavaScript Coding Standards you must conform to when writing JS in XHTMLized projects.

## Indentation

Use an indent of 1 tab. Drop anything that breaks a line and indent one full level:

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

## Line Endings

Format files with \n as the line ending (Unix line endings). Do not use \r\n (Windows line endings) or \r (Apple OS's).

## Naming Conventions

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

## Control Structures

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

### Why are comments so important?

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
