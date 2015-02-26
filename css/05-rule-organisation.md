CSS code standards guide

# Rule organisation

As Jonathan Snook says in [Scalable and Modular Architecture for CSS](https://smacss.com/book/categorizing "Categorizing CSS Rules"):

> Every project needs some organization. Throwing every new style you create
> onto the end of a single file would make finding things more difficult and 
> would be very confusing for anybody else working on the project.

We use Jonathan Snook's Scalable and Modular Architecture for CSS, aka SMACSS, to inform how to organise the rules within a CSS (or Sass) file.





## In this section
<!-- MarkdownTOC -->

- [Categorise your CSS rules](#categorise-your-css-rules)
- [1. Base](#1-base)
    - [CSS resets](#css-resets)
    - [Frameworks](#frameworks)
    - [Further reading](#further-reading)
- [2. Layout](#2-layout)
    - [Further reading](#further-reading-1)
- [3. Modules](#3-modules)
    - [Further reading](#further-reading-2)
- [4. State](#4-state)
    - [Prefix classes with -is](#prefix-classes-with--is)
    - [Isnʼt it just a module?](#isnʼt-it-just-a-module)
    - [Using !important](#using-important)
    - [Further reading](#further-reading-3)
- [5. Theme](#5-theme)
    - [Further reading](#further-reading-4)

<!-- /MarkdownTOC -->





## Categorise your CSS rules

At the heart of SMACSS is categorisation. CSS rules are grouped into five categories:

1. Base
2. Layout
3. Module
4. State
5. Theme

By separating our rules into these categories it keeps our code simpler, more modular and cleaner. As Snook remarks,

> Much of the purpose of categorizing things is to codify patterns—things that
> repeat themselves within our design. Repetition results in less code, easier 
> maintenance, and greater consistency in the user experience. These are all 
> wins. Exceptions to the rule can be advantageous but they should be 
> justified.

[Source](https://smacss.com/book/categorizing "SMACSS: Categorizing CSS Rules")

Let's examine each of these categories.





## 1. Base

Base rules set the default styling for how any 'vanilla' element should look in all occurrences on the page.

These are more often than not simple element selectors (e.g. `a`, `h1`, `p`) but could also include, for example, attribute selectors (e.g. `input[type="submit"]`), pseudo-class selectors (e.g. `a:hover`, `p:first-child`) or sibling selectors (e.g. `h1 + p`).

* Base rules set default text sizes and font styles, headings, links, and body background colours (it's always a good practice to define these).
* Base rules do not include any classes or IDs.
* There should be no need to use `!important` in base styles.

An example might look like:

```
/* ==========================================================================
   1. Base
   ========================================================================== */

html,
body,
form {
    margin: 0;
    padding: 0;
}


a {
    color: rgb(0, 83, 155); /* St Andrews blue */
}

a:hover {
    color: rgb(238, 50, 36); /* St Andrews red */
}


input[type="text"] {
    border: 1px solid rgb(153, 153, 153);
}

```


### CSS resets

CSS resets (which are designed to strip out, or standardise, across all browsers the default margins, padding, and other properties) are a particular subset of base styles.

If you use a separate CSS reset (for example, Eric Meyer's [Reset CSS](http://meyerweb.com/eric/tools/css/reset/ "CSS Tools: Reset CSS") or [Normalize](http://necolas.github.io/normalize.css/ "A modern, HTML5-ready alternative to CSS resets")) then you should include this at the top of the base section before any of your own rules.

Any CSS reset / normalise code should be clearly commented indicating its version number and source URL.


### Frameworks

CSS frameworks, such as [Bootstrap](http://getbootstrap.com/) and [Foundation](http://foundation.zurb.com/), should NOT be regarded as base rules as they style far more than simple elements and often have more classes than a perpetual student.

If you need to include frameworks (whole or in part) within your stylesheet — which you may if you are `@import`-ing from numerous sources into a Sass file for production — then you should precede the base section with a section zero called `0. Framework` and include comments clearly indicating its version number and source URL.


### Further reading

* [SMACSS: Categorizing CSS rules](https://smacss.com/book/categorizing "Scalable and Modular Architecture for CSS by Jonathan Snook")
* [SMACSS: Base rules](https://smacss.com/book/type-base "Scalable and Modular Architecture for CSS by Jonathan Snook")





## 2. Layout

Layout rules define the major layout components of a page, such as header, footer, navigation, main content, and sidebar. These are the areas in which modules sit.


### Further reading

* [SMACSS: Layout rules](https://smacss.com/book/type-layout "Scalable and Modular Architecture for CSS by Jonathan Snook")





## 3. Modules

Modules are the reusable, modular components of our design. These are usually defined by distinct patterns in our digital pattern library, e.g. accordion, breadcrumps, hero banner, navbox, etc.

* Modules sit inside layout components.
* Modules can sometimes sit within other modules, too.
* Each Module should be designed to exist as a standalone component.
* Modules can easily be moved to different parts of the layout without breaking.


### Further reading

* [SMACSS: Module rules](https://smacss.com/book/type-module "Scalable and Modular Architecture for CSS by Jonathan Snook")





## 4. State

"A state is something that augments and overrides all other styles. For example, an accordion section may be in a collapsed or expanded state. A message may be in a success or error state." [Source](https://smacss.com/book/type-state "Scalable and Modular Architecture for CSS by Jonathan Snook")

State rules describe how our layouts or modules will look when in a particular state such as visible or hidden, collapsed or expanded, active or inactive, error or success.

But the state may also refer to how something looks on a larger or smaller screen, or how an element might appear in a different view such as on the homepage.


### Prefix classes with -is

Jonathan Snook's idea is that "states are generally applied to the same element as a layout rule or applied to the same element as a base module class." 

In some cases it can be very useful to prefix the class name with the verb `is-`, for example:

* `.is-hidden`
* `.is-expanded`
* `.is-active`
* `.is-inactive`


### Isnʼt it just a module?

The answer to this question is worth quoting in full:

"There is plenty of similarity between a sub-module style and a state style. They both modify the existing look of an element. However, they differ in two key ways:

1. State styles can apply to layout and/or module styles; and
2. State styles indicate a JavaScript dependency.

"It is this second point that is the most important distinction. Sub-module styles are applied to an element at render time and then are never changed again. State styles, however, are applied to elements to indicate a change in state while the page is still running on the client machine.

"For example, clicking on a tab will activate that tab. Therefore, an is-active or is-tab-active class is appropriate. Clicking on a dialog close button will hide the dialog. Therefore, an is-hidden class is appropriate."

[Source](https://smacss.com/book/type-state "Scalable and Modular Architecture for CSS by Jonathan Snook")


### Using !important

States should be stand-alone and built from one single class selector, e.g. `.is-selected`.

Use of `!important` is allowed if required, but hang back from applying it unless it is absolutely necessary.


### Further reading

* [SMACSS: State rules](https://smacss.com/book/type-state "Scalable and Modular Architecture for CSS by Jonathan Snook")
* [SMACSS: Changing state](https://smacss.com/book/state "Scalable and Modular Architecture for CSS by Jonathan Snook")





## 5. Theme

Theme rules define the colours and images of your web application or site.

Separating out theme rules allows you to very easily reuse layouts and modules across a site but apply different 'skins' to each. For example, undergraduates, postgraduates and staff pages might have the same basic layout and functionality but use different colour palettes.

It is probably self-evident that not all colour and image information needs to sit within a theme section. It can be helpful to define default colour scheme for a layout or module within their respective sections and then use theme CSS to override these later, e.g.

```
// in module-name.css
.module {
    border: 1px solid black;
}


// in theme.css
.module {
    border-colour: rgb(0, 83, 155);
}
```

or you may prefer to separate these out completely. The context should determine which approach is used.

```
// in module-name.css
.module {
    border: 1px solid;
}


// in theme.css
.module {
    border-colour: rgb(0, 83, 155);
}
```

### Further reading

* [SMACSS: Theme rules](https://smacss.com/book/type-theme "Scalable and Modular Architecture for CSS by Jonathan Snook")