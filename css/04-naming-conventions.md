CSS code style guide

# Naming conventions

Naming conventions in CSS are hugely useful in making your code more strict, more transparent, and more informative.

A good naming convention will tell you and your team:

*   what type of thing a class does;
*   where a class can be used;
*   what (else) a class might be related to.

The naming convention I follow is very simple: hyphen (-) delimited strings, with BEM-like naming for more complex pieces of code.

It's worth noting that a naming convention is not normally useful CSS-side of development; they really come into their own when viewed in HTML.





## In this section
<!-- MarkdownTOC -->

- [Accepted characters in class and ID names](#accepted-characters-in-class-and-id-names)
    - [Characters to avoid](#characters-to-avoid)
- [Hyphen delimited](#hyphen-delimited)
- [BEM-like naming](#bem-like-naming)
    - [Starting context](#starting-context)
- [Modifying elements](#modifying-elements)
- [Naming conventions in HTML](#naming-conventions-in-html)
- [JavaScript hooks](#javascript-hooks)
    - [HTML5 data-* attributes](#html5-data--attributes)

<!-- /MarkdownTOC -->





## Accepted characters in class and ID names

In keeping with the [grammatical rules defined for CSS 2.1](http://www.w3.org/TR/CSS21/grammar.html#scanner) a class name or ID must follow these rules:

**First two characters**

*   letters
*   underscores
*   hyphens

**Thereafter, any number of**

*   underscores
*   hyphens
*   letters
*   numbers

**Do not start with...**



### Characters to avoid

*   Asterisks (*) are universal selectors: they will apply styling to every 
    element in the document. Do not use them in class or ID names.
*   Forward slashes (/) and backward slashes (\) are not accepted.




## Hyphen delimited

All strings in classes are delimited with a hyphen (-), like so:

```
.page-head {}
.sub-content {}
```

Camel case and underscores are not used for regular classes; the following are incorrect:

```
.pageHead {}
.sub_content {}
```





## BEM-like naming

For larger, more interrelated pieces of UI that require a number of classes, we use a BEM-like naming convention.

BEM, meaning Block, Element, Modifier, is a front-end methodology coined by developers working at Yandex. Whilst BEM is a complete methodology, here we are only concerned with its naming convention. Further, the naming convention here only is BEM-like; the principles are exactly the same, but the actual syntax differs slightly.

BEM splits components' classes into three groups:

* Block: The sole root of the component.
* Element: A component part of the Block.
* Modifier: A variant or extension of the Block.

To take an analogy (note, not an example):

```
.person {}
.person__head {}
.person--tall {}
```

Elements are delimited with two (2) underscores (__), and modifiers are delimited by two (2) hyphens (--).

Here we can see that `.person {}` is the Block; it is the sole root of a discrete entity. `.person__head {}` is an Element; it is a smaller part of the .person {} Block. Finally, `.person--tall {} is a Modifier; it is a specific variant of the .person {} Block.


### Starting context

Your Block context starts at the most logical, self-contained, discrete location. To continue with our person-based analogy, we'd not have a class like `.room__person {}`, as the room is another, much higher context. We'd probably have separate Blocks, like so:

```
.room {}

    .room__door {}

.room--kitchen {}


.person {}

    .person__head {}
```

If we did want to denote a `.person {}` inside a `.room {}`, it is more correct to use a selector like `.room .person {}` which bridges two Blocks than it is to increase the scope of existing Blocks and Elements.

A more realistic example of properly scoped blocks might look something like this, where each chunk of code represents its own Block:

```
.page {}


.content {}


.sub-content {}


.footer {}

    .footer__copyright {}
```

Incorrect notation for this would be:

```
.page {}

    .page__content {}

    .page__sub-content {}

    .page__footer {}

        .page__copyright {}
```

It is important to know when BEM scope starts and stops. As a rule, BEM applies to self-contained, discrete parts of the UI.
More layers

If we were to add another Element—called, let's say, .person__eye {}—to this .person {} component, we would not need to step through every layer of the DOM. That is to say, the correct notation would be .person__eye {}, and not .person__head__eye {}. Your classes do not reflect the full paper-trail of the DOM.





## Modifying elements

You can have variants of Elements, and these can be denoted in a number of ways depending on how and why they are being modified. Carrying on with our person example, a blue eye might look like this:

```
.person__eye--blue {}
```

Here we can see we're directly modifying the eye Element.

Things can get more complex, however. Please excuse the crude analogy, and let's imagine we have a face Element that is handsome. The person themselves isn't that handsome, so we modify the face Element directly—a handsome face on a regular person:

```
.person__face--handsome {}
```

But what if that person is handsome, and we want to style their face because of that fact? A regular face on a handsome person:

```
.person--handsome .person__face {}
```

Here is one of a few occasions where we'd use a descendant selector to modify an Element based on a Modifier on the Block.

If using Sass, we would likely write this like so:

```
.person {}

    .person__face {

        .person--handsome & {}

    }

.person--handsome {}
```

Note that we do not nest a new instance of `.person__face {}` inside of `.person--handsome {};` instead, we make use of Sass' parent selectors to prepend `.person--handsome` onto the existing `.person__face {}` selector. This means that all of our `.person__face {}`-related rules exist in once place, and aren't spread throughout the file. This is general good practice when dealing with nested code: keep all of your context (e.g. all `.person__face {}` code) encapsulated in one location.





## Naming conventions in HTML

As I previously hinted at, naming conventions aren't necessarily all that useful in your CSS. Where naming conventions' power really lies is in your markup. Take the following, non-naming-conventioned HTML:

```
<div class="box  profile  pro-user">

    <img class="avatar  image" />

    <p class="bio">...</p>

</div>
```

How are the classes box and profile related to each other? How are the classes profile and avatar related to each other? Are they related at all? Should you be using pro-user alongside bio? Will the classes image and profile live in the same part of the CSS? Can you use avatar anywhere else?

From that markup alone, it is very hard to answer any of those questions. Using a naming convention, however, changes all that:

```
<div class="box  profile  profile--is-pro-user">

    <img class="avatar  profile__image" />

    <p class="profile__bio">...</p>

</div>
```

Now we can clearly see which classes are and are not related to each other, and how; we know what classes we can't use outside of the scope of this component; and we know which classes we may be free to reuse elsewhere.





## JavaScript hooks

As a rule, it is unwise to bind your CSS and your JS onto the same class in your HTML. This is because doing so means you can't have (or remove) one without (removing) the other. It is much cleaner, much more transparent, and much more maintainable to bind your JS onto specific classes.

I have known occasions before when trying to refactor some CSS has unwittingly removed JS functionality because the two were tied to each other—it was impossible to have one without the other.

Typically, these are classes that are prepended with js-, for example:

```
<input type="submit" class="btn  js-btn" value="Follow" />
```

This means that we can have an element elsewhere which can carry with style of `.btn {}`, but without the behaviour of `.js-btn`.


### HTML5 data-* attributes

A common practice is to use `data-*` attributes as JS hooks, but this is incorrect. `data-*` attributes, as per the spec, are used to store custom data private to the page or application (emphasis mine). `data-*` attributes are designed to store data, not be bound to.