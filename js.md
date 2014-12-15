# JS Style Guide

We use JSLint as a standard specification for our code. That implies some decisions about style. This document highlights some of the more important ramifications of JSLint and any additional stylistic requirements we have. See the full documentation [JSLint](http://www.jslint.com/lint.html) for more information.

TODO: Merge in style guide advice from Douglas Crockford (author of JSLint) http://javascript.crockford.com/code.html

### Naming conventions

<sub>Based on [Google JS Style Guide][googlestyle].</sub>

<table>
<tr><th>Entity</th><th>Example</th></tr>
<tr><td>function name</td><td>`functionNameLikeThis`</td></tr>
<tr><td>variable name</td><td>`variableNameLikeThis`</td></tr>
<tr><td>class name</td><td>`ClassNameLikeThis`</td></tr>
<tr><td>enum name</td><td>` EnumNamesLikeThis`</td></tr>
<tr><td>method name</td><td>`methodNamesLikeThis`</td></tr>
<tr><td>constant name</td><td>`CONSTANT_VALUES_LIKE_THIS`</td></tr>
<tr><td>filenames</td><td>`filenameslikethis.js.`</td></tr>
</table>

### Semicolon

<sub>From [JSLint][].</sub>

Every statement should be followed by a semicolon except for `for`, `function`, `if`, `switch`, `try`, and `while`.


### Scope

<sub>From [JSLint][].</sub>

Declare all variables at the top of the function with one `var` statement.


### Spaces vs. Tabs

<sub>From [JSLint][].</sub>

Use only spaces, and indent 2 spaces at a time.

We use spaces for indentation. Do not use tabs in your code. You should set your editor to emit spaces when you hit the tab key.

### Blocks

<sub>Based on requirements from [JSLint][].</sub>

Use explicit blocks for `if`, `while`, `do` and `for` statements. Always start your curly braces on the same line as whatever they're opening, and leave the closing brace on it's own line. For example:

```
// Good
if (condition) {
  // ...
}
else {
  // ...
}

// Not so good
if (condition) {
  // ...
  } else {
    // ...
  }

  // Bad
  if (condition) statement;

  // Bad
  if (condition) statement;
  else statement2;

  ```

  ### Line length

  <sub>Based on [Google JS Style Guide][googlestyle].</sub>

  Each line of text in your code should be at most 80 characters long.

  **Allowable Exceptions**

  * If a comment line contains an example command or a literal URL longer than 80 characters, that line may be longer than 80 characters for ease of cut and paste.

  * A raw-string literal may have content that exceeds 80 characters. Except for test code, such literals should appear near top of a file.

  * Statements with a long URL may exceed 80 characters.

  ### Don't use `eval`.

  <sub>From [JSLint][].</sub>

  ### Multiline Function arguments

  <sub>From [Google JS Style Guide][googlestyle].</sub>

  When possible, all function arguments should be listed on the same line. If doing so would exceed the 80-column limit, the arguments must be line-wrapped in a readable way. To save space, you may wrap as close to 80 as possible, or put each argument on its own line to enhance readability. The indentation may be either four spaces, or aligned to the parenthesis. Below are the most common patterns for argument wrapping:

  ```
  // Four-space, wrap at 80.  Works with very long function names, survives
  // renaming without reindenting, low on space.
  goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
      // ...
    };

    // Four-space, one argument per line.  Works with long function names,
    // survives renaming, and emphasizes each argument.
    goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
      veryDescriptiveArgumentNumberOne,
      veryDescriptiveArgumentTwo,
      tableModelEventHandlerProxy,
      artichokeDescriptorAdapterIterator) {
        // ...
      };

      // Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
      // low on space.
      function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
        tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
          // ...
        }

        // Parenthesis-aligned, one argument per line.  Emphasizes each
        // individual argument.
        function bar(veryDescriptiveArgumentNumberOne,
          veryDescriptiveArgumentTwo,
          tableModelEventHandlerProxy,
          artichokeDescriptorAdapterIterator) {
            // ...
          }
          ```

          ### Binary and Ternary Operators

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

          ### Quoting strings

          <sub>From [Google JS Style Guide][googlestyle].</sub>

          Single-quotes (') are preferred to double-quotes ("). This is helpful when creating strings that include HTML:

          ```
          var msg = 'This is some <a href="#url">HTML</a>';
          ```



          ## JSLint Configuration

          The pattern library provides a JSLint config file that implements many of these rules and can be used to ensure that your code matches our work.

          ---

          ### References

          For more in depth treatment, see the following.

          * [JSLint][jslint]
          * [Google JS Style Guide][googlestyle]


          [jslint]: http://www.jslint.com/lint.html "JSLint"
          [googlestyle]:  https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml "Google JS Style Guide"
          
