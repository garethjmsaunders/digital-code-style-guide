# HTML Style Guide

Table of Contents

<!-- MarkdownTOC -->

- [1. Syntax](#1-syntax)
    - [General formatting](#general-formatting)
    - [Accessibility](#accessibility)
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
- [Error Pages](#error-pages)
    - [Error templates](#error-templates)
- [References](#references)

<!-- /MarkdownTOC -->




## 1. Syntax 

### General formatting

* Use soft tabs with FOUR spaces. Spaces are the only way to guarantee code renders the same in any environment.
* Nested elements should be indented once (four spaces).
* Always use double quotes ("), never single quotes ('), on attributes. While optional, include quotes to improve code readability.
* Do not include a trailing slash on self-closing elements. These are optional in the [HTML5 specification](http://dev.w3.org/html5/spec-author-view/syntax.html#syntax-start-tag).


### Accessibility
* Do not set `tabindex` manually; rely on the browser to set the order.
* Paragraphs of text should always be placed in a `<p>` tag. Never use multiple `<br>` tags.


### Boolean attributes

Many attributes don't require a value to be set, like `disabled` or `checked`, so don't set them.

```
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
    <option value="1" selected>1</option>
</select>
```

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
<span class="avatar">
    <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
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




---

## Error Pages

Error pages should be built such that they require zero scripting, zero JavaScript, and zero dependency on anything whatsoever. That means static HTML with inline CSS and base64-encoded images.

The following are banned from every error page:

* All `<script>` tags with an src attribute.
* All JavaScript that loads external data.
* All `<link>` tags.
* All `<img>` tags with an src pointing to a URL.

### Error templates

We use error pages for very specific purposes.


* **500** — An exception occurred and we couldn't recover.
<mark>See Github [500](https://github.com/500.html)</mark>

* **502** — The page likely timed out.
<mark>See Github [502](https://github.com/502.html)</mark>

* **503** — We are having a bad problem and the app server will not talk to us.
<mark>See Github [503](https://github.com/503.html)</mark>

* **404** — Not found.
<mark>See Github [404](https://github.com/404.html) and [404-pages](https://github.com/404-pages.html)</mark>

* **410** — Feature gone.
<mark>See Github [410](https://github.com/410.html). Not sure we need this one.</mark>

* **422** — When Nginx can't figure out what to do with your request, you could get this.
<mark>See Github [422](https://github.com/422.html). Don't need this.</mark>

* **maintenance** — For the rare case we must take the website down to perform maintenance. <mark>See Github [maintenance](https://github.com/maintenance.html). May need this for other systems, e.g. Pure.</mark>




---

## References

The initial version of this style guide was based on [Github's HTML style guide](https://github.com/styleguide/templates).


TODO: Avoid <address> element.
TODO: Microformats? This should be in the CSS guide.
