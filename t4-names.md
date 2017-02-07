# TerminalFOUR naming style guide

version 0.5.3
Last updated: Tuesday 7 February 2017

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

<!-- MarkdownTOC depth=4 -->

- [1. Introduction](#1-introduction)
- [2. T4 assets](#2-t4-assets)
    - [2.1 Section names](#21-section-names)
    - [2.2 Page layouts](#22-page-layouts)
    - [2.3 Content types](#23-content-types)
        - [2.3.1 Content item names](#231-content-item-names)
        - [2.3.2 Content type name in content layout](#232-content-type-name-in-content-layout)
        - [2.3.3 Content type elements](#233-content-type-elements)
        - [2.3.4 List items](#234-list-items)
        - [2.3.5 Character limits](#235-character-limits)
    - [2.4 Navigation objects](#24-navigation-objects)
    - [2.5 Groups](#25-groups)
    - [2.6 Channel names](#26-channel-names)
    - [2.7 Media types](#27-media-types)
    - [2.8 Media library](#28-media-library)
    - [2.9 File names](#29-file-names)
    - [2.10 Metadata](#210-metadata)
- [References](#references)

<!-- /MarkdownTOC -->


## 1. Introduction

TERMINALFOUR is a software company based in Dublin, their primary product, an enterprise content management system is also called TERMINALFOUR. In this document the software will be refered to as T4 and the company as TERMINALFOUR. 

Any new T4 assests MUST use these guidelines for naming.




---

## 2. T4 assets


### 2.1 Section names

In T4, section names are used to create the page URL unless an output URI is specified. It does this by stripping out all spaces and punctuation and converting the result to lowercase.

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




### 2.2 Page layouts

TODO: Discuss more if we will need more than 1 or 2 page layouts. May remove this section if needed.
TODO: Need to research/test what is capable with programmable layouts




### 2.3 Content types

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



#### 2.3.1 Content item names

When using content types, content item names SHOULD include the content type name followed by a short description of its use. This makes it easier for users to understand the structure of the page.

* Separate the content type name from the description by a space-hyphen-space.

```
Navbox - Guardbridge energy project
Staff profile - Professor Sally Mapstone, Principal
```


#### 2.3.2 Content type name in content layout

The content type name MUST never be output onto the HTML page. In other words, never use the following T4 tag in a content type layout:

```
<t4 type="content" name="Name" output="normal" modifiers=""  />
```

The content type name MUST be used solely as an identifier in the T4 backend.


#### 2.3.3 Content type elements

* Content type element names MUST be simple and easy to understand.
* Content type element descriptions MUST be completed for all elements.

Element names need to be straightforward and simple. Description must also be filled out (unless the name alone is sufficent, eg. Section links).


#### 2.3.4 List items

Try to make lists as reusable as you can, and make the list and list items names simple but descriptive. 

eg. To control the sizing of an element you make a list holding various bootstrap sizing classes. Name this `Bootstrap sizing` and elements `Small` with a value of `col-sm-4` and etc.

#### 2.3.5 Character limits

In general we have several levels of character limits.

*Usage* | *Character limit* 
--- | --- 
Title / button text | 80
Links / small items | 1024-2048
Plain text | 25,000
General / Large containers  | 96,000

### 2.4 Navigation objects

Navigation objects will primarily sit in page layouts, but still make them descriptive with their names, as the names now show up in the navigation object tag. We use a BEM-like naming for navigation objects.

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

### 2.5 Groups

Users are NOT assigned things, rather we put Users in Groups and assign those Groups theings (Sections, Content types, page layouts, naviagtion objects, media library folders, etc). 

### 2.6 Channel names

We name channels and stuff.

### 2.7 Media types

Media types should be named following this structure:

File extension/*

e.g.
```
css/*
js/*
html/*
```

### 2.8 Media library

The media library should match the structure of the website. 

### 2.9 File names

Filenames

TODO for t4: Regex pattern: ```(([a-z])+-*)*.filename```

Following this convention:

- Files SHOULD be named descriptively using lowercase letters.
- Words MUST be separated by hyphens.
- Filenames MUST never end with .inc. If you use an included file use a double suffix: .inc.php.
```
filename.jpg
my-document-name.pdf
```

### 2.10 Metadata

We do metadata.

## References


