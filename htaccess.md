# .htaccess style and standards guide

Version 0.1.0
Last updated: Thursday 21 July 2016

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

<!-- MarkdownTOC -->

- [1. About .htaccess](#1-about-htaccess)
- [2. Our use of .htaccess](#2-our-use-of-htaccess)
- [3. Version control](#3-version-control)
- [4. Rules](#4-rules)
- [5. Style](#5-style)
    - [5.1 General layout](#51-general-layout)
    - [5.2 Comments](#52-comments)
    - [5.3 Add rules](#53-add-rules)
    - [5.4 Delete rules](#54-delete-rules)

<!-- /MarkdownTOC -->




---

## 1. About .htaccess

> For websites hosted on Apache-powered servers, .htaccess is the perfect tool for a wide range of tasks. From protecting and redirecting pages to compressing and delivering content to specific browsers, .htaccess is both powerful and practical, enabling you to streamline, optimize and secure your website with ease.
> 
> Written with a deceptively simple syntax, .htaccess enables admins and designers to customize core functionality involving how content is delivered and how traffic flows throughout your site. [Just as CSS is meant for styling pages,]...] .htaccess is meant for configuring and fine-tuning the server at the directorylevel, giving you much control over the functionality of your
site.

— _.htaccess made easy: a practical guide for administrators, designers and developers_ by Jeff Starr




---

## 2. Our use of .htaccess

Our use of `.htaccess` files is largely restricted to two use-cases:

1. Temporary page redirects.
2. Permanent redirects and/or URL rewrites.

Where possible all other settings SHOULD be incorporated into the server configuration.

This short guide outlines how `.htaccess` files SHOULD be organised.

If the `.htaccess` file at the root of the server is not configured properly then redirects will not work which may result in broken links, a poor user-experience, and reputational risk.

```
Impact:     3/3
Likelihood: 3/5
Total:      9/15
```




---

## 3. Version control

The `.htaccess` file MUST be version controlled in a private Git repository (e.g. Bitbucket), so that we have a definite version that we can roll back to.




---

## 4. Rules

* When do we create a redirect?
* Where is the redirect kept (htaccess or server config)?
* How long should the redirect be kept? (where do we keep track of these?)

.htaccess directives apply to all sub-directories, so we want as few rules as possible in the root folder .htaccess file as Apache reads the .htaccess for EVERY visit to the server.

Bear in mind too that the rules cascade: rules further down the file will overrule directives further up.



---

## 5. Style

### 5.1 General layout

1. Error messages
2. Temporary redirects
3. Approved redirects
4. Rewrite engine




### 5.2 Comments

"Inline comments — when working with .htaccess, it’s helpful (and encouraged) to leave descriptive comments• along with your various directives. To do so, simply prepend a hashsymbol `#`` to the beginning of the line, like so:

```
# this is a helpful comment
# that continues on this line
    # you may indent comments
    # whenever you would like
        # and as much as you’d like
```

Comments in .htaccess files must exist on their own line, and you may add as many
comments as needed. If you place a comment on the same line as a directive, Apache will
throw the dreaded 500 — Internal Server Error•. You can indent your comments too,
because Apache ignores any white space and blank lines that may appear before a directive." p.13


### 5.3 Add rules


### 5.4 Delete rules