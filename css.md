
<!-- MarkdownTOC depth=3 -->

- Sam's document
    - General
    - Spacing
    - Formatting
    - Misc
    - Examples
    - File organization
    - Pixels vs. ems vs. rems vs. %
    - Class naming conventions
    - CSS Specificity guidelines
    - References
- Gareth's notes

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
