# JavaScript style guide

version 0.4
Last updated: Tuesday 5 July 2016

<!-- MarkdownTOC depth=4 -->

- [1 Introduction](#1-introduction)
- [2. General](#2-general)
  - [2.1 Naming conventions](#21-naming-conventions)
  - [2.2 Semicolon](#22-semicolon)
  - [2.3 Scope](#23-scope)
  - [2.4 Comments](#24-comments)
  - [2.5 Avoid mixing technology](#25-avoid-mixing-technology)
  - [2.6 Don't use `eval`](#26-dont-use-eval)
- [3. Formatting](#3-formatting)
  - [3.1 Spaces vs tabs](#31-spaces-vs-tabs)
  - [3.2 Blocks](#32-blocks)
  - [3.3 Line length](#33-line-length)
    - [Allowable exceptions](#allowable-exceptions)
  - [3.4 Multi-line function arguments](#34-multi-line-function-arguments)
  - [3.5 Binary and ternary operators](#35-binary-and-ternary-operators)
  - [3.6 Quoting strings](#36-quoting-strings)
- [4. Configuration and references](#4-configuration-and-references)
  - [4.1 JSLint configuration](#41-jslint-configuration)
- [References](#references)

<!-- /MarkdownTOC -->



TODO: Merge in style guide advice from Douglas Crockford (author of JSLint) http://javascript.crockford.com/code.html


---


## 1 Introduction

We use JSLint as a standard specification for our code. That implies some decisions about style. This document highlights some of the more important ramifications of JSLint and any additional stylistic requirements we have. See the full documentation [JSLint][jslint] for more information.




## 2. General 

### 2.1 Naming conventions

We call things by their name. Good variable and function names should be easy to understand and tell you what is going on — not more and not less. 

<sub>Based on [Google JS Style Guide][googlestyle].</sub>

<table>
    <tr>
        <th>Entity</th>
        <th>Example</th>
    </tr>
    <tr>
        <td>function name</td>
        <td><code>functionNameLikeThis</code></td>
    </tr>
    <tr>
        <td>variable name</td>
        <td><code>variableNameLikeThis</code></td>
    </tr>
    <tr>
        <td>class name</td>
        <td><code>ClassNameLikeThis</code></td>
    </tr>
    <tr>
        <td>enum name</td>
        <td><code>EnumNamesLikeThis</code></td>
    </tr>
    <tr>
        <td>method name</td>
        <td><code>methodNamesLikeThis</code></td>
    </tr>
    <tr>
        <td>constant name</td>
        <td><code>CONSTANT_VALUES_LIKE_THIS</code></td>
    </tr>
    <tr>
        <td>filenames</td>
        <td><code>filenameslikethis.js.</code></td>
    </tr>
</table>


### 2.2 Semicolon

<sub>From [JSLint][].</sub>

Every statement should be followed by a semicolon except for `for`, `function`, `if`, `switch`, `try`, and `while`.


### 2.3 Scope

<sub>From [JSLint][].</sub>

Declare all variables at the top of the function with one `var` statement. They should be listed in alphabetical order if possible.
```
var currentStudentID;
var graduationYear;
var orientation;
```


### 2.4 Comments

Comment as much as needed but not more. Comments are your messages to other developers (and yourself, if you come back to your code after several months working on something else). We prefer to use the `/* */` rather than the `//`.
```
module = function(){
    var current = null;
    function init(){
    };
/*
  function show(){
      current = 1;
  };
  function hide(){
      show();
  };
*/

return{init:init,show:show,current:current}
}();
```


### 2.5 Avoid mixing technology

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


### 2.6 Don't use `eval`

<sub>From [JSLint][].</sub>

`eval` is probably the most misused feature of JavaScript, because there is almost always a better way to achieve the same thing. See the [JSLint article](https://jslinterrors.com/eval-is-evil) for more information.




## 3. Formatting

### 3.1 Spaces vs tabs

<sub>From [JSLint][].</sub>

Use only spaces, and indent FOUR (4) spaces at a time.

Use spaces for indentation. Do not use tabs in your code. You should set your editor to emit spaces when you hit the tab key.


### 3.2 Blocks

<sub>Based on requirements from [JSLint][].</sub>

Use explicit blocks for `if`, `while`, `do` and `for` statements. Always start your curly braces on the same line as whatever they're opening, and leave the closing brace on its own line. For example:

```
// Good
if (condition) {
   ...
}
else {
   ...
}

// Not so good
if (condition) {
   ...
  } else {
     ...
  }

// Bad
if (condition) statement;

// Bad
if (condition) statement;
else statement2;

```


### 3.3 Line length

<sub>Based on [Google JS Style Guide][googlestyle].</sub>

Each line of text in your code should be at most 80 characters long.

#### Allowable exceptions

*   If a comment line contains an example command or a literal URL longer than 
    80 characters, that line may be longer than 80 characters for ease of cut and paste.
*   A raw-string literal may have content that exceeds 80 characters. Except 
    for test code, such literals should appear near top of a file.
*   Statements with a long URL may exceed 80 characters.


### 3.4 Multi-line function arguments

<sub>From [Google JS Style Guide][googlestyle].</sub>

When possible, all function arguments should be listed on the same line. If doing so would exceed the 80-column limit, the arguments must be line-wrapped in a readable way. To save space, you may wrap as close to 80 as possible, or put each argument on its own line to enhance readability. The indentation may be either four spaces, or aligned to the parenthesis. Below are the most common patterns for argument wrapping:

```
// Four-space, wrap at 80.  Works with very long function names, survives
// renaming without reindenting, low on space.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
ryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
bleModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
// ...


// Four-space, one argument per line.  Works with long function names,
// survives renaming, and emphasizes each argument.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
veryDescriptiveArgumentNumberOne,
veryDescriptiveArgumentTwo,
tableModelEventHandlerProxy,
artichokeDescriptorAdapterIterator) {
 ...
};

// Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
// low on space.
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
bleModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
// ...


// Parenthesis-aligned, one argument per line.  Emphasizes each
// individual argument.
nction bar(veryDescriptiveArgumentNumberOne,
veryDescriptiveArgumentTwo,
tableModelEventHandlerProxy,
artichokeDescriptorAdapterIterator) {
 ...
}
```


### 3.5 Binary and ternary operators

<sub>From [Google JS Style Guide][googlestyle].</sub>

Always put the operator on the preceding line. Otherwise, line breaks and indentation follow the same rules as in other Google style guides. This operator placement was initially agreed upon out of concerns about automatic semicolon insertion. In fact, semicolon insertion cannot happen before a binary operator, but new code should stick to this style for consistency.

```
var x = a ? b : c;  // All on one line if it will fit.

// Indentation +4 is OK.
var y = a ?
longButSimpleOperandB : longButSimpleOperandC;

// Indenting to the line position of the first operand is also OK.
var z = a ?
moreComplicatedB :
moreComplicatedC;
```

This includes the dot operator.

```
var x = foo.bar().
doSomething().
doSomethingElse();
```


### 3.6 Quoting strings

<sub>From [Google JS Style Guide][googlestyle].</sub>

Single-quotes (') are preferred to double-quotes ("). This is helpful when creating strings that include HTML:

```
var msg = 'This is some <a href="#url">HTML</a>';
```




## 4. Configuration and references


### 4.1 JSLint configuration

The pattern library provides a JSLint config file that implements many of these rules and can be used to ensure that your code matches our work.

---

## References

For more in depth treatment, see the following.

* [JSLint]([jslint])
* [Google JS Style Guide][googlestyle]

[jslint]:  http://www.jslint.com/help.html "JSLint"
[googlestyle]:  https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml "Google JS Style Guide"

