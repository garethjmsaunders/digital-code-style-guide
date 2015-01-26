CSS code style guide

# 2. Syntax and formatting

One of the simplest forms of a style guide is a set of rules regarding syntax and formatting. Having a standard way of writing CSS means that code will always look and feel familiar to all members of the team: consistency is key.

Further, code that looks clean feels clean. It is a much nicer environment to work in, and prompts other team members to maintain the standard of cleanliness that they found. Ugly code sets a bad precedent.

Source: [CSS guidelines](http://cssguidelin.es/#syntax-and-formatting "Harry Roberts")





## In this section
<!-- MarkdownTOC -->

- [Anatomy of a ruleset](#anatomy-of-a-ruleset)
- [80 characters wide](#80-characters-wide)
- [Block style](#block-style)
    - [Multi-line CSS](#multi-line-css)
    - [Indent with four (4) spaces, no tabs](#indent-with-four-4-spaces-no-tabs)
        - [Indenting Sass (SHOULD WE HAVE A SEPARATE Sass guide?)](#indenting-sass-should-we-have-a-separate-sass-guide)
    - [Colons and semicolons, braces and spaces](#colons-and-semicolons-braces-and-spaces)
    - [List declarations in alphabetical order](#list-declarations-in-alphabetical-order)
        - [Positioned elements](#positioned-elements)
        - [Vendor prefixes](#vendor-prefixes)
    - [Alignment](#alignment)
- [Meaningful whitespace](#meaningful-whitespace)
- [Syntax](#syntax)
    - [Colours](#colours)
        - [Use the approved St Andrews palette of colours](#use-the-approved-st-andrews-palette-of-colours)
        - [Colour keywords](#colour-keywords)
        - [Prefer RGB over hex](#prefer-rgb-over-hex)
        - [Alpha transparency](#alpha-transparency)
        - [Hex codes](#hex-codes)
    - [Quotation marks](#quotation-marks)
        - [Font-family](#font-family)
        - [URLs](#urls)
    - [Shorthand properties](#shorthand-properties)
        - [Background](#background)
        - [Border](#border)
        - [List-style](#list-style)
        - [Margin and padding](#margin-and-padding)
    - [Units](#units)
    - [Zero](#zero)
- [Don't use IE hacks](#dont-use-ie-hacks)
    - [Filters](#filters)
    - [IE hacks](#ie-hacks)
    - [shame.css](#shamecss)

<!-- /MarkdownTOC -->






## Anatomy of a ruleset

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





## 80 characters wide

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





## Block style

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

Reference: [CSS Guidelines "Harry Roberts"](http://cssguidelin.es/#anatomy-of-a-ruleset "Harry Roberts")





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





## Meaningful whitespace

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





## Syntax


### Colours


#### Use the approved St Andrews palette of colours

Unless you have a very good reason not to, you must use the approved pallete of St Andrews colours.


#### Colour keywords

The [CSS Color Module Level 3](http://www.w3.org/TR/css3-color/#html4) specification defines 16 basic colour keywords: aqua, black, blue, fuchsia, gray, green, lime, maroon, navy, olive, purple, red, silver, teal, white, and yellow.

You may use only `black` and `white`; although consider this article [Design tip: never use black](http://ianstormtaylor.com/design-tip-never-use-black/) by Ian Storm Taylor. Do not use the other values, except in debug files.


#### Prefer RGB over hex

Use `rgb(r, g, b)` and `rgba(r, g, b, a)` codes for colours; there must be a space after each comma.

The reason for preferring RGB is three-fold:

1.   Colours in RGB format are easier to guess.
2.   It is quicker to add transparency if required (see alpha transparency)
     below.
3.   RGB format is more widely supported in graphic design applications.

To expand on the first point, while colours on the web have traditionally been specified using hex codes (e.g. St Andrews Blue is `#00539b`) it is not as easy to estimate the colour just by looking at the code, unless you can convert hex to decimal in your head. For example, at a glance `rgb(0, 83, 155)` has about 60% blue and 30% green so you may safely estimate that this is dark blue.

There is a current trend to prefer HSL over RGB as it allows you to more easily make them lighter or darker. With a fixed pallette, such as ours, we don't need this.


#### Alpha transparency

Specifying colours in `rgb(r, g, b)` format makes it much easier to add alpha transparency as you simply need to append an ‘a’ and a fourth value:

```
.black {
    background-color: rgb(0, 0, 0);
}

.darkglass {
    background-color: rgba(0, 0, 0, 0.5);
}
```

Alpha values below zero MUST always begin with a zero (`0.75` rather than `.75`); without a zero it can trigger errors in CSS pre-processors.

If the alpha value is 1 then simply use `rgb(r, g, b)` rather than `rgba(r, g, b, 1);`.


#### Hex codes

If you must use hex codes: shorten values where possible (`#fff` instead of `#ffffff`) and use lowercase alphabetical values (`#fff` not `#FFF`).





### Quotation marks

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





## Don't use IE hacks


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

Further reading

* [Microsoft Developer Network](https://msdn.microsoft.com/en-us/library/ms537512%28v=vs.85%29.aspx)
* [Quirksmode](http://www.quirksmode.org/css/condcom.html)


### shame.css

Consider Harry Roberts, Chris Coyier, and Dave Rupert's idea of a [shame.css](http://csswizardry.com/2013/04/shame-css/ "Article from 17 April 2013") file that groups all "bodges, hacks and quick-fixes in their own file". Their reasons are:

1. You make them stick out like a sore thumb.
2. You keep your 'main' codebase clean.
3. You make developers aware that their hacks are made very visible.
4. You make them easier to isolate and fix.
5. `$ git blame shame.css`.
