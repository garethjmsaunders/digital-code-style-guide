# XML style guide

Version 0.2
Last updated: Thursday 28 April 2016


<!-- MarkdownTOC -->

- [1. Syntax](#1-syntax)
    - [General formatting](#general-formatting)
    - [Entity references](#entity-references)
    - [Empty tags](#empty-tags)
- [2. Reuse existing XML formats](#2-reuse-existing-xml-formats)
- [3. XML prolog](#3-xml-prolog)
- [4. Character encoding](#4-character-encoding)
- [5. Schemas](#5-schemas)
- [6. Namespaces](#6-namespaces)
- [7. Names](#7-names)
- [8. Elements](#8-elements)
- [9. Attributes](#9-attributes)
- [10. Key-value pairs](#10-key-value-pairs)
- [11. Elements vs. Attributes](#11-elements-vs-attributes)
- [12. CDATA](#12-cdata)
- [13. Comments](#13-comments)
- [References](#references)

<!-- /MarkdownTOC -->




## 1. Syntax


### General formatting

All XML documents MUST be 'well-formed' in accordance with the [latest XML specification](https://www.w3.org/TR/xml/).

For consistency:

* Use soft tabs with FOUR spaces. Spaces are the only way to guarantee code renders the same in any environment.
* Nested elements should be indented once (four spaces).
* Element names should be written in lower camel case, e.g. `lowerCamelCase`.
* Attributes should be wrapped in double quotes (`"`) rather than single quotes (`'`), on attributes.
* Use one space before attributes in an opening-tag. If the tag is too long, the space may be replaced by a newline.


### Entity references

Entity references other than the five XML standard entity references MUST NOT be used. The five acceptable XML standard entity references are:

* `&amp;` - ampersand (&)
* `&apos;` - apostrophe (')
* `&gt;` - greater than (>)
* `&lt;` - less than (<)
* `&quot;` - double quotation (")

 
Character references MAY be used, but actual characters are preferred, unless the character encoding is not UTF-8.  As usual, textual formats are exempt from this rule.


### Empty tags

* Self-closing (empty) elements must include a trailing slash, e.g. `<empty />`
* . OR Empty elements MAY be expressed as empty tags or a start-tag immediately followed by an end-tag. No distinction should be made between these two formats by any application.  [Rationale: They are not distinguished by XML parsers.]




## 2. Reuse existing XML formats

"Attempt to reuse existing XML formats whenever possible, especially those which allow extensions.  Creating an entirely new format should be done only with care and consideration; read Tim Bray's warnings first.  Try to get wide review of your format, from outside your organization as well, if possible.  [Rationale: New document formats have a cost: they must be reviewed, documented, and learned by users.]

"If you are reusing or extending an existing format, make sensible use of the prescribed elements and attributes, especially any that are required.  Don't completely repurpose them, but do try to see how they might be used in creative ways if the vanilla semantics aren't suitable.  As a last resort when an element or attribute is required by the format but is not appropriate for your use case, use some fixed string as its value.  [Rationale:  Markup reuse is good, markup abuse is bad.]

"When extending formats, use the implicit style of the existing format, even if it contradicts this guide.  [Rationale: Consistency.]




## 3. XML prolog

XML documents SHOULD begin with an XML prolog that contains:

    1. A declaration that specifies the version of XML being used;
    2. A document type declaration (DTD)

```
<?xml version="1.0" encoding="UTF-8"? standalone="yes"?>
<!DOCTYPE foo SYSTEM "foo.dtd">
<!-- End of XML prolog -->
```

* The XML prolog is optional. If it exists, it must come first in the document.
* XML documents may contain international characters, like Norwegian `øæå` or French `êèé`.
* To avoid errors, you should specify the encoding used, or save your XML files as UTF-8; UTF-8 is the default character encoding for XML documents.


## 4. Character encoding

The character encoding used SHOULD be UTF-8.  Exceptions should require extremely compelling circumstances.  [Rationale: UTF-8 is universal and in common use.]




## 5. Schemas

"Document formats SHOULD be expressed using a schema language.  [Rationale: Clarity and machine-checkability.]

The schema language SHOULD be RELAX NG compact syntax.  Embedded Schematron rules MAY be added to the schema for additional fine control.  [Rationale: RELAX NG is the most flexible schema language, with very few arbitrary restrictions on designs.  The compact syntax is quite easy to read and learn, and can be converted one-to-one to and from the XML syntax when necessary.  Schematron handles arbitrary cross-element and cross-attribute constraints nicely.]

Schemas SHOULD use the "Salami Slice" style (one rule per element).  Schemas MAY use the "Russian Doll" style (schema resembles document) if they are short and simple.  The "Venetian Blind" style (one rule per element type) is unsuited to RELAX NG and SHOULD NOT be used.

Regular expressions SHOULD be provided to assist in validating complex values.

DTDs and/or W3C XML Schemas MAY be provided for compatibility with existing products, tools, or users.  [Rationale: We can't change the world all at once.]"



## 6. Namespaces

Namespaces SHOULD be declared in the root element of a document wherever possible.  [Rationale: Clarity and consistency.]

Well-known prefixes such as html: (for XHTML), dc: (for Dublin Core metadata), and xs: (for XML Schema) should be used for standard namespaces.  [Rationale: Human readability.]



"Element names MUST be in a namespace, except when extending pre-existing document types that do not use namespaces.  A default namespace SHOULD be used.  [Rationale: Namespace-free documents are obsolete; every set of names should be in some namespace.  Using a default namespace improves readability.]

Attribute names SHOULD NOT be in a namespace unless they are drawn from a foreign document type or are meant to be used in foreign document types.  [Rationale: Attribute names in a namespace must always have a prefix, which is annoying to type and hard to read.]

Namespace names are HTTP URIs.  Namespace names SHOULD take the form https://example.com/whatever/year, where whatever is a unique value based on the name of the document type, and year is the year the namespace was created.  There may be additional URI-path parts before the year.  [Rationale: Existing convention.  Providing the year allows for the possible recycling of code names.]

Namespaces MUST NOT be changed unless the semantics of particular elements or attributes has changed in drastically incompatible ways.  [Rationale: Changing the namespace requires changing all client code.]

Namespace prefixes SHOULD be short (but not so short that they are likely to be conflict with another project).  Single-letter prefixes MUST NOT be used. Prefixes SHOULD contain only lower-case ASCII letters.  [Rationale: Ease of typing and absence of encoding compatibility problems.]"



## 7. Names

"Note: "Names" refers to the names of elements, attributes, and enumerated values.

All names MUST use lowerCamelCase. That is, they start with an initial lower-case letter, then each new word within the name starts with an initial capital letter. [Rationale: Adopting a single style provides consistency, which helps when referring to names since the capitalization is known and so does not have to be remembered.  It matches Java style, and other languages can be dealt with using automated name conversion.]

Names MUST contain only ASCII letters and digits.  [Rationale: Ease of typing and absence of encoding compatibility problems.]

Names SHOULD NOT exceed 25 characters. Longer names SHOULD be avoided by devising concise and informative names.  If a name can only remain within this limit by becoming obscure, the limit SHOULD be ignored.  [Rationale: Longer names are awkward to use and require additional bandwidth.]

Published standard abbreviations, if sufficiently well-known, MAY be employed in constructing names. Ad hoc abbreviations MUST NOT be used.  Acronyms MUST be treated as words for camel-casing purposes: informationUri, not informationURI. [Rationale:  An abbreviation that is well known to one community is often incomprehensible to others who need to use the same document format (and who do understand the full name); treating an acronym as a word makes it easier to see where the word boundaries are.] "





## 8. Elements

"All elements MUST contain either nothing, character content, or child elements.  Mixed content MUST NOT be used.  [Rationale: Many XML data models don't handle mixed content properly, and its use makes the element order-dependent.  As always, textual formats are not covered by this rule.]

XML elements that merely wrap repeating child elements SHOULD NOT be used.  [Rationale: They are not used in Atom and add nothing.]"



## 9. Attributes

"Document formats MUST NOT depend on the order of attributes in a start-tag.  [Rationale: Few XML parsers report the order, and it is not part of the XML Infoset.]

Elements SHOULD NOT be overloaded with too many attributes (no more than 10 as a rule of thumb).  Instead, use child elements to encapsulate closely related attributes.  [Rationale: This approach maintains the built-in extensibility that XML provides with elements, and is useful for providing forward compatibility as a specification evolves.]

Attributes MUST NOT be used to hold values in which line breaks are significant.  [Rationale: Such line breaks are converted to spaces by conformant XML parsers.]

Document formats MUST allow either single or double quotation marks around attribute values.  [Rationale:  XML parsers don't report the difference.]
"

Redundant whitespace in a tag SHOULD NOT be used.  Use one space before each attribute in a start-tag; if the start tag is too long, the space MAY be replaced by a newline.  [Rationale: Consistency and conciseness.]

Attribute values MAY be surrounded with either quotation marks or apostrophes. Specifications MUST NOT require or forbid the use of either form.  &apos; and &quot; may be freely used to escape each type of quote.  [Rationale: No XML parsers report the distinction.]


## 10. Key-value pairs

"Simple key-value pairs SHOULD be represented with an empty element whose name represents the key, with the value attribute containing the value. Elements that have a value attribute MAY also have a unit attribute to specify the unit of a measured value.  For physical measurements, the SI system SHOULD be used.  [Rationale: Simplicity and design consistency.  Keeping the value in an attribute hides it from the user, since displaying just the value without the key is not useful.]

If the number of possible keys is very large or unbounded, key-value pairs MAY be represented by a single generic element with key, value, and optional unit and scheme attributes (which serve to discriminate keys from different domains).  In that case, also provide (not necessarily in the same document) a list of keys with human-readable explanations."


## 11. Elements vs. Attributes

Note:  There are no hard and fast rules for deciding when to use attributes and when to use elements.  Here are some of the considerations that designers should take into account; no rationales are given.
12.1. General points:
Attributes are more restrictive than elements, and all designs have some elements, so an all-element design is simplest -- which is not the same as best.

In a tree-style data model, elements are typically represented internally as nodes, which use more memory than the strings used to represent attributes.  Sometimes the nodes are of different application-specific classes, which in many languages also takes up memory to represent the classes.

When streaming, elements are processed one at a time (possibly even piece by piece, depending on the XML parser you are using), whereas all the attributes of an element and their values are reported at once, which costs memory, particularly if some attribute values are very long.

Both element content and attribute values need to be escaped appropriately, so escaping should not be a consideration in the design.

In some programming languages and libraries, processing elements is easier; in others, processing attributes is easier.  Beware of using ease of processing as a criterion.  In particular, XSLT can handle either with equal facility.

If a piece of data should usually be shown to the user, consider using an element; if not, consider using an attribute.  (This rule is often violated for one reason or another.)

If you are extending an existing schema, do things by analogy to how things are done in that schema.

Sensible schema languages, meaning RELAX NG and Schematron, treat elements and attributes symmetrically.  Older and cruder schema languages such as DTDs and XML Schema, tend to have better support for elements.
12.2 Using elements
If something might appear more than once in a data model, use an element rather than introducing attributes with names like foo1, foo2, foo3 ....

Use elements to represent a piece of information that can be considered an independent object and when the information is related via a parent/child relationship to another piece of information.

Use elements when data incorporates strict typing or relationship rules.

If order matters between two pieces of data, use elements for them: attributes are inherently unordered.

If a piece of data has, or might have, its own substructure, use it in an element: getting substructure into an attribute is always messy.  Similarly, if the data is a constituent part of some larger piece of data, put it in an element.

An exception to the previous rule: multiple whitespace-separated tokens can safely be put in an attribute.  In principle, the separator can be anything, but schema-language validators are currently only able to handle whitespace, so it's best to stick with that.

If a piece of data extends across multiple lines, use an element: XML parsers will change newlines in attribute values into spaces. 

If a piece of data is very large, use an element so that its content can be streamed.

If a piece of data is in a natural language, put it in an element so you can use the xml:lang attribute to label the language being used.  Some kinds of natural-language text, like Japanese, often make use annotations that are conventionally represented using child elements; right-to-left languages like Hebrew and Arabic may similarly require child elements to manage bidirectionality properly.
12.3 Using attributes
If the data is a code from an enumeration, code list, or controlled vocabulary, put it in an attribute if possible.  For example, language tags, currency codes, medical diagnostic codes, etc. are best handled as attributes.

If a piece of data is really metadata on some other piece of data (for example, representing a class or role that the main data serves,  or specifying a method of processing it), put it in an attribute if possible.

In particular, if a piece of data is an ID for some other piece of data, or a reference to such an ID, put the identifying piece in an attribute.  When it's an ID, use the name xml:id for the attribute.

Hypertext references are conventionally put in href attributes.

If a piece of data is applicable to an element and any descendant elements unless it is overridden in some of them, it is conventional to put it in an attribute.  Well-known examples are xml:lang, xml:space, xml:base, and namespace declarations.

If terseness is really the most important thing, use attributes, but consider gzip compression instead -- it works very well on documents with highly repetitive structures.




## 12. CDATA

CDATA sections MAY be used; they are equivalent to the use of &amp; and &lt;.  Specifications MUST NOT require or forbid the use of CDATA sections.  [Rationale: Few XML parsers report the distinction, and combinations of CDATA and text are often reported as single objects anyway.]

CDATA sections allow the use of all valid Unicode characters in their literal forms. The CDATA
contents bypass parsing so are great to use when trying to include content containing markup
that should be taken in its literal form and not processed as part of the document. CDATA sections
begin with `<![CDATA[`, which is followed by your content, and end with ``]]>`, like so:

```
<![CDATA[Lorem ipsum dolor sit amet, consectetuer adipiscing elit.]]>
```




## 13. Comments

Comments are your messages to other developers, as well as to yourself, if you come back to your code after several months working on something else.

Write comments as complete, grammatical sentences with an initial capital and a full-stop at the end.

As a rule, comment anything that isn't immediately obvious from the code alone. These could be explaining:

* the structure and/or role of a file;
* the thought process behind a way of doing things;
* the name of a digital pattern library pattern being used.

Keep comments up-to-date when code changes.

Comments may make their way into production environments.

Avoid writing closing tag comments, like `<!-- /.element -->`. This just adds to page load time. Plus, most editors have indentation guides and open/close tag highlighting.

Comments MUST NOT be used to carry real data.  Comments MAY be used to contain TODOs in hand-written XML.  Comments SHOULD NOT be used at all in publicly transmitted documents. [Rationale:  Comments are often discarded by parsers.]

If comments are nevertheless used, they SHOULD appear only in the document prolog or in elements that contain child elements.  If pretty-printing is required, pretty-print comments like elements, but with line wrapping.  Comments SHOULD NOT appear in elements that contain character content.  [Rationale:  Whitespace in and around comments improves readability, but embedding a comment in character content can lead to confusion about what whitespace is or is not in the content.]

Comments SHOULD have whitespace following <!-- and preceding -->.  [Rationale: Readability.]

---

## References

The initial version of this style guide was based on [Google XML document format style guide](https://google.github.io/styleguide/xmlstyle.html)