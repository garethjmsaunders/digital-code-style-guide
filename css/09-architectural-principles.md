

# Architectural principles

You would be forgiven for thinking that an architecture for CSS is a somewhat grandiose and unnecessary concept: why would something so simple, so straightforward, need something as complex or considered as an architecture?!

Well, as we've seen, CSS' simplicity, its looseness, and its unruly nature mean that the best way of managing (read, taming) it at any reasonable scale is through a strict and specific architecture. A solid architecture can help us control our specificity, enforce naming conventions, manage our source order, create a sane development environment, and generally make managing our CSS projects a lot more consistent and comfortable.

There is no tool, no preprocessor, no magic bullet, that will make your CSS better on its own: a developer's best tool when working with such a loose syntax is self-discipline, conscientiousness, and diligence, and a well-defined architecture will help enforce and facilitate these traits.

Architectures are large, overarching, principle-led collections of smaller conventions which come together to provide a managed environment in which code is written and maintained. Architectures are typically quite high level, and leave implementation details—such as naming conventions or syntax and formatting, for example—to the team implementing it.

Most architectures are usually based around existing design patterns and paradigms, and, more often than not, these paradigms were born of computer scientists and software engineers. For all CSS isn't ‘code', and doesn't exhibit many traits that programming languages do, we find that we can apply some of these same principles to our own work.

In this section, we'll take a look at some of these design patterns and paradigms, and how we can use them to reduce code—and increase code reuse—in our CSS projects.


## High-level overview

At a very high-level, your architecture should help you:

* provide a consistent and sane environment;
* accommodate change;
* grow and scale your codebase;
* promote reuse and efficiency;
* increase productivity.

Typically, this will mean a class-based and componentised architecture, split up into manageable modules, probably using a preprocessor. Of course, there is far more to an architecture than that, so let's look at some principles…


## Object-orientation

Object-orientation is a programming paradigm that breaks larger programs up into smaller, in(ter)dependent objects that all have their own roles and responsibilities. From Wikipedia:

> Object-oriented programming (OOP) is a programming paradigm that represents
> the concept of ‘objects' […] which are usually instances of classes, [and] 
> are used to interact with one another to design applications and computer 
> programs.
> When applied to CSS, we call it object-oriented CSS, or OOCSS. OOCSS was 
> coined and popularised by Nicole Sullivan, whose Media Object has become the 
> poster child of the methodology.

OOCSS deals with the separation of UIs into structure and skin: breaking UI components into their underlying structural forms, and layering their cosmetic forms on separately. This means that we can recycle common and recurring design patterns very cheaply without having to necessarily recycle their specific implementation details at the same time. OOCSS promotes reuse of code, which makes us quicker, as well as keeping the size of our codebase down.

Structural aspects can be thought of like skeletons; common, recurring frames that provide design-free constructs known as objects and abstractions. Objects and abstractions are simple design patterns that are devoid of any cosmetics; we abstract out the shared structural traits from a series of components into a generic object.

Skin is a layer that we (optionally) add to our structure in order to give objects and abstractions a specific look-and-feel. Let's look at an example:

```
/**
 * A simple, design-free button object. Extend this object with a `.btn--*` skin
 * class.
 */
.btn {
    display: inline-block;
    padding: 1em 2em;
    vertical-align: middle;
}


/**
 * Positive buttons' skin. Extends `.btn`.
 */
.btn--positive {
    background-color: green;
    color: white;
}

/**
 * Negative buttons' skin. Extends `.btn`.
 */
.btn--negative {
    background-color: red;
    color: white;
}
```

Above, we can see how the `.btn {}` class simply provides structural styling to an element, and doesn't concern itself with any cosmetics. We supplement the `.btn {}` object with a second class, such as `.btn--negative {}` in order to give that DOM node specific cosmetics:

```
<button class="btn  btn--negative">Delete</button>
```

Favour the multiple-class approach over using something like `@extend:` using multiple classes in your markup—as opposed to wrapping the classes up into one using a preprocessor:

*   gives you a better paper-trail in your markup, and allows you to see 
    quickly and explicitly which classes are acting on a piece of HTML;
*   allows for greater composition in that classes are not tightly bound to 
    other styles in your CSS.

Whenever you are building a UI component, try and see if you can break it into two parts: one for structural styles (paddings, layout, etc.) and another for skin (colours, typefaces, etc.).


### Further reading

