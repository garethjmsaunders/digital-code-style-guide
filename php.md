# PHP style guide

Version 0.1
Last updated: Thursday 26 May 2016

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).


<!-- MarkdownTOC -->

- [1. File format](#1-file-format)
- [Principles of writing secure code](#principles-of-writing-secure-code)
- [Code standards](#code-standards)
    - [Bracket and parenthetic spacing](#bracket-and-parenthetic-spacing)
    - [Class and method naming](#class-and-method-naming)
    - [Code indenting](#code-indenting)
    - [Commenting](#commenting)
    - [Constants](#constants)
    - [File naming](#file-naming)
    - [Logical operators](#logical-operators)
    - [PHP closing tag](#php-closing-tag)
    - [Variable names](#variable-names)

<!-- /MarkdownTOC -->




## 1. File format

Files MUST be saved with Unicode (UTF-8) encoding; saving with the byte-order mark (UTF-8 with BOM) MUST NOT be used.





## Principles of writing secure code





## Code standards

### Bracket and parenthetic spacing

In general, parenthesis and brackets should not use any additional whitespaces. The exception is that a space should always follow PHP control structures that accept arguments with parenthesis to help distinguish them from functions and to increase readability.

Incorrect:

```
$arr[ $foo ] = 'foo';
```

Correct:

```
$arr[$foo] = 'foo';
```

Incorrect:

```
function foo ( $bar )
{
    
}
```

Correct:

```
function foo($bar)
{

}
```

Incorrect:

```
foreach( $query->result() as $row )
```

Correct:

```
foreach ($query->result() as $row)
```


### Class and method naming

Class names should always start with an uppercase letter. Multiple words should be separated with an underscore.

```
class Super_class
```

Class methods should be entirely lowercased and named to clearly indicate their function, preferably with a verb. Multiple words should be separated with an underscore.

```
function get_file_properties()
```

### Code indenting


[Link](url) 


### Commenting

In general, code should be commented proflifically. There is not a required format for comments, but the following are recommended.

DocBlock style comments preceding class, method and property declarations allow them to be picked up by IDEs.

```
/**
* Super Class
*
* @package Package name
* @subpackage Subpackage
* @category Category
* @author Auther name
* @link http://example.com
* /
```

```
/**
* Encodes string for use in XML 
*
* @param string $str Input string
* @return string
* /

function xml_encode($str)
```

Use single line comments within code, leaving a blank line between large comment blocks and code.

```
//break up the string by newlines
$parts = explode("\n", $str);

//A longer comment that needs more detail
//on what is occurring and why can use multiple single-line comments.

$parts = $this -> foo($parts);
```

### Constants

Constants follow the same guidelines as variables, except constants should always be uppercase.

### File naming

### Logical operators

Use of the `||` "or" comparison operator is discouraged as its clarity on some output devices is low (looking like the number 11 for instance). `&&` is preferred over `and` but either are acceptable. A space should always precede and follow `!`



### PHP closing tag

The PHP closing tag `?>` is optional to the PHP parser. If used, any whitespace following the closing tag can cause unwanted output, PHP errors, or if the latter are suppressed, blank pages. For this reason, all PHP files must omit the PHP closing tag and end with a single empty line instead. 









### Variable names

Guidelines for variable naming are similar to those used for class methods. Variables should only contain lowercase letters, use underscore separators, and be reasonably named to indicate their purpose and contents. Very short, non-word variable sdhould only used for iterations in `for()` loops.

Incorrect:

```
$j = 'foo'; //single letter variables should only be used in for() loops
$Str //contains uppercase letters
$bufferedText //uses CamelCase and could be shortened without losing semantic meaning
$groupid //multiple words, needs underscore separator
$name_of_last_city_used //too long
```

Correct:

```
for($j = 0; $j < 0; $j++)
$str
$buffer
$group_id
$last_city
```















