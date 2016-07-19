# Commit message style guide

Version 1.1
Last updated: Tuesday 19 July 2016

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

* TODO: Tag formats
* TODO: Version numbers

<!-- MarkdownTOC -->

- [1. Introduction](#1-introduction)
- [2. Commit message](#2-commit-message)
    - [2.1 Subject line](#21-subject-line)
        - [i. Type](#i-type)
        - [ii. Component](#ii-component)
        - [iii. Brief summary](#iii-brief-summary)
    - [2.2 Description \(optional\)](#22-description-optional)
    - [2.3 Reference\(s\) \(optional\)](#23-references-optional)
- [4. Examples](#4-examples)
- [References](#references)

<!-- /MarkdownTOC -->




---

## 1. Introduction

<sub>Based on [WordPress][wordpresscommit]</sub>

This guide outlines how messages SHOULD be formatted when committing code to any version control system, such as Git or Subversion (SVN).

Commit messages are an integral part of each project's history, along with the changesets themselves. We write commit messages for multiple audiences: 

* Colleagues (developers on the same project)
* Future contributors
* Computers
 
Good commit messages serve each of these audiences well. They describe the what and the why of the changeset; the how is described by the diff itself.




---

## 2. Commit message

<sub>Based on [BlueJava][bluejavacommit]</sub>

Each commit message SHOULD include:

* **Subject line** — with TYPE, Component, and a Brief summary.
* **Description** (optional) — always preceded by a blank line.
* **Reference** (optional) — always preceded by a blank line.

A well-formed commit message SHOULD look something like this:

```
TYPE (Component) Brief summary

Longer description with more details, such as a `code` being introduced
within the context of a `function`.

Multiple paragraphs may be added as required.

Bulleted lists:
* are
* also
* okay

Closes #123
```

Only the top line is required, so a minimal commit message might look like

```
TYPE (Component) Brief summary
```


### 2.1 Subject line

Generally, the subject line comprises three elements:

* `TYPE`
* `(Component)`
* `Brief summary`

The only **exception** is when populating a **new repository**. All that is required is a subject line of `Initial commit`.


#### i. Type

Every commit subject line MUST start with a TYPE in all CAPS and no spaces or other characters preceding it. The recognised types are:

<table>
    <thead>
        <tr>
            <th>TYPE</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>BREAK</code></td>
            <td>A breaking change such as removing a feature.</td>
        </tr>
        <tr>
            <td><code>DOCS</code></td>
            <td>Changes to the documentation (readme, API docs, etc.).</td>
        </tr>        
        <tr>
            <td><code>FEAT</code></td>
            <td>New feature in production code.</td>
        </tr>
        <tr>
            <td><code>FIX</code></td>
            <td>Bug fix in production code.</td>
        </tr>
        <tr>
            <td><code>FORMAT</code></td>
            <td>Code formatting, code comment change, etc; (compiled-code neutral).</td>
        </tr>
        <tr>
            <td><code>MAINT</code></td>
            <td>Updating dev-related maintenance files ("non-production code" files).</td>
        </tr>
        <tr>
            <td><code>MERGE</code></td>
            <td>Pull request to merge branch into another branch or master.</td>
        </tr>
        <tr>
            <td><code>TEST</code></td>
            <td>Adding missing tests or editing tests.</td>
        </tr>        
    </tbody>
</table>


#### ii. Component

Briefly describe the component, feature or module being developed; in the case of a pull request MERGE simply add the branch name.

Consistency is important. Make sure you have a definitive list of the various components being developed somewhere in your project notes so that all code contributors are aware of them. Adding a new component should be a considered decision, not just a whim when making your commit.

* MUST be separated from the TYPE with a single space.
* MUST be enclosed in parentheses/round brackets, i.e. `()`.
* MUST be consistently named throughout a project. For example, don't name it `(Long-form content)` in one commit but `(long form)` in another.


#### iii. Brief summary

The first line of a commit message is a brief summary of the changeset. 

The brief summary is used for email subject lines, changelogs, and features prominently in most version control system log formats such as `git log --format=oneline`.

The high visibility of the summary makes it critical to craft something that is as descriptive as possible within space limits.

* MUST be one line; no line breaks.
* MUST begin with a capital.
* MUST NOT include a dot (full stop/period) at the end.
* SHOULD use the [imperative mood][wikipedia-imperative] when possible, e.g. "change" not "changed" nor "changes".
* SHOULD aim for **around 50 characters or fewer, stopping at 70**. This is important because log-viewing tools nearly all expect the first line of commit messages to fit within these limits. This difficult restriction may force you to think critically about the essence of your commit; if you can’t describe the change in a short sentence, the commit may not be atomic enough. Note that the TYPE counts toward the 50/70 character count.


### 2.2 Description (optional)

The longer, multi-line description is optional, but if you wish to include it always separate it from the subject line by a blank line. In other words, the second line in your commit message SHOULD always be blank if you are making a multi-line commit.

The longer description is a chance to elaborate on the change you made. **Focus on the motivation and extra considerations for the change rather than detailing what you changed**. The details of what changed can be seen in the file diff. But extra considerations such as side effects or migration hints are less obvious from the code, and could be helpful to detail here.

* MUST be separated from the subject line by a blank line.
* SHOULD describe the _what_ and the _why_ of the changeset, rather than the _how_.
* SHOULD Use the [imperative mood][wikipedia-imperative].
* MAY be multiple paragraphs if required, separated by blank lines for clarity.
* MAY include bulleted lists (using asterisks).


### 2.3 Reference(s) (optional)

The footer of your commit message is where you should reference issues or ticket numbers to which the change pertains. The format of each footer line should be specific and understood by all team members. For example:

```
Closes GitHub issue #123, #456
Implements #543
```

* MUST be separated from the description (if present) or subject line by a blank line.
* Ticket references SHOULD be on their own line. Include (in parentheses) the name of the ticketing system if this clarifies things.
* Multiple ticket references SHOULD be separated by a comma and space.
* If referencing both fixed and related tickets, SHOULD begin with "Fixes" and end each set with a full-stop, e.g. `Fixes #123, #456. See #765.`.




---

## 4. Examples

```
FEAT (Scrollspy) Add Scrollspy into long-form-content module

Scrollspy was previously removed to reduce file size but is
now required for a number of projects. This has been added
back in, including full documentation.

Fixes GitHub issue #15
```

```
DOCS (Commit messages) Textual clarifications to subject line rules

* I changed my mind about insisting on a full stop after the brief 
  summary as it takes up one of the 50/70 character limit, it looks
  more like a heading this way, and it is less fussy.
* I teased out rules about how to style a component, to remove 
  any ambiguity.
```

```
PULL (Sticky-nav) Merge into master

Sticky-nav feature is completed and tested. Final testing is required before 
merging into master for release v0.5.2

Acceptance criteria
* Code complies with style guide.
* Compile in Grunt without error.
* Examples work without error.

Fixes GitHub issue #45
Fixes GitHub issue #47
Fixes GitHub issue #51
```




---

## References

Inspired by and based heavily on:

* [Bluejava Git commit message format guide][bluejavacommit]
* [Make WordPress core handbook: Commit messages][wordpresscommit]
* [AngularJS Git commit message conventions][angularjs]

[bluejavacommit]: https://github.com/bluejava/git-commit-guide "Bluejava Git commit message format guide"
[wordpresscommit]: https://make.wordpress.org/core/handbook/best-practices/commit-messages/ "Make WordPress Core commit messages"
[wikipedia-imperative]: https://en.wikipedia.org/wiki/Imperative_mood "The imperative is a grammatical mood that forms commands or requests, including the giving of prohibition or permission, or any other kind of advice or exhortation."
[angularjs]: https://gist.github.com/stephenparish/9941e89d80e2bc58a153 "Commit Message Conventions by Stephen Parish"