* [The media object saves hundreds of lines of code](http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/)
* [The flag object](http://csswizardry.com/2013/05/the-flag-object/)
* [Naming UI components in OOCSS](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)


## The single responsibility principle

The _single responsibility principle_ is a paradigm that, very loosely, states that all pieces of code (in our case, classes) should focus on doing one thing and one thing only. More formally:

> …the single responsibility principle states that every context (class, 
> function, variable, etc.) should have a single responsibility, and that 
> responsibility should be entirely encapsulated by the context.
> What this means for us is that our CSS should be composed of a series of 
> much smaller classes that focus on providing very specific and limited 
> functionality. This means that we need to decompose UIs into their smallest 
> component pieces that each serve a single responsibility; they all do just 
> one job, but can be very easily combined and composed to make much more 
> versatile and complex constructs. Let's take some example CSS that does not 
> adhere to the single responsibility principle:

```
.error-message {
    display: block;
    padding: 10px;
    border-top: 1px solid f00;
    border-bottom: 1px solid f00;
    background-color: fee;
    color: f00;
    font-weight: bold;
}

.success-message {
    display: block;
    padding: 10px;
    border-top: 1px solid 0f0;
    border-bottom: 1px solid 0f0;
    background-color: efe;
    color: 0f0;
    font-weight: bold;
}
```

Here we can see that—despite being named after one very specific use-case—these classes are handling quite a lot: layout, structure, and cosmetics. We also have a lot of repetition. We need to refactor this in order to abstract out some shared objects (OOCSS) and bring it more inline with the single responsibility principle. We can break these two classes out into four much smaller responsibilities:

```
.box {
    display: block;
    padding: 10px;
}


.message {
    border-style: solid;
    border-width: 1px 0;
    font-weight: bold;
}

.message--error {
    background-color: fee;
    color: f00;
}

.message--success {
    background-color: efe;
    color: 0f0;
}
```

Now we have a general abstraction for boxes which can live, and be used, completely separately from our message component, and we have a base message component that can be extended by a number of smaller responsibility classes. The amount of repetition has been greatly reduced, and our ability to extend and compose our CSS has been greatly increased. This is a great example of OOCSS and the single responsibility principle working in tandem.

By focussing on single responsibilities, we can give our code much more flexibility, and extending components' functions becomes very simple when sticking to the open/closed principle, which we're going to look at next.


### Further reading

* The single responsibility principle applied to CSS





## The open/closed principle

The open/closed principle, in my opinion, is rather poorly named. It is poorly named because 50% of the vital information is omitted from its title. The open/closed principle states that

> [s]oftware entities (classes, modules, functions, etc.) should be open for 
> extension, but closed for modification.

See? The most important words—extension and modification—are completely missing from the name, which isn't very useful at all.

Once you have trained yourself to remember what the words open and closed actually relate to, you'll find that open/closed principle remarkably simple: any additions, new functionality, or features we add to our classes should be added via extension—we should not modify these classes directly. This really trains us to write bulletproof single responsibilities: because we shouldn't modify objects and abstractions directly, we need to make sure we get them as simple as possible the first time. This means that we should never need to actually change an abstraction—we'd simply stop using it—but any slight variants of it can be made very easily by extending it.

Let's take an example:

```
.box {
    display: block;
    padding: 10px;
}

.box--large {
    padding: 20px;
}
```

Here we can see that the `.box {}` object is incredibly simple: we've stripped it right back into one very small and very focussed responsibility. To modify that box, we extend it with another class; `.box--large {}`. Here the `.box {} class is closed to modification, but open to being extended.

An incorrect way of achieving the same might look like this:

```
.box {
    display: block;
    padding: 10px;
}

.content .box {
    padding: 20px;
}
```

Not only is this overly specific, locationally dependent, and potentially displaying poor Selector Intent, we are modifying the `.box {}` directly. We should rarely—if ever—find an object or abstraction's class as a key selector in a compound selector.

A selector like `.content .box {}` is potentially troublesome because

*   it forces all `.box` components into that style when placed inside of
    `.content`, which means the modification is dictated to developers, 
    whereas developers should be allowed to opt into changes explicitly;
*   the `.box` style is now unpredictable to developers; the single
    responsibility no longer exists because nesting the selector produces a 
    forced caveat.

All modifications, additions, and changes should always be opt-in, not mandatory. If you think something might need a slight adjustment to take it away from the norm, provide another class which adds this functionality.

When working in a team environment, be sure to write API-like CSS; always ensure that existing classes remain backward compatible (i.e. no changes at their root) and provide new hooks to bring in new features. Changing the root object, abstraction, or component could have huge knock-on effects for developers making use of that code elsewhere, so never modify existing code directly.

Exceptions may present themselves when it transpires that a root object does need a rewrite or refactor, but it is only in these specific cases that you should modify code. Remember: **open for extension; closed for modification**.


### Further reading

* [The open/closed principle applied to CSS](http://csswizardry.com/2012/06/the-open-closed-principle-applied-to-css/)





## DRY

DRY, which stands for _Don't repeat yourself_, is a micro-principle used in software development which aims to keep the repetition of key information to a minimum. Its formal definition is that

> [e]very piece of knowledge must have a single, unambiguous, authoritative 
> representation within a system.

Although a very simple principle—in principle—DRY is often misinterpreted as the necessity to never repeat the exact same thing twice at all in a project. This is impractical and usually counterproductive, and can lead to forced abstractions, over-thought and -engineered code, and unusual dependencies.

The key isn't to avoid all repetition, but to normalise and abstract meaningful repetition. If two things happen to share the same declarations coincidentally, then we needn't DRY anything out; that repetition is purely circumstantial and cannot be shared or abstracted. For example:

```
.btn {
    display: inline-block;
    padding: 1em 2em;
    font-weight: bold;
}

[...]

.page-title {
    font-size: 3rem;
    line-height: 1.4;
    font-weight: bold;
}

[...]

    .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        font-weight: bold;
    }
```

From the above code, we can reasonably deduce that the font-weight: bold; declaration appears three times purely coincidentally. To try and create an abstraction, mixin, or `@extend` directive to cater for this repetition would be overkill, and would tie these three rulesets together based purely on circumstance.

However, imagine we're using a web-font that requires `font-weight: bold;` to be declared every time the font-family is:

```
.btn {
    display: inline-block;
    padding: 1em 2em;
    font-family: "My Web Font", sans-serif;
    font-weight: bold;
}

[...]

.page-title {
    font-size: 3rem;
    line-height: 1.4;
    font-family: "My Web Font", sans-serif;
    font-weight: bold;
}

[...]

    .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        font-family: "My Web Font", sans-serif;
        font-weight: bold;
    }
```

Here we're repeating a more meaningful snippet of CSS; these two declarations have to always be declared together. In this instance, we probably would DRY out our CSS.

I would recommend using a mixin over @extend here because, even though the two declarations are thematically grouped, the rulesets themselves are still separate, unrelated entities: to use @extend would be to physically group these unrelated rulesets together in our CSS, thus making the unrelated related.

Our mixin:

```
@mixin my-web-font() {
    font-family: "My Web Font", sans-serif;
    font-weight: bold;
}

.btn {
    display: inline-block;
    padding: 1em 2em;
    @include my-web-font();
}

[...]

.page-title {
    font-size: 3rem;
    line-height: 1.4;
    @include my-web-font();
}

[...]

    .user-profile__title {
        font-size: 1.2rem;
        line-height: 1.5;
        @include my-web-font();
    }
```

Now the two declarations only exist once, meaning we're not repeating ourselves. If we ever switch out our web-font, or move to a font-weight: regular; version, we only need to make that change in one place.

In short, only DRY code that is actually, thematically related. Do not try to reduce purely coincidental repetition: **duplication is better than the wrong abstraction**.

### Further reading

* [Writing DRYer vanilla CSS](http://csswizardry.com/2013/07/writing-dryer-vanilla-css/)





## Composition over inheritance

Now that we're used to spotting abstractions and creating single responsibilities, we should be in a great position to start composing more complex composites from a series of much smaller component parts. Nicole Sullivan likens this to using Lego; tiny, single responsibility pieces which can be combined in a number of different quantities and permutations to create a multitude of very different looking results.

This idea of building through composition is not a new one, and is often referred to as _composition over inheritance_. This principle suggests that larger systems should be composed from much smaller, individual parts, rather than inheriting behaviour from a much larger, monolithic object. This should keep your code decoupled—nothing inherently relies on anything else.

Composition is a very valuable principle for an architecture to make use of, particularly considering the move toward component-based UIs. It will mean you can more easily recycle and reuse functionality, as well rapidly construct larger parts of UI from a known set of composable objects. Think back to our error message example in the single responsibility principle section; we created a complete UI component by composing a number of much smaller and unrelated objects.





## The separation of concerns

The separation of concerns is a principle which, at first, sounds a lot like the single responsibility principle. The separation of concerns states that code should be broken up

> into distinct sections, such that each section addresses a separate concern.
> A concern is a set of information that affects the code of a computer 
> program. […] A program that embodies SoC well is called a modular program.

Modular is a word we're probably used to; the idea of breaking UIs and CSS into much smaller, composable pieces. The separation of concerns is just a formal definition which covers the concepts of modularity and encapsulation in code. In CSS this means building individual components, and writing code which only focusses itself on one task at a time.

The term was coined by Edsger W. Dijkstra, who rather elegantly said:

> Let me try to explain to you, what to my taste is characteristic for all 
> intelligent thinking. It is, that one is willing to study in depth an aspect 
> of one's subject matter in isolation for the sake of its own consistency, 
> all the time knowing that one is occupying oneself only with one of the 
> aspects. We know that a program must be correct and we can study it from 
> that viewpoint only; we also know that it should be efficient and we can 
> study its efficiency on another day, so to speak. In another mood we may ask 
> ourselves whether, and if so: why, the program is desirable. But nothing is 
> gained—on the contrary!—by tackling these various aspects simultaneously. It 
> is what I sometimes have called ‘the separation of concerns', which, even if 
> not perfectly possible, is yet the only available technique for effective 
> ordering of one's thoughts, that I know of. This is what I mean by ‘focusing 
> one's attention upon some aspect': it does not mean ignoring the other 
> aspects, it is just doing justice to the fact that from this aspect's point 
> of view, the other is irrelevant. It is being one- and multiple-track minded 
> simultaneously.

Beautiful. The idea here is to focus fully on one thing at once; build one thing to do its job very well whilst paying as little attention as possible to other facets of your code. Once you have addressed and built all these separate concerns in isolation—meaning they're probably very modular, decoupled, and encapsulated—you can begin bringing them together into a larger project.

A great example is layout. If you are using a grid system, all of the code pertaining to layout should exist on its own, without including anything else. You've written code that handles layout, and that's it:

```
<div class="layout">

    <div class="layout__item  two-thirds">
    </div>

    <div class="layout__item  one-third">
    </div>

</div>
```

You will now need to write new, separate code to handle what lives inside of that layout:

```
<div class="layout">

    <div class="layout__item  two-thirds">
        <section class="content">
            ...
        </section>
    </div>

    <div class="layout__item  one-third">
        <section class="sub-content">
            ...
        </section>
    </div>

</div>
```

The separation of concerns allows you to keep code self-sufficient, ignorant, and ultimately a lot more maintainable. Code which adheres to the separation of concerns can be much more confidently modified, edited, extended, and maintained because we know how far its responsibilities reach. We know that modifying layout, for example, will only ever modify layout—nothing else.

The separation of concerns increases reusability and confidence whilst reducing dependency.





## Misconceptions

There are, I feel, a number of unfortunate misconceptions surrounding the separation of concerns when applied to HTML and CSS. They all seem to revolve around some format of:

> Using classes for CSS in your markup breaks the separation of concerns.

Unfortunately, this is simply not true. The separation of concerns does exist in the context of HTML and CSS (and JS), but not in the way a lot of people seem to believe.

The separation of concerns when applied to front-end code is not about classes-in-HTML-purely-for-styling-hooks-blurring-the-lines-between-concerns; it is about the very fact that we are using different languages for markup and styling at all.

Back before CSS was widely adopted, we'd use tables to lay content out, and font elements with color attributes to provide cosmetic styling. The problem here is that HTML was being used to create content and also to style it; there was no way of having one without the other. This was a complete lack of separation of concerns, which was a problem. CSS' job was to provide a completely new syntax to apply this styling, allowing us to separate our content and style concerns across two technologies.

Another common argument is that putting classes in your HTML puts style information in your markup.

So, in a bid to circumvent this, people adopt selectors that might look a little like this:

```
body > header:first-of-type > nav > ul > li > a {
}
```

This CSS—presumably to style our site's main nav—has the usual problems of location dependency, poor Selector Intent, and high specificity, but it also manages to do exactly what developers are trying to avoid, only in the opposite direction: it puts DOM information in your CSS. Aggressive attempts to avoid putting any style hints or hooks in markup only lead to overloading stylesheets with DOM information.

In short: having classes in your markup does not violate the separation of concerns. Classes merely act as an API to link two separate concerns together. The simplest way to separate concerns is to write well formed HTML and well formed CSS, and link to two together with sensible, judicious use of classes.