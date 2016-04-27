# HTML style guide

Version 0.7
Last updated: Wednesday 27 April 2016

* TODO: Clarify the 'Avoid JavaScript generated markup' section.
* TODO: Merge in elements from https://github.com/joshbuchea/.
* TODO: Microformats.

<!-- MarkdownTOC -->

- [1. Syntax](#1-syntax)
    - [General formatting](#general-formatting)
    - [Accessibility](#accessibility)
    - [Attribute order](#attribute-order)
    - [Boolean attributes](#boolean-attributes)
    - [Lean markup](#lean-markup)
- [2. HTML5 doctype](#2-html5-doctype)
- [3. Language attribute](#3-language-attribute)
- [4. Character encoding](#4-character-encoding)
- [5. Page title](#5-page-title)
- [6. Links to external CSS and JavaScript files](#6-links-to-external-css-and-javascript-files)
    - [Do not use `type`](#do-not-use-type)
- [7. Element rules](#7-element-rules)
    - [Address](#address)
    - [Comments](#comments)
    - [Forms](#forms)
    - [Lists](#lists)
    - [Tables](#tables)
- [8. Avoid JavaScript-generated markup](#8-avoid-javascript-generated-markup)
- [9. Error pages](#9-error-pages)
    - [Error templates](#error-templates)
- [References](#references)

<!-- /MarkdownTOC -->




## 1. Syntax 

### General formatting

As [@mdo](http://mdo.github.io/code-guide/) says in his code guide, "Strive to maintain HTML standards and semantics, but not at the expense of practicality. Use the least amount of markup with the fewest intricacies whenever possible."

* Use soft tabs with FOUR spaces. Spaces are the only way to guarantee code renders the same in any environment.
* Nested elements should be indented once (four spaces).
* Elements should always be written in lowercase.
* Always use double quotes (`"`), never single quotes (`'`), on attributes. While optional, include quotes to improve code readability.
* Do not include a trailing slash on self-closing elements, such as `<br>`, `<hr>`, `<img>`, `<link>` and `<meta>`. These are optional in the [HTML5 specification](http://dev.w3.org/html5/spec-author-view/syntax.html#syntax-start-tag).


### Accessibility
* Do not set `tabindex` manually; rely on the browser to set the order.
* Paragraphs of text should always be placed in a `<p>` tag. Never use multiple `<br>` tags.


### Attribute order

HTML attributes should come in this particular order for easier reading of code.

* `class`
* `id`, `name`
* `data-*`
* `src`, `for`, `type`, `href`, `value`, `rel`
* `title`, `alt`
* `role`, `aria-*`

Classes make for great reusable components, so they come first; `id`s are more specific and should be used sparingly (e.g., for in-page bookmarks or JavaScript hooks), so they come second.


### Boolean attributes

Unlike in XHTML, in HTML5 many attributes don't require a value to be set, like `disabled` or `checked`, so do not set them.

```
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
    <option value="1" selected>1</option>
</select>
```

If you _must_ include the attribute's value (if you are using XHTML5, for instance) then follow the [WhatWG guideline](https://html.spec.whatwg.org/multipage/infrastructure.html#boolean-attributes):

> If the attribute is present, its value must either be the empty string or [...] the attribute's canonical name, with no leading or trailing whitespace.

For more information, read the latest [HTML5 specification](http://www.w3.org/html/wg/drafts/html/master/infrastructure.html#boolean-attributes).


### Lean markup

Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML. For example:

```
<!-- Not so great -->
<span class="user-photo">
    <img src="...">
</span>

<!-- Better -->
<img class="user-photo" src="...">
```




## 2. HTML5 doctype 

Use a doctype that triggers standards mode in your browser; this ensures more consistent rendering in browsers. Quirks mode should always be avoided.

For simplicity, use the HTML5 doctype:

```
<!DOCTYPE html>
```




## 3. Language attribute

The HTML5 specification recommends specifying a language attribute on the root HTML element. This aids speech synthesis tools to determine what pronounciation to use, translation tools what rules to use, etc.

Read more about the `lang` attribute in the latest [HTML5 spec](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-html-element).

Sitepoint lists all [ISO two-letter language codes](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/). W3C Internationalization site discusses [Language tags in HTML and XML](https://www.w3.org/International/articles/language-tags/).

```
<html lang="en-GB">
    <!-- ... -->
</html>
```




## 4. Character encoding

Ensure proper rendering of your content by declaring an explicit character encoding. When doing so, you may avoid using character entities in your HTML, provided their encoding matches that of the document, generally UTF-8 ([Unicode](http://unicode.org/)).

The character encoding should be the first element within `head` as this affects the character set for the entire document, including the `title`.

```
<head>
    <meta charset="utf-8">
    <title> ... </title>
</head>
```




## 5. Page title

The standard format for the `<title> ... </title>` tag uses a pipe (`|`) character to separate the page name from the University name:

```
Page name | University of St Andrews
```




## 6. Links to external CSS and JavaScript files

Link to external CSS and JavaScript files so that the files may be cached by your browser, saving bandwidth.

Do not embed CSS or JavaScript code within files (unless absolutely necessary) using `<style>` or `<script>` elements.


### Do not use `type`

In line with the HTML5 specification, there is no need to specify a `type` when including CSS and JavaScript files, as `text/css` and `text/javascript` are their respective defaults.

```
<!-- Do this -->
<link href="screen.css" rel="stylesheet">
<script src="file.js"></script>

<!-- Not this -->
<link type="text/css" rel="stylesheet" href="screen.css">
<script type="text/javascript" src="file.js"></script>
```




## 7. Element rules

Specific guidelines about certain HTML elements.


### Address

Do not use the `<address>` element. Despite having been around since HTML3 in 1995, it is invariably used the wrong way.

According to the [W3C HTML specification](http://w3c.github.io/html/sections.html#the-address-element):

> The `address` element represents the contact information for its nearest `article` or `body` element ancestor. If that is the `body` element, then the contact information applies to the document as a whole.
> 
>The `address` element must not be used to represent arbitrary addresses (e.g., postal addresses), unless those addresses are in fact the relevant contact information. (The `p` element is the appropriate element for marking up postal addresses in general.)

Rather than causing confusion, simply do not use it.


### Comments

Comments are your messages to other developers, as well as to yourself, if you come back to your code after several months working on something else.

Write comments as complete, grammatical sentences with an initial capital and a full-stop at the end.

As a rule, comment anything that isn't immediately obvious from the code alone. These could be explaining:

* the structure and/or role of a file;
* the thought process behind a way of doing things;
* the name of a digital pattern library pattern being used.

Keep comments up-to-date when code changes.

Comments may make their way into production environments.

Avoid writing closing tag comments, like `<!-- /.element -->`. This just adds to page load time. Plus, most editors have indentation guides and open/close tag highlighting.


### Forms

* Lean towards radio or checkbox lists instead of select menus; the former are more accessible.
* Wrap radio and checkbox inputs and their text in `<label>`s. No need for `for` attributes here: the wrapping automatically associates the two.
* Form buttons should always include an explicit `type`. Use primary buttons for the `type="submit"` button and regular buttons for `type="button"`.
* The primary form button must come first in the DOM, especially for forms with multiple submit buttons.


### Lists

List items should always be within `<ul>`, `<ol>`, or `<dl>` elements. Never use a set of `<div>` or `<p>` tags.

Although in HTML5 you may omit closing tags from certain elements such as list items, always close list items:

```
<!-- Do this -->
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<!-- Not this -->
<ul>
    <li>Item 1
    <li>Item 2
    <li>Item 3
</ul>
```


### Tables

Make use of `<thead>`, `<tfoot>`, `<tbody>`, and `<th>` tags (and `scope` attribute) when appropriate. (Note: `<tfoot>` goes above `<tbody>` for speed reasons. You want the browser to load the footer before a table full of data.)

```
<table summary="This is a chart of invoices for 2015.">
    <thead>
        <tr>
            <th scope="col">Table header 1</th>
            <th scope="col">Table header 2</th>
        </tr>
    </thead>
    <tfoot>
        <tr>
            <td>Table footer 1</td>
            <td>Table footer 2</td>
        </tr>
    </tfoot>
    <tbody>
        <tr>
            <td>Table data 1</td>
            <td>Table data 2</td>
        </tr>
    </tbody>
</table>
```




## 8. Avoid JavaScript-generated markup

Unless you are using a JavaScript templating engine such as [Handlebars]](http://handlebarsjs.com/), do not 'hide' markup in JavaScript files. It makes content harder to find, harder to edit and diminishes performance.

If you must, in the document into which you are injecting code prefix the section ID with `js-`, e.g.

```
<div id="js-generated-message"></div>
```




## 9. Error pages

Error pages should be built such that they require no external dependency on anything whatsoever. That means static HTML with inline CSS and base64-encoded images.

The following are banned from every error page:

* All `<script>` tags with a `src` attribute.
* All JavaScript that loads external data.
* All `<link>` tags.
* All `<img>` tags with a `src` pointing to a URL.


### Error templates

We use error pages for very specific purposes.

* **403** — Access denied/forbidden.
Requests that require authentication may return 404 Not Found, instead of 403 Forbidden, in some places. This is to prevent the accidental leakage of private information to unauthorized users. See GitHub [API Authentication](https://developer.github.com/v3/#authentication).

* **404** — Not found.
See Github [404](https://github.com/404.html) and [404-pages](https://github.com/404-pages.html)

* **410** — Feature gone.
See Github [410](https://github.com/410.html). Not sure we need this one.

* **500** — An exception occurred and we couldn't recover.
See Github [500](https://github.com/500.html)

* **502** — The page likely timed out.
See Github [502](https://github.com/502.html)

* **503** — We are having a bad problem and the app server will not talk to us.
See Github [503](https://github.com/503.html)

* **maintenance** — For the rare case we must take the website down to perform maintenance. See Github [maintenance](https://github.com/maintenance.html). May need this for other systems, e.g. Pure.




---

## References

The initial version of this style guide was based on [Github's HTML style guide](https://github.com/styleguide/templates), with inspiration too from [MDO's code guide](http://mdo.github.io/code-guide/).

Boolean attributes, Lean markup, Forms and Tables taken from [PrimerCSS](http://primercss.io/guidelines/).