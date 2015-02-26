CSS code standards guide

# CSS Selectors

Perhaps somewhat surprisingly, one of the most fundamental, critical aspects of writing maintainable and scalable CSS is selectors. Their specificity, their reusability, and their performance all have a direct impact on the efficiency and effectiveness of our CSS.


**TODO: This whole section needs considerable editing.**




## In this section
<!-- MarkdownTOC depth=3 -->

- [General rules](#general-rules)
- [Selector intent](#selector-intent)
- [Specificity](#specificity)
    - [Keep specificity low at all times](#keep-specificity-low-at-all-times)
    - [Do not use !important as a hack](#do-not-use-important-as-a-hack)
    - [Use !important proactively not reactively](#use-important-proactively-not-reactively)
    - [Hacking specificity](#hacking-specificity)
- [Reusability](#reusability)
    - [Location independence](#location-independence)
    - [Portability](#portability)
    - [Object-orientation](#object-orientation)
    - [The single responsibility principle](#the-single-responsibility-principle)
    - [Open to extension / closed to modification](#open-to-extension--closed-to-modification)
    - [The separation of concerns](#the-separation-of-concerns)
    - [DRY](#dry)
- [Selector performance](#selector-performance)
    - [The key selector](#the-key-selector)
- [Further reading](#further-reading)

<!-- /MarkdownTOC -->





## General rules

**KEEP THIS BUT EXTEND IT IN LIGHT OF WHAT COMES AFTER IT**

Your selectors are fundamental to writing good CSS. To very briefly sum up the above sections:

*   **Avoid using IDs**, prefer classes or elements or attributes.
*   **Select what you want explicitly**, rather than relying on circumstance or
    coincidence. Good selector intent will rein in the reach and leak of your styles.
*   **Write selectors for reusability**, so that you can work more efficiently
    and reduce waste and repetition.
*   **Do not nest selectors unnecessarily**, because this will increase 
    specificity and affect where else you can use your styles.
*   **Do not qualify selectors unnecessarily**, as this will impact the number 
    of different elements you can apply styles to.
*   **Keep selectors as short as possible**, in order to keep specificity down 
    and performance up.

Focussing on these points will keep your selectors a lot more sane and easy to work with on changing and long-running projects.




## Selector intent

It is important when writing CSS that we scope our selectors correctly, and that we're selecting the right things for the right reasons. Selector intent is the process of deciding and defining what you want to style and how you will go about selecting it. For example, if you are wanting to style your website's main navigation menu, a selector like this would be incredibly unwise:

```
header ul {}
```

This selector's intent is to style any `ul` inside any header element, whereas our intent was to style the site's main navigation. This is poor selector intent: you can have any number of header elements on a page, and they in turn can house any number of `ul`s, so a selector like this runs the risk of applying very specific styling to a very wide number of elements. This will result in having to write more CSS to undo the greedy nature of such a selector.

A better approach would be a selector like:

```
.site-nav {}
```

An unambiguous, explicit selector with good selector intent. We are explicitly selecting the right thing for exactly the right reason.

Poor selector intent is one of the biggest reasons for headaches on CSS projects. Writing rules that are far too greedy — and that apply very specific treatments via very far reaching selectors — causes unexpected side effects and leads to very tangled stylesheets, with selectors overstepping their intentions and impacting and interfering with otherwise unrelated rulesets.

CSS cannot be encapsulated, it is inherently leaky, but we can mitigate some of these effects by not writing such globally-operating selectors: your selectors should be as explicit and well reasoned as your reason for wanting to select something.





## Specificity


### Keep specificity low at all times

"CSS isn't the most friendly of languages: globally operating, very leaky, dependent on location, hard to encapsulate, based on inheritance. But none of that even comes close to the horrors of specificity." — Harry Roberts

CSS specificity can, among other things:

* Limit your ability to extend your classes.
* Interfere with the cascade, how CSS inherits from parent rules.
* Make your code unnecessarily long and/or complex.
* Prevent code from working as expected when moved from one project to another.

All of these issues are greatly magnified when working on a larger project with a number of developers contributing code.

The problem with specificity isn't necessarily that it's high or low; it's the fact it is so variant and that it cannot be opted out of: the only way to deal with it is to get progressively more specific.

One of the single, simplest tips for an easier life when writing CSS—particularly at any reasonable scale — is to **always try and keep specificity as low as possible at all times**. Try to make sure there isn't a lot of variance between selectors in your codebase, and that all selectors strive for as low a specificity as possible.

Doing so will instantly help you tame and manage your project, meaning that no overly-specific selectors are likely to impact or affect anything of a lower specificity elsewhere. It also means you're less likely to need to fight your way out of specificity corners, and you'll probably also be writing much smaller stylesheets.

Simple changes to the way we work include, but are not limited to:

* **Avoid using IDs in your CSS.**
* **Avoid nesting selectors.**
* **Avoid qualifying classes.**
* **Avoid chaining selectors.**

To quote Jonathan Snook: "whenever declaring your styles, use the least number of selectors required to style an element."

As a rule, if a selector will work without it being nested then do not nest it.


### Do not use !important as a hack

`!important` is often used as a way to cheat your way out of specificity wars. The general rule is this: **do not use !important**, especially if it is used as a ham-fisted hack to 'just make things work'.

How many times have we seen code like this?

```
#navigation ul.nav-list li.nav-item a {
    color: blue !important;
}
```

How much more specific will the next rule need to be?!

If you find that you need to use `!important` to get something to work then that is a good sign that your code needs to be refactored. As Harry Roberts says, `!important` is "often viewed as a last resort — a desperate, defeated stab at patching over the symptoms of a much bigger problem with your code."


### Use !important proactively not reactively

`!important` does have a place in CSS projects, but only if used sparingly and proactively.

Proactive use of `!important` is when it is **used before you've encountered any specificity problems**; when it is used **as a guarantee rather than as a fix**. For example:

```
.one-half {
    width: 50% !important;
}

.is-hidden {
    display: none !important;
}
```

These two helper, or utility, classes are very specific in their intentions: you would only use them if you wanted something to be rendered at 50% width or not rendered at all. If you didn't want this behaviour, you would not use these classes, therefore whenever you do use them you will definitely want them to win.

Here we proactively apply `!important` to ensure that these styles always win. This is correct use of `!important` to guarantee that these trumps always work, and don't accidentally get overridden by something else more specific.

Only use `!important` proactively, not reactively.


### Hacking specificity

With all that said on the topic of specificity, and keeping it low, it is inevitable that we will encounter problems. No matter how hard we try, and how conscientious we are, there will always be times that we need to hack and wrangle specificity.

When these situations do arise, it is important that we handle the hacks as safely and elegantly as possible.


#### Chain a class with itself

In the event that you need **to increase the specificity of a class selector**, there are a number of options. We could nest the class inside something else to bring its specificity up. For example, we could use `.header .site-nav {}` to bring up the specificity of a simple `.site-nav {}` selector.

The problem with this, as we've discussed, is that it introduces location dependency: these styles will only work when the `.site-nav` component is in the `.header` component.

Instead, we can use a much safer hack that will not impact this component's portability: we can chain that class with itself:

```
.site-nav.site-nav {}
```

This chaining doubles the specificity of the selector, but does not introduce any dependency on location.


#### Use an attribute selector to select an ID

In the event that we do, for whatever reason, have an ID in our markup that we cannot replace with a class, select it via an attribute selector as opposed to an ID selector. For example, let's imagine we have embedded a third-party widget on our page. We can style the widget via the markup that it outputs, but we have no ability to edit that markup ourselves:

```
<div id="third-party-widget">
    ...
</div>
```

Even though we know not to use IDs in CSS, what other option do we have? We want to style this HTML but have no access to it, and all it has on it is an ID.

We do this:

```
[id="third-party-widget"] {}
```

Here we are selecting based on an attribute rather than an ID, and **attribute selectors have the same specificity as a class**. This allows us to style based on an ID, but without introducing its specificity.

Do keep in mind that these are hacks, and should not be used unless you have no better alternative.


#### Further reading
[Hacks for dealing with specificity](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)





## Reusability

With a move toward a more component-based approach to constructing UIs, the idea of reusability is paramount. We want the option to be able to move, recycle, duplicate, and syndicate components across our projects.

To this end, we make heavy use of classes. IDs, as well as being hugely over-specific, cannot be used more than once on any given page, whereas classes can be reused an infinite amount of times. Everything you choose, from the type of selector to its name, should lend itself toward being reused.


### Location independence

Given the ever-changing nature of most UI projects, and the move to more component-based architectures, it is in our interests not to style things based on where they are, but on what they are. That is to say, our components' styling should not be reliant upon where we place them—they should remain entirely location independent.

Let's take an example of a call-to-action button that we have chosen to style via the following selector:

```
.promo a {}
```

Not only does this have poor selector intent—it will greedily style any and every link inside of a `.promo` to look like a button — it is also pretty wasteful as a result of being so locationally dependent: we can't reuse that button with its correct styling outside of `.promo` because it is explicitly tied to that location. A far better selector would have been:

```
.btn {}
```

This single class can be reused anywhere outside of `.promo` and will always carry its correct styling. As a result of a better selector, this piece of UI is more portable, more recyclable, doesn't have any dependencies, and has much better selector intent. A component shouldn't have to live in a certain place to look a certain way.


### Portability

Reducing, or, ideally, removing, location dependence means that we can move components around our markup more freely, but how about improving our ability to move classes around components? On a much lower level, there are changes we can make to our selectors that make the selectors themselves more portable, as opposed to the components they create. Take the following example:

```
input.btn {}
```

This is a qualified selector; the leading input ties this ruleset to only being able to work on input elements. By omitting this qualification, we allow ourselves to reuse the `.btn` class on any element we choose, like an a, for example, or a button.

Qualified selectors do not lend themselves well to being reused, and every selector we write should be authored with reuse in mind.

Of course, there are times when you may want to legitimately qualify a selector — you might need to apply some very specific styling to a particular element when it carries a certain class, for example:

```
/**
 * Embolden and colour any element with a class of `.error`.
 */
.error {
    color: red;
    font-weight: bold;
}

/**
 * If the element is a `div`, also give it some box-like styling.
 */
div.error {
    padding: 10px;
    border: 1px solid;
}
```

This is one example where a qualified selector might be justifiable, but I would still recommend an approach more like:

```
/**
 * Text-level errors.
 */
.error-text {
    color: red;
    font-weight: bold;
}

/**
 * Elements that contain errors.
 */
.error-box {
    padding: 10px;
    border: 1px solid;
}
```

This means that we can apply `.error-box` to any element, and not just a `div` — it is more reusable than a qualified selector.


#### Quasi-qualified selectors

One thing that qualified selectors can be useful for is signalling where a class might be expected or intended to be used, for example:

```
ul.nav {}
```

Here we can see that the `.nav` class is meant to be used on a `ul` element, and not on a `nav`. By using quasi-qualified selectors we can still provide that information without actually qualifying the selector:

```
/*ul*/.nav {}
```

By commenting out the leading element, we can still leave it to be read, but avoid qualifying and increasing the specificity of the selector.


### Object-orientation

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


#### Further reading

* [The media object saves hundreds of lines of code](http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/)
* [The flag object](http://csswizardry.com/2013/05/the-flag-object/)
* [Naming UI components in OOCSS](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)





### The single responsibility principle

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


#### Further reading

* The single responsibility principle applied to CSS





### Open to extension / closed to modification

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


#### Further reading

* [The open/closed principle applied to CSS](http://csswizardry.com/2012/06/the-open-closed-principle-applied-to-css/)





### The separation of concerns

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





### DRY

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

#### Further reading

* [Writing DRYer vanilla CSS](http://csswizardry.com/2013/07/writing-dryer-vanilla-css/)




## Selector performance

A topic which is — with the quality of today's browsers — more interesting than it is important, is selector performance. That is to say, how quickly a browser can match the selectors your write in CSS up with the nodes it finds in the DOM.

Generally speaking, the longer a selector is (i.e. the more component parts) the slower it is, for example:

```
body.home div.header ul {}
```

…is a far less efficient selector than:

```
.primary-nav {}
```

This is because browsers read CSS selectors right-to-left. A browser will read the first selector as:

1.   Find all `ul` elements in the DOM;
2.   Now check if they live anywhere inside an element with a class of 
     `.header`;
3.   Next check that `.header` class exists on a `div` element;
4.   Check that that all lives anywhere inside any elements with a class
     of `.home;`
5.   Finally, check that `.home` exists on a `body` element.

The second, in contrast, is simply a case of the browser reading: find all the elements with a class of `.primary-nav`.

To further compound the problem, we are using descendant selectors (e.g. `.foo .bar {}`). The upshot of this is that a browser is required to start with the rightmost part of the selector (i.e. `.bar`) and keep looking up the DOM indefinitely until it finds the next part (i.e. `.foo`). This could mean stepping up the DOM dozens of times until a match is found.

This is just one reason why nesting with preprocessors is often a false economy; as well as making selectors unnecessarily more specific, and creating location dependency, it also creates more work for the browser.

By using a child selector (e.g. `.foo > .bar {}`) we can make the process much more efficient, because this only requires the browser to look one level higher in the DOM, and it will stop regardless of whether or not it found a match.


### The key selector

Because browsers read selectors right-to-left, the rightmost selector is often critical in defining a selector's performance: this is called the key selector.

The following selector might appear to be highly performant at first glance. It uses an ID which is nice and fast, and there can only ever be one on a page, so surely this will be a nice and speedy lookup—just find that one ID and then style everything inside of it:

```
#foo * {}
```

The problem with this selector is that the key selector (`*`) is very, very far reaching. What this selector actually does is finds every single node in the DOM (even `<title>`, `<link>`, and `<head>` elements; everything) and then looks to see if it lives anywhere at any level within `#foo`. This is a very, very expensive selector, and should most likely be avoided or rewritten.

Thankfully, by writing selectors with good selector intent, we are probably avoiding inefficient selectors by default; we are very unlikely to have greedy key selectors if we're targeting the right things for the right reason.

That said, however, CSS selector performance should be fairly low on your list of things to optimise; browsers are fast, and are only ever getting faster, and it is only on notable edge cases that inefficient selectors would be likely to pose a problem.

As well as their own specific issues, nesting, qualifying, and poor selector intent all contribute to less efficient selectors.

## Further reading

* [Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)
* ['Scope' in CSS](http://csswizardry.com/2013/05/scope-in-css/)
* [Keep your CSS selectors short](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)
* [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [Naming UI components in OOCSS](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)
* [Writing efficient CSS selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)
