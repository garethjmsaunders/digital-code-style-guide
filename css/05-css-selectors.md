## CSS Selectors

Perhaps somewhat surprisingly, one of the most fundamental, critical aspects of writing maintainable and scalable CSS is selectors. Their specificity, their portability, and their reusability all have a direct impact on the mileage we will get out of our CSS, and the headaches it might bring us.


### Selector intent

It is important when writing CSS that we scope our selectors correctly, and that we're selecting the right things for the right reasons. Selector intent is the process of deciding and defining what you want to style and how you will go about selecting it. For example, if you are wanting to style your website's main navigation menu, a selector like this would be incredibly unwise:

```
header ul {}
```

This selector's intent is to style any ul inside any header element, whereas our intent was to style the site's main navigation. This is poor selector intent: you can have any number of header elements on a page, and they in turn can house any number of uls, so a selector like this runs the risk of applying very specific styling to a very wide number of elements. This will result in having to write more CSS to undo the greedy nature of such a selector.

A better approach would be a selector like:

```
.site-nav {}
```

An unambiguous, explicit selector with good selector intent. We are explicitly selecting the right thing for exactly the right reason.

Poor selector intent is one of the biggest reasons for headaches on CSS projects. Writing rules that are far too greedy—and that apply very specific treatments via very far reaching selectors—causes unexpected side effects and leads to very tangled stylesheets, with selectors overstepping their intentions and impacting and interfering with otherwise unrelated rulesets.

CSS cannot be encapsulated, it is inherently leaky, but we can mitigate some of these effects by not writing such globally-operating selectors: your selectors should be as explicit and well reasoned as your reason for wanting to select something.


### Reusability

With a move toward a more component-based approach to constructing UIs, the idea of reusability is paramount. We want the option to be able to move, recycle, duplicate, and syndicate components across our projects.

To this end, we make heavy use of classes. IDs, as well as being hugely over-specific, cannot be used more than once on any given page, whereas classes can be reused an infinite amount of times. Everything you choose, from the type of selector to its name, should lend itself toward being reused.


### Location independence

Given the ever-changing nature of most UI projects, and the move to more component-based architectures, it is in our interests not to style things based on where they are, but on what they are. That is to say, our components' styling should not be reliant upon where we place them—they should remain entirely location independent.

Let's take an example of a call-to-action button that we have chosen to style via the following selector:

```
.promo a {}
```

Not only does this have poor selector intent—it will greedily style any and every link inside of a .promo to look like a button—it is also pretty wasteful as a result of being so locationally dependent: we can't reuse that button with its correct styling outside of .promo because it is explicitly tied to that location. A far better selector would have been:

```
.btn {}
```

This single class can be reused anywhere outside of .promo and will always carry its correct styling. As a result of a better selector, this piece of UI is more portable, more recyclable, doesn't have any dependencies, and has much better selector intent. A component shouldn't have to live in a certain place to look a certain way.


### Portability

Reducing, or, ideally, removing, location dependence means that we can move components around our markup more freely, but how about improving our ability to move classes around components? On a much lower level, there are changes we can make to our selectors that make the selectors themselves—as opposed to the components they create—more portable. Take the following example:

```
input.btn {}
```

This is a qualified selector; the leading input ties this ruleset to only being able to work on input elements. By omitting this qualification, we allow ourselves to reuse the .btn class on any element we choose, like an a, for example, or a button.

Qualified selectors do not lend themselves well to being reused, and every selector we write should be authored with reuse in mind.

Of course, there are times when you may want to legitimately qualify a selector—you might need to apply some very specific styling to a particular element when it carries a certain class, for example:

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

This means that we can apply .error-box to any element, and not just a div—it is more reusable than a qualified selector.


### Quasi-qualified selectors

One thing that qualified selectors can be useful for is signalling where a class might be expected or intended to be used, for example:

```
ul.nav {}
```

Here we can see that the .nav class is meant to be used on a ul element, and not on a nav. By using quasi-qualified selectors we can still provide that information without actually qualifying the selector:

```
/*ul*/.nav {}
```

By commenting out the leading element, we can still leave it to be read, but avoid qualifying and increasing the specificity of the selector.


### Naming

As Phil Karlton once said, 'There are only two hard things in Computer Science: cache invalidation and naming things.'

I won't comment on the former claim here, but the latter has plagued me for years. My advice with regard to naming things in CSS is to pick a name that is sensible, but somewhat ambiguous: aim for high reusability. For example, instead of a class like .site-nav, choose something like .primary-nav; rather than .footer-links, favour a class like .sub-links.

The differences in these names is that the first of each two examples is tied to a very specific use case: they can only be used as the site's navigation or the footer's links respectively. By using slightly more ambiguous names, we can increase our ability to reuse these components in different circumstances.

To quote Nicolas Gallagher:

> Tying your class name semantics tightly to the nature of the content has
> already reduced the ability of your architecture to scale or be easily put 
> to use by other developers.

That is to say, we should use sensible names—classes like `.border` or `.red` are never advisable—but we should avoid using classes which describe the exact nature of the content and/or its use cases. Using a class name to describe content is redundant because content describes itself.

The debate surrounding semantics has raged for years, but it is important that we adopt a more pragmatic, sensible approach to naming things in order to work more efficiently and effectively. Instead of focussing on 'semantics', look more closely at sensibility and longevity—choose names based on ease of maintenance, not for their perceived meaning.

Name things for people; they're the only things that actually read your classes (everything else merely matches them). Once again, it is better to strive for reusable, recyclable classes rather than writing for specific use cases. Let's take an example:

```
/**
 * Runs the risk of becoming out of date; not very maintainable.
 */
.blue {
    color: blue;
}

/**
 * Depends on location in order to be rendered properly.
 */
.header span {
    color: blue;
}

/**
 * Too specific; limits our ability to reuse.
 */
.header-color {
    color: blue;
}

/**
 * Nicely abstracted, very portable, doesn't risk becoming out of date.
 */
.highlight-color {
    color: blue;
}
```

It is important to strike a balance between names that do not literally describe the style that the class brings, but also ones that do not explicitly describe specific use cases. Instead of .home-page-panel, choose .masthead; instead of .site-nav, favour .primary-nav; instead of .btn-login, opt for .btn-primary.


### Naming UI components

Naming components with agnosticism and reusability in mind really helps developers construct and modify UIs much more quickly, and with far less waste. However, it can sometimes be beneficial to provide more specific or meaningful naming alongside the more ambiguous class, particularly when several agnostic classes come together to form a more complex and specific component that might benefit from having a more meaningful name. In this scenario, we augment the classes with a data-ui-component attribute which houses a more specific name, for example:

```
<ul class="tabbed-nav" data-ui-component="Main Nav">
```

Here we have the benefits of a highly reusable class name which does not describe—and, therefore, tie itself to—a specific use case, and added meaning via our data-ui-component attribute. The data-ui-component's value can take any format you wish, like title case:

```
<ul class="tabbed-nav" data-ui-component="Main Nav">
```

Or class-like:

```
<ul class="tabbed-nav" data-ui-component="main-nav">
```

Or namespaced:

```
<ul class="tabbed-nav" data-ui-component="nav-main">
```

The implementation is largely personal preference, but the concept still remains: Add any useful or specific meaning via a mechanism that will not inhibit your and your team's ability to recycle and reuse CSS.


### Selector performance

A topic which is—with the quality of today's browsers—more interesting than it is important, is selector performance. That is to say, how quickly a browser can match the selectors your write in CSS up with the nodes it finds in the DOM.

Generally speaking, the longer a selector is (i.e. the more component parts) the slower it is, for example:

```
body.home div.header ul {}
```

…is a far less efficient selector than:

