
<!-- MarkdownTOC depth=3 -->

- [Sam's document](#sams-document)
    - [General](#general)
    - [Spacing](#spacing)
    - [Formatting](#formatting)
    - [Misc](#misc)
    - [Examples](#examples)
    - [File organization](#file-organization)
    - [Pixels vs. ems vs. rems vs. %](#pixels-vs-ems-vs-rems-vs-%)
    - [Class naming conventions](#class-naming-conventions)
    - [CSS Specificity guidelines](#css-specificity-guidelines)
    - [References](#references)
- [Gareth's notes](#gareths-notes)

<!-- /MarkdownTOC -->


## Sam's document

Note that this document gives the overview of how CSS should be formatted here at the University of St Andrews. You will want to consider patterns for examples of how to structure HTML based on our core CSS and JS.

<mark>This might not be necessary:</mark> Before continuing, you should have a general understanding for specificity, the SCSS syntax, and KSS documentation.

### General

### Spacing

* Use soft-tabs with a two space indent. Spaces are the only way to guarantee code renders the same in any person's environment.
* Put spaces after `:` in property declarations.
* Put spaces before `{` in rule declarations.
* Put line breaks between rulesets.
* When grouping selectors, keep individual selectors to a single line.
* Place closing braces of declaration blocks on a new line.
* Each declaration should appear on its own line for more accurate error reporting.

### Formatting

* Use hex color codes `000` unless using `rgba()`.
* Use `//` for comment blocks (instead of `/* */`). <mark>This is because of KSS, which uses the `//` syntax. We need to decide if this is something we wish to adopt.</mark>
* Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.
* Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values.

### Misc

* Keep lines fewer than 80 characters.
* As a rule of thumb, avoid unnecessary nesting in SCSS. At most, aim for three levels. If you cannot help it, step back and rethink your overall strategy (either the specificity needed, or the layout of the nesting).
* Document styles with KSS. <mark>Obviously depends on whether we use KSS.</mark>

### Examples

Here are some good examples that apply the above guidelines:

```
// Example of good basic formatting practices
.style guide-format {
color: 000;
background-color: rgba(0, 0, 0, .5);
border: 1px solid 0f0;
}

// Example of individual selectors getting their own lines (for error reporting)
.multiple,
.classes,
.get-new-lines {
display: block;
}

// Avoid unnecessary shorthand declarations
.not-so-good {
margin: 0 0 20px;
}
.good {
margin-bottom: 20px;
}
```

### File organization

<mark>Github include a section on [File organization](https://github.com/style guide/css). Would this make sense for us? In what cases would we be dictating file organization for SCSS code that isn't inside the pattern library?</mark>

...

### Pixels vs. ems vs. rems vs. %

<mark>I think this is worthy of our consideration.</mark>

When do we use each one?

Use `px` for `font-size`, because it offers absolute control over text. Additionally, unit-less `line-height` is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the font-size.

### Class naming conventions

Never reference `js-` prefixed class names from CSS files. `js-` are used exclusively from JS files.

Use the `is-` prefix for state rules that are shared between CSS and JS.

Specificity (classes vs. ids)

Elements that occur **exactly once** inside a page should use IDs, otherwise, use classes. When in doubt, use a class name.

* **Good** candidates for ids: header, footer, modal popups.
* **Bad** candidates for ids: navigation, item listings, item view pages.

When styling a component, start with an element + class namespace (prefer class names over ids), prefer direct descendant selectors by default, and use as little specificity as possible. Here is a good example:

```
<ul class="category-list">
<li class="item">Category 1</li>
<li class="item">Category 2</li>
<li class="item">Category 3</li>
</ul>
```

```
.category-list { // element + class namespace

// Direct descendant selector > for list items
> li {
list-style-type: disc;
}

// Minimal specificity for all links
a {
color: f00;
}
}
```

### CSS Specificity guidelines

* If you must use an id selector (`selector`) make sure that you have no more than _one_ in your rule declaration. A rule like `header .search quicksearch { ... }` is considered harmful.
* When modifying an existing element for a specific use, try to use specific class names. Instead of `.listings-layout.bigger` use rules like `.listings-layout.listings-bigger`. Think about ack/greping your code in the future.
* The class names `disabled`, `mousedown`, `danger`, `hover`, `selected`, and `active` should always be namespaced by a class (`button.selected` is a good example).


---

### References

The initial version of this style guide was based on [Github's HTML style guide](https://github.com/style guide/templates).


---

## Gareth's notes

TODO: Order of rules, e.g. A-Z, or block first, etc.
TODO: Order of box model: top, right, bottom, left
TODO: Concatination and minification (Pro CSS, 2.8, p.362)
TODO: CSS sprites (Pro CSS, 2.9, p.362)
TODO: Don't use CSS behaviours (HTC files) (Pro CSS, 2.11, p.362)
TODO: SHOULD never used data URIs (except for Error pages) (Pro CSS, 2.12, p.362)
TODO: The one "rule"ish thing thing I really believe in: keep your selector specificities fairly low and flat across your whole project. [Harry's specificity graph](http://csswizardry.com/2014/10/the-specificity-graph/) is a nice way to think about this. Specificity will trend upward, so never start high, as the ceiling can easily become problematic. Mostly: .class {}. http://css-tricks.com/just-try-and-do-a-good-job


http://csswizardry.com/2012/11/code-smells-in-css/
"Rulesets should only ever inherit and add to previous ones, never undo. [...] If you find you are having to undo styling as you go down your document the chances are you jumped the gun and started adding too much too soon."


http://csswizardry.com/2012/11/code-smells-in-css/
Never every use magic numbers. "Avoid magic numbers like the plague."

"A magic number is a value that is used ‘because it just works’." If you absolutely must use a magic number then you must comment it to explain why: what does this relate to, e.g. 

```
/**
We've used 37px here because the li elements inside .site-nav happen to be 37px tall, and the .dropdown flyout menu needs to appear at the bottom of it.
*/
```


http://csswizardry.com/2012/11/code-smells-in-css/
Similarly, avoid brute-forcing, e.g.

```
foo {
    margin-left: -3px;
    position: relative;
    z-index: 99999;
    height: 59px;
    float: left;
}
```
"All of these declarations are heavy-handed, brute-forced, layout-affecting declarations which are clearly only used to force something to render as and where it’s wanted."


http://csswizardry.com/2012/11/code-smells-in-css/
Avoid qualified selectors, e.g.

```
ul.nav {}
a.button {}
div.header {}
```

* They prevent reusability on another element.
* They increase specificity.
* They increase browser workload (decreasing performance).

These selectors would be much better:

```
.nav {}
.button {}
.header {}
```

More extreme examples might be:

```
ul.nav li.active a {}
div.header a.logo img {}
.content ul.features a.button {}
```

All of these selectors can be trimmed down massively, or totally rewritten, to:

```
.nav .active a {}
.logo > img  {}
.features-button {}
```


http://csswizardry.com/2012/11/code-smells-in-css/
Line heights should always be set relatively, so rather than

```
h1 {
    font-size: 24px;
    line-height: 32px;
}
```

use

```
h1 {
    font-size: 24px;
    line-height: 1.333;
}
```


http://csswizardry.com/2012/11/code-smells-in-css/
"!important should only ever be used proactively, not reactively. For example, you know that you will always want errors to be red, so this rule is totally fine:""

```
.error-text {
    color: #c00 !important;
}
```

NEED TO MAKE NOTE ABOUT space before !important


http://csswizardry.com/2012/11/code-smells-in-css/
Don't use "loose class names"
Be specific about class names, e.g. `.card` isn't specific enough. Does this mean a Trello or Google idea of cards? Or is it a credit card.

Also they could more easily be reused and could unwittingly be overwritten elsewhere in the code.

TODO: What is the minimum guide that could be created to add value NOW? What would that look like and could I create it from the text here?

TODO: What from Harry Roberts' work do I need to unpick?