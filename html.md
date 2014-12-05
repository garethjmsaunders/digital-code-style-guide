# HTML Style Guide

Table of Contents

1. [Doctype](#doctype)
2. [Coding style](#codingstyle)
3. [Page titles](#pagetitles)
4. [Error pages](#errorpages)



## 1. Doctype <a name="doctype"></a>

A proper doctype which triggers standards mode in your browser should always be used. Quirks mode should always be avoided.

For simplicity, we use the html5 doctype:

```
<!DOCTYPE html>
```

## 2. Coding style <a name="codingstyle"></a>

### General formatting


* Paragraphs of text should always be placed in a `<p>` tag. Never use multiple `<br>` tags.
* Items in list form should always be in `<ul>`, `<ol>`, or `<dl>`. Never use a set of `<div>` or `<p>`.
* Every form input that has text attached should utilize a <label> tag. Especially radio or checkbox elements.
* Even though quotes around attributes is optional, always put quotes around attributes for readability.
* <mark>Avoid writing closing tag comments, like `<!-- /.element -->`. This just adds to page load time. Plus, most editors have indentation guides and open-close tag highlighting.</mark>
* Avoid trailing slashes in self-closing elements. For example, `<br>`, `<hr>`, `<img>`, and `<input>`.
* Don't set tabindex manually—rely on the browser to set the order.

```
<p class="line-note" data-attribute="106">This is my paragraph of special text.</p>
```

### Boolean attributes

Many attributes don't require a value to be set, like disabled or checked, so don't set them.

```
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
<option value="1" selected>1</option>
</select>
```

For more information, read the WhatWG section.

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

### Forms

* <mark>Lean towards radio or checkbox lists instead of select menus.</mark>
* Wrap radio and checkbox inputs and their text in `<label>`s. No need for for attributes here—the wrapping automatically associates the two.
* Form buttons should always include an explicit `type`. Use primary buttons for the `type="submit"` button and regular buttons for `type="button"`.
* The primary form button must come first in the DOM, especially for forms with multiple submit buttons. The visual order should be preserved with `float: right;` on each button.

### Tables

Make use of `<thead>`, `<tfoot>`, `<tbody>`, and `<th>` tags (and scope attribute) when appropriate. (Note: `<tfoot>` goes above `<tbody>` for speed reasons. You want the browser to load the footer before a table full of data.)

```
<table summary="This is a chart of invoices for 2011.">
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

## 3. Page Titles <a name="pagetitles"></a>

A standard format for the `<title></title>` tag.

<mark>Thoughts on using the dot `·` instead of `-`?</mark>

```
PAGENAME · University of St Andrews
```

For example:

```
Summer schools and programmes - University of St Andrews
```

## 4. Error Pages <a name="errorpages"></a>

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

* **maintenance** — For the rare case we must take the website down to perform maintenance. <mark>See Github [maintenance](https://github.com/maintenance.html). Don't need this.</mark>




---

#### References

The initial version of this style guide was based on [Github's HTML style guide](https://github.com/styleguide/templates).
