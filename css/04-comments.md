CSS code standards guide

# Comments

As Harry Roberts points out in his [CSS Guidelines](http://cssguidelin.es/) document: "CSS needs more comments".





## In this section
<!-- MarkdownTOC -->

- [CSS needs more comments](#css-needs-more-comments)
- [General advice](#general-advice)
- [Sass comments](#sass-comments)
  - [Further reading](#further-reading)
- [Every CSS file must have...](#every-css-file-must-have)
  - [File information](#file-information)
    - [project](#project)
    - [version](#version)
    - [author](#author)
    - [copyright](#copyright)
    - [license](#license)
    - [since](#since)
    - [deprecated](#deprecated)
    - [example](#example)
    - [TODO](#todo)
  - [Table of contents](#table-of-contents)
  - [Section titles](#section-titles)
- [Magic numbers](#magic-numbers)
- [High-level](#high-level)
- [Object–extension pointers](#object–extension-pointers)
- [Reverse footnote comments](#reverse-footnote-comments)
- [Preprocessor comments](#preprocessor-comments)

<!-- /MarkdownTOC -->





## CSS needs more comments

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





## General advice

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





## Sass comments

If you are using [Sass](http://sass-lang.com/) please take note of the following distinction between the two type of comments used within Sass:

1.   Standard, multi-line CSS comments (`/* comment */`) remain visible after 
     the code has been compiled.
2.   Single-line comments (`// comment`) are removed from production code 
     after the script has been executy.


### Further reading

* [Comments: /* */ and //](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#comments)
* [Commenting on Sass Guidelines](http://sass-guidelin.es/#commenting)





## Every CSS file must have...

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






## Magic numbers

"Magic number" is an old school programming term for unnamed numerical constant. Basically, it’s just a random number that happens to just work™ yet is not tied to any logical explanation.

Needless to say magic numbers are a plague and should be avoided at all costs. When you cannot manage to find a reasonable explanation for why a number works, add an extensive comment explaining how you got there and why you think it works. Admitting you don’t know why something works is still more helpful to the next developer than them having to figure out what’s going on from scratch.

/**
 * 1. Magic number. This value is the lowest I could find to align the top of
 * `.foo` with its parent. Ideally, we should fix it properly.
 */
.foo {
  top: 0.327em; /* 1 */
}

See also

* [Sass styleguide CSS ](http://sass-guidelin.es/#magic-numbers)
* [Magic numbers in CSS](http://css-tricks.com/magic-numbers-in-css/)


## High-level

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


## Object–extension pointers
When working across multiple partials, or in an OOCSS manner, you will often find that rulesets that can work in conjunction with each other are not always in the same file or location. For example, you may have a generic button object—which provides purely structural styles—which is to be extended in a component-level partial which will add cosmetics. We document this relationship across files with simple object–extension pointers. In the object file:

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


## Reverse footnote comments

NOTE: I quite like this approach.

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

TODO:
From Trello: If you find an answer online (read: on Stack Overflow) then add the link to a comment so future people know what’s up.


## Preprocessor comments

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