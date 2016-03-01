# Markdown style guide

Version 0.1
Last updated: Tuesday 01 March 2016

TODO: 

<!-- MarkdownTOC -->

- [1. File layout](#1-file-layout)
    - [Filenames](#filenames)
    - [Spacing](#spacing)
        - [Intro block](#intro-block)
- [2. Block Elements](#2-block-elements)
    - [Paragraphs and line breaks](#paragraphs-and-line-breaks)
    - [Headings](#headings)
    - [Blockquotes](#blockquotes)
    - [Lists](#lists)
        - [Unordered lists](#unordered-lists)
        - [Ordered lists](#ordered-lists)
        - [Formatting lists](#formatting-lists)
    - [Code blocks](#code-blocks)
    - [Horizontal rules](#horizontal-rules)
- [3. Span elements](#3-span-elements)
    - [Links](#links)
        - [Inline links](#inline-links)
        - [Reference links](#reference-links)
        - [Automatic links](#automatic-links)
    - [Emphasis](#emphasis)
        - [Bold](#bold)
        - [Italic](#italic)
    - [Code](#code)
    - [Images](#images)
- [4. Miscellaneous](#4-miscellaneous)
    - [Backslash escapes](#backslash-escapes)

<!-- /MarkdownTOC -->




## 1. File layout

dddd


### Filenames


### Spacing

#### Intro block

Use


## 2. Block Elements


### Paragraphs and line breaks

According to the [Markdown definition of a paragraph](https://daringfireball.net/projects/markdown/syntax#p):

> A paragraph is simply one or more consecutive lines of text, separated 
> by one or more blank lines. (A blank line is any line that looks like a 
> blank line — a line containing nothing but spaces or tabs is considered 
> blank.) Normal paragraphs should not be indented with spaces or tabs.

* Paragraphs must be separated with a single blank line.
* Do not indent normal paragraphs with either tabs or spaces.
* To create a line break (to insert a `<br />` tag) end a line with two or more spaces, then type return.
 

### Headings

Markdown supports two styles of headings: [Setext](http://docutils.sourceforge.net/mirror/setext.html) and [atx](http://www.aaronsw.com/2002/atx/); we use atx.

Atx-style headings use **one to six number sign characters** (`#`), also called a hash or pound sign, at the start of the line. These correspond to heading levels 1 to 6. For example:

```
# This is a heading 1 (H1)

## This is a heading 2 (H2)

### This is a heading 3 (H3)

#### This is a heading 4 (H4)

##### This is a heading 5 (H5)

###### This is a heading 6 (H6)
```

There must be at least **one blank line either side** of the heading.

```
\\ This is correct

## Heading

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua.


\\ This is wrong
## Heading
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua.

```

**Do not close** atx-style headings.

```
\\ This is correct

## This is a heading 2 (H2)


\\ This is wrong

## This is a heading 2 (H2) ##

```


### Blockquotes

Prefix each line with a **greater-than sign** `>`. Do not use the lazy method of only prefixing the first line.

```
> This is a blockquote with two paragraphs. Notice how each
> line is prefixed with a greater-than symbol. You may be
> familiar with this convention from quoting passages in
> your email client.
> 
> You'll notice that blank lines also include a single `>`
> character.
```

Try to avoid nesting blockquotes.


### Lists

#### Unordered lists

Use **asterisks** (`*`) for unordered lists.

```
* Apples
* Bananas
* Oranges
* Pears
```

#### Ordered lists

Use the **number one followed by a full-stop** (`1.`) for ordered lists. The markdown interpreter will automatically number the list correctly, but by using `1.` for each list item you can easily reorder lists without having to labouriously renumber everything.

```
1. Apples
1. Bananas
1. Oranges
1. Pears
```

#### Formatting lists

You may use hanging indents, using either 4 spaces or a tab.

```
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit. 
    Aliquam endrerit mi posuere lectus. Vestibulum enim wisi, 
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.
```

To include a code block within a list item indent it twice — use 8 spaces or two tabs.

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit. 
    Aliquam endrerit mi posuere lectus. Vestibulum enim wisi, 
    viverra nec, fringilla in, laoreet vitae, risus.

        <code>This is a code block</code>

*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.

To separate list items (wrapping each list item with a `<p>` tag) add a blank line between each item:

```
1. Apples

1. Bananas

1. Oranges

1. Pears
```


### Code blocks

To produce pre-formatted code blocks, add **three backticks** (`` ``` ``) on blank lines above and below your code.

    ```
    <html lang="en">
        <!-- ... -->
    </html>
    ```


### Horizontal rules

Use **three hyphens on their own line** to add a horizontal rule (`<hr />`). There should be a **blank line above and below** the row of hyphens (otherwise the previous line may be misinterpreted as a Setext heading 2.

```
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum
dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident. End of previous paragraph.

---

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. 
```




## 3. Span elements


### Links

Markdown supports three styles of links: inline links, reference links, and automatic links.


#### Inline links

Link text is wrapped in square brackets, followed immediately (no space) by parentheses containing the URL. There may be an optional title, wrapped in quotes, after the URL.

```
This is [an example](http://www.example.com/ "Title") inline link.

This [example](http://www.example.com/) inline link has no title attribute.
```

#### Reference links

Reference-style links are best used when you need to link to the same resource repeatedly throughout a document.

Link text is wrapped in square brackets, followed immediately by a space and then a link label also wrapped in square brackets.

```
This is [an example] [label] reference-style link.
```

At the bottom of the section you are editing (above the next `## Heading 2,`) define your link using the label wrapped in square brackets, followed by a colon, space, URL, space, and optional title wrapped in double quotes.

```
[label]: http://www.example.com/ "Optional title"
```

For longer URLs you may put the title attribute on a separate line, indented with 4 spaces or a tab, like this:

```
[label]: http://www.example.com/longer/path/to/resource/here/
    "Optional title"
```


#### Automatic links

Markdown also supports a shortcut style for creating automatic links for URLs where you want to show the URL itself, or for email addresses.

Simply wrap the URL or email address in angle brackets, e.g.

```
* <http://digitalcommunications.wp.st-andrews.ac.uk>
* <digitalcommunications@st-andrews.ac.uk>
```

These will display as:

* <http://digitalcommunications.wp.st-andrews.ac.uk>
* <digitalcommunications@st-andrews.ac.uk>


### Emphasis

#### Bold

To make text bold, wrap the text with **two asterisks**.

```
To make text bold, wrap the text with **two asterisks**.
```


#### Italic

To make text italic, wrap the text with _one underscore_.

```
To make text italic, wrap the text with _one underscore_.
```

Although asterisks and underscores can be used for both bold and italic (one for italic, two for bold) they are easier to distinguish if used for different purposes.


### Code

Use single backticks to markup inline code, such as `<code>`.

```
Use single backticks to markup inline code, such as `<code>`.
```


### Images

Although images are rarely used in our markdown documents, use the fuller syntax:

```
![Alt text](http://example.com/path/to/img.jpg "Optional title")
```




## 4. Miscellaneous


### Backslash escapes

Markdown allows you to use backslash escapes to generate literal characters that would otherwise have special meaning in Markdown’s formatting syntax.

Markdown provides backslash escapes for the following characters:

```
\   backslash
`   backtick
*   asterisk
_   underscore
{}  curly braces
[]  square brackets
()  parentheses
#   hash mark
+   plus sign
-   minus sign (hyphen)
.   dot
!   exclamation mark
```