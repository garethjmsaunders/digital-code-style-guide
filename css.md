# CSS standards guide

Version 0.9
Last updated: Wednesday 30 September 2015

<!-- MarkdownTOC depth=3 -->

- [1. Introduction](#1-introduction)
    - [1.1 The importance of a style guide](#11-the-importance-of-a-style-guide)
    - [1.2 When to be inconsistent](#12-when-to-be-inconsistent)
    - [1.3 Write valid CSS](#13-write-valid-css)
        - [Vendor prefixes](#vendor-prefixes)
    - [1.4 Acknowledgements](#14-acknowledgements)
- [2. File format](#2-file-format)
    - [2.1 Use multiple files, concatinate and minify](#21-use-multiple-files-concatinate-and-minify)
    - [2.2 Character encoding](#22-character-encoding)
        - [@charset "UTF-8";](#charset-utf-8)
        - [Save as UTF-8 with BOM](#save-as-utf-8-with-bom)
        - [Further reading](#further-reading)
    - [2.3 Use LF (Unix) line endings](#23-use-lf-unix-line-endings)
        - [Further reading](#further-reading-1)
    - [2.4 Filenames](#24-filenames)
        - [Meaningful and descriptive](#meaningful-and-descriptive)
        - [Lowercase, no spaces](#lowercase-no-spaces)
        - [Use a hyphen (-) to separate words](#use-a-hyphen---to-separate-words)
        - [Underscores (_) for Sass files](#underscores-_-for-sass-files)
    - [2.5 Link to external CSS files](#25-link-to-external-css-files)
        - [Link](#link)
        - [@import for debug and Sass only](#import-for-debug-and-sass-only)
        - [Do not use inline CSS](#do-not-use-inline-css)
        - [Do not use style elements](#do-not-use-style-elements)
- [3. Syntax and formatting](#3-syntax-and-formatting)
    - [3.1 Anatomy of a ruleset](#31-anatomy-of-a-ruleset)
    - [3.2 80 characters wide](#32-80-characters-wide)
    - [3.3 Block style](#33-block-style)
        - [Multi-line CSS](#multi-line-css)
        - [Indent with four (4) spaces, no tabs](#indent-with-four-4-spaces-no-tabs)
        - [Colons and semicolons, braces and spaces](#colons-and-semicolons-braces-and-spaces)
        - [List declarations in alphabetical order](#list-declarations-in-alphabetical-order)
        - [Alignment](#alignment)
    - [3.4 Meaningful whitespace](#34-meaningful-whitespace)
    - [3.5 Colours](#35-colours)
        - [Use the approved St Andrews palette of colours](#use-the-approved-st-andrews-palette-of-colours)
        - [Colour keywords - use only black and white](#colour-keywords---use-only-black-and-white)
        - [Prefer RGB over hex](#prefer-rgb-over-hex)
        - [Use short hex codes](#use-short-hex-codes)
        - [Alpha transparency - below one prefix with a zero](#alpha-transparency---below-one-prefix-with-a-zero)
    - [3.6 Syntax](#36-syntax)
        - [Use single quotation marks](#use-single-quotation-marks)
        - [Shorthand properties](#shorthand-properties)
        - [Units](#units)
        - [Zero](#zero)
    - [3.7 Don't use IE hacks](#37-dont-use-ie-hacks)
        - [Filters](#filters)
        - [IE hacks](#ie-hacks)
        - [Consider using shame.css](#consider-using-shamecss)
        - [Further reading](#further-reading-2)
- [4. Comments](#4-comments)
    - [4.1 CSS needs more comments](#41-css-needs-more-comments)
    - [4.2 General advice](#42-general-advice)
    - [4.3 Sass comments](#43-sass-comments)
        - [Further reading](#further-reading-3)
    - [4.4 Every CSS file must have...](#44-every-css-file-must-have)
        - [File information](#file-information)
        - [Table of contents](#table-of-contents)
        - [Section titles](#section-titles)
    - [4.5 Magic numbers](#45-magic-numbers)
    - [4.6 High-level comments](#46-high-level-comments)
    - [4.7 Object–extension pointers](#47-object–extension-pointers)
    - [4.8 Reverse footnote comments](#48-reverse-footnote-comments)
    - [4.9 Preprocessor comments](#49-preprocessor-comments)
- [5. Rule organisation](#5-rule-organisation)
    - [5.1 Categorise your CSS rules](#51-categorise-your-css-rules)
        - [1. Base](#1-base)
        - [2. Layout](#2-layout)
        - [3. Modules](#3-modules)
        - [4. State](#4-state)
        - [5. Theme](#5-theme)
    - [5.2 Further reading](#52-further-reading)
- [6. Naming conventions](#6-naming-conventions)
    - [6.1 Naming](#61-naming)
    - [6.2 Naming UI components](#62-naming-ui-components)
    - [6.3 Accepted characters in class and ID names](#63-accepted-characters-in-class-and-id-names)
        - [Characters to avoid](#characters-to-avoid)
    - [6.4 Hyphen delimited](#64-hyphen-delimited)
    - [6.5 BEM-like naming](#65-bem-like-naming)
        - [Starting context](#starting-context)
    - [6.6 Modifying elements](#66-modifying-elements)
    - [6.7 Naming conventions in HTML](#67-naming-conventions-in-html)
    - [6.8 JavaScript hooks](#68-javascript-hooks)
        - [Do not use HTML5 data-* attributes as JavaScript hooks](#do-not-use-html5-data--attributes-as-javascript-hooks)
- [7. CSS Selectors](#7-css-selectors)
    - [7.1 General rules](#71-general-rules)
    - [7.2 Selector intent](#72-selector-intent)
    - [7.3 Specificity](#73-specificity)
        - [Keep specificity low at all times](#keep-specificity-low-at-all-times)
        - [Do not use !important as a hack](#do-not-use-important-as-a-hack)
        - [Use !important proactively not reactively](#use-important-proactively-not-reactively)
        - [Hacking specificity](#hacking-specificity)
    - [7.4 Reusability](#74-reusability)
        - [Location independence](#location-independence)
        - [Portability](#portability)
        - [Object-orientation](#object-orientation)
        - [The single responsibility principle](#the-single-responsibility-principle)
        - [Open to extension / closed to modification](#open-to-extension--closed-to-modification)
        - [The separation of concerns](#the-separation-of-concerns)
        - [DRY](#dry)
    - [7.5 Selector performance](#75-selector-performance)
        - [The key selector](#the-key-selector)
    - [7.6 Further reading](#76-further-reading)

<!-- /MarkdownTOC -->


---


# 1. Introduction

These CSS guidelines are applicable to all websites and web applications created and managed by and for the University of St Andrews under the st-andrews.ac.uk domain.


## 1.1 The importance of a style guide

As Harry Roberts writes in [CSS Guidelines](http://cssguidelin.es/#introduction):

"CSS is not a pretty language. While it is simple to learn and get started with, it soon becomes problematic at any reasonable scale. There isn't much we can do to change how CSS works, but we can make changes to the way we author and structure it.

"In working on large, long-running projects, with dozens of developers of differing specialities and abilities, it is important that we all work in a unified way in order to, among other things:

*   **keep stylesheets maintainable**;
*   **keep code transparent, sane, and readable**;
*   **keep stylesheets scalable**.

"There are a variety of techniques we must employ in order to satisfy these goals."

This CSS style guide contains recommendations and approaches that will help us to acheive these goals.

Roberts continues, "a coding style guide (note, not a visual style guide) is a valuable tool for teams who:

*   build and maintain products for a reasonable length of time;
*   have developers of differing abilities and specialisms;
*   have a number of different developers working on a product at any
    given time;
*   on-board new staff regularly;
*   have a number of codebases that developers dip in and out of.

"While style guides are typically more suited to product teams—large codebases on long-lived and evolving projects, with multiple developers contributing over prolonged periods of time—all developers should strive for a degree of standardisation in their code.

"A good style guide, when well followed, will:

*   **set the standard for code quality across a codebase**;
*   **promote consistency across codebases**;
*   **give developers a feeling of familiarity across codebases**;
*   **increase productivity**.

"Style guides should be learned, understood, and implemented at all times on a project which is governed by one, and any deviation must be fully justified."

Source: [CSS Styleguide](http://cssguidelin.es/#the-importance-of-a-styleguide "Harry Roberts")




## 1.2 When to be inconsistent

While consistency is important, equally important is knowing when to be inconsistent—sometimes the style guide just doesn’t apply.

Ask yourself if applying the rule would make the code less readable, even for someone who is used to reading code that follows the rules. When in doubt use your best judgment, look at other examples, and decide what looks best.

The ground rule is simple: **readability is preferential to strict adherence to rules**.




## 1.3 Write valid CSS

Ideally, all CSS code should validate to the latest CSS specification for which it is written.

The [W3C CSS validation service](http://jigsaw.w3.org/css-validator/) is a useful resource. You may also find CSS validators that integrate with your code editor of choice, or your browser.


### Vendor prefixes

There are occasions when this is not possible, for example in CSS3 vendor-specific prefixes (e.g. `-webkit-`, `–moz-`, `-ms-`, `-o-`) are permitted. 

As Andy Clarke says in _Hardboiled Web Design_ (2010):

> using [vendor-specific prefixes] will render a style sheet technically
> invalid, but you should know by now that validation is a tool, not a 
> religion. An invalid style sheet is a small price to pay for all we can 
> achieve using emerging CSS3 standards.




## 1.4 Acknowledgements

This style guide draws heavily on the work of Harry Roberts’ work at [CSS guidelines: High-level advice and guidelines for writing sane, manageable, scalable CSS](http://cssguidelin.es/).

As Roberts says, "These guidelines are opinionated, but they have been repeatedly tried, tested, stressed, refined, broken, reworked, and revisited over a number of years on projects of all sizes."

This has been used with his permission: "There isn’t an actual license in place for CSS Guidelines (if there was I suppose it would be Apache 2) but take this in writing as permission to slice and dice it to for your needs, provided there is reasonable attribution :)"


---


# 2. File format

This section outlines standards for creating and saving CSS files to ensure that they are not affected by encoding or file system differences. There is also general information about linking to external CSS files.


## 2.1 Use multiple files, concatinate and minify

With the meteoric rise of pre-processors (such as Sass and Less) of late, more often is the case that developers are splitting CSS across multiple files. Even if not using a pre-processor, it is a good idea to split discrete chunks of code into their own files, which can then be concatenated and minified during a build process. \[[HR](http://cssguidelin.es/#multiple-files)\]




## 2.2 Character encoding

Although rare, it is worth bearing in mind that character encoding can affect CSS files. According to the [W3C](http://www.w3.org/International/questions/qa-css-charset):

> You should always use UTF-8 as the character encoding of your style sheets 
> and your HTML pages, and declare that encoding in your HTML. If you do that, 
> there is no need to declare the encoding of your stylesheet.
>
> Other approaches are only needed if your style sheet contains non-ASCII 
> characters and, for some reason, you can't rely on the encoding of the HTML 
> and the associated stylesheet to be the same. In this case you should use 
> `@charset` or HTTP headers to declare the encoding. (If your HTML and CSS 
> files use the same encoding, the latest versions of major browsers will 
> apply the encoding of the HTML file to the CSS stylesheet.)

We recommend that you both **set the character encoding within the stylesheet** and then **save the file in the UTF-8 encoding**.


### @charset "UTF-8";

To set the character encoding inside the stylesheet, use the following sequence of bytes **at the very start of the file**, one byte per character:

```
@charset "UTF-8";
```

Only one `@charset` byte sequence may appear in an external style sheet and it must appear at the very start of the document. It must not be preceded by any characters, not even comments.

Accompanying HTML files should similarly have the character encoding set by adding a `<meta charset="utf-8>"` element to the head of the document.


### Save as UTF-8 with BOM

Files should be saved with Unicode (UTF-8) encoding; saving with the byte-order mark (UTF-8 with BOM) is optional, but recommended.

The CSS3 syntax specification indicates that if you have a UTF-8 byte-order mark (BOM) at the start of your file then this should cause the browser to read the stylesheet as UTF-8 regardless of any other declaration. This is not, however, currently supported universally. IE 10 and IE 11 still give higher precedence to the HTTP header and `@charset` declaration. 

If given the option, use Unicode normalization form C (also known as 'NFC'). The W3C recommends the use of NFC normalized text on the Web. 

### Further reading

*   [Declaring character encodings in CSS (W3C)]
        (http://www.w3.org/International/questions/qa-css-charset)
*   [Normalization in HTML and CSS (W3C)]
        (http://www.w3.org/International/questions/qa-html-css-normalization)
*   [The byte-order mark (BOM) in HTML]
        (http://www.w3.org/International/questions/qa-byte-order-mark)
*   [Unicode FAQ on Normalization (Unicode Consortium)]
        (http://unicode.org/faq/normalization.html)




## 2.3 Use LF (Unix) line endings

Line feed (LF) Unix style line endings (sometimes called line breaks) should be used.

This is more of an issue for developers who work in Windows, but in any case ensure that your text editor is set up to save files with Unix line breaks.
For example, in Sublime Text you can add the following to your user settings: 

```
    "default_line_ending": "LF",
```

### Further reading

*   [The Great Newline Schism]
        (http://blog.codinghorror.com/the-great-newline-schism/)




## 2.4 Filenames

### Meaningful and descriptive

Filenames MUST be meaningful and descriptive, e.g. `external-02-standard.css` rather than `xtn-02s.css`. It can be useful to prefix the name of the project to the CSS file, e.g. `divinity-external-02-standard.css`.

If concatinated and minified most production files will be called something short anyway, e.g. `screen.css`.


### Lowercase, no spaces

Filenames MUST be all lowercase, with no spaces. This makes them easier to read and prevents links that substitute `%20` codes for spaces.


### Use a hyphen (-) to separate words

Use a hyphen (`-`) to separate words, e.g. `external-stylesheet.css`. This makes filenames easier to read than `externalstylsheetalloneword.css`.


### Underscores (_) for Sass files

Underscores (`_`) may be used only for naming Sass or Less partial files.




## 2.5 Link to external CSS files

All CSS files SHOULD be referenced externally because it enables caching control and makes the HTML smaller.


### Link
External CSS MUST be referenced via the `link` element, which MUST be placed in the head section of the document before any links to JavaScript and as close as possible to the top, but after the `title` element. This will improve performance and not impede SEO.

```
<link rel="stylesheet" type="text/css" href="filename.css" />
```

### @import for debug and Sass only
External CSS MUST NOT be imported using `@import` because it impairs caching and blocks rendering.

Debug files and pre-processor source files (e.g. Sass) are the only exceptions to this rule. `@import` rules must appear before any other rules in the document. You may include (and in fact are recommended) to include comments before the `@import` rules.


### Do not use inline CSS
You MUST NOT use inline styles. To do so makes these rules uncacheable and inconsistent. And it makes the HTML pages larger.

Inline styles MAY BE used where necessary to debug, but ALWAYS then move the code into linked stylesheets.


### Do not use style elements

Document head CSS (between `style` tags) SHOULD NOT be used Where a style rule is only required for a specific page. To do so makes these rules uncacheable and inconsistent.

Avoid using embedded styles which control the style of only one page; also avoid using `@import` rules within a style block.


---


# 3. Syntax and formatting

One of the simplest forms of a style guide is a set of rules regarding syntax and formatting. Having a standard way of writing CSS means that code will always look and feel familiar to all members of the team: consistency is key.

Further, code that looks clean feels clean. It is a much nicer environment to work in, and prompts other team members to maintain the standard of cleanliness that they found. Ugly code sets a bad precedent.

Source: [CSS guidelines](http://cssguidelin.es/#syntax-and-formatting "Harry Roberts")


## 3.1 Anatomy of a ruleset

Before we discuss how we write out our rulesets, let's first familiarise ourselves with the relevant terminology.

Every CSS rule has two parts: 

1.   a selector
2.   a declaration block, containing one or more declarations.

This is a RULE:

```
h1, h2,
.foo, .foo-bar,
# baz {
    background-color: green;
    color: red;
    display: block;
}
```

These are SELECTORS:

```
h1, h2,
.foo, .foo-bar,
#baz
```

This is a DECLARATION BLOCK:

```
{
    background-color: green;
    color: red;
    display: block;
}
```

This is a DECLARATION:

```
    background-color: green;
```

Each declaration is a pairing of a property name and a property value separated by a colon, and concluding with a semi-colon.

Property-name     `background-color`
Property-value    `green`




## 3.2 80 characters wide

Where possible, **limit CSS files' width to 80 characters**. Reasons for this include:

*   the ability to have multiple files open side by side;
*   viewing CSS on sites like GitHub, or in a terminal window;
*   providing a comfortable line length for comments.

```
/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
 * such a long comment that I easily break the 80 character limit, so I am
 * broken across several lines.
 */
```

Do not worry about unavoidable exceptions to this rule, such as URLs, or gradient syntax.




## 3.3 Block style

### Multi-line CSS

**CSS should be written across multiple lines**, except in very specific circumstances. There are a number of benefits to this:

*   A reduced chance of merge conflicts, because each piece of functionality
    exists on its own line.
*   More 'truthful' and reliable diffs, because one line only ever carries 
    one change.

Exceptions to this rule should be fairly apparent, such as similar rulesets that only carry one declaration each, for example:

```
.icon {
    display: inline-block;
    width:  16px;
    height: 16px;
    background-image: url(/img/sprite.svg);
}

.icon--home     { background-position:   0     0  ; }
.icon--person   { background-position: -16px   0  ; }
.icon--files    { background-position:   0   -16px; }
.icon--settings { background-position: -16px -16px; }
```

These types of ruleset benefit from being single-lined because:

*   they still conform to the one-reason-to-change-per-line rule;
*   they share enough similarities that they don't need to be read as
    thoroughly as other rulesets—there is more benefit in being able to scan their selectors, which are of more interest to us in these cases.

Source: [CSS guidelines](http://cssguidelin.es/#multi-line-css "Harry Roberts")


### Indent with four (4) spaces, no tabs

**The purpose of indentation is to improve the legibility of the code** and optionally to also understand the structure of the HTML documents being styled.

The debates about tabs-vs-spaces and two-vs-four-spaces are much older than CSS development. What matters though are:

*   Consistency in documents and across projects
*   Code legibility

With this in mind we recommend:

*    **Indent declarations with four (4) spaces**.
*    **Never mix tabs and spaces**. Code indented with a mixture of tabs and 
     spaces should be converted to using spaces only; if your coding editor allows, set the option to convert tabs to spaces.

As well as intending individual declarations, **you may indent entire related rulesets to signal their relation to one another**, for example:

```
.foo {
    // code
}

    .foo__bar {
        // code
    }

        .foo__baz {
            // code
        }
```

By doing this, a developer can see at a glance that `.foo__baz {}` lives inside `.foo_bar {}` lives inside `.foo {}`.

This quasi-replication of the DOM tells developers a lot about where classes are expected to be used without them having to refer to a snippet of HTML.


#### Indenting Sass (SHOULD WE HAVE A SEPARATE Sass guide?)
Sass provides nesting functionality. That is to say, by writing this:

```
.foo {
    color: red;

    .bar {
        color: blue;
    }

}
```

…we will be left with this compiled CSS:

```
.foo { color: red; }
.foo .bar { color: blue; }
```

When indenting Sass, we stick to the same four (4) spaces, and we also leave a blank line before and after the nested ruleset.

N.B. Nesting in Sass should be avoided wherever possible. See the Specificity section for more details.


### Colons and semicolons, braces and spaces

Consider this example rule:

```
.foo, .foo-bar,
.baz {
    background-color: green;
    color: red;
    display: block;
}
```

Here you can see we have:

*   Related selectors on the same line; unrelated selectors on new lines.
*   The opening brace ({) on the same line as the last selector.
*   A space before the opening brace ({).
*   Each declaration on its own new line; the first declaration on a new line 
    after the opening brace ({);
*   Properties and values on the same line.
*   No space between the property-name and colon (:).
*   A space after the property–value delimiting colon (:).
*   Each declaration indented by four (4) spaces;
*   A trailing semi-colon (;) MUST be included after our last declaration; this
    enables authors to add new declarations after it without the possibility of
    missing colons introducing errors.
*   The closing brace (}) must be on its own new line using the same level of 
    indentation as its opening selectors.

This format seems to be the largely universal standard, except for variations in number of spaces, many developers prefer two (2).

Source: [CSS Guidelines "Harry Roberts"](http://cssguidelin.es/#anatomy-of-a-ruleset "Harry Roberts")


### List declarations in alphabetical order

Multiple selectors should be listed in alphabetical order as this makes it much easier to find declaration blocks.

For example:

```
.foo {
    border-top: 1px solid rgb(224, 224, 224);
    color: black;
    display: block;
    line-height: 22px;
    margin: 0;
    overflow: hidden;
    text-decoration: none;
    width: 180px;
}
```


#### Positioned elements

An exception is where elements are being positioned on the page. In this case it can help to group the `top`, `right`, `bottom`, and `left` declarations (in that order) immediately after `position`:

```
.foo {
    border-top: 1px solid black;
    color: black;
    display: block;
    line-height: 22px;
    margin: 0;
    overflow: hidden;
    position: absolute;
        top:    0;
        right:  0;
        bottom: 0;
        left:   0;
    text-decoration: none;
    width: 180px;
}
```


#### Vendor prefixes

Another exception is prefixed vendor-specific property pairs which should appear directly before the generic property to which they refer. This allows newer browsers that support the W3C standards to use the final declaration.

```
.foo {
    border: 1px solid black;
    -webkit-box-shadow: 0 3px 3px rgba(0, 0, 0, 0.2);
       -moz-box-shadow: 0 3px 3px rgba(0, 0, 0, 0.2);
        -ms-box-shadow: 0 3px 3px rgba(0, 0, 0, 0.2);
         -o-box-shadow: 0 3px 3px rgba(0, 0, 0, 0.2);
            box-shadow: 0 3px 3px rgba(0, 0, 0, 0.2);
    display: none;
    float: left;
}
```

It can greatly aid readability if the prefixes are ordered from longest to shortest: `-webkit-`, `-moz-`, `-ms-`, `-o-`.


### Alignment

Attempt to align common and related identical strings in declarations, for example:

```
.foo {
    -webkit-border-radius: 3px;
       -moz-border-radius: 3px;
            border-radius: 3px;
}

.bar {
    position: absolute;
    top:    0;
    right:  0;
    bottom: 0;
    left:   0;
    margin-right: -10px;
    margin-left:  -10px;
    padding-right: 10px;
    padding-left:  10px;
}
```

This makes life a little easier for developers whose text editors support column editing, allowing them to change several identical and aligned lines in one go.

Source: [CSS Guidelines](http://cssguidelin.es/#alignment "Harry Roberts")




## 3.4 Meaningful whitespace

As well as indentation, we can provide a lot of information through liberal and judicious use of whitespace between rulesets. We use:

*   One (1) empty line between closely related rulesets.
*   Two (2) empty lines between loosely related rulesets.
*   Five (5) empty lines between entirely new sections.

For example:

```
/*------------------------------------*\
    FOO
\*------------------------------------*/

.foo {}

    .foo__bar {}


.foo--baz {}




/*------------------------------------*\
    BAR
\*------------------------------------*/

.bar {}

    .bar__baz {}

    .bar__foo {}
```

There should never be a scenario in which two rulesets do not have an empty line between them. This would be incorrect:

```
.foo {}
    .foo__bar {}
.foo--baz {}
```

Source: [CSS Guidelines](http://cssguidelin.es/#meaningful-whitespace)




## 3.5 Colours

### Use the approved St Andrews palette of colours

Unless you have a very good reason not to, you must use the approved palette of St Andrews colours.


### Colour keywords - use only black and white

The [CSS Color Module Level 3](http://www.w3.org/TR/css3-color/#html4) specification defines 16 basic colour keywords: aqua, black, blue, fuchsia, gray, green, lime, maroon, navy, olive, purple, red, silver, teal, white, and yellow.

You may use only `black` and `white`; although consider this article [Design tip: never use black](http://ianstormtaylor.com/design-tip-never-use-black/) by Ian Storm Taylor. Do not use the other values, except in debug files.


### Prefer RGB over hex

Use `rgb(r, g, b)` and `rgba(r, g, b, a)` codes for colours; there must be a space after each comma.

The reason for preferring RGB is three-fold:

1.   Colours in RGB format are easier to guess.
2.   It is quicker to add transparency if required (see alpha transparency)
     below.
3.   RGB format is more widely supported in graphic design applications.

To expand on the first point, while colours on the web have traditionally been specified using hex codes (e.g. St Andrews Blue is `#00539b`) it is not as easy to estimate the colour just by looking at the code, unless you can convert hex to decimal in your head. For example, at a glance `rgb(0, 83, 155)` has about 60% blue and 30% green so you may safely estimate that this is dark blue.

There is a current trend to prefer HSL over RGB as it allows you to more easily make them lighter or darker. With a fixed pallette, such as ours, we don't need this.


### Use short hex codes

If you must use hex codes: shorten values where possible (`#fff` instead of `#ffffff`) and use lowercase alphabetical values (`#fff` not `#FFF`).


### Alpha transparency - below one prefix with a zero

Specifying colours in `rgb(r, g, b)` format also makes it much easier to add alpha transparency later, as you simply need to append an ‘a’ and a fourth value:

```
.black {
    background-color: rgb(0, 0, 0);
}

.darkglass {
    background-color: rgba(0, 0, 0, 0.5);
}
```

Alpha values below one MUST always begin with a zero (`0.75` rather than `.75`); without a zero it can trigger errors in CSS pre-processors.

If the alpha value is 1 then simply use `rgb(r, g, b)` rather than `rgba(r, g, b, 1);`.




## 3.6 Syntax

### Use single quotation marks

In CSS quotation marks are optional, however, languages that do not require strings to be quoted are a minority. **Always use single quotes** unless there is a compelling reason to not use, for example to greatly aid clarity.

It is preferable to use single quotes for CSS and double-quotes for HTML so that you may easily drop CSS code into inline styles:

```
<div style="background-image: url('img.gif');"> [...] </div>
```

Not that you should be using inline CSS, you understand!


#### Font-family

Use single-quotes in a `font-family` declaration (or in the shorthand `font` declaration) when listing a font name that has spaces in it, or if the font name includes non-alphanumeric characters such as the symbols '#' or '$'.

By consistently using single-quotes for this type of declaration you can use the same code in both external and in-line styles without needing to edit it.

```
h1 {
    font-family: 'Times New Roman', Times, serif;
}

h2 {
    font-family: '$dollarfont';
}

<h1 style="font-family: 'Times New Roman', Times, serif;">...
```


#### URLs

**Do not use quotations marks in URL values.**

```
@embed url(http://www.st-andrews.ac.uk/code/framework.css);
```

There may be situations where the URL contains characters that would otherwise need to be escaped, such as parentheses, white space characters, single quotes (') or double quotes(").

In these cases use the most appropriate quotation mark to aid clarity without needing to escape anything; if in doubt, use single quotes.


### Shorthand properties

Use of shorthand properties is generally discouraged as they are harder to read for non-experts; exceptions are noted below. Priority should be given to code readability and scanability.

Compare the following for clarity:

```
.unclear {
    font: 1em/1.1em bold italic small-caps Verdana, Arial, Helvetica, sans-serif;
}

.clearer {
    font-family:  Verdana, Arial, Helvetica, sans-serif;
    font-size:    1em;
    font-style:   italic;
    font-variant: small-caps;
    font-weight:  bold;
    line-height:  1.1em;
}
```

The following exceptions may be made for using shorthand properties due to their wide-spread use.


#### Background

```
selector {
    background: bg-color bg-image bg-repeat bg-attachment bg-position;
}

div {
    background: rgb(0, 83, 155) url('img/bg.png') no-repeat fixed left bottom;
}
```


#### Border

```
selector {
    border-width border-style border-color;
}

div {
    border: 1px solid #000;
}
```


#### List-style

```
selector {
    list-style: list-style-type list-style-image list-style-position;
}

div {
    list-style: square url(img/bullet.png) outer;
}

```


#### Margin and padding

When specifying margin and padding you MUST use either

*   Two values  (`[top/bottom] [left/right]`), or
*   Four values (`[top], [right], [bottom], [left]`)

```
selector {
    margin:  [top/bottom] [left/right];
    padding: [top], [right], [bottom], [left];
}

div {
    margin:  5px 10px;
    padding: 1px 2px 3px 4px;
}
```

NEVER use three values as it is not immediately obvious what this means; it is actually `[top], [right/left], [bottom]`.


### Units

Consider using `rem` (which sizes elements relative to the `body` element) instead of `px` when sizing fonts, line-heights, etc.

Do not use units with `line-height`; a raw number assigns a scaling factor.

```
element {
    line-height: 2;       /* Correct */
    line-height: 24px;    /* Incorrect */
}
```


### Zero

When a length value is zero (0) do not use a unit designator. Zero is always zero regardless of how you measure it.

```
.example {
    margin:  10px 0;     // Correct
    padding: 10px 0px    // Incorrect
}
```




## 3.7 Don't use IE hacks

### Filters

Do not use Microsoft Internet Explorer filters, e.g. 

```
-ms-filter : "progid:DXImageTransform.Microsoft.Alpha(opacity=50)";
```

as these can have a serious negative impact on a website's performance.


### IE hacks

Try to not use other [browser-specific hacks](http://browserhacks.com/ "Browser hacks") for Internet Explorer. But if you must then these must be served from a separate style sheet, targetted using an IE conditional, e.g.

```
<!--[if IE]>
<link rel="stylesheet" type="text/css" href="ie.css">
<![endif]-->
```


### Consider using shame.css

Consider Harry Roberts, Chris Coyier, and Dave Rupert's idea of a [shame.css](http://csswizardry.com/2013/04/shame-css/ "Article from 17 April 2013") file that groups all "bodges, hacks and quick-fixes in their own file". Their reasons are:

1. You make them stick out like a sore thumb.
2. You keep your 'main' codebase clean.
3. You make developers aware that their hacks are made very visible.
4. You make them easier to isolate and fix.
5. `$ git blame shame.css`.


### Further reading

* [Microsoft Developer Network](https://msdn.microsoft.com/en-us/library/ms537512%28v=vs.85%29.aspx)
* [Quirksmode](http://www.quirksmode.org/css/condcom.html)


---


# 4. Comments

As Harry Roberts points out in his [CSS Guidelines](http://cssguidelin.es/) document: "CSS needs more comments".


## 4.1 CSS needs more comments

The cognitive overhead of working with CSS is huge. With so much to be aware of, and so many project-specific nuances to remember, the worst situation most developers find themselves in is being the-person-who-didn't-write-this-code. Remembering your own classes, rules, objects, and helpers is manageable to an extent, but anyone inheriting CSS barely stands a chance.

**CSS needs more comments.**

As CSS is something of a declarative language that doesn't really leave much of a paper-trail, it is often hard to discern—from looking at the CSS alone:

*   whether some CSS relies on other code elsewhere;
*   what effect changing some code will have elsewhere;
*   where else some CSS might be used;
*   what styles something might inherit (intentionally or otherwise);
*   what styles something might pass on (intentionally or otherwise);
*   where the author intended a piece of CSS to be used.

This doesn't even take into account some of CSS's many quirks—such as various sates of `overflow` triggering block formatting context, or certain transform properties triggering hardware acceleration—that make it even more baffling to developers inheriting projects.

As a result of CSS not telling its own story very well, it is a language that really does benefit from being heavily commented.

Source: [CSS Guidelines](http://cssguidelin.es/#commenting "Harry Roberts")




## 4.2 General advice

Write comments as complete, grammatical sentences with an initial capital and a full-stop at the end. (The only exception to initial capital is class and ID identifiers.)

As a rule, you should comment anything that isn't immediately obvious from the code alone. These could be explaining:

* the structure and/or role of a file;
* the goal of a ruleset;
* the idea behind a 'magic number';
* the reason for a CSS declaration;
* the order of CSS declarations;
* the thought process behind a way of doing things.

That is to say, there is no need to tell someone that `color: red;` will make something red, but if you're using `overflow: hidden;` to clear floats—as opposed to clipping an element's overflow—this is probably something worth documenting.

It should go without saying, **keep comments up-to-date when code changes**.

**No comments should make their way into production environments**. All CSS should be minified, resulting in loss of comments, before being deployed.




## 4.3 Sass comments

If you are using [Sass](http://sass-lang.com/) please take note of the following distinction between the two type of comments used within Sass:

1.   Standard, multi-line CSS comments (`/* comment */`) remain visible after 
     the code has been compiled.
2.   Single-line comments (`// comment`) are removed from production code 
     after the script has been executy.


### Further reading

* [Comments: /* */ and //](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#comments)
* [Commenting on Sass Guidelines](http://sass-guidelin.es/#commenting)




## 4.4 Every CSS file must have...

Every CSS file MUST have the following comment blocks:

*   File information at the top of the file.
*   Table of contents.
*   Section titles.


### File information

All CSS files should begin with the following standard template to describe the file. This follows the CSSdoc conventions for commenting.

See [CSS Automatic Documentation](https://github.com/Paratron/CSSdoc)

At least the version number should be updated every time you make a change, especially once the file goes into production.

TODO: This is currently a combination of docblock and CSSdoc -- is that okay?
TODO: What information is required here?
TODO: Add release date?

```
/**
 * Stylesheet title
 * 
 * Long description about the file, what it is for, its scope, and
 * optionally when it may expire. The description should consist of
 * normal sentences with punctuation.
 *
 * @project     Project name
 * @version     1.0
 * @author      gjms1
 * @copyright   2014
 * @license     Apache 2.0
*/
```


####@project
Use this tag to describe the name of the project; in other words, what this CSS file is being used for.


####@version
Can be used on modules and elements to show the revision they are currently in.    
Example:

    @version 12

You may as well append a date after the version number.

    @version: 12 2011-10-26


####@author
Use this tag to define an author for an element. It can either be only the authors' name, or append a connection in <> brackets. Example:

    @author Gareth J M Saunders <gjms1@st-andrews.ac.uk>

The following connections are recognized: URL (http://example.com), email (hello@example.com), Twitter handle (@example) 
The tag can be used multiple times.


####@copyright
This tag is used to apply copyright information to the CSS document.    
It can be used on the project definition block. Example:

    @copyright Copyright (c) 2015 University of St Andrews


####@license
This displays a hyperlink to a url for a license. Can be used in the project definition block. It is made of two parts: the URL and a title, separated by comma. Example:

    @license http://opensource.org/licenses/gpl-license.php, GNU Public License


####@since
Can be used on modules and elements to show in which revision they have been implemented. Example:

    @since 3.0


####@deprecated
This indicates that the following element is, or will be deprecated in the future. Define a upcoming version number to indicate that the element will be deprecated then. Example:

    @deprecated 18.0

Alternatively any string can be placed as well:

    @deprecated Will be used no more since 2011-11-13


####@example
Can be used on the project, modules and elements to link to a real world example where the styles are used. Example:

    @example http://example.com/contact.html


####@TODO
The TODO marker indicates if something has to be done on either projects, modules or elements.     
Example:

    @TODO Make layout responsive


### Table of contents

A table of contents is a fairly substantial maintenance overhead, but the benefits it brings far outweigh any costs. It takes a diligent developer to keep a table of contents up to date, but it is well worth sticking with. An up-to-date table of contents provides a team with a single, canonical catalogue of what is in a CSS project, what it does, and in what order.

A simple table of contents will—in order, naturally—simply provide the name of the section and a brief summary of what it is and does, for example:

```
/**
 * CONTENTS
 *
 * SETTINGS
 * Global...............Globally-available variables and config.
 *
 * TOOLS
 * Mixins...............Useful mixins.
 *
 * GENERIC
 * Normalize.css........A level playing field.
 * Box-sizing...........Better default `box-sizing`.
 *
 * BASE
 * Headings.............Single element selectors, e.g. H1–H6 styles.
 *
 * LAYOUT
 * Page-head............The main page header.
 * Page-foot............The main page footer.
 *
 * MODULES
 * Patterns.............Reusable, modular parts of the design.
 * Buttons..............Button elements.
 *
 * STATE RULES
 * States...............Hidden or expanded, active or inactive.
 */
```

Each item maps to a section and/or include.

Naturally, this section would be substantially larger on the majority of projects, but hopefully we can see how this section—in the master stylesheet—provides developers with a project-wide view of what is being used where, and why.


TODO: How about this, adapted from https://sublime.wbond.net/packages/CSS%20Comments
TODO: What about prefixing the names with a character, e.g. $ from http://csswizardry.com/2012/04/my-html-css-coding-style/ or =, e.g. `$MODULES` or `=MODULES`.

```
/* ==========================================================================
   Section comment block
   ========================================================================== */


/* Sub-section comment block
   --------------------------------------------------------------------------
   */



/* ==========================================================================
   MODULES
   ========================================================================== */


/* ==========================================================================
   LAYOUT
   ========================================================================== */


/* Accordion pattern
   --------------------------------------------------------------------------
   This area is used right underneath the page head menu.
   It increases the color contrast and font size of the child elements (h1, p).
   The intro area is a bit darker than the rest of the page to make it pop out.

   @TODO Add rounded corners - looks nicer.
   @package content
   @since 2   
   */
```


### Section titles

Begin every new major section of a CSS project with a title:


This is Harry Roberts' style:

```
/*------------------------------------*\
    SECTION-TITLE
\*------------------------------------*/

.selector {}
```

```
c-
```


@TODO It might make sense to use the CSSdoc convention here, to keep things consistent, e.g.

```
*------------------------------------
    Introducional area
    This area is used right underneath the page head menu.
    It increases the color contrast and font size of the child elements (h1, p).
    The intro area is a bit darker than the rest of the page to make it pop out.

    @TODO Add rounded corners - looks nicer.
    @package content
    @since 2
*/
```


The title of the section is prefixed with a hash () symbol to allow us to perform more targeted searches (e.g. grep, etc.): instead of searching for just SECTION-TITLE—which may yield many results—a more scoped search of SECTION-TITLE should return only the section in question.

Leave a carriage return between this title and the next line of code (be that a comment, some Sass, or some CSS).

If you are working on a project where each section is its own file, this title should appear at the top of each one. If you are working on a project with multiple sections per file, each title should be preceded by five (5) carriage returns. This extra whitespace coupled with a title makes new sections much easier to spot when scrolling through large files:

```
/*------------------------------------*\
    A-SECTION
\*------------------------------------*/

.selector {}





/*------------------------------------*\
    ANOTHER-SECTION
\*------------------------------------*/

/**
 * Comment
 */

.another-selector {}
```




## 4.5 Magic numbers

"Magic number" is an old school programming term for an unnamed numerical constant. Basically, it’s just a random number that happens to _just work_™ yet is not tied to any logical explanation.

Needless to say, magic numbers are a plague and should be avoided at all costs. When you cannot manage to find a reasonable explanation for why a number works, add an extensive comment explaining how you got there and why you think it works. Admitting you don’t know why something works is still more helpful to the next developer than them having to figure out what's going on from scratch.

```
/**
 * 1. Magic number. This value is the lowest I could find to align the top
 *    of `.foo` with its parent. Ideally, we should fix it properly.
 */

.foo {
  top: 0.327em; /* [1] */
}
```

See also

* [Sass styleguide CSS ](http://sass-guidelin.es/#magic-numbers)
* [Magic numbers in CSS](http://css-tricks.com/magic-numbers-in-css/)


## 4.6 High-level comments

For large comments that document entire sections or components, we use a DocBlock-esque multi-line comment which adheres to our 80 column width.
Here is a real-life example from the CSS which styles the page header on [CSS Wizardry](http://csswizardry.com): 

"Front-end architecture and performance engineering by Harry Roberts"

```
/**
 * The site's main page-head can have two different states:
 *
 * 1) Regular page-head with no backgrounds or extra treatments; it just
 *    contains the logo and nav.
 * 2) A masthead that has a fluid-height (becoming fixed after a certain point)
 *    which has a large background image, and some supporting text.
 *
 * The regular page-head is incredibly simple, but the masthead version has 
 * some slightly intermingled dependency with the wrapper that lives inside it.
 */
```

This level of detail should be the norm for all non-trivial code—descriptions of states, permutations, conditions, and treatments.




## 4.7 Object–extension pointers

When working across multiple partials, or in an OOCSS (object-oriented CSS) manner, you will often find that rulesets that can work in conjunction with each other are not always in the same file or location. For example, you may have a generic button object—which provides purely structural styles—which is to be extended in a component-level partial which will add cosmetics. We document this relationship across files with simple object–extension pointers. In the object file:

```
/**
 * Extend `.btn {}` in _components.buttons.scss.
 */

.btn {}
```

And in your theme file:

```
/**
 * These rules extend `.btn {}` in _objects.buttons.scss.
 */
.btn--positive {}
.btn--negative {}
```

This simple, low effort commenting can make a lot of difference to developers who are unaware of relationships across projects, or who are wanting to know how, why, and where other styles might be being inherited from.




## 4.8 Reverse footnote comments

Oftentimes we want to comment on specific declarations (i.e. lines) in a ruleset. To do this we use a kind of reverse footnote. Here is a more complex comment detailing the larger site headers mentioned above:

```
/**
 * Large site headers act more like mastheads. They have a faux-fluid-height
 * which is controlled by the wrapping element inside it.
 *
 * 1. Mastheads will typically have dark backgrounds, so we need to make sure
 *    the contrast is okay. This value is subject to change as the background
 *    image changes.
 * 2. We need to delegate a lot of the masthead's layout to its wrapper element
 *    rather than the masthead itself: it is to this wrapper that most things
 *    are positioned.
 * 3. The wrapper needs positioning context for us to lay our nav and masthead
 *    text in.
 * 4. Faux-fluid-height technique: simply create the illusion of fluid height
      by creating space via a percentage padding, and then position everything 
      over the top of that. This percentage gives us a 16:9 ratio.
 * 5. When the viewport is at 758px wide, our 16:9 ratio means that the 
      masthead is currently rendered at 480px high. Let's…
 * 6. …seamlessly snip off the fluid feature at this height, and…
 * 7. …fix the height at 480px. This means that we should see no jumps in
      height as the masthead moves from fluid to fixed. This actual value 
      takes into account the padding and the top border on the header itself.
 */
.page-head--masthead {
    margin-bottom: 0;
    background: url(/img/css/masthead.jpg) center center 2e2620;
    @include vendor(background-size, cover);
    color: $color-masthead; /* [1] */
    border-top-color: $color-masthead;
    border-bottom-width: 0;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1) inset;

    @include media-query(lap-and-up) {
        background-image: url(/img/css/masthead-medium.jpg);
    }
    @include media-query(desk) {
        background-image: url(/img/css/masthead-large.jpg);
    }
    > .wrapper { /* [2] */
        position: relative; /* [3] */
        padding-top: 56.25%; /* [4] */

        @media screen and (min-width: 758px) { /* [5] */
            padding-top: 0; /* [6] */
            height: $header-max-height - double($spacing-unit) - $header-border-width; /* [7] */
        }
    }
}
```

These types of comment allow us to keep all of our documentation in one place whilst referring to the parts of the ruleset to which they belong.

@TODO From Trello: If you find an answer online (read: on Stack Overflow) then add the link to a comment so future people know what’s up.




## 4.9 Preprocessor comments

With most—if not all—preprocessors, we have the option to write comments that will not get compiled out into our resulting CSS file. As a rule, use these comments to document code that would not get written out to that CSS file either. If you are documenting code which will get compiled, use comments that will compile also. For example, this is correct:

```
// Dimensions of the @2x image sprite:
$sprite-width:  920px;
$sprite-height: 212px;

/**
 * 1. Default icon size is 16px.
 * 2. Squash down the retina sprite to display at the correct size.
 */
.sprite {
    width:  16px; /* [1] */
    height: 16px; /* [1] */
    background-image: url(/img/sprites/main.png);
    background-size: ($sprite-width / 2 ) ($sprite-height / 2); /* [2] */
}
```

We have documented variables—code which will not get compiled into our CSS file—with preprocessor comments, whereas our CSS—code which will get compiled into our CSS file—is documented using CSS comments. This means that we have only the correct and relevant information available to us when debugging our compiled stylesheets.



TODO: HTML in CSS
http://csswizardry.com/2012/04/my-html-css-coding-style/

In situations where it would be useful for a developer to know exactly how a chunk of CSS applies to some HTML, I often include a snippet of HTML in a CSS comment, for example:

```
/*------------------------------------*\
    $TOOLTIPS
\*------------------------------------*/
/*
<small class=tooltip><span>Lorem ipsum dolor</span></small>
*/
.tooltip{
    [styles]
}
    .tooltip > span{
        [styles]
    }
```


---


# 5. Rule organisation

As Jonathan Snook says in [Scalable and Modular Architecture for CSS](https://smacss.com/book/categorizing "Categorizing CSS Rules"):

> Every project needs some organization. Throwing every new style you create
> onto the end of a single file would make finding things more difficult and 
> would be very confusing for anybody else working on the project.

We use Jonathan Snook's Scalable and Modular Architecture for CSS, aka SMACSS, to inform how to organise the rules within a CSS (or Sass) file.


## 5.1 Categorise your CSS rules

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




### 1. Base

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


#### CSS resets

CSS resets (which are designed to strip out, or standardise, across all browsers the default margins, padding, and other properties) are a particular subset of base styles.

If you use a separate CSS reset (for example, Eric Meyer's [Reset CSS](http://meyerweb.com/eric/tools/css/reset/ "CSS Tools: Reset CSS") or [Normalize](http://necolas.github.io/normalize.css/ "A modern, HTML5-ready alternative to CSS resets")) then you should include this at the top of the base section before any of your own rules.

Any CSS reset / normalise code should be clearly commented indicating its version number and source URL.


#### Frameworks

CSS frameworks, such as [Bootstrap](http://getbootstrap.com/) and [Foundation](http://foundation.zurb.com/), should NOT be regarded as base rules as they style far more than simple elements and often have more classes than a perpetual student.

If you need to include frameworks (whole or in part) within your stylesheet — which you may if you are `@import`-ing from numerous sources into a Sass file for production — then you should precede the base section with a section zero called `0. Framework` and include comments clearly indicating its version number and source URL.


#### Further reading

* [SMACSS: Categorizing CSS rules](https://smacss.com/book/categorizing "Scalable and Modular Architecture for CSS by Jonathan Snook")
* [SMACSS: Base rules](https://smacss.com/book/type-base "Scalable and Modular Architecture for CSS by Jonathan Snook")




### 2. Layout

Layout rules define the major layout components of a page, such as header, footer, navigation, main content, and sidebar. These are the areas in which modules sit.


#### Further reading

* [SMACSS: Layout rules](https://smacss.com/book/type-layout "Scalable and Modular Architecture for CSS by Jonathan Snook")




### 3. Modules

Modules are the reusable, modular components of our design. These are usually defined by distinct patterns in our digital pattern library, e.g. accordion, breadcrumps, hero banner, navbox, etc.

* Modules sit inside layout components.
* Modules can sometimes sit within other modules, too.
* Each Module should be designed to exist as a standalone component.
* Modules can easily be moved to different parts of the layout without breaking.


#### Further reading

* [SMACSS: Module rules](https://smacss.com/book/type-module "Scalable and Modular Architecture for CSS by Jonathan Snook")




### 4. State

"A state is something that augments and overrides all other styles. For example, an accordion section may be in a collapsed or expanded state. A message may be in a success or error state." [Source](https://smacss.com/book/type-state "Scalable and Modular Architecture for CSS by Jonathan Snook")

State rules describe how our layouts or modules will look when in a particular state such as visible or hidden, collapsed or expanded, active or inactive, error or success.

But the state may also refer to how something looks on a larger or smaller screen, or how an element might appear in a different view such as on the homepage.


#### Prefix classes with -is

Jonathan Snook's idea is that "states are generally applied to the same element as a layout rule or applied to the same element as a base module class." 

In some cases it can be very useful to prefix the class name with the verb `is-`, for example:

* `.is-hidden`
* `.is-expanded`
* `.is-active`
* `.is-inactive`


#### Isnʼt it just a module?

The answer to this question is worth quoting in full:

"There is plenty of similarity between a sub-module style and a state style. They both modify the existing look of an element. However, they differ in two key ways:

1. State styles can apply to layout and/or module styles; and
2. State styles indicate a JavaScript dependency.

"It is this second point that is the most important distinction. Sub-module styles are applied to an element at render time and then are never changed again. State styles, however, are applied to elements to indicate a change in state while the page is still running on the client machine.

"For example, clicking on a tab will activate that tab. Therefore, an is-active or is-tab-active class is appropriate. Clicking on a dialog close button will hide the dialog. Therefore, an is-hidden class is appropriate."

[Source](https://smacss.com/book/type-state "Scalable and Modular Architecture for CSS by Jonathan Snook")


#### Using !important

States should be stand-alone and built from one single class selector, e.g. `.is-selected`.

Use of `!important` is allowed if required, but hang back from applying it unless it is absolutely necessary.


#### Further reading

* [SMACSS: State rules](https://smacss.com/book/type-state "Scalable and Modular Architecture for CSS by Jonathan Snook")
* [SMACSS: Changing state](https://smacss.com/book/state "Scalable and Modular Architecture for CSS by Jonathan Snook")




### 5. Theme

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




## 5.2 Further reading

* [SMACSS: Theme rules](https://smacss.com/book/type-theme "Scalable and Modular Architecture for CSS by Jonathan Snook")


---


# 6. Naming conventions

Naming conventions in CSS are hugely useful in making your code more strict, more transparent, and more informative.

A good naming convention will tell you and your team:

*   what type of thing a class does;
*   where a class can be used;
*   what (else) a class might be related to.

The naming convention I follow is very simple: hyphen (-) delimited strings, with BEM-like naming for more complex pieces of code.

It's worth noting that a naming convention is not normally useful CSS-side of development; they really come into their own when viewed in HTML.


## 6.1 Naming

As Phil Karlton once said, 'There are only two hard things in Computer Science: cache invalidation and naming things.'

I won't comment on the former claim here, but the latter has plagued me for years. My advice with regard to naming things in CSS is to pick a name that is sensible, but somewhat ambiguous: aim for high reusability. For example, instead of a class like `.site-nav`, choose something like `.primary-nav`; rather than `.footer-links`, favour a class like `.sub-links`.

The differences in these names is that the first of each two examples is tied to a very specific use case: they can only be used as the site's navigation or the footer's links respectively. By using slightly more ambiguous names, we can increase our ability to reuse these components in different circumstances.

To quote Nicolas Gallagher:

> Tying your class name semantics tightly to the nature of the content has
> already reduced the ability of your architecture to scale or be easily put 
> to use by other developers.

That is to say, we should use sensible names — classes like `.border` or `.red` are never advisable — but we should avoid using classes that describe the exact nature of the content and/or its use cases. Using a class name to describe content is redundant because content describes itself.

The debate surrounding semantics has raged for years, but it is important that we adopt a more pragmatic, sensible approach to naming things in order to work more efficiently and effectively. Instead of focussing on 'semantics', look more closely at sensibility and longevity. Choose names based on ease of maintenance, not for their perceived meaning.

Name things for people; they're the only things that actually read your classes (everything else merely matches them). Once again, it is better to strive for reusable, recyclable classes rather than writing for specific use cases. Let's take an example:

```
/**
 * Runs the risk of becoming out of date; not very maintainable.
 */
.blue {
    color: blue;
}

/**
 * Depends on location in order to be rendered properly.
 */
.header span {
    color: blue;
}

/**
 * Too specific; limits our ability to reuse.
 */
.header-color {
    color: blue;
}

/**
 * Nicely abstracted, very portable, doesn't risk becoming out of date.
 */
.highlight-color {
    color: blue;
}
```

It is important to strike a balance between names that do not literally describe the style that the class brings, but also ones that do not explicitly describe specific use cases. Instead of .home-page-panel, choose .masthead; instead of .site-nav, favour .primary-nav; instead of .btn-login, opt for .btn-primary.




## 6.2 Naming UI components

Naming components with agnosticism and reusability in mind really helps developers construct and modify UIs much more quickly, and with far less waste. However, it can sometimes be beneficial to provide more specific or meaningful naming alongside the more ambiguous class, particularly when several agnostic classes come together to form a more complex and specific component that might benefit from having a more meaningful name. In this scenario, we augment the classes with a `data-ui-component` attribute which houses a more specific name, for example:

```
<ul class="tabbed-nav" data-ui-component="Main Nav">
```

Here we have the benefits of a highly reusable class name which does not describe—and, therefore, tie itself to—a specific use case, and added meaning via our data-ui-component attribute. The data-ui-component's value can take any format you wish, like title case:

```
<ul class="tabbed-nav" data-ui-component="Main Nav">
```

Or class-like:

```
<ul class="tabbed-nav" data-ui-component="main-nav">
```

Or namespaced:

```
<ul class="tabbed-nav" data-ui-component="nav-main">
```

The implementation is largely personal preference, but the concept still remains: add any useful or specific meaning via a mechanism that will not inhibit your and your team's ability to recycle and reuse CSS.




## 6.3 Accepted characters in class and ID names

In keeping with the [grammatical rules defined for CSS 2.1](http://www.w3.org/TR/CSS21/grammar.html#scanner) a class name or ID must follow these rules:

**First two characters**

*   letters
*   underscores
*   hyphens

**Thereafter, any number of**

*   underscores
*   hyphens
*   letters
*   numbers

**Do not start with...**


### Characters to avoid

*   Asterisks (*) are universal selectors: they will apply styling to every 
    element in the document. Do not use them in class or ID names.
*   Forward slashes (/) and backward slashes (\) are not accepted.




## 6.4 Hyphen delimited

All strings in classes are delimited with a hyphen (-), like so:

```
.page-head {}
.sub-content {}
```

Camel case and underscores are not used for regular classes; the following are incorrect:

```
.pageHead {}
.sub_content {}
```




## 6.5 BEM-like naming

For larger, more interrelated pieces of UI that require a number of classes, we use a BEM-like naming convention.

BEM, meaning Block, Element, Modifier, is a front-end methodology coined by developers working at Yandex. Whilst BEM is a complete methodology, here we are only concerned with its naming convention. Further, the naming convention here only is BEM-like; the principles are exactly the same, but the actual syntax differs slightly.

BEM splits components' classes into three groups:

* Block: The sole root of the component.
* Element: A component part of the Block.
* Modifier: A variant or extension of the Block.

To take an analogy (note, not an example):

```
.person {}
.person__head {}
.person--tall {}
```

Elements are delimited with two (2) underscores (__), and modifiers are delimited by two (2) hyphens (--).

Here we can see that `.person {}` is the Block; it is the sole root of a discrete entity. `.person__head {}` is an Element; it is a smaller part of the .person {} Block. Finally, `.person--tall {} is a Modifier; it is a specific variant of the .person {} Block.


### Starting context

Your Block context starts at the most logical, self-contained, discrete location. To continue with our person-based analogy, we'd not have a class like `.room__person {}`, as the room is another, much higher context. We'd probably have separate Blocks, like so:

```
.room {}

    .room__door {}

.room--kitchen {}


.person {}

    .person__head {}
```

If we did want to denote a `.person {}` inside a `.room {}`, it is more correct to use a selector like `.room .person {}` which bridges two Blocks than it is to increase the scope of existing Blocks and Elements.

A more realistic example of properly scoped blocks might look something like this, where each chunk of code represents its own Block:

```
.page {}


.content {}


.sub-content {}


.footer {}

    .footer__copyright {}
```

Incorrect notation for this would be:

```
.page {}

    .page__content {}

    .page__sub-content {}

    .page__footer {}

        .page__copyright {}
```

It is important to know when BEM scope starts and stops. As a rule, BEM applies to self-contained, discrete parts of the UI.
More layers

If we were to add another Element—called, let's say, .person__eye {}—to this .person {} component, we would not need to step through every layer of the DOM. That is to say, the correct notation would be .person__eye {}, and not .person__head__eye {}. Your classes do not reflect the full paper-trail of the DOM.




## 6.6 Modifying elements

You can have variants of Elements, and these can be denoted in a number of ways depending on how and why they are being modified. Carrying on with our person example, a blue eye might look like this:

```
.person__eye--blue {}
```

Here we can see we're directly modifying the eye Element.

Things can get more complex, however. Please excuse the crude analogy, and let's imagine we have a face Element that is handsome. The person themselves isn't that handsome, so we modify the face Element directly—a handsome face on a regular person:

```
.person__face--handsome {}
```

But what if that person is handsome, and we want to style their face because of that fact? A regular face on a handsome person:

```
.person--handsome .person__face {}
```

Here is one of a few occasions where we'd use a descendant selector to modify an Element based on a Modifier on the Block.

If using Sass, we would likely write this like so:

```
.person {}

    .person__face {

        .person--handsome & {}

    }

.person--handsome {}
```

Note that we do not nest a new instance of `.person__face {}` inside of `.person--handsome {};` instead, we make use of Sass' parent selectors to prepend `.person--handsome` onto the existing `.person__face {}` selector. This means that all of our `.person__face {}`-related rules exist in once place, and aren't spread throughout the file. This is general good practice when dealing with nested code: keep all of your context (e.g. all `.person__face {}` code) encapsulated in one location.




## 6.7 Naming conventions in HTML

As I previously hinted at, naming conventions aren't necessarily all that useful in your CSS. Where naming conventions' power really lies is in your markup. Take the following, non-naming-conventioned HTML:

```
<div class="box  profile  pro-user">

    <img class="avatar  image" />

    <p class="bio">...</p>

</div>
```

How are the classes box and profile related to each other? How are the classes profile and avatar related to each other? Are they related at all? Should you be using pro-user alongside bio? Will the classes image and profile live in the same part of the CSS? Can you use avatar anywhere else?

From that markup alone, it is very hard to answer any of those questions. Using a naming convention, however, changes all that:

```
<div class="box  profile  profile--is-pro-user">

    <img class="avatar  profile__image" />

    <p class="profile__bio">...</p>

</div>
```

Now we can clearly see which classes are and are not related to each other, and how; we know what classes we can't use outside of the scope of this component; and we know which classes we may be free to reuse elsewhere.




## 6.8 JavaScript hooks

As a rule, it is unwise to bind your CSS and your JS onto the same class in your HTML. This is because doing so means you can't have (or remove) one without (removing) the other. It is much cleaner, much more transparent, and much more maintainable to bind your JS onto specific classes.

I have known occasions before when trying to refactor some CSS has unwittingly removed JS functionality because the two were tied to each other—it was impossible to have one without the other.

Typically, these are classes that are prepended with js-, for example:

```
<input type="submit" class="btn  js-btn" value="Follow" />
```

This means that we can have an element elsewhere which can carry with style of `.btn {}`, but without the behaviour of `.js-btn`.


### Do not use HTML5 data-* attributes as JavaScript hooks

A common practice is to use `data-*` attributes as JavaScript hooks, but this is incorrect. `data-*` attributes, as per the spec, are used to store custom data private to the page or application (emphasis mine). `data-*` attributes are designed to store data, not be bound to.


---


# 7. CSS Selectors

Perhaps somewhat surprisingly, one of the most fundamental, critical aspects of writing maintainable and scalable CSS is selectors. Their specificity, their reusability, and their performance all have a direct impact on the efficiency and effectiveness of our CSS.

**TODO: This whole section needs considerable editing.**


## 7.1 General rules

**KEEP THIS BUT EXTEND IT IN LIGHT OF WHAT COMES AFTER IT**

Your selectors are fundamental to writing good CSS. To very briefly sum up the above sections:

*   **Avoid using IDs**, prefer classes or elements or attributes.
*   **Select what you want explicitly**, rather than relying on circumstance or
    coincidence. Good selector intent will rein in the reach and leak of your styles.
*   **Write selectors for reusability**, so that you can work more efficiently
    and reduce waste and repetition.
*   **Do not nest selectors unnecessarily**, because this will increase 
    specificity and affect where else you can use your styles.
*   **Do not qualify selectors unnecessarily**, as this will impact the number 
    of different elements you can apply styles to.
*   **Keep selectors as short as possible**, in order to keep specificity down 
    and performance up.

Focussing on these points will keep your selectors a lot more sane and easy to work with on changing and long-running projects.




## 7.2 Selector intent

It is important when writing CSS that we scope our selectors correctly, and that we're selecting the right things for the right reasons. Selector intent is the process of deciding and defining what you want to style and how you will go about selecting it. For example, if you are wanting to style your website's main navigation menu, a selector like this would be incredibly unwise:

```
header ul {}
```

This selector's intent is to style any `ul` inside any header element, whereas our intent was to style the site's main navigation. This is poor selector intent: you can have any number of header elements on a page, and they in turn can house any number of `ul`s, so a selector like this runs the risk of applying very specific styling to a very wide number of elements. This will result in having to write more CSS to undo the greedy nature of such a selector.

A better approach would be a selector like:

```
.site-nav {}
```

An unambiguous, explicit selector with good selector intent. We are explicitly selecting the right thing for exactly the right reason.

Poor selector intent is one of the biggest reasons for headaches on CSS projects. Writing rules that are far too greedy — and that apply very specific treatments via very far reaching selectors — causes unexpected side effects and leads to very tangled stylesheets, with selectors overstepping their intentions and impacting and interfering with otherwise unrelated rulesets.

CSS cannot be encapsulated, it is inherently leaky, but we can mitigate some of these effects by not writing such globally-operating selectors: your selectors should be as explicit and well reasoned as your reason for wanting to select something.




## 7.3 Specificity

### Keep specificity low at all times

"CSS isn't the most friendly of languages: globally operating, very leaky, dependent on location, hard to encapsulate, based on inheritance. But none of that even comes close to the horrors of specificity." — Harry Roberts

CSS specificity can, among other things:

* Limit your ability to extend your classes.
* Interfere with the cascade, how CSS inherits from parent rules.
* Make your code unnecessarily long and/or complex.
* Prevent code from working as expected when moved from one project to another.

All of these issues are greatly magnified when working on a larger project with a number of developers contributing code.

The problem with specificity isn't necessarily that it's high or low; it's the fact it is so variant and that it cannot be opted out of: the only way to deal with it is to get progressively more specific.

One of the single, simplest tips for an easier life when writing CSS—particularly at any reasonable scale — is to **always try and keep specificity as low as possible at all times**. Try to make sure there isn't a lot of variance between selectors in your codebase, and that all selectors strive for as low a specificity as possible.

Doing so will instantly help you tame and manage your project, meaning that no overly-specific selectors are likely to impact or affect anything of a lower specificity elsewhere. It also means you're less likely to need to fight your way out of specificity corners, and you'll probably also be writing much smaller stylesheets.

Simple changes to the way we work include, but are not limited to:

* **Avoid using IDs in your CSS.**
* **Avoid nesting selectors.**
* **Avoid qualifying classes.**
* **Avoid chaining selectors.**

To quote Jonathan Snook: "whenever declaring your styles, use the least number of selectors required to style an element."

As a rule, if a selector will work without it being nested then do not nest it.


### Do not use !important as a hack

`!important` is often used as a way to cheat your way out of specificity wars. The general rule is this: **do not use !important**, especially if it is used as a ham-fisted hack to 'just make things work'.

How many times have we seen code like this?

```
#navigation ul.nav-list li.nav-item a {
    color: blue !important;
}
```

How much more specific will the next rule need to be?!

If you find that you need to use `!important` to get something to work then that is a good sign that your code needs to be refactored. As Harry Roberts says, `!important` is "often viewed as a last resort — a desperate, defeated stab at patching over the symptoms of a much bigger problem with your code."


### Use !important proactively not reactively

`!important` does have a place in CSS projects, but only if used sparingly and proactively.

Proactive use of `!important` is when it is **used before you've encountered any specificity problems**; when it is used **as a guarantee rather than as a fix**. For example:

```
.one-half {
    width: 50% !important;
}

.is-hidden {
    display: none !important;
}
```

These two helper, or utility, classes are very specific in their intentions: you would only use them if you wanted something to be rendered at 50% width or not rendered at all. If you didn't want this behaviour, you would not use these classes, therefore whenever you do use them you will definitely want them to win.

Here we proactively apply `!important` to ensure that these styles always win. This is correct use of `!important` to guarantee that these trumps always work, and don't accidentally get overridden by something else more specific.

Only use `!important` proactively, not reactively.


### Hacking specificity

With all that said on the topic of specificity, and keeping it low, it is inevitable that we will encounter problems. No matter how hard we try, and how conscientious we are, there will always be times that we need to hack and wrangle specificity.

When these situations do arise, it is important that we handle the hacks as safely and elegantly as possible.


#### Chain a class with itself

In the event that you need **to increase the specificity of a class selector**, there are a number of options. We could nest the class inside something else to bring its specificity up. For example, we could use `.header .site-nav {}` to bring up the specificity of a simple `.site-nav {}` selector.

The problem with this, as we've discussed, is that it introduces location dependency: these styles will only work when the `.site-nav` component is in the `.header` component.

Instead, we can use a much safer hack that will not impact this component's portability: we can chain that class with itself:

```
.site-nav.site-nav {}
```

This chaining doubles the specificity of the selector, but does not introduce any dependency on location.


#### Use an attribute selector to select an ID

In the event that we do, for whatever reason, have an ID in our markup that we cannot replace with a class, select it via an attribute selector as opposed to an ID selector. For example, let's imagine we have embedded a third-party widget on our page. We can style the widget via the markup that it outputs, but we have no ability to edit that markup ourselves:

```
<div id="third-party-widget">
    ...
</div>
```

Even though we know not to use IDs in CSS, what other option do we have? We want to style this HTML but have no access to it, and all it has on it is an ID.

We do this:

```
[id="third-party-widget"] {}
```

Here we are selecting based on an attribute rather than an ID, and **attribute selectors have the same specificity as a class**. This allows us to style based on an ID, but without introducing its specificity.

Do keep in mind that these are hacks, and should not be used unless you have no better alternative.


#### Further reading
[Hacks for dealing with specificity](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)




## 7.4 Reusability

With a move toward a more component-based approach to constructing UIs, the idea of reusability is paramount. We want the option to be able to move, recycle, duplicate, and syndicate components across our projects.

To this end, we make heavy use of classes. IDs, as well as being hugely over-specific, cannot be used more than once on any given page, whereas classes can be reused an infinite amount of times. Everything you choose, from the type of selector to its name, should lend itself toward being reused.


### Location independence

Given the ever-changing nature of most UI projects, and the move to more component-based architectures, it is in our interests not to style things based on where they are, but on what they are. That is to say, our components' styling should not be reliant upon where we place them—they should remain entirely location independent.

Let's take an example of a call-to-action button that we have chosen to style via the following selector:

```
.promo a {}
```

Not only does this have poor selector intent—it will greedily style any and every link inside of a `.promo` to look like a button — it is also pretty wasteful as a result of being so locationally dependent: we can't reuse that button with its correct styling outside of `.promo` because it is explicitly tied to that location. A far better selector would have been:

```
.btn {}
```

This single class can be reused anywhere outside of `.promo` and will always carry its correct styling. As a result of a better selector, this piece of UI is more portable, more recyclable, doesn't have any dependencies, and has much better selector intent. A component shouldn't have to live in a certain place to look a certain way.


### Portability

Reducing, or, ideally, removing, location dependence means that we can move components around our markup more freely, but how about improving our ability to move classes around components? On a much lower level, there are changes we can make to our selectors that make the selectors themselves more portable, as opposed to the components they create. Take the following example:

```
input.btn {}
```

This is a qualified selector; the leading input ties this ruleset to only being able to work on input elements. By omitting this qualification, we allow ourselves to reuse the `.btn` class on any element we choose, like an a, for example, or a button.

Qualified selectors do not lend themselves well to being reused, and every selector we write should be authored with reuse in mind.

Of course, there are times when you may want to legitimately qualify a selector — you might need to apply some very specific styling to a particular element when it carries a certain class, for example:

```
/**
 * Embolden and colour any element with a class of `.error`.
 */
.error {
    color: red;
    font-weight: bold;
}

/**
 * If the element is a `div`, also give it some box-like styling.
 */
div.error {
    padding: 10px;
    border: 1px solid;
}
```

This is one example where a qualified selector might be justifiable, but I would still recommend an approach more like:

```
/**
 * Text-level errors.
 */
.error-text {
    color: red;
    font-weight: bold;
}

/**
 * Elements that contain errors.
 */
.error-box {
    padding: 10px;
    border: 1px solid;
}
```

This means that we can apply `.error-box` to any element, and not just a `div` — it is more reusable than a qualified selector.


#### Quasi-qualified selectors

One thing that qualified selectors can be useful for is signalling where a class might be expected or intended to be used, for example:

```
ul.nav {}
```

Here we can see that the `.nav` class is meant to be used on a `ul` element, and not on a `nav`. By using quasi-qualified selectors we can still provide that information without actually qualifying the selector:

```
/*ul*/.nav {}
```

By commenting out the leading element, we can still leave it to be read, but avoid qualifying and increasing the specificity of the selector.


### Object-orientation

Object-orientation is a programming paradigm that breaks larger programs up into smaller, in(ter)dependent objects that all have their own roles and responsibilities. From Wikipedia:

> Object-oriented programming (OOP) is a programming paradigm that represents
> the concept of ‘objects' […] which are usually instances of classes, [and] 
> are used to interact with one another to design applications and computer 
> programs.
> When applied to CSS, we call it object-oriented CSS, or OOCSS. OOCSS was 
> coined and popularised by Nicole Sullivan, whose Media Object has become the 
> poster child of the methodology.

OOCSS deals with the separation of UIs into structure and skin: breaking UI components into their underlying structural forms, and layering their cosmetic forms on separately. This means that we can recycle common and recurring design patterns very cheaply without having to necessarily recycle their specific implementation details at the same time. OOCSS promotes reuse of code, which makes us quicker, as well as keeping the size of our codebase down.

Structural aspects can be thought of like skeletons; common, recurring frames that provide design-free constructs known as objects and abstractions. Objects and abstractions are simple design patterns that are devoid of any cosmetics; we abstract out the shared structural traits from a series of components into a generic object.

Skin is a layer that we (optionally) add to our structure in order to give objects and abstractions a specific look-and-feel. Let's look at an example:

```
/**
 * A simple, design-free button object. Extend this object with a `.btn--*` skin
 * class.
 */
.btn {
    display: inline-block;
    padding: 1em 2em;
    vertical-align: middle;
}


/**
 * Positive buttons' skin. Extends `.btn`.
 */
.btn--positive {
    background-color: green;
    color: white;
}

/**
 * Negative buttons' skin. Extends `.btn`.
 */
.btn--negative {
    background-color: red;
    color: white;
}
```

Above, we can see how the `.btn {}` class simply provides structural styling to an element, and doesn't concern itself with any cosmetics. We supplement the `.btn {}` object with a second class, such as `.btn--negative {}` in order to give that DOM node specific cosmetics:

```
<button class="btn  btn--negative">Delete</button>
```

Favour the multiple-class approach over using something like `@extend:` using multiple classes in your markup—as opposed to wrapping the classes up into one using a preprocessor:

*   gives you a better paper-trail in your markup, and allows you to see 
    quickly and explicitly which classes are acting on a piece of HTML;
*   allows for greater composition in that classes are not tightly bound to 
    other styles in your CSS.

Whenever you are building a UI component, try and see if you can break it into two parts: one for structural styles (paddings, layout, etc.) and another for skin (colours, typefaces, etc.).


#### Further reading

* [The media object saves hundreds of lines of code](http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/)
* [The flag object](http://csswizardry.com/2013/05/the-flag-object/)
* [Naming UI components in OOCSS](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)


### The single responsibility principle

The _single responsibility principle_ is a paradigm that, very loosely, states that all pieces of code (in our case, classes) should focus on doing one thing and one thing only. More formally:

> …the single responsibility principle states that every context (class, 
> function, variable, etc.) should have a single responsibility, and that 
> responsibility should be entirely encapsulated by the context.
> What this means for us is that our CSS should be composed of a series of 
> much smaller classes that focus on providing very specific and limited 
> functionality. This means that we need to decompose UIs into their smallest 
> component pieces that each serve a single responsibility; they all do just 
> one job, but can be very easily combined and composed to make much more 
> versatile and complex constructs. Let's take some example CSS that does not 
> adhere to the single responsibility principle:

```
.error-message {
    display: block;
    padding: 10px;
    border-top: 1px solid f00;
    border-bottom: 1px solid f00;
    background-color: fee;
    color: f00;
    font-weight: bold;
}

.success-message {
    display: block;
    padding: 10px;
    border-top: 1px solid 0f0;
    border-bottom: 1px solid 0f0;
    background-color: efe;
    color: 0f0;
    font-weight: bold;
}
```

Here we can see that—despite being named after one very specific use-case—these classes are handling quite a lot: layout, structure, and cosmetics. We also have a lot of repetition. We need to refactor this in order to abstract out some shared objects (OOCSS) and bring it more inline with the single responsibility principle. We can break these two classes out into four much smaller responsibilities:

```
.box {
    display: block;
    padding: 10px;
}


.message {
    border-style: solid;
    border-width: 1px 0;
    font-weight: bold;
}

.message--error {
    background-color: fee;
    color: f00;
}

.message--success {
    background-color: efe;
    color: 0f0;
}
```

Now we have a general abstraction for boxes which can live, and be used, completely separately from our message component, and we have a base message component that can be extended by a number of smaller responsibility classes. The amount of repetition has been greatly reduced, and our ability to extend and compose our CSS has been greatly increased. This is a great example of OOCSS and the single responsibility principle working in tandem.

By focussing on single responsibilities, we can give our code much more flexibility, and extending components' functions becomes very simple when sticking to the open/closed principle, which we're going to look at next.


#### Further reading

* The single responsibility principle applied to CSS


### Open to extension / closed to modification

The open/closed principle, in my opinion, is rather poorly named. It is poorly named because 50% of the vital information is omitted from its title. The open/closed principle states that

> [s]oftware entities (classes, modules, functions, etc.) should be open for 
> extension, but closed for modification.

See? The most important words—extension and modification—are completely missing from the name, which isn't very useful at all.

Once you have trained yourself to remember what the words open and closed actually relate to, you'll find that open/closed principle remarkably simple: any additions, new functionality, or features we add to our classes should be added via extension—we should not modify these classes directly. This really trains us to write bulletproof single responsibilities: because we shouldn't modify objects and abstractions directly, we need to make sure we get them as simple as possible the first time. This means that we should never need to actually change an abstraction—we'd simply stop using it—but any slight variants of it can be made very easily by extending it.

Let's take an example:

```
.box {
    display: block;
    padding: 10px;
}

.box--large {
    padding: 20px;
}
```

Here we can see that the `.box {}` object is incredibly simple: we've stripped it right back into one very small and very focussed responsibility. To modify that box, we extend it with another class; `.box--large {}`. Here the `.box {} class is closed to modification, but open to being extended.

An incorrect way of achieving the same might look like this:

```
.box {
    display: block;
    padding: 10px;
}

.content .box {
    padding: 20px;
}
```

Not only is this overly specific, locationally dependent, and potentially displaying poor Selector Intent, we are modifying the `.box {}` directly. We should rarely—if ever—find an object or abstraction's class as a key selector in a compound selector.

A selector like `.content .box {}` is potentially troublesome because

*   it forces all `.box` components into that style when placed inside of
    `.content`, which means the modification is dictated to developers, 
    whereas developers should be allowed to opt into changes explicitly;
*   the `.box` style is now unpredictable to developers; the single
    responsibility no longer exists because nesting the selector produces a 
    forced caveat.

All modifications, additions, and changes should always be opt-in, not mandatory. If you think something might need a slight adjustment to take it away from the norm, provide another class which adds this functionality.

When working in a team environment, be sure to write API-like CSS; always ensure that existing classes remain backward compatible (i.e. no changes at their root) and provide new hooks to bring in new features. Changing the root object, abstraction, or component could have huge knock-on effects for developers making use of that code elsewhere, so never modify existing code directly.

Exceptions may present themselves when it transpires that a root object does need a rewrite or refactor, but it is only in these specific cases that you should modify code. Remember: **open for extension; closed for modification**.


#### Further reading

* [The open/closed principle applied to CSS](http://csswizardry.com/2012/06/the-open-closed-principle-applied-to-css/)


### The separation of concerns

The separation of concerns is a principle which, at first, sounds a lot like the single responsibility principle. The separation of concerns states that code should be broken up

> into distinct sections, such that each section addresses a separate concern.
> A concern is a set of information that affects the code of a computer 
> program. […] A program that embodies SoC well is called a modular program.

Modular is a word we're probably used to; the idea of breaking UIs and CSS into much smaller, composable pieces. The separation of concerns is just a formal definition which covers the concepts of modularity and encapsulation in code. In CSS this means building individual components, and writing code which only focusses itself on one task at a time.

The term was coined by Edsger W. Dijkstra, who rather elegantly said:

> Let me try to explain to you, what to my taste is characteristic for all 
> intelligent thinking. It is, that one is willing to study in depth an aspect 
> of one's subject matter in isolation for the sake of its own consistency, 
> all the time knowing that one is occupying oneself only with one of the 
> aspects. We know that a program must be correct and we can study it from 
> that viewpoint only; we also know that it should be efficient and we can 
> study its efficiency on another day, so to speak. In another mood we may ask 
> ourselves whether, and if so: why, the program is desirable. But nothing is 
> gained—on the contrary!—by tackling these various aspects simultaneously. It 
> is what I sometimes have called ‘the separation of concerns', which, even if 
> not perfectly possible, is yet the only available technique for effective 
> ordering of one's thoughts, that I know of. This is what I mean by ‘focusing 
> one's attention upon some aspect': it does not mean ignoring the other 
> aspects, it is just doing justice to the fact that from this aspect's point 
> of view, the other is irrelevant. It is being one- and multiple-track minded 
> simultaneously.

Beautiful. The idea here is to focus fully on one thing at once; build one thing to do its job very well whilst paying as little attention as possible to other facets of your code. Once you have addressed and built all these separate concerns in isolation—meaning they're probably very modular, decoupled, and encapsulated—you can begin bringing them together into a larger project.

A great example is layout. If you are using a grid system, all of the code pertaining to layout should exist on its own, without including anything else. You've written code that handles layout, and that's it:

```
<div class="layout">

    <div class="layout__item  two-thirds">
    </div>

    <div class="layout__item  one-third">
    </div>

</div>
```

You will now need to write new, separate code to handle what lives inside of that layout:

```
<div class="layout">

    <div class="layout__item  two-thirds">
        <section class="content">
            ...
        </section>
    </div>

    <div class="layout__item  one-third">
        <section class="sub-content">
            ...
        </section>
    </div>

</div>
```

The separation of concerns allows you to keep code self-sufficient, ignorant, and ultimately a lot more maintainable. Code which adheres to the separation of concerns can be much more confidently modified, edited, extended, and maintained because we know how far its responsibilities reach. We know that modifying layout, for example, will only ever modify layout—nothing else.

The separation of concerns increases reusability and confidence whilst reducing dependency.


### DRY

DRY, which stands for _Don't repeat yourself_, is a micro-principle used in software development which aims to keep the repetition of key information to a minimum. Its formal definition is that

> [e]very piece of knowledge must have a single, unambiguous, authoritative 
> representation within a system.

Although a very simple principle—in principle—DRY is often misinterpreted as the necessity to never repeat the exact same thing twice at all in a project. This is impractical and usually counterproductive, and can lead to forced abstractions, over-thought and -engineered code, and unusual dependencies.

The key isn't to avoid all repetition, but to normalise and abstract meaningful repetition. If two things happen to share the same declarations coincidentally, then we needn't DRY anything out; that repetition is purely circumstantial and cannot be shared or abstracted. For example:

```
.btn {
    display: inline-block;
    padding: 1em 2em;
    font-weight: bold;
}

[...]

.page-title {
    font-size: 3rem;
    line-height: 1.4;
    font-weight: bold;
}

[...]

    .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        font-weight: bold;
    }
```

From the above code, we can reasonably deduce that the font-weight: bold; declaration appears three times purely coincidentally. To try and create an abstraction, mixin, or `@extend` directive to cater for this repetition would be overkill, and would tie these three rulesets together based purely on circumstance.

However, imagine we're using a web-font that requires `font-weight: bold;` to be declared every time the font-family is:

```
.btn {
    display: inline-block;
    padding: 1em 2em;
    font-family: "My Web Font", sans-serif;
    font-weight: bold;
}

[...]

.page-title {
    font-size: 3rem;
    line-height: 1.4;
    font-family: "My Web Font", sans-serif;
    font-weight: bold;
}

[...]

    .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        font-family: "My Web Font", sans-serif;
        font-weight: bold;
    }
```

Here we're repeating a more meaningful snippet of CSS; these two declarations have to always be declared together. In this instance, we probably would DRY out our CSS.

I would recommend using a mixin over @extend here because, even though the two declarations are thematically grouped, the rulesets themselves are still separate, unrelated entities: to use @extend would be to physically group these unrelated rulesets together in our CSS, thus making the unrelated related.

Our mixin:

```
@mixin my-web-font() {
    font-family: "My Web Font", sans-serif;
    font-weight: bold;
}

.btn {
    display: inline-block;
    padding: 1em 2em;
    @include my-web-font();
}

[...]

.page-title {
    font-size: 3rem;
    line-height: 1.4;
    @include my-web-font();
}

[...]

    .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        @include my-web-font();
    }
```

Now the two declarations only exist once, meaning we're not repeating ourselves. If we ever switch out our web-font, or move to a font-weight: regular; version, we only need to make that change in one place.

In short, only DRY code that is actually, thematically related. Do not try to reduce purely coincidental repetition: **duplication is better than the wrong abstraction**.

#### Further reading

* [Writing DRYer vanilla CSS](http://csswizardry.com/2013/07/writing-dryer-vanilla-css/)




## 7.5 Selector performance

A topic which is — with the quality of today's browsers — more interesting than it is important, is selector performance. That is to say, how quickly a browser can match the selectors your write in CSS up with the nodes it finds in the DOM.

Generally speaking, the longer a selector is (i.e. the more component parts) the slower it is, for example:

```
body.home div.header ul {}
```

…is a far less efficient selector than:

```
.primary-nav {}
```

This is because browsers read CSS selectors right-to-left. A browser will read the first selector as:

1.   Find all `ul` elements in the DOM;
2.   Now check if they live anywhere inside an element with a class of 
     `.header`;
3.   Next check that `.header` class exists on a `div` element;
4.   Check that that all lives anywhere inside any elements with a class
     of `.home;`
5.   Finally, check that `.home` exists on a `body` element.

The second, in contrast, is simply a case of the browser reading: find all the elements with a class of `.primary-nav`.

To further compound the problem, we are using descendant selectors (e.g. `.foo .bar {}`). The upshot of this is that a browser is required to start with the rightmost part of the selector (i.e. `.bar`) and keep looking up the DOM indefinitely until it finds the next part (i.e. `.foo`). This could mean stepping up the DOM dozens of times until a match is found.

This is just one reason why nesting with preprocessors is often a false economy; as well as making selectors unnecessarily more specific, and creating location dependency, it also creates more work for the browser.

By using a child selector (e.g. `.foo > .bar {}`) we can make the process much more efficient, because this only requires the browser to look one level higher in the DOM, and it will stop regardless of whether or not it found a match.


### The key selector

Because browsers read selectors right-to-left, the rightmost selector is often critical in defining a selector's performance: this is called the key selector.

The following selector might appear to be highly performant at first glance. It uses an ID which is nice and fast, and there can only ever be one on a page, so surely this will be a nice and speedy lookup—just find that one ID and then style everything inside of it:

```
#foo * {}
```

The problem with this selector is that the key selector (`*`) is very, very far reaching. What this selector actually does is finds every single node in the DOM (even `<title>`, `<link>`, and `<head>` elements; everything) and then looks to see if it lives anywhere at any level within `#foo`. This is a very, very expensive selector, and should most likely be avoided or rewritten.

Thankfully, by writing selectors with good selector intent, we are probably avoiding inefficient selectors by default; we are very unlikely to have greedy key selectors if we're targeting the right things for the right reason.

That said, however, CSS selector performance should be fairly low on your list of things to optimise; browsers are fast, and are only ever getting faster, and it is only on notable edge cases that inefficient selectors would be likely to pose a problem.

As well as their own specific issues, nesting, qualifying, and poor selector intent all contribute to less efficient selectors.




## 7.6 Further reading

* [Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)
* ['Scope' in CSS](http://csswizardry.com/2013/05/scope-in-css/)
* [Keep your CSS selectors short](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)
* [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [Naming UI components in OOCSS](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)
* [Writing efficient CSS selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)
