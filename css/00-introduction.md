<!-- MarkdownTOC depth=3 -->

- CSS standards guide
    - Introduction
        - The importance of a style guide
        - Disclaimers and acknowledgements

<!-- /MarkdownTOC -->





# CSS standards guide





## Introduction

These CSS guidelines are application to all websites and web applications created and managed by the University of St Andrews digital communications team and under the st-andrews.ac.uk domain.

CSS is not a pretty language. While it is simple to learn and get started with, it soon becomes problematic at any reasonable scale. There isn't much we can do to change how CSS works, but we can make changes to the way we author and structure it.

In working on large, long-running projects, with dozens of developers of differing specialities and abilities, it is important that we all work in a unified way in order to, among other things:

*   keep stylesheets maintainable;
*   keep code transparent, sane, and readable;
*   keep stylesheets scalable.

There are a variety of techniques we must employ in order to satisfy these goals, and this CSS style guide is a document of recommendations and approaches that will help us to do so.


### The importance of a style guide

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
While consistency is important, equally important is knowing when to be inconsistent—sometimes the style guide just doesn’t apply.  Ask yourself if applying the rule would make the code less readable, even for someone who is used to reading code that follows the rules. When in doubt use your best judgment, look at other examples, and decide what looks best. Readability is preferential to strict adherence to rules.


### Disclaimers and acknowledgements

This style guide draws heavily on the work of Harry Roberts’ website CSS guidelines : high-level advice and guidelines for writing sane, manageable, scalable CSS (http://cssguidelin.es/).

These guidelines are opinionated, but they have been repeatedly tried, tested, stressed, refined, broken, reworked, and revisited over a number of years on projects of all sizes.