[**↺**BACK](./README.md)
# General SCSS

  - [Linting](#linting)
  - [General Rules](#general-rules)
  - [Strings](#strings)
  - [Selector Nesting](#selector-nesting)
  - [Numbers](#numbers)
  - [Constants](#constants)
  - [Variables](#variables)
  - [Colour Formats](#colour-formats)
  - [BEM Block Element Modifier](#bem-block-element-modifier)
  - [Naming Conventions](#naming-conventions)
  - [Architecture](#architecture)

Describing the way developers want code to look.

When several developers are involved in writing CSS on the same project(s), it is only a matter of time before one of them starts doing things their own way. Code guidelines that promote consistency not only prevent this, but also help when it comes to reading and updating the code


## Linting

Use [Prettier](https://prettier.io/) in your editor to fix basic css styling errors on save.

Use [Stylelint](https://stylelint.io/) for fixing more things such as a wrong HEX number.



## General Rules

- Create good selector intent.

```scss
// Avoid
.header ul {}

// Do
.main__nav {}

// Avoid
.sidebar h2 {}

// Do
.sidebar__title {}

// Avoid
.sidebar form {}

// Do
.search-form {}
```

> **Why ?** Maintainability, prevent style leaks.

- Write efficient CSS selectors.

```html
<!--- Before -->
<ul class="device-nav">
  <li><a href="#" class="online">Online</a></li>
  <li><a href="#" class="offline">Offline</a></li>
  <li><a href="#" class="terminated">Terminated</a></li>
</ul>

<!-- After -->
<ul class="device-nav">
  <li><a href="#" class="device-nav__link online">Online</a></li>
  <li><a href="#" class="device-nav__link offline">Offline</a></li>
  <li><a href="#" class="device-nav__link terminated">Terminated</a></li>
</ul>
```

```scss
// Before
.device-nav a {}

// After
.device-nav {
  
  &__link {
    // .. code
  }
}
```

> **Why ?** Performance and prevent the browser looking for every `a href` before settling on the ones it needs to style. This new key selector will match far fewer elements and means that the browser can find them and style them faster and can move on to the next thing.

- Write selectors for reusability.

```scss
// Avoid
.myHeader h2 {
  color: #000;
}

// Do
.heading {
  
  .&__text {
  color: $variableColor;
  }
}

```

> **Why ?** More efficient, reduce waste and repetition.

- Avoid nesting selectors unnecessarily.

```scss
// Avoid
.content {
  .nav {
    width: 75%;
  }
}

// Do (dependant on purpose)
.main-navigation {
  width: 75%;
}

.sidebar-naviagtion {
  width: 50%;
}

.navigation {
  background: blue;
  padding: 4px;
}

// Do (BEM)

.navigation {
  background: blue;
  padding: 4px;

  // modifier
  &--main {
    width: 75%;
  }

  // modifier
  &--sidebar {
    width: 50%;
  }
}
```

> **Why ?** Because this will increase specificity and affect where else you can use the styles.

- Avoid qualifying selectors unnecessarily

```scss
// Avoid
.content .header-title {}
.menu .header-title {}

// Do
h1.header-title {}
h2.header-title {}
```

> **Why ?** This will impact the number of different elements you can apply styles to.

- Use short selectors.

```scss
// Avoid
html body .overview .stats {}

// Do
.overview-stats {}
```

> **Why ?** Better maintenence and keeps specificity down and performance up.

- Two (2) space indents, no tabs

```scss
// Avoid
.foo {
        display: block;
        background-color: green;
        color: red;
				}

// Do
.foo {
  display: block;
  background-color: green;
  color: red;
}
```

> **Why ?** Readability, maintainable and largely universal.

- Limit code to 80 character wide columns

```scss
// Avoid
/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am such a long comment that I easily break the 80 character limit, so I am
 * broken across several lines.
 */

// Do
/*
I am a long-form comment. I describe,
in detail, the CSS that follow. I am
such a long comment that I easily
break the 80 character limit, so I am
broken across several lines.
*/
```

> **Why ?** Readability, the ability to see files side by side and easy viewing on git repos or terminal windows.

- Use multi-line CSS and meaningful use of whitespace.

```scss
// Avoid
.foo {
padding-left:8px; padding-right: 0; padding-bottom: 8px margin:8px;

border:1px solid #000;
}

// Do
.foo {
  padding: 4px 0px;
  margin: 8px 0px;
  border: 1px solid #000;
}

```

> **Why ?** Consistency, readability and reduced chance of merge conflicts.

- Avoid using the same rule repetitively.

```scss
// Avoid
.header__title {
  color: #3498db;
}

.footer__title {
  color: #3498db;
}

.sidebar__title {
  color: #3498db;
}

// Do
.section-title {
  color: $variableColor;
}
```

> **Why ?** Reuseable, maintainable

- Avoid overuse the `!important` Rule

```scss
// Avoid
.card-body {
  color: #e74c3c;
}

.card-body .intro {
  color: #3498db !important;
  font-size: 20px;
}

.card-body .capture {
  color: #2ecc71;
  font-size: 20px;
}

// Do ( if overriding styles from third party plugins or unavoidable inline css)
.plugin-specific-element {
  color: #3498db !important;
}
```

> **Why ?** Maintainability, to avoid clutter and unnecessary specificity.

- Use shorthand properties

```scss
// Avoid
.form-button {
  margin-top: 4px;
  margin-right: 8px;
  margin-bottom: 4px;
  margin-left: 8px;
}

// Do
.form-button {
  margin: 4px 8px;
}
```

> **Why ?** Maintainable, readable

## Strings

- Use UTF-8 encoding in the main-stylesheet using the `@charset` directive. Make sure it is the very first element of the stylesheet and there is no character of any kind before it.

```scss
@charset 'utf-8';
```

> **Why ?** To avoid any potential issue with character encoding.

- Strings should always be wrapped with single quotes (`'`)

```scss
// Avoid
$direction: left;

// Do
$direction: "left";
```

> **Why ?** It helps general readability?

- Specific CSS values (identifiers) such as `initial` or `sans-serif` require not to be quoted.

```scss
// Avoid
$font-type: "sans-serif";

// Do
$font-type: sans-serif;
```

> **Why ?** To prevent errors failing silently

- URLs should be quoted.

```scss
// Avoid
.foo {
  background-image: url(/images/logo.png);
}

// Do
.foo {
  background-image: url("/images/logo.png");
}
```

> **Why ?** To prevent errors

## Selector Nesting

- Compute long selectors by nesting shorter selectors within each others.

```scss
.foo {
  .bar {
    
    &:hover {
      color: #ff0000;
    }
  }
}

/// generates
.foo .bar:hover {
  color: #ff0000;
}
```

- Use the current selector reference (`&`) to generate advanced selectors.

```scss
.block {
  
  &--modified {
    color: #ff0000;
  }
}

///generates
.block-modified {
  color: #ff0000;
}
```

> **Why ?** Readability, maintainability, consistency.

## Numbers

- Numbers should display leading zeros before a decimal value less than one. Never display trailing zeros.

```scss
// Avoid
.foo {
  padding: 2.0em;
  opacity: 0.5;
}

// Do
.foo {
  padding: 2em;
  opacity: 0.5;
}
```

> **Why ?** Consistency

- Lengths with a `0` value should never ever have a unit.

```scss
// Avoid
$length: 0em;

// Do
$length: 0;
```

- Prevent unit values becoming strings.

```scss
$value: 42;

// Avoid
$length: $value + px;

// Do
$length: $value + 0px;
```

> **Why ?** Appending a unit as a string to a number results in a string, preventing any additional operation on the value.

- Top-level numeric calculations should always be wrapped in parentheses.

```scss
// Avoid
.foo {
  width: 100% / 3;
}

// Do
.foo {
  width: (100% / 3);
}
```

> **Why ?** Improve readability.

## Constants

- Define constants with all-caps snakerized variables.

```scss
// Do
$CSS_POSITIONS: (top, right, bottom, left, center);

// Avoid
$css-positions: (top, right, bottom, left, center);
```

> **Why ?** Readability, Contrasts well with usual lowercased hyphenated variables.

## Variables

- Scoping

Any configuration variables should be defined with the `!default` flag so they can be overwritten.

```css
$baseline: 1em !default;
```

> **Why ?** Maintainability.

## Colour Formats

- When using a colour more than once, store it in a variable with a meaningful name representing the colour.

```scss
$sass-pink: #ff69b4;
```

- If usage is strongly tied to a theme, store it in another variable with a name explaining how it should be used.

```scss
$main-theme-color: $sass-pink;
```

> **Why ?** Readability, maintainability, consistency.

## BEM Block Element Modifier

- Use BEM methodology for naming our CSS classes.

```scss
/// .block represents the higher level of an abstraction or component.
.block {}

/// .block__element represents a descendent of .block that helps form .block as a whole.
.block__element {}

/// .block--modifier represents a different state or version of .block.
.block--modifier {}
```

- Write classes that are related with BEM, something might just be a component, something might be a child, or _element_, of that component, and something might be a variation or _modifier_ of that component.

```scss
/// Avoid
.house {}
.door {} // <-- door of what, a cinema, a garage ?
.window {} // <-- window of what ?
.door-window {} // <-- of a taxi ?
.door-open {}

/// When not needed
.site-logo {}

/// Avoid doing this
.header {}
.header__logo {}

/// Do
.house {
  //...code

  &__door {
    // (element) house can have a door
    //...

    &--open-yes {
      // (modifier) house door can be open
      //...code
    }
  }

  &__window {
    // (element) house can have a window
    //...code

    //// 3 levels deep max & thinking ahead with modiers based
    //// on size and shape / open and closed

    &--open-yes {}

    &--closed-yes {}

    &--round-lg {
      // (modifier) window can be round & large
      //...code
    }

    &--round-md {
      // (modifier) window can be round & medium
      //...code
    }

    &--square-lg {
      // (modifier) window can be square & large
      //...code
    }

    &--square-md {
      // (modifier) window can be square & medium
      //...code
    }
  }
}
```



```scss
// Block
.house {}
```

```html
<!-- Block -->
<div class="house"></div>
```



```scss
// Block element = house with a door
.house__door {}
```

```html
<!-- Block element = house with a door -->
<div class="house">
<span class="house__door"></span>
</div>
```



```scss
// Block element = House with a door with a window
.house__window {}
```

```html
<!-- Block element = House with a door with a window -->
<div class="house">
	<div class="house__door">
		<span class="house__window"></span>
	</div>
</div>
```



```scss
/// Block Element with a Modifier = house door that is open
.house__door--open-yes {}
```

```html
<!-- Block Element with a Modifier = house door that is open -->
<div class="house">
	<span class="house__door house__door--open-yes"></span>
</div>
```



```scss
// Block Element with
// more than one Modifier = House door that is open
// and house window that is open and one that is closed
// One window round and large and one medium and square
.house__window--open-yes {}
.house__window--closed-yes {}
.house__window--round-lg {}
.house__window--square-md {}
```

```html
<!-- Block Element with
more than one Modifier = House door that is open
and house window that is open and one that is closed
One window round and large and one medium and square
-->
<div class="house">
  <div class="house__door house__door--open-yes">
  </div>
  <div class="house__window house__window--open-yes house__window--round-lg">
  </div>
  <div class="house__window house__window--closed-yes house__window--square-md">
  </div>
</div>
```



> **Why ?** Maintainability, scaleability, readability.

## Naming Conventions

- Name variables, functions and mixins with **lowercase hyphen-delimited**, and above all meaningful.

```scss
$vertical-margin: 1.5rem;

@mixin size($width, $height: $width) {
  // …
}

@function opposite-direction($direction) {
  // …
}
```

> **Why ?** Readability, maintainability.

## Architecture

- Components can be anything, as long as they:
  - do one thing and one thing only;
  - are re-usable and re-used across the project;
  - are independent.

> **Why ?** Maintainability.

Read more:

- Sass Guidlines: https://sass-guidelin.es/

- BEM http://getbem.com/

- CSS guide lines : https://cssguidelin.es/

- Csswizardry: https://csswizardry.com/

[**⇪**TOP](#General-SCSS)