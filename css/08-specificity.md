CSS code style guide

# Specificity

"CSS isn't the most friendly of languages: globally operating, very leaky, dependent on location, hard to encapsulate, based on inheritance. But none of that even comes close to the horrors of specificity."

This section is largely based on Harry Roberts' [CSS Guidelines - Specificity](http://cssguidelin.es/#specificity "CSS Guidelines - Specificity")









## In this section
<!-- MarkdownTOC -->

- [Keep specificity low at all times](#keep-specificity-low-at-all-times)
- [Do not use !important as a hack](#do-not-use-important-as-a-hack)
- [Use !important proactively not reactively](#use-important-proactively-not-reactively)
- [Hacking specificity](#hacking-specificity)
    - [Chain a class with itself](#chain-a-class-with-itself)
    - [Use an attribute selector to select an ID](#use-an-attribute-selector-to-select-an-id)
    - [Further reading](#further-reading)

<!-- /MarkdownTOC -->





## Keep specificity low at all times

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





## Do not use !important as a hack

`!important` is often used as a way to cheat your way out of specificity wars. The general rule is this: **do not use !important**, especially if it is used as a ham-fisted hack to 'just make things work'.

How many times have we seen code like this?

```
#navigation ul.nav-list li.nav-item a {
    color: blue !important;
}
```

How much more specific will the next rule need to be?!

If you find that you need to use `!important` to get something to work then that is a good sign that your code needs to be refactored. As Harry Roberts says, `!important` is "often viewed as a last resort — a desperate, defeated stab at patching over the symptoms of a much bigger problem with your code."





## Use !important proactively not reactively

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





## Hacking specificity

With all that said on the topic of specificity, and keeping it low, it is inevitable that we will encounter problems. No matter how hard we try, and how conscientious we are, there will always be times that we need to hack and wrangle specificity.

When these situations do arise, it is important that we handle the hacks as safely and elegantly as possible.


### Chain a class with itself

In the event that you need **to increase the specificity of a class selector**, there are a number of options. We could nest the class inside something else to bring its specificity up. For example, we could use `.header .site-nav {}` to bring up the specificity of a simple `.site-nav {}` selector.

The problem with this, as we've discussed, is that it introduces location dependency: these styles will only work when the `.site-nav` component is in the `.header` component.

Instead, we can use a much safer hack that will not impact this component's portability: we can chain that class with itself:

```
.site-nav.site-nav {}
```

This chaining doubles the specificity of the selector, but does not introduce any dependency on location.


### Use an attribute selector to select an ID

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


### Further reading
[Hacks for dealing with specificity](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/)
