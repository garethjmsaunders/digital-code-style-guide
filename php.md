# PHP style guide

Version 0.3.0
Last updated: Monday 11 July 2016

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).


<!-- MarkdownTOC -->

- [1. Introduction](#1-introduction)
- [2. File format](#2-file-format)
    - [Unicode \(UTF-8\)](#unicode-utf-8)
    - [Use LF \(Unix\) line endings](#use-lf-unix-line-endings)
- [3. No shorthand PHP tags](#3-no-shorthand-php-tags)
- [4. PHP closing tag](#4-php-closing-tag)
- [5. General formatting](#5-general-formatting)
    - [Indentation](#indentation)
    - [Line width \(80 characters\)](#line-width-80-characters)
    - [One statement per line](#one-statement-per-line)
    - [Semicolons](#semicolons)
    - [Parentheses](#parentheses)
    - [Brace style](#brace-style)
    - [Single and double quotation marks](#single-and-double-quotation-marks)
- [6. Spaces](#6-spaces)
    - [Whitespace](#whitespace)
    - [Remove trailing spaces](#remove-trailing-spaces)
    - [Array items](#array-items)
    - [Blocks](#blocks)
    - [Functions](#functions)
    - [Logical comparisons](#logical-comparisons)
    - [String concatenation](#string-concatenation)
    - [Type casting](#type-casting)
- [7. Comments](#7-comments)
- [8. Naming conventions](#8-naming-conventions)
    - [Classes and methods](#classes-and-methods)
        - [Class names](#class-names)
        - [Class method names](#class-method-names)
    - [Constant names](#constant-names)
    - [Filenames](#filenames)
    - [Function names](#function-names)
    - [Variable names](#variable-names)
- [9. Language specifics](#9-language-specifics)
    - [Arrays - EDIT THIS](#arrays---edit-this)
        - [Numerically indexed arrays](#numerically-indexed-arrays)
        - [Associative arrays](#associative-arrays)
    - [elseif, not else if #](#elseif-not-else-if-)
    - [Logical operators](#logical-operators)
    - [Regular expressions #](#regular-expressions-)
    - [Ternary operator](#ternary-operator)
    - [TRUE, FALSE, and NULL](#true-false-and-null)
    - [Yoda conditions](#yoda-conditions)
- [10. Debug code](#10-debug-code)
- [Further reading](#further-reading)

<!-- /MarkdownTOC -->

TODO: Update comments
TODO: Rewrite introduction
TODO: Arrays
TODO: Security
TODO: Avoid magic numbers


## 1. Introduction

This style guide is based mainly around the assumption that we will be writing simple code and/or WordPress development, so it is based heavily on the [WordPress PHP coding standards](https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/).

Important thing is code consistency and comprehensibility. If you use another framework (such as CodeIgniter or Symphony) it is more important to write your code consistently with the parent framework than follow this guide to the letter.

Focus on code, not formatting
Consistency
Readability
Collaboration

Don’t invent your own standard. You are not special and your PHP source code is not unique.




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



## 3. No shorthand PHP tags

You must NEVER use shorthand PHP start tags; always choose full PHP tags.

```
// Correct
<?php ... ?>
<?php echo $var; ?>


// Incorrect
<? ... ?>
<?= $var ?>
```




## 4. PHP closing tag

The PHP closing tag (`?>`) is optional for the PHP parser. However, if used any whitespace following the closing tag can cause unexpected output, errors, or blank pages (if errors are suppressed).

For files that contain only PHP code you MUST omit the PHP closing tag. Remove any trailing whitespace and end the file with a single empty line.

```
// Wrong
<?php
    example () {
        // code        
    }
?>

// Correct
<?php
    example () {
        // code        
    }

```




## 5. General formatting

### Indentation

PHP parsers do not care about indentation, it is solely used for the convenience of human readers. Indentation should be used to enhance readability of the source code.

* Do not indent code unnecessarily.
* Indent on purpose.
* Indent consistently.

Code indentation should always reflect the logical structure of the code.

* Use soft tabs with FOUR spaces. Spaces are the only way to guarantee code renders the same in any environment.
* Nested elements SHOULD be indented once (four spaces).


### Line width (80 characters)

Where possible, limit PHP files' width to 80 characters. Reasons for this include:

* the ability to have multiple files open side by side;
* viewing PHP on sites like GitHub, or in a terminal window;
* providing a comfortable line length for comments.

Do not worry about unavoidable exceptions to this rule, such as URLs, or within a `heredoc`.


### One statement per line

Statements SHOULD always be written one per line; do not combine statements on one line.

One statement per line makes code easier to read and compare using a diff tool.

At best multiple, combined statements makes code look messy and confusing, at worst it can contribute to the insertion of errors or missing something when reviewing code.

There MAY be some exceptions, such as `switch` statements, but readability and ease of debugging and code maintenance should take precidence over strict adherence to this rule, e.g.

```
<?php
switch ($_REQUEST['tag']) {
    default:   $string=FALSE;                     break; 
    case 1:    $string='first choice';            break; 
    case 2:    $string='another possible choice'; break; 
    case 3:    $string='maybe something else';    break; 
    case 4:    $string='yet another idea';        break; 
}
```


### Semicolons

PHP generally uses semicolons (`;`) to mark the end of a statement. However, if the PHP closing tag is on the same line after a statement, the semicolon is optional and should not be used.

A code block, enclosed in braces `{...}` is not a statement, it is a group of statements. Each statement within the code block MUST be terminated with a semicolon, but the code block itself is NOT terminated with a semicolon.

<small>Source: MIT Sloan School of Management</small>


### Parentheses

Parentheses SHOULD only be used where they are required. Additional parentheses may be used to clarify groupings in complex conditional constructs, but knowing operator precedence should eliminate their necessity.

Parentheses SHOULD NOT be used when using language constructs such as `echo`, `print`, `include`, or `require`. These are not functions and don't require parentheses around their parameters.

When calling class constructors with no arguments, always include parentheses: The constructors are functions, so constructor calls need to look like function calls.

<small>Source: MIT Sloan School of Management</small>


### Brace style

You MUST use 1TBS (one true brace style) to indent braces, e.g.

```
if ( condition ) {
    action1();
    action2();
} elseif ( condition2 && condition3 ) {
    action3();
    action4();
} else {
    defaultaction();
}
```

Braces MUST always be used, even when they are not required. This means that single-statement inline control structures MUST NOT be used.

You MAY use alternative syntax for control structures (e.g. `if/endif`, `while/endwhile`) especially in your templates where PHP code is embedded within HTML, for instance in WordPress:

```
<?php if ( have_posts() ) : ?>
    <div class="hfeed">
        <?php while ( have_posts() ) : the_post(); ?>
            <article id="post-<?php the_ID() ?>" class="<?php post_class() ?>">
                <!-- ... -->
            </article>
        <?php endwhile; ?>
    </div>
<?php endif; ?>
```

<small>Source: WordPress</small>


### Single and double quotation marks

Use single and double quotes when appropriate. If you’re not evaluating anything in the string, you SHOULD use single quotes.

You SHOULD almost never have to escape quotes in a string, because you can just alternate your quoting style, like so:

```
echo '<a href="/static/link" title="Yeah yeah!">Link name</a>';
echo "<a href='$link' title='$linktitle'>$linkname</a>";
```

In WordPress, text that goes into attributes should be run through `esc_attr()` so that single or double quotes do not end the attribute value and invalidate the HTML and cause a security issue.

<small>Source: WordPress</small>




## 6. Spaces


### Whitespace

There MUST NOT be any whitespace before the opening PHP tag.


### Remove trailing spaces

You MUST remove trailing whitespace at the end of each line of code.


### Array items

Spaces MUST always be inserted after commas, and on both sides of logical, comparison, string and assignment operators.

When referring to array items, one space MUST be inserted around the index ONLY if it is a variable.

```
x = array( 1, 2, 3 );  // Note no space after array keyword

$x = $foo['bar'];
$x = $foo[0];
$x = $foo[ $bar ];
```


### Blocks

Spaces MUST be inserted on both sides of the opening and closing parenthesis of `if`, `elseif`, `foreach`, `for`, and `switch` blocks.

```
for ( expr1; expr2; expr3 ) {
    ... 
}

foreach ( $foo as $bar ) { 
    ... 
}

if ( x < 45 ) {
    elseif ( x > 45 ) {
}

switch ( $i ) { 
    ... 
}
```


### Functions

When defining a function:

```
function my_function( $param1 = 'foo', $param2 = 'bar' ) {
    ...
}
```


When calling a function:

```
my_function( $param1, func_param( $param2 ) );
```


### Logical comparisons

When performing logical comparisons:

```
if ( ! $foo ) { 
    ...
}

x == 23;
$baz === '-5';
$term .= 'X';
foo && bar;
! foo;

```


### String concatenation

When concatenating strings using the `.` operator, a space MUST be inserted on both sides of the operator to improve readability.

```
$example = 'University' . ' of ' . 'St Andrews';
```


### Type casting

When type casting:

```
foreach ( (array) $foo as $bar ) { 
    ...
}

$foo = (boolean) $bar;
```
 
Source: WordPress




## 7. Comments

TODO: Organize Your Code
•Learn to utilize @category, @package, @subpackage
•PEAR style is the de facto standard
•Always Prefix Your Classes (Foo_)

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



## 8. Naming conventions


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

Variables should only contain UPPERCASE letters, use underscore separators, and be reasonably named to indicate their purpose and contents. Numbers SHOULD NOT be used in constants.

```
define('MIN_VALUE', '0.0');
define('MAX_VALUE', '1.0');

class Constants {
  const MIN_VALUE = 0.0;      // RIGHT - Works INSIDE of a class definition.
  const MAX_VALUE = 1.0;      // RIGHT - Works INSIDE of a class definition.
}
```


### Filenames

Regex pattern: `(([a-z])+-*)+(.inc)*.php`

Following the WordPress convention:

* Files SHOULD be named descriptively using lowercase letters.
* Words MUST be separated by hyphens.
* Filenames MUST never end with `.inc`. If you use an included file use a double suffix: `.inc.php`.

```
filename.php
my-plugin-name.php
helper-class-library.inc.php
```

Class file filenames should be based on the class name with `class-` prepended and the underscores in the class name replaced with hyphens, for example `WP_Error` becomes:

```
class-wp-error.php
```


### Function names

Regex pattern: `(([a-z])+_*)+`

Function MUST contain only lowercase letters, use underscore separators, and be reasonably named to indicate their purpose and contents.

```
function write_message() {
    echo 'Hello world!';
}

function greet_fullname( $first_name, $last_name ) {
    echo "Hello $first_name $last_name";
}
```



### Variable names

Regex pattern: `\$(([a-z])+_*)+`

Variable names MUST contain only lowercase letters, use underscore separators, and be reasonably named to indicate their purpose and contents. Very short, non-word variable sdhould only used for iterations in `for()` loops.

```
for ( $j = 0; $j < 0; $j++ ) { ... }
$str
$buffer
$group_id
$last_city
```


## 9. Language specifics

### Arrays - EDIT THIS

#### Numerically indexed arrays

Negative numbers are not permitted as indices.

An indexed array may start with any non-negative number, however all base indices besides 0 are discouraged.

When declaring indexed arrays with the Array function, a trailing space must be added after each comma delimiter to improve readability:

$sampleArray = array(1, 2, 3, 'Zend', 'Studio');
It is permitted to declare multi-line indexed arrays using the "array" construct. In this case, each successive line must be padded with spaces such that beginning of each line is aligned:

```
$sampleArray = array(1, 2, 3, 'Zend', 'Studio',
                     $a, $b, $c,
                     56.44, $d, 500);
```

Alternately, the initial array item may begin on the following line. If so, it should be padded at one indentation level greater than the line containing the array declaration, and all successive lines should have the same indentation; the closing paren should be on a line by itself at the same indentation level as the line containing the array declaration:

```
$sampleArray = array(
    1, 2, 3, 'Zend', 'Studio',
    $a, $b, $c,
    56.44, $d, 500,
);
```

When using this latter declaration, we encourage using a trailing comma for the last item in the array; this minimizes the impact of adding new items on successive lines, and helps to ensure no parse errors occur due to a missing comma.

#### Associative arrays
When declaring associative arrays with the Array construct, breaking the statement into multiple lines is encouraged. In this case, each successive line must be padded with white space such that both the keys and the values are aligned:

```
$sampleArray = array('firstKey'  => 'firstValue',
                     'secondKey' => 'secondValue');
```

Alternately, the initial array item may begin on the following line. If so, it should be padded at one indentation level greater than the line containing the array declaration, and all successive lines should have the same indentation; the closing paren should be on a line by itself at the same indentation level as the line containing the array declaration. For readability, the various "=>" assignment operators should be padded such that they align.

```
$sampleArray = array(
    'firstKey'  => 'firstValue',
    'secondKey' => 'secondValue',
);
```

When using this latter declaration, we encourage using a trailing comma for the last item in the array; this minimizes the impact of adding new items on successive lines, and helps to ensure no parse errors occur due to a missing comma.

<small>Source: Zend</small>


### elseif, not else if #

`else if` is not compatible with the colon syntax for `if|elseif` blocks. For this reason, use `elseif` for conditionals.


### Logical operators

Use of the `||` "or" comparison operator is discouraged as its clarity on some output devices is low (looking like the number 11 for instance). `&&` is preferred over `and` but either are acceptable. A space should always precede and follow `!`


### Regular expressions #

Perl compatible regular expressions (PCRE, `preg_` functions) SHOULD be used in preference to their POSIX counterparts.

Single-quoted strings SHOULD be used for regular expressions as they have only two metasequences (sequences of characters that have special meaning in a regular expression pattern): `\'` and `\\`.

### Ternary operator

Ternary operators are fine, but always have them test if the statement is true, not false. Otherwise, it just gets confusing. (An exception would be using ! empty(), as testing for false here is generally more intuitive.)

For example:

```
// (if statement is true) ? (do this) : (else, do this);
$musictype = ( 'jazz' == $music ) ? 'cool' : 'blah';
```


### TRUE, FALSE, and NULL

TRUE, FALSE, and NULL are PHP keywords that should always be written fully uppercase.


### Yoda conditions

```
if ( true == $the_force ) {
    $victorious = you_will( $be );
}
```

When doing logical comparisons, always put the variable on the right side, constants or literals on the left.

In the above example, if you omit an equals sign (admit it, it happens even to the most seasoned of us), you'll get a parse error, because you can’t assign to a constant like true. If the statement were the other way around ( $the_force = true ), the assignment would be perfectly valid, returning 1, causing the `if` statement to evaluate to true, and you could be chasing that bug for a while.

A little bizarre it is to read. Get used to it you will.

This applies to `==`, `!=`, `===`, and `!==`. Yoda conditions for `<`, `>`, `<=` or `>=` are significantly more difficult to read and are best avoided.




## 10. Debug code

Debugging code MUST NOT be left in production code, even if commented out.

Functions such as `var_dump()`, `print_r()`, `die()`/`exit()`` SHOULD NOT remain in your code unless it serves a specific purpose other than debugging.



---

## Further reading

* [CodeIgniter PHP style guide](https://codeigniter.com/user_guide/general/styleguide.html)
* [WordPress PHP coding standards](https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/)
* [MIT Sloan School of Management](http://mitsloan.mit.edu/shared/content/PHP_Code_Style_Guide.php)
* [Zend framework coding standard for PHP](https://framework.zend.com/manual/1.11/en/coding-standard.html)