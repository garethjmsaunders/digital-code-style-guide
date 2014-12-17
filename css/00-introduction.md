CSS code style guide

# Introduction

These CSS guidelines are application to all websites and web applications created and managed by the University of St Andrews digital communications team and under the st-andrews.ac.uk domain.




## In this section
<!-- MarkdownTOC depth=3 -->

- [The importance of a style guide](#the-importance-of-a-style-guide)
- [When to be inconsistent](#when-to-be-inconsistent)
- [Write valid CSS](#write-valid-css)
    - [Vendor prefixes](#vendor-prefixes)
- [Acknowledgements](#acknowledgements)

<!-- /MarkdownTOC -->




## The importance of a style guide

CSS is not a pretty language. While it is simple to learn and get started with, it soon becomes problematic at any reasonable scale. There isn't much we can do to change how CSS works, but we can make changes to the way we author and structure it.

In working on large, long-running projects, with dozens of developers of differing specialities and abilities, it is important that we all work in a unified way in order to, among other things:

*   keep stylesheets maintainable;
*   keep code transparent, sane, and readable;
*   keep stylesheets scalable.

There are a variety of techniques we must employ in order to satisfy these goals, and this CSS style guide is a document of recommendations and approaches that will help us to do so.

A coding style guide (note, not a visual style guide) is a valuable tool for teams who:

*   build and maintain products for a reasonable length of time;
*   have developers of differing abilities and specialisms;
*   have a number of different developers working on a product at any
    given time;
*   on-board new staff regularly;
*   have a number of codebases that developers dip in and out of.

While style guides are typically more suited to product teams—large codebases on long-lived and evolving projects, with multiple developers contributing over prolonged periods of time—all developers should strive for a degree of standardisation in their code.

A good style guide, when well followed, will:

*   set the standard for code quality across a codebase;
*   promote consistency across codebases;
*   give developers a feeling of familiarity across codebases;
*   increase productivity.

Style guides should be learned, understood, and implemented at all times on a project which is governed by one, and any deviation must be fully justified.





## When to be inconsistent

While consistency is important, equally important is knowing when to be inconsistent—sometimes the style guide just doesn’t apply.

Ask yourself if applying the rule would make the code less readable, even for someone who is used to reading code that follows the rules. When in doubt use your best judgment, look at other examples, and decide what looks best.

Readability is preferential to strict adherence to rules.





## Write valid CSS

All CSS code should validate to the latest CSS specification for which it is written.

The [W3C CSS validation service](http://jigsaw.w3.org/css-validator/) is a useful resource. You may also find CSS validators that integrate with your code editor of choice, or your browser.


### Vendor prefixes

There are occasions when this is not possible, for example in CSS3 vendor-specific prefixes (e.g. `-webkit-`, `–moz-`, `-ms-`, `-o-`) are permitted. 

As Andy Clarke says in _Hardboiled Web Design_ (2010):

> using [vendor-specific prefixes] will render a style sheet technically
> invalid, but you should know by now that validation is a tool, not a 
> religion. An invalid style sheet is a small price to pay for all we can 
> achieve using emerging CSS3 standards.





## Acknowledgements

This style guide draws heavily on the work of Harry Roberts’ work at [CSS guidelines: High-level advice and guidelines for writing sane, manageable, scalable CSS](http://cssguidelin.es/).

As Roberts says, "These guidelines are opinionated, but they have been repeatedly tried, tested, stressed, refined, broken, reworked, and revisited over a number of years on projects of all sizes."
