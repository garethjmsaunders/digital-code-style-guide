# HTML style guide

Version 0.2
Last updated: Tuesday 29 September 2015

TODO: Avoid `<address>` element.
TODO: Microformats? This should be in the CSS guide.

<!-- MarkdownTOC -->

- [1. Syntax](#1-syntax)
    - [General formatting](#general-formatting)
    - [Accessibility](#accessibility)
    - [Attribute order](#attribute-order)
    - [Boolean attributes](#boolean-attributes)
    - [Comments](#comments)
    - [Forms](#forms)
    - [Lean markup](#lean-markup)
    - [Lists](#lists)
    - [Tables](#tables)
- [2. HTML5 doctype](#2-html5-doctype)
- [3. Language attribute](#3-language-attribute)
- [4. Character encoding](#4-character-encoding)
- [5. Page title](#5-page-title)
- [6. IE compatibility](#6-ie-compatibility)
- [7. Including CSS and JavaScript](#7-including-css-and-javascript)
- [8. Avoid JavaScript generated markup](#8-avoid-javascript-generated-markup)
- [9. Error pages](#9-error-pages)
    - [Error templates](#error-templates)
- [References](#references)

<!-- /MarkdownTOC -->




## 1. Syntax 

### General formatting

As [@mdo](http://mdo.github.io/code-guide/) says in his code guide, "Strive to maintain HTML standards and semantics, but not at the expense of practicality. Use the least amount of markup with the fewest intricacies whenever possible."

* Use soft tabs with FOUR spaces. Spaces are the only way to guarantee code renders the same in any environment.
* Nested elements should be indented once (four spaces).
* Always use double quotes ("), never single quotes ('), on attributes. While optional, include quotes to improve code readability.
* Do not include a trailing slash on self-closing elements. These are optional in the [HTML5 specification](http://dev.w3.org/html5/spec-author-view/syntax.html#syntax-start-tag).


### Accessibility
* Do not set `tabindex` manually; rely on the browser to set the order.
* Paragraphs of text should always be placed in a `<p>` tag. Never use multiple `<br>` tags.


### Attribute order

HTML attributes should come in this particular order for easier reading of code.

* `class`
* `id`, `name`
* `data-*`
* `src`, `for`, `type`, `href`, `value`
* `title`, `alt`
* `role`, `aria-*`

Classes make for great reusable components, so they come first. Ids are more specific and should be used sparingly (e.g., for in-page bookmarks or JavaScript hooks), so they come second.


### Boolean attributes

Unlike in XHTML, in HTML5 many attributes don't require a value to be set, like `disabled` or `checked`, so do not set them.

```
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
    <option value="1" selected>1</option>
</select>
```

If you _must_ include the attribute's value then follow the [WhatWG guideline](https://html.spec.whatwg.org/multipage/infrastructure.html#boolean-attributes):

> If the attribute is present, its value must either be the empty string or [...] the attribute's canonical name, with no leading or trailing whitespace.

For more information, read the latest [HTML5 specification](http://www.w3.org/html/wg/drafts/html/master/infrastructure.html#boolean-attributes).


### Comments

Avoid writing closing tag comments, like `<!-- /.element -->`. This just adds to page load time. Plus, most editors have indentation guides and open-close tag highlighting.


### Forms

* Lean towards radio or checkbox lists instead of select menus.
* Wrap radio and checkbox inputs and their text in `<label>`s. No need for `for` attributes here: the wrapping automatically associates the two.
* Form buttons should always include an explicit `type`. Use primary buttons for the `type="submit"` button and regular buttons for `type="button"`.
* The primary form button must come first in the DOM, especially for forms with multiple submit buttons.


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


### Lists

List items should always be within `<ul>`, `<ol>`, or `<dl>` elements. Never use a set of `<div>` or `<p>` tags.


### Tables

Make use of `<thead>`, `<tfoot>`, `<tbody>`, and `<th>` tags (and scope attribute) when appropriate. (Note: `<tfoot>` goes above `<tbody>` for speed reasons. You want the browser to load the footer before a table full of data.)

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




## 2. HTML5 doctype 

Use a doctype that triggers standards mode in your browser; this ensures more consistent rendering in browsers. Quirks mode should always be avoided.

For simplicity, use the HTML5 doctype:

```
<!DOCTYPE html>
```




## 3. Language attribute

The HTML5 specification recommends specifying a language attribute on the root HTML element. This aids speech synthesis tools to determine what pronounciation to use, translation tools what rules to use, etc.

Read more abount the `lang` attribute in the latest [HTML5 spec](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-html-element).

Sitepoint lists all [ISO two-letter language codes](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/).

```
<html lang="en">
    <!-- ... -->
</html>
```




## 4. Character encoding

Ensure proper rendering of your content by declaring an explicit character encoding. When doing so, you may avoid using character entities in your HTML, provided their encoding matches that of the document (generally UTF-8).

The character encoding should be the first element within `head` as this affects the character set for the entire document, including the `title`.

```
<head>
    <meta charset="UTF-8">
    <title> ... </title>
</head>
```




## 5. Page title

The standard format for the `<title> ... </title>` tag uses a pipe (`|`) character to separate the page name from the University name:

```
Page name | University of St Andrews
```




## 6. IE compatibility

Internet Explorer 8 and newer supports the use of a document compatibility `<meta>` tag to specify what version of IE the page should be rendered as.

Unless you have a very specific use-case, it is most helpful to instruct IE to use the latest version of IE using edge mode.

For more information, read this comprehensive [Stack Overflow article](http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e).

```
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```




## 7. Including CSS and JavaScript

In line with the HTML5 specification, there is no need to specify a `type` when including CSS and JavaScript files, as `text/css` and `text/javascript` are their respective defaults.

```
<!-- Do this -->
<link rel="stylesheet" href="screen.css">
<script src="file.js"></script>

<!-- Not this -->
<link rel="stylesheet" type="text/css" href="screen.css">
<script type="text/javascript" src="file.js"></script>
```




## 8. Avoid JavaScript generated markup

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

Boolean attributes, Lean markup, Forms and Tables taken from [PrimerCSS](http://primercss.io/guidelines/)
