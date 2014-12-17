CSS code style guide

# 1. File format

This section outlines standards for creating and saving CSS files to ensure that they are not affected by encoding or file system differences. There is also general information about linking to external CSS files.





## In this section
<!-- MarkdownTOC depth=4 -->

- [Use multiple files, concatinate and minify](#use-multiple-files-concatinate-and-minify)
- [Character encoding](#character-encoding)
    - [@charset "UTF-8";](#charset-utf-8)
    - [Save as UTF-8 with BOM](#save-as-utf-8-with-bom)
    - [Further reading](#further-reading)
- [Use LF (Unix) line endings](#use-lf-unix-line-endings)
    - [Further reading](#further-reading-1)
- [Filenames](#filenames)
    - [Meaningful and descriptive](#meaningful-and-descriptive)
    - [Lowercase, no spaces](#lowercase-no-spaces)
    - [Use a hyphen (-) to separate words](#use-a-hyphen---to-separate-words)
    - [Underscores (_) for Sass files](#underscores-_-for-sass-files)
- [Link to external CSS files](#link-to-external-css-files)
    - [Link](#link)
    - [@import for debug and Sass only](#import-for-debug-and-sass-only)
    - [Do not use inline CSS](#do-not-use-inline-css)
    - [Do not use style elements](#do-not-use-style-elements)

<!-- /MarkdownTOC -->





## Use multiple files, concatinate and minify

With the meteoric rise of pre-processors (such as Sass and Less) of late, more often is the case that developers are splitting CSS across multiple files.
Even if not using a pre-processor, it is a good idea to split discrete chunks of code into their own files, which can then be concatenated and minified during a build process.





## Character encoding

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





## Use LF (Unix) line endings

Line feed (LF) Unix style line endings (sometimes called line breaks) should be used.

This is more of an issue for developers who work in Windows, but in any case ensure that your text editor is set up to save files with Unix line breaks.
For example, in Sublime Text you can add the following to your user settings: 

```
"default_line_ending": "LF",
```

### Further reading

*   [The Great Newline Schism]
        (http://blog.codinghorror.com/the-great-newline-schism/)





## Filenames

### Meaningful and descriptive

Filenames MUST be meaningful and descriptive, e.g. `external-02-standard.css` rather than `xtn-02s.css`. It can be useful to prefix the name of the project to the CSS file, e.g. `divinity-external-02-standard.css`.

If concatinated and minified most production files will be called something short anyway, e.g. `screen.css`.


### Lowercase, no spaces

Filenames MUST be all lowercase, with no spaces. This makes them easier to read and prevents links that substitute `%20` codes for spaces.


### Use a hyphen (-) to separate words

Use a hyphen (-) to separate words, e.g. `external-stylesheet.css`. This makes filenames easier to read than `externalstylsheetalloneword.css`.


### Underscores (_) for Sass files

Underscores (_) MUST be used only for naming Sass partial files.





## Link to external CSS files

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
