# Digital code style and standards guides

Version 1.4.1
Last updated: Thursday 21 July 2016

These style and standards guides are applicable to all websites and web applications created and managed by and for the University of St Andrews under the st-andrews.ac.uk domain.

<!-- MarkdownTOC -->

- [1. Background](#1-background)
    - [1.1 Potential issues](#11-potential-issues)
- [2. Objective](#2-objective)
- [3. Benefits](#3-benefits)
- [4. Scope](#4-scope)
- [5. Constraints](#5-constraints)
    - [5.1 What stops us?](#51-what-stops-us)
    - [5.2 How do we enforce it?](#52-how-do-we-enforce-it)
- [6. Assumptions](#6-assumptions)
- [7. Risks](#7-risks)
    - [7.1 Not doing](#71-not-doing)
    - [7.2 Doing](#72-doing)
- [8. Deliverables](#8-deliverables)
- [9. Stakeholders](#9-stakeholders)
    - [9.1 Governance](#91-governance)
    - [9.2 Users](#92-users)
- [10. Information \(and data\)](#10-information-and-data)

<!-- /MarkdownTOC -->




---

## 1. Background


### 1.1 Potential issues

Currently every developer has their own way of doing things, which may be fine for small, stand-alone projects but within an enterprise-level project this can lead to issues such as:

* Inconsistent code in terms of organisation, syntax, formatting, and naming conventions.
* Code bloat in production systems, often including code that is either never used or is out-of-date (e.g. hacks for redundant versions of Internet Explorer).
* Multiple implementations of functionality, with the consequential maintenance overload due to multiple chunks of code that solve the same problem in different ways, and an inconsistent look-and-feel due to multiple implementations of similar features e.g. tabs, sliders.
* Bugs and typos.
* Uncommented or poorly documented code.
* Unreadable code.
* Code from one site linked to from other sites, that if updated at source runs the risk of breaking features implemented elsewhere.

While it's obvious that these inconsistencies and issues can result from multiple developers working across multiple projects, it can also be true for solo developers working on single projects. In other words, developers can be inconsistent even with themselves in the same project.

The consequences of this are many:

* Code that is difficult or impossible to maintain.
* Code that is fragile and easy to break in unknown ways.
* Fear of updating or improving code that leads to forked code and/or duplicating functionality using different resources.
* Maintenance overload.
* Slows down development

The reason that we've reached this position is primarily that the web presence at St&nbsp;Andrews has evolved organically: there is still no formal, overarching web governance; the University had no central web team until 2006 (13 years after the introduction of the World Wide Web); there are currently no agreed standards; and we have multiple developers within multiple groups (digital communications team, IT Services, schools and support services, as well as external consultants).




---

## 2. Objective

Our objectives for introducing code standards and style guides are:

1. Develop an agreed standard for all code and ensure that code within scope adheres to these standards.
2. Use industry best practices.
3. Promote efficiency in maintaning code.
4. Continuously improve our code.




---

## 3. Benefits

Standard conventions will make it easier for developers to make decisions about how to code which should result in faster development, and make it easier to spot errors and typos.




---

## 4. Scope

These standards and style guides apply to all new websites and applications for which the digital communications team is responsible (whether developed in-house or outsourced). Guidelines will be written for the following languages:

* Cascading Stylesheets (CSS), including pre-processors such as Sass.
* HTML
* JavaScript, including frameworks such as jQuery
* PHP
* XML, including RSS and XSLT

as well as 

* Commit messages (for version control software, e.g. Git.)
* Markdown (for writing documentation)
* Sublime Text packages (standard packages for developing the DPL).

These standards and style guides will also apply to existing code in the digital pattern library; these patterns will need to be refactored to comply with these guidelines.

It is understood that other developers within the University may choose to adopt these guidelines, but at this stage this is not mandatory. 




---

## 5. Constraints

### 5.1 What stops us?

* It's a lot of work to define and document exactly what we want.
* Building consensus with other developers.


### 5.2 How do we enforce it?

External standards, policies and regulations, e.g.

* HTML specifications (W3C)
* CSS specifications (W3C)
* ECMAScript (JavaScript) specifications
* PHP specifications
* XML specifications (W3C), including RSS/Atom and XSLT
* In-code documentation formatting standards such as PHPDoc, JSDoc, etc.
* Other relevant code standards such as Microformats (hCalendar, hCard), microdata, FOAF, DOAC, Dublin Core metadata, RDF, WordPress Codex, etc.

It is imperative that we introduce these code standards and style guides as soon as possible so that we may reduce existing code-debt (code that has been developed prior to the introduction of these standards) in the digital pattern library.




---

## 6. Assumptions

* We're allowed to enforce governance on front-end code.
* Delivered in a digital manner.
* We will maintain and continuously improve the code standards guides.




---

## 7. Risks

### 7.1 Not doing

* Current issues (described in 1. Background) and consequences will continue or even get worse.


### 7.2 Doing
* Code that is developed before the standard is completed will need to be refactored.
* May slow down some development.
* Developers refuse to use it because of personal coding preferences and habits.
* Developers may feel frustrated because their coding requirements are not addressed.




---

## 8. Deliverables

Standards and/or style guide documentation for each language in scope, written in Markdown (which can be converted easily to HTML):

1. Commit messages style guide
2. CSS style and standards guide
3. HTML style guide
4. JavaScript style guide
5. Markdown style guide
6. PHP style guide
7. Sublime Text editor standards guide
8. XML style guide




---

## 9. Stakeholders

### 9.1 Governance

* Chief Information Officer
* Director of Corporate Communications
* Digital communications team


### 9.2 Users

* Digital communications team
* (Development teams)
    * IT Services
    * Schools
    * Support services
* (External)
    * Developers
    * Software providers
    * Consultants




---

## 10. Information (and data)

* List of applications and scripts for which we are responsible. https://trello.com/b/dhSK5nzg/service-catalogue