```
.primary-nav {}
```

This is because browsers read CSS selectors right-to-left. A browser will read the first selector as

* find all `ul` elements in the DOM;
* now check if they live anywhere inside an element with a class of `.header`;
* next check that `.header` class exists on a `div` element;
* now check that that all lives anywhere inside any elements with a class of 
  `.home;`
* finally, check that `.home` exists on a `body` element.
* 
The second, in contrast, is simply a case of the browser reading

* find all the elements with a class of `.primary-nav`.

To further compound the problem, we are using descendant selectors (e.g. `.foo .bar {}`). The upshot of this is that a browser is required to start with the rightmost part of the selector (i.e. `.bar`) and keep looking up the DOM indefinitely until it finds the next part (i.e. `.foo`). This could mean stepping up the DOM dozens of times until a match is found.

This is just one reason why nesting with preprocessors is often a false economy; as well as making selectors unnecessarily more specific, and creating location dependency, it also creates more work for the browser.

By using a child selector (e.g. `.foo > .bar {}`) we can make the process much more efficient, because this only requires the browser to look one level higher in the DOM, and it will stop regardless of whether or not it found a match.


### The key selector

Because browsers read selectors right-to-left, the rightmost selector is often critical in defining a selector's performance: this is called the key selector.

The following selector might appear to be highly performant at first glance. It uses an ID which is nice and fast, and there can only ever be one on a page, so surely this will be a nice and speedy lookup—just find that one ID and then style everything inside of it:

```
foo * {}
```

The problem with this selector is that the key selector (`*`) is very, very far reaching. What this selector actually does is finds every single node in the DOM (even `<title>`, `<link>`, and `<head>` elements; everything) and then looks to see if it lives anywhere at any level within foo. This is a very, very expensive selector, and should most likely be avoided or rewritten.

Thankfully, by writing selectors with good selector intent, we are probably avoiding inefficient selectors by default; we are very unlikely to have greedy key selectors if we're targeting the right things for the right reason.

That said, however, CSS selector performance should be fairly low on your list of things to optimise; browsers are fast, and are only ever getting faster, and it is only on notable edge cases that inefficient selectors would be likely to pose a problem.

As well as their own specific issues, nesting, qualifying, and poor selector intent all contribute to less efficient selectors.


### General rules

Your selectors are fundamental to writing good CSS. To very briefly sum up the above sections:

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


### Further reading

* [Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)
* ['Scope' in CSS](http://csswizardry.com/2013/05/scope-in-css/)
* [Keep your CSS selectors short](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)
* [About HTML semantics and front-end architecture](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
* [Naming UI components in OOCSS](http://csswizardry.com/2014/03/naming-ui-components-in-oocss/)
* [Writing efficient CSS selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)





## Writing efficient CSS selectors

In Steve Souders’ book _Even Faster Websites_ (O'Reilly, 2009) he quotes David Hyatt’s article [Writing Efficient CSS for use in the Mozilla UI](https://developer.mozilla.org/en/Writing_Efficient_CSS) which discusses how CSS can be optimised to take advantage of how browsers interpret CSS code.

Taking the following rule as an example:

```
#toc > li {
    color: #444;
}
```

one might assume, particularly by someone who reads from left-to-right, that the browsers would locate the element with an  ID of toc and then apply the style to its children who are li elements.

In reality though, browsers match from right-to-left. So the browser iterates over every li element on the page and determine whether its parent is toc.
We can use this knowledge to write more efficient CSS selectors. The following are David Hyatt and Steve Souders’ guidelines:

1.  Avoid universal rules: use ID, class and tag selectors exclusively.
2.  Don’t qualify ID selectors.
3.  Don’t qualify class selectors.
4.  Make rules as specific as possible.
5.  Avoid descendant selectors.
6.  Avoid tag-child selectors.
7.  Question all usages of the child selector.
8.  Rely on inheritance.

