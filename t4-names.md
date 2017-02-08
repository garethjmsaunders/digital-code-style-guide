# T4 naming style guide

version 0.6.5
Last updated: Wednesday 8 February 2017

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

<!-- MarkdownTOC depth=2 -->

- [1. Introduction](#1-introduction)
- [2. Sections](#2-sections)
    - [2.1 Section names](#21-section-names)
    - [2.2 Output URIs](#22-output-uris)
- [3. Page layouts](#3-page-layouts)
- [4. Content types \(creating\)](#4-content-types-creating)
    - [4.1 Name and description](#41-name-and-description)
    - [4.2 Elements](#42-elements)
    - [4.3 Character limits](#43-character-limits)
    - [4.4 Layout](#44-layout)
- [5. Content types \(using\)](#5-content-types-using)
- [6. List items](#6-list-items)
    - [6.1 Name](#61-name)
    - [6.2 Value](#62-value)
- [7. Navigation objects](#7-navigation-objects)
- [8. Groups](#8-groups)
    - [8.1 Group names](#81-group-names)
- [9. Channel names](#9-channel-names)
    - [10. Media content types](#10-media-content-types)
    - [11. Media library](#11-media-library)
    - [12. Filenames](#12-filenames)
- [13. Metadata](#13-metadata)
    - [13.1 DC.title](#131-dctitle)
    - [13.2 DC.description](#132-dcdescription)
- [14. References](#14-references)

<!-- /MarkdownTOC -->


## 1. Introduction

TERMINALFOUR is a software company based in Dublin, their primary product, an enterprise content management system is also called TERMINALFOUR. In this document the software will be refered to as T4 and the company as TERMINALFOUR. 

Any new T4 assets MUST use these guidelines for naming.




---

## 2. Sections

### 2.1 Section names

In T4, section names are used to create the page URL unless an output URI is specified. It does this by stripping out all spaces and punctuation and converting the result to lowercase.

### 2.2 Output URIs

See http://www.st-andrews.ac.uk/digital-standards/service-manual/links/

So, for example, a section name of "Academic Schools and Departments" will become `academicschoolsanddepartments`.

* Output URIs SHOULD always be defined.
* Output URIs MUST use hyphens to separate words and all lower case letters.
* Output URLs SHOULD always be meaningful: avoid obscure abbreviations.

```
events
current-students
alumni-and-development
research-and-teaching
```

For subjects, output URIs MUST include the subject first, followed by speciality or otherwise

```
english
english-creative-writing
physics
physics-pod
```




---

## 3. Page layouts

Page layouts are used to standardise the appearance of content on your page. Page layout names:

Use a [BEM](http://getbem.com/naming/)-like naming convention which splits components' classes into three groups:

* Block: The root of the component (e.g. external website, school website, etc.).
* Element: A component part of the block (e.g. homepage, content page, etc.).
* Modifier: A variant or extension of the block or element.

Page layout names MUST use only one of the following formats:

```
block__element
block__element--modifier
block--modifier
```

* MUST use only a-z, 0-9, underscore or hyphen.
* MUST NOT end with a full-stop.
* MAY use abbreviations only if these are well known.
* MUST use two underscores (`__`) between block and element.
* MUST use two hyphens (`--`) between block and modifier, or element and modifier.

Good examples

```
// block__element
external__home

// block__element--modifier
external__content--full-width
external__content--aside
global__blank--html
school__home--arts
school__home--divinity
school__home--medicine
school__home--science

// block--modifier
htaccess--staff-only
htaccess--staff-student

```




---

## 4. Content types (creating)

### 4.1 Name and description

The name of a content type MUST correspond one-to-one with the name of its pattern in the [digital pattern library](https://www.st-andrews.ac.uk/dpl/). 

* Must begin with a capital letter.
* MUST use only A-Z, a-z, 0-9, spaces or hyphens.
* MUST NOT end with a full-stop.
* MAY use abbreviations only if these are well known.
* Deprecated patterns MUST be marked as `(deprecated)`.

The description of a content type MUST be added for every content type and be meaningful.

* Must begin with a capital letter.
* MUST use only A-Z, a-z, 0-9, spaces or hyphens.
* MUST NOT end with a full-stop.
* MAY use abbreviations only if these are well known.


Good examples

| DPL pattern name | Content type name | Description                 |
|:---------------- |:----------------- |:--------------------------- |
| Alert            | `Alert`           | Feedback message |
| Footer           | `Footer`          | Default option for bottom of all pages |
| Info bite (deprecated) | Info bite (deprecated) | Short snippet of information |


#### 4.1.1 More than one content type per pattern

One exception is when more than one content type is required to build the pattern. In this case the content type name SHOULD be prefixed with the pattern name followed by a space-hyphen-space and then the modifier or option.

| DPL pattern name | Content type name     | Description                 |
|:---------------- |:--------------------- |:--------------------------- |
| Navbox grid      | `Navbox grid - start` | Navbox grid - START - use this to start the row. |
| Navbox           | `Navbox`              | Flexible navbox allows different sizes and elements, including picture or solid colour background, text options. |
| Navbox grid      | `Navbox grid - end`   | Navbox grid - END - use this to end the row. |


### 4.2 Elements

#### 4.2.1 Element names

Content type element names MUST be simple and easy to understand.

* Must begin with a capital letter.
* MUST use only A-Z, a-z, 0-9, spaces or hyphens.
* MUST NOT end with a full-stop.
* MAY use abbreviations only if these are well known.


#### 4.2.2 Element descriptions

Descriptions MUST be completed for all elements.

* Must begin with a capital letter.
* MUST use only A-Z, a-z, 0-9, spaces or hyphens.
* MUST end with a full-stop.
* MAY use abbreviations only if these are well known.


### 4.3 Character limits

In general we have several levels of character limits.

| Usage                       | Character limit |
|:--------------------------- |:--------------- |
| Title / button text         | 80              |
| Links / small items         | 1024 to 2048    |
| Plain text                  | 25,000          |
| General / Large containers  | 96,000          |



### 4.4 Layout

The content type name MUST NOT be output onto the HTML page. In other words, never use the following T4 tag in a content type layout:

```
// Never use
<t4 type="content" name="Name" output="normal" modifiers=""  />
```

The content type name MUST be used solely as an identifier in the T4 backend.




---

## 5. Content types (using)

When using content types, content item names MUST include the content type name followed by a short description of its use. This makes it easier for users to understand the structure of the page.

* Must begin with the content type name.
* Content type and short description MUST be separated by a space, hyphen and space, thus: `Content type - Description`.
* Both content type and description MUST begin with a capital letter.
* MUST use only A-Z, a-z, 0-9, spaces or hyphens.
* MUST NOT end with a full-stop.
* MAY use abbreviations only if these are well known.

Good examples

```
Code - Facts and figures page
General - Banner style
Navbox - Guardbridge energy project
Page title - Facts and figures
Staff profile - Professor Sally Mapstone, Principal
```




---

## 6. List items

Before creating a new list check to see if an existing list may be used or extended. 

Try to make lists as reusable as you can, and make the list and list items names simple and descriptive.


### 6.1 Name

The list item names should be user-centred and descriptive. This is what appears in the list in the content type in T4.

* MUST begin with a capital letter.
* MUST use only A-Z, a-z, 0-9, spaces, hyphens or parentheses.
* MUST NOT end with a full-stop.
* MAY use abbreviations only if these are well known.


### 6.2 Value

The value is what is inserted into the HTML code on the page.

* MUST use only a-z, 0-9, or hyphens.
* MUST NOT end with a full-stop.

Good examples

#### List: Alert

| Name               | Value         |
|:------------------ |:------------- |
| Success (green)    | alert-success |
| Information (blue) | alert-info    |
| Warning (beige)    | alert-warning |
| Danger (red)       | alert-danger  |


#### List: Bootstrap sizing

| Name   | Value     |
|:------ |:--------- |
| Small  | col-sm-4  | 
| Medium | col-sm-6  |
| Large  | col-sm-8  |
| Full   | col-xs-12 |




---

## 7. Navigation objects

Navigation objects are used primarily within page layouts.


section name


STEVE: T4 style guide for related content navigation objects - the name of the navigation object must refer to the content type and alternate formatter in the name e.g. 'programmable layout - text/footer'.  This saves a lot of detective work.

Also name for navigation objects must be lowercase.

 will primarily sit in page layouts, but still make them descriptive with their names, as the names now show up in the navigation object tag. We use a BEM-like naming for navigation objects.



An example:

This is the template for related content:
 - page element - section this is for

e.g.
```
footer - scripts
```

Template for section details:
 - name of the nav object type - section it refers to / usage

e.g.
```
Generate file - file-name.txt
link - about
```




---

## 8. Groups

Access to content and assets within T4 MUST be assigned on a group basis.

* Users MUST NOT be assigned to individual pages.
* Users MUST be assigned to groups.
* Groups must be assigned to sections, content types, page layouts, navigation objects, media library directories, etc.


### 8.1 Group names

Ideally, groups SHOULD be named by function (such as Orientation) rather than organisational structure (such as Student Services). Group names:

* MUST begin with a capital letter.
* MUST use only A-Z, a-z, 0-9 spaces and hyphens.
* MUST NOT end with a full-stop.
* MAY use abbreviations only if these are well known.

Good examples

```
External website
Visiting days
Alumni and donors
About - facts and figures
Service manual - corporate ID
```




---

## 9. Channel names

Channels are used to assemble content to publish to a website. Channel names:

* MUST be short and descriptive.
* MUST begin with a capital letter.
* MUST NOT include camelCase.
* MUST NOT end with a full-stop.

Good examples
```
External website
Internal website
Sandbox
RSS feed
```



---

### 10. Media content types

Media is a special, system-wide content type that determines how media items from the media library appear on a published webpage.

Content layouts for media content types MUST follow this pattern:

> file_type/*


* The file type MUST be descriptive using either a generic type (image, application, path) or the file extension (e.g. css, docx, pdf).
* The content layout name MUST be lowercase

Good examples

```
application/*
css/*
docx/*
image/*
js/*
path/*
pdf/*
pptx/*
xslx/*
xml/*
```




---

### 11. Media library

The media library should match the structure of the website. 




---

### 12. Filenames

Regex pattern: `([a-z0-9\-]+).([a-z0-9]{3,})`

The following guidance is taken from the digital standard service manual page on [filenames](https://www.st-andrews.ac.uk/digital-standards/service-manual/filenames/).

Files MUST be named in a consistent way according to the guidelines below. This will ensure they are web safe.

* You MUST use only lowercase letters (`a-z`), numerals (`0-9`), and hyphens (`-`).
* You MUST NOT use special characters (e.g. `á`, `ê`, `ï`, `õ`, `ù`) or other punctuation marks, including underscores (`_`).
* You MUST NOT use spaces: instead you MUST use hyphens in place of spaces to delimit words.
* You MUST NOT include dates or version numbers in filenames.
* Filenames MUST be short, meaningful and descriptive.

Correct
```
guidance-notes-for-direct-applicants.pdf
visiting-day-programme.pdf
william-and-mary.docx
ug-prospectus.pdf
```

Incorrect
```
Guidance notes for direct applicants.pdf
VDprog.pdf
william-&-mary-version-2.1.docx
ug-prospectus-2016-2017.pdf
```

The digital communications team reserves the right to change (or request changes to) filenames if they do not meet digital best practice.




---

## 13. Metadata

Metadata MUST be completed for all new sections. 

There are currently only two [Dublin Core metadata](http://dublincore.org/documents/usageguide/) elements used in T4:

* `DC.title`
* `DC.description`


### 13.1 DC.title

Dublin Core defines [DC.title](http://dublincore.org/documents/usageguide/elements.shtml) as "the name given to the resource. Typically, a title will be a name by which the resource is formally known."

* This SHOULD be the page heading, which also SHOULD be the same as the section name.


### 13.2 DC.description

Dublin Core defines [DC.description](http://dublincore.org/documents/usageguide/elements.shtml) as "An account of the content of the resource. Description may include but is not limited to: an abstract, table of contents, reference to a graphical representation of content or a free-text account of the content."

* Full sentences MUST be used.
* House style MUST be adhered to.
* Sentences MUST NOT exceed 160 characters.




---

## 14. References

* [Dublin Core metadata](http://dublincore.org/documents/usageguide/elements.shtml)