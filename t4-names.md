# T4 naming style guide

version 0.6.0
Last updated: Wednesday 8 February 2017

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

<!-- MarkdownTOC depth=4 -->

- [1. Introduction](#1-introduction)
- [2. Sections](#2-sections)
    - [2.1 Section names](#21-section-names)
    - [2.2 Output URIs](#22-output-uris)
- [3. Page layouts](#3-page-layouts)
- [4. Content types](#4-content-types)
    - [4.1 Content item names](#41-content-item-names)
    - [4.2 Content type name in content layout](#42-content-type-name-in-content-layout)
    - [4.3 Content type elements](#43-content-type-elements)
    - [4.4 List items](#44-list-items)
    - [4.5 Character limits](#45-character-limits)
- [5. Navigation objects](#5-navigation-objects)
- [6. Groups](#6-groups)
- [7. Channel names](#7-channel-names)
    - [8. Media types](#8-media-types)
    - [9. Media library](#9-media-library)
    - [10. Filenames](#10-filenames)
- [11. Metadata](#11-metadata)
    - [11.1 DC.title](#111-dctitle)
    - [11.2 DC.description](#112-dcdescription)
- [References](#references)

<!-- /MarkdownTOC -->


## 1. Introduction

TERMINALFOUR is a software company based in Dublin, their primary product, an enterprise content management system is also called TERMINALFOUR. In this document the software will be refered to as T4 and the company as TERMINALFOUR. 

Any new T4 assests MUST use these guidelines for naming.




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

TODO: Discuss more if we will need more than 1 or 2 page layouts. May remove this section if needed.
TODO: Need to research/test what is capable with programmable layouts




---

## 4. Content types

* The names of content types MUST correspond one-to-one with the names of patterns in the [digital pattern library](https://www.st-andrews.ac.uk/dpl/). 
* The content type description MUST be meaningful.
* Deprecated patterns MUST be marked as such.

| DPL pattern name | Content type name | Description                 |
|:---------------- |:----------------- |:--------------------------- |
| Alert            | Alert             | Feedback message |
| Footer           | Footer            | Default option for bottom of all pages |
| Info bite (deprecated) | Info bite (deprecated) | Short snippet of information |

One exception is when more than one content type is required to build the pattern. In this case the content type name SHOULD be prefixed with the pattern name followed by a space-hyphen-space and then the modifier or option.

| DPL pattern name | Content type name | Description                 |
|:---------------- |:----------------- |:--------------------------- |
| Navbox           | Navbox            | Feature navigation with optional background image |
| Navbox           | Navbox - 2 col    | Two columns of navboxes     |
| Navbox           | Navbox - 3 col    | Three columns of navboxes   |


### 4.1 Content item names

When using content types, content item names SHOULD include the content type name followed by a short description of its use. This makes it easier for users to understand the structure of the page.

* Separate the content type name from the description by a space-hyphen-space.

```
Navbox - Guardbridge energy project
Staff profile - Professor Sally Mapstone, Principal
```


### 4.2 Content type name in content layout

The content type name MUST never be output onto the HTML page. In other words, never use the following T4 tag in a content type layout:

```
<t4 type="content" name="Name" output="normal" modifiers=""  />
```

The content type name MUST be used solely as an identifier in the T4 backend.


### 4.3 Content type elements

* Content type element names MUST be simple and easy to understand.
* Content type element descriptions MUST be completed for all elements.

Element names need to be straightforward and simple. Description must also be filled out (unless the name alone is sufficent, eg. Section links).


### 4.4 List items

Try to make lists as reusable as you can, and make the list and list items names simple but descriptive. 

eg. To control the sizing of an element you make a list holding various bootstrap sizing classes. Name this `Bootstrap sizing` and elements `Small` with a value of `col-sm-4` and etc.


### 4.5 Character limits

In general we have several levels of character limits.

*Usage* | *Character limit* 
--- | --- 
Title / button text | 80
Links / small items | 1024-2048
Plain text | 25,000
General / Large containers  | 96,000




---

## 5. Navigation objects

Navigation objects are used primarily within page layouts.


section name


STEVE: T4 style guide for related content navigation objects - the name of the navigation object must refer to the content type and alternate formatter in the name e.g. 'programmable layout - text/footer'.  This saves a lot of detective work.

Also name for navigation objects must be lowercase.

 will primarily sit in page layouts, but still make them descriptive with their names, as the names now show up in the navigation object tag. We use a BEM-like naming for navigation objects.

BEM, meaning block, element, modifier, is a front-end methodology coined by developers working at Yandex. While BEM is a complete methodology, here we are only concerned with its naming convention. Further, the naming convention here only is BEM-like; the principles are exactly the same, but the actual syntax differs slightly.

BEM splits components' classes into three groups:

* Block: The sole root of the component.
* Element: A component part of the block.
* Modifier: A variant or extension of the block.

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

## 6. Groups

Users are NOT assigned things, rather we put Users in Groups and assign those Groups theings (Sections, Content types, page layouts, naviagtion objects, media library folders, etc). 




---

## 7. Channel names

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

### 8. Media types

Media types should be named following this structure:

File extension/*

e.g.
```
css/*
js/*
html/*
```




---

### 9. Media library

The media library should match the structure of the website. 




---

### 10. Filenames

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

## 11. Metadata

Metadata MUST be completed for all new sections. 

There are currently only two [Dublin Core metadata](http://dublincore.org/documents/usageguide/) elements used in T4:

* `DC.title`
* `DC.description`


### 11.1 DC.title

Dublin Core defines [DC.title](http://dublincore.org/documents/usageguide/elements.shtml) as "the name given to the resource. Typically, a title will be a name by which the resource is formally known."

* This SHOULD be the page heading, which also SHOULD be the same as the section name.


### 11.2 DC.description

Dublin Core defines [DC.description](http://dublincore.org/documents/usageguide/elements.shtml) as "An account of the content of the resource. Description may include but is not limited to: an abstract, table of contents, reference to a graphical representation of content or a free-text account of the content."

* Full sentences MUST be used.
* House style MUST be adhered to.
* Sentences MUST NOT exceed 160 characters.




---

## References

* [Dublin Core metadata](http://dublincore.org/documents/usageguide/elements.shtml)