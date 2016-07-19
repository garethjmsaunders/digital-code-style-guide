# JavaScript style guide

version 0.6.0
Last updated: Tuesday 19 July 2016

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

<!-- MarkdownTOC depth=4 -->

- [1. Introduction](#1-introduction)
- [2. File format](#2-file-format)
    - [Unicode \(UTF-8\)](#unicode-utf-8)
    - [Use LF \(Unix\) line endings](#use-lf-unix-line-endings)
- [3. General formatting](#3-general-formatting)
    - [Indentation](#indentation)
    - [Line width \(80 characters\)](#line-width-80-characters)
    - [One statement per line](#one-statement-per-line)
    - [Semicolons](#semicolons)
    - [Parentheses](#parentheses)
    - [Brace style](#brace-style)
    - [Single and double quotation marks](#single-and-double-quotation-marks)
- [4. Spaces](#4-spaces)
    - [Remove trailing spaces](#remove-trailing-spaces)
    - [Array items](#array-items)
    - [Blocks](#blocks)
    - [Functions](#functions)
    - [Logical comparisons](#logical-comparisons)
    - [String concatenation](#string-concatenation)
- [5. Comments](#5-comments)
- [6 Naming conventions](#6-naming-conventions)
    - [Classes and methods](#classes-and-methods)
        - [Class names](#class-names)
        - [Class method names](#class-method-names)
    - [Constant names](#constant-names)
    - [Enumerated types \(enum\)](#enumerated-types-enum)
    - [Filenames](#filenames)
    - [Function names](#function-names)
    - [Variable names](#variable-names)
- [7. Language specifics](#7-language-specifics)
    - [Arrays and objects](#arrays-and-objects)
    - [Avoid mixing technologies](#avoid-mixing-technologies)
    - [Continue](#continue)
    - [Eval](#eval)
    - [Function arguments](#function-arguments)
    - [JavaScript Object Notation \(JSON\)](#javascript-object-notation-json)
    - [Quoting strings](#quoting-strings)
    - [Ternary operators](#ternary-operators)
    - [Variable declarations](#variable-declarations)
    - [With](#with)
- [8. JSLint configuration](#8-jslint-configuration)
- [Further reading](#further-reading)

<!-- /MarkdownTOC -->



TODO: Merge in style guide advice from Douglas Crockford (author of JSLint) http://javascript.crockford.com/code.html
TODO: Rewrite to be more prescriptive, and less first-person plural.




## 1. Introduction

JavaScript code SHOULD pass [JSLint](http://www.jslint.com/). JSLint defines an opinionated subset of JavaScript with a very strict definition of acceptable style.




---

## 2. File format

### Unicode (UTF-8)

* Files MUST be saved with Unicode (UTF-8) encoding.
* Files MUST NOT be saved with the byte-order mark (UTF-8 with BOM).


### Use LF (Unix) line endings

Lines MUST end with a single, Unix-style line feed (LF) character.

Do not use carriage returns (CR) as used by Apple OS, or carriage return/line feed (CRLF) as used by Windows.

Ensure that your text editor is set up to save files with Unix-style line breaks. For example, in Sublime Text you can add the following to your user settings:

```
    "default_line_ending": "LF",
```




---
## 3. General formatting

### Indentation

JavaScript parsers do not care about indentation, it is solely used for the convenience of human readers. Indentation should be used to enhance readability of the source code.

* Do not indent code unnecessarily.
* Indent on purpose.
* Indent consistently.

Code indentation should always reflect the logical structure of the code.

* Use only spaces, and indent FOUR (4) spaces at a time. Spaces are the only way to guarantee code renders the same in any environment.
* Use spaces for indentation. Do not use tabs in your code. You should set your editor to emit spaces when you hit the tab key.
* Nested elements SHOULD be indented once (four spaces).


### Line width (80 characters)

Where possible, limit JavaScript files' width to 80 characters. Reasons for this include:

* the ability to have multiple files open side by side;
* viewing JavaScript on sites like GitHub, or in a terminal window;
* providing a comfortable line length for comments.

Do not worry about unavoidable exceptions to this rule, such as URLs.


### One statement per line

Statements SHOULD always be written one per line; do not combine statements on one line.

One statement per line makes code easier to read and compare using a diff tool.

At best multiple, combined statements makes code look messy and confusing, at worst it can contribute to the insertion of errors or missing something when reviewing code.

There MAY be some exceptions, such as `switch` statements, but readability and ease of debugging and code maintenance should take precidence over strict adherence to this rule, e.g.

```
switch (new Date().getDay()) {
    case 0:   day = "Sunday";        break;
    case 1:   day = "Monday";        break;
    case 2:   day = "Tuesday";       break;
    case 3:   day = "Wednesday";     break;
    case 4:   day = "Thursday";      break;
    case 5:   day = "Friday";        break;
    case 6:   day = "Saturday";      break;
}
```


### Semicolons

JavaScript uses semicolons (`;`) to mark the end of a statement; it is required on these statements:

* `break`
* `continue`
* `debugger`
* `do`
* `empty`
* `expression`
* `for` (separating control clauses)
* `return`
* `throw`
* `var`

Every statement MUST be followed by a semicolon except for

* `for`
* `function`
* `if`
* `switch`
* `try`
* `while`.

You MUST NOT rely on automatic semicolon insertion.

A code block, enclosed in braces `{...}` is not a statement, it is a group of statements. Each statement within the code block MUST be terminated with a semicolon, but the code block itself is NOT terminated with a semicolon.


### Parentheses

Parentheses SHOULD only be used where they are required. Additional parentheses may be used to clarify groupings in complex conditional constructs, but knowing operator precedence should eliminate their necessity.

When calling class constructors with no arguments, always include parentheses: The constructors are functions, so constructor calls need to look like function calls.

Never use parentheses for unary operators such as `delete`, `typeof` and `void` or after keywords such as `return`, `throw` as well as others (`case`, `in` or `new`).


### Brace style

You MUST use 1TBS (one true brace style) to indent braces, e.g.

```
if ( condition ) {
    action1();
    action2();
} else if ( condition2 && condition3 ) {
    action3();
    action4();
} else {
    defaultaction();
}
```

Braces MUST always be used, even when they are not required. This means that single-statement inline control structures MUST NOT be used.


### Single and double quotation marks

Use single quotes (`'`) for symbols, character constants, and internal strings such as property names.

Use double quotes (`"`) for strings that will be exported from the program, such as HTML fragments, URLs, or messages to the user.




---

## 4. Spaces

Spaces MUST always be inserted after commas, and on both sides of logical, comparison, string and assignment operators.


### Remove trailing spaces

You MUST remove trailing whitespace at the end of each line of code.


### Array items

Spaces MUST always be inserted after commas.

When referring to array items, one space MUST be inserted around the index ONLY if it is a variable.

```
x = [ 1, 2, 3 ];

x = foo['bar'];
x = foo[0];
x = foo[ bar ];
```


### Blocks

Spaces MUST be inserted on both sides of the opening and closing parenthesis of `if`, `elseif`, `foreach`, `for`, and `switch` blocks.

```
for ( expr1; expr2; expr3 ) {
    ... 
}

let iterable = [10, 20, 30];
for ( let value of iterable ) {
  console.log(value);
}

if ( x < 45 ) {
    else if ( x > 45 ) {
}

switch ( $i ) { 
    ... 
}
```


### Functions

When defining a function:

```
function my_function( parameter1, parameter2, parameter3 ) {
    ...
}
```


When calling a function:

```
my_function( parameter1, parameter2, parameter3 );
```


### Logical comparisons

When performing logical comparisons:

```
if ( ! $foo ) { 
    ...
}

x == 23;
baz === '-5';
foo && bar;
! foo;

```


### String concatenation

When concatenating strings using the `+` operator, a space MUST be inserted on both sides of the operator to improve readability.

```
institution = "University";
town = "St Andrews";
name = institution + " of " + town;
```




---
## 5. Comments

Comment as much as needed but not more. Comments are your messages to other developers (and yourself, if you come back to your code after several months working on something else). We prefer to use the `/* */` rather than the `//`.

TODO: Expand this. Consider JSDoc. Compare with PHP guide.

```
module = function() {
    var current = null;
    function init() {
    };

    /*
    function show(){
        current = 1;
    };

    function hide(){
        show();
    };
    */

return { init:init, show:show, current:current }
}();
```




---

## 6 Naming conventions

### Classes and methods

#### Class names

Regex pattern: `(([A-Z]{1}[a-zA-Z]*)_*)+`

* Class names MUST always start with an uppercase letter.
* Multiple words MUST be separated with an underscore.
* Subsequent words MUST also begin with an uppercase letter.
* Abbreviations MUST be written in all-uppercase.

```
class Class_Name
class Longer_Class_Name
class WP_HTTP
```


#### Class method names

Regex pattern: `(([a-z]+)_*)+`

A method is a function used in the context of a class/object.

* Class methods MUST be entirely lowercase
* Class methods SHOULD be named to clearly indicate their function, preferably beginning with a verb.
* Multiple words MUST be separated with an underscore.

```
function get_file_properties()
```


### Constant names

Regex pattern: `(([A-Z]+)_*)+`

Constants MUST only contain UPPERCASE letters, use underscore separators, and be reasonably named to indicate their purpose and contents. Numbers SHOULD NOT be used in constants.

```
const MIN_VALUE = 0.0;
const MAX_VALUE = 1.0;
```


### Enumerated types (enum)

Regex pattern: `(([a-z]+)_*)+`

An enumerated type (also called enumeration or enum) is a data type that consists of a set of named values called elements, members or enumerators of the type.

The enumerator names are usually identifiers that behave as constants in the language. A variable that has been declared as having an enumerated type can be assigned any of the enumerators as a value.

In other words, an enum restricts variables to one value from a predefined set of constants. For example,

```
var WeekDay = { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY };
```

* Enums MUST be entirely lowercase
* Enums SHOULD be named to clearly indicate their function, preferably beginning with a verb.
* Multiple words MUST be separated with an underscore.


### Filenames

Regex pattern: `(([a-z])+-*)+(.inc)*.js

* Files SHOULD be named descriptively.
* Files MUST be named using only lowercase letters.
* Words MUST be separated by hyphens.

```
filename.js
my-plugin-name.js
helper-class-library.js
```


### Function names

Regex pattern: `(([a-z])+_*)+`

Function MUST contain only lowercase letters, use underscore separators, and be reasonably named to indicate their purpose and contents.

```
function write_message() {
    ...
}

function greet_fullname( first_name, last_name ) {
    ...
}
```



### Variable names

Regex pattern: `\$(([a-z])+_*)+`

Variable names MUST contain only lowercase letters, use underscore separators, and be reasonably named to indicate their purpose and contents. Very short, non-word variables should only used for iterations in `for()` loops.

```
for ( var j = 0; j < 0; j++ ) { ... }
var str = '';
var buffer = '';
var group_id = 0;
var last_city = 'St Andrews';
```



---

## 7. Language specifics

### Arrays and objects

* Use `[]` instead of `new Array()`.
* Use `{}` instead of `new Object()`.


### Avoid mixing technologies

While it is possible to create everything you need in a document using JavaScript and the DOM it is not necessarily the most effective way of doing so. We could write CSS inline on a DOM element, but it would be far better to apply a class and let the styling be handled in the style sheet.

This
```
var f = document.getElementById('mainform');
var inputs = f.getElementsByTagName('input');
for(var i=0,j=inputs.length;i<j;i++){
  if(inputs[i].className === 'mandatory' &&
     inputs[i].value === ''){
    inputs[i].className += ' error';
  }
}
```

Not this
```
var f = document.getElementById('mainform');
var inputs = f.getElementsByTagName('input');
for(var i=0,j=inputs.length;i<j;i++){
    if(inputs[i].className === 'mandatory' &&
    inputs[i].value === ''){
    inputs[i].style.borderColor = '#f00';
    inputs[i].style.borderStyle = 'solid';
    inputs[i].style.borderWidth = '1px';
    }
}
```


### Continue

Avoid use of the `continue` statement as it tends to obscure the control flow of a function.

### Eval

You MUST NOT use `eval`.

`eval` is probably the most misused feature of JavaScript, because there is almost always a better way to achieve the same thing.

See the [JSLint article](https://jslinterrors.com/eval-is-evil) for more information.


### Function arguments

Where possible, all function arguments SHOULD be listed on the same line.

If doing so would exceed the 80-column limit, the arguments must be line-wrapped in a readable way. To save space, you may wrap as close to 80 as possible, or put each argument on its own line to enhance readability. The indentation may be either four spaces, or aligned to the parenthesis.

Either of these is acceptable:

```
// Indent arguments by four spaces
function my_function( parameter1, parameter2, parameter3, 
    parameter4, parameter5 ) {
    ...
}

// Align arguments with first row
function my_function( parameter1, parameter2, parameter3, 
                      parameter4, parameter5 ) {
    ...
}
```


### JavaScript Object Notation (JSON)

If manually creating a JavaScript Object Notation (JSON) file use the following layout:

```
{"employees":[
    { "firstName":"John",  "lastName":"Burnet" },
    { "firstName":"Agnes", "lastName":"Blackadder" },
    { "firstName":"David", "lastName":"Russell" }
]}
```

* Records MUST be indented with FOUR (4) spaces.
* You MAY align name:value pairs to make the lines easier to read.
* Records SHOULD be listed on a single line. If lines exceed 80 characters then split across multiple lines, e.g.

```
{"employees":[
    { "firstName":  "John",
      "lastName":   "Burnet",
      "employeeID": "0001"
    },
    { "firstName":  "Agnes",
      "lastName":   "Blackadder",
      "employeeID": "0002"
    },
    { "firstName":  "David",
      "lastName":   "Russell",
      "employeeID": "0003" }
]}
```


### Quoting strings

You SHOULD always use single-quotes (`'`) rather than double-quotes (`"`). This is helpful when creating strings that include HTML:

```
var msg = 'This is some <a href="#url">HTML</a>';
```




### Ternary operators

A ternary operator is a conditional operator that uses the syntax:

```
(condition) ? (if_true) : (if_false)
```

* Ternary operators SHOULD only be used for simple evaluations.
* Ternary operators MUST NOT be used for complex or nested conditionals.
* The complete statement SHOULD fit onto a single 80-character line; if the line exceeds 80-characters then split and indent across multiple lines, prefixing the true and false evaluations with the `?` and `:` operators.

```
(condition) 
    ? (if_true) 
    : (if_false)
```


### Variable declarations

* All variables MUST be declared before being used.
* Implied global variables MUST NOT be used.
* Use of global variables SHOULD be minimized.

Listed variables in alphabetical order, if possible and comment each.

```
var currentStudentID;   // This is taken from the SITS student record
var graduationYear;     // Calculated from start date
var orientation;        // options: landscape or portrait
```


### With

The `with` statement MUST not be used.

See [with Statement Considered Harmful](http://yuiblog.com/blog/2006/04/11/with-statement-considered-harmful/) on the Yahoo! UI blog.




---


## 8. JSLint configuration

The pattern library provides a JSLint config file that implements many of these rules and can be used to ensure that your code matches our work.

---




## Further reading

For more in-depth treatment, see the following:

* [Code conventions for the JavaScript programming language](http://javascript.crockford.com/code.html) by Douglas Crockford
* [JSLint](http://www.jslint.com/help.html)
* [Google JavaScript style guide](https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
