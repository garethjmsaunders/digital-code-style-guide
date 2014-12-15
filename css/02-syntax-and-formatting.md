## Syntax and formatting

One of the simplest forms of a style guide is a set of rules regarding syntax and formatting. Having a standard way of writing CSS means that code will always look and feel familiar to all members of the team.
Further, code that looks clean feels clean. It is a much nicer environment to work in, and prompts other team members to maintain the standard of cleanliness that they found. Ugly code sets a bad precedent.


### tl;dr

At a very high-level, we want:

*   four (4) space indents, no tabs;
*   one true brace (1TBS) style indentation;
*   multi-line CSS;
*   80 character wide columns;
*   meaningful use of whitespace.

But, as with anything, the specifics are somewhat irrelevant—consistency is key.


### Multi-line CSS

CSS should be written across multiple lines, except in very specific circumstances. There are a number of benefits to this:

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


### Indenting
As well as intending individual declarations, you MAY indent entire related rulesets to signal their relation to one another, for example:

TODO: Review this in light of advice given in 'Pro CSS for High Traffic Websites' book, p.42.


```
.foo {}

    .foo__bar {}

        .foo__baz {}
```

By doing this, a developer can see at a glance that `.foo__baz {}` lives inside `.foo__bar {}` lives inside `.foo {}`.

This quasi-replication of the DOM tells developers a lot about where classes are expected to be used without them having to refer to a snippet of HTML.


### Indenting Sass

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


### 80 characters wide

Where possible, limit CSS files' width to 80 characters. Reasons for this include:

*   the ability to have multiple files open side by side;
*   viewing CSS on sites like GitHub, or in terminal windows;
*   providing a comfortable line length for comments.

```
/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
 * such a long comment that I easily break the 80 character limit, so I am
 * broken across several lines.
 */
```

There will be unavoidable exceptions to this rule—such as URLs, or gradient syntax—which shouldn't be worried about.


### File info

All CSS files should begin with the following standard template to describe the file. This follows the CSSdoc conventions for commenting.

See [CSS Automatic Documentation](https://github.com/Paratron/CSSdoc)

At least the version number should be updated every time you make a change, especially once the file goes into production.

TODO: This is currently a combination of docblock and CSSdoc -- is that okay?
TODO: What information is required here?


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


### Section titles

Begin every new major section of a CSS project with a title:


This is Harry Roberts' style:

```
/*------------------------------------*\
    SECTION-TITLE
\*------------------------------------*/

.selector {}
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

### Anatomy of a ruleset

Before we discuss how we write out our rulesets, let's first familiarise ourselves with the relevant terminology.

Every CSS rule has two parts: a selector and a declaration block which is wrapped in braces: {}.

```
[selector] {
    [property]: [value];
    [<--declaration--->]
}
```

For example:


```
.foo, .foo--bar,
.baz {
    background-color: green;
    color: red;
    display: block;
}
```

Here you can see we have:

*   related selectors on the same line; unrelated selectors on new lines;
*   a space before our opening brace ({);
*   properties and values on the same line;
*   a space after our property–value delimiting colon (:);
*   each declaration on its own new line;
*   the opening brace ({) on the same line as our last selector;
*   our first declaration on a new line after our opening brace ({);
*   our closing brace (}) on its own new line;
*   each declaration indented by four (4) spaces;
*   a trailing semi-colon (;) on our last declaration.

This format seems to be the largely universal standard (except for variations in number of spaces, with a lot of developers preferring two (2)).

As such, the following would be incorrect:

```
.foo, .foo--bar, .baz
{
  display:block;
  background-color:green;
  color:red }
```

Problems here include:

*   tabs instead of spaces;
*   unrelated selectors on the same line;
*   the opening brace ({) on its own line;
*   the closing brace (}) does not sit on its own line;
*   the trailing (and, admittedly, optional) semi-colon (;) is missing;
*   no spaces after colons (:).

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

### Meaningful whitespace

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



