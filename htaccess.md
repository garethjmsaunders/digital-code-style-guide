# .htaccess style and standards guide

Version 0.2.0
Last updated: Monday 8 August 2016

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

<!-- MarkdownTOC -->

- [1. About .htaccess](#1-about-htaccess)
- [2. What we use .htaccess for](#2-what-we-use-htaccess-for)
- [4. Version control](#4-version-control)
- [5. Filenames](#5-filenames)
- [6. Style](#6-style)
    - [6.1 General layout](#61-general-layout)
    - [6.2 Redirect rules](#62-redirect-rules)
    - [6.3 Comments](#63-comments)
    - [6.4 Add rules](#64-add-rules)
    - [6.5 Delete rules](#65-delete-rules)

<!-- /MarkdownTOC -->




---

## 1. About .htaccess

An .htaccess file is a nameless file with an extension of `.htaccess` which is used by Apache httpd servers to make configuration changes on a per-directory basis. It is often placed in the root directory, but it may also be placed in any number of subdirectories.

In Unix-like operating systems, any file or folder that begins with a dot character (commonly called a 'dot file' or 'dotfile') is treated by the operating system as hidden.

.htaccess files can be used for a wide range of tasks, including password-protecting directories, redirecting pages, compressing content and delivering content to specific browsers.

A word of caution, though, from the Apache httpd server documentation:

> You should avoid using .htaccess files completely if you have access to httpd main server config file. Using .htaccess files slows down your Apache http server. Any directive that you can include in a .htaccess file is better set in a Directory block, as it will have the same effect with better performance.
> 
> Source: [Apache HTTP Server Tutorial: .htaccess files](https://httpd.apache.org/docs/current/howto/htaccess.html)




---

## 2. What we use .htaccess for

As .htaccess directives apply to all sub-directories, we want as few rules as possible in the root folder Remember that the web server reads the .htaccess for _every_ visit to the server.

.htaccess files MUST only be used for the following use-cases:

<table>
    <thead>
        <tr>
            <th>Use-case</th>
            <th>Description</th>
            <th>Removed&nbsp;after</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Error&nbsp;messages</td>
            <td>Location of HTTP custom error responses.</td>
            <td>Permanent</td>
        </tr>

        <tr>
            <td>Quick fix</td>
            <td>Temporary, quick-fix page redirects to deal with errors such as the wrong URL being sent out in an email.</td>
            <td>3 to 6 months</td>
        </tr>

        <tr>
            <td>Restructed site</td>
            <td>Temporary, page redirects following a site restructure (such as moving a site into T4) to allow people to update their bookmarks and search engines to update their listings.</td>
            <td>3 to 6 months</td>
        </tr>

        <tr>
            <td>Rewrite</td>
            <td>Permanent rewrite engine rules.</td>
            <td>Permanent</td>
        </tr>                
    </tbody>
</table>

Long-term redirects (over 6 months) and other directives MUST be incorporated into the main server config file.

This short guide outlines how .htaccess files MUST be organised and managed.

If the .htaccess file at the root of the server is not configured properly then redirects will not work which may result in at best broken links and at worst an unusable web server, which will obviously also create a poor user-experience and introduce reputational risk.

Impact:     3/3
Likelihood: 3/5
Total risk  9/15

Following this guide will reduce the likelihood of errors being introduced and reduce the risk associated with editing the .htaccess file.




---

## 4. Version control

The .htaccess file MUST be version controlled in a _private_ Git repository (e.g. Bitbucket), so that there is always a working version that can be rolled back to.

Commits MUST be made only after the file has been tested on the server; in other words, only commit verifiably working .htaccess files.

Commit messages MUST follow the [Commit message style guide](https://github.com/standrewsdigital/digital-code-style-guide/blob/master/commit-messages.md).




---

## 5. Filenames

The .htaccess filename SHOULD be named `.htaccess`, that is a nameless file with a `.htaccess` extension.

However, you MAY alternatively name the file `htaccess.acl`.

Files MUST be saved with Unicode (UTF-8) encoding; saving with the byte-order mark (UTF-8 with BOM) is optional, but recommended.




---

## 6. Style

### 6.1 General layout

The .htaccess SHOULD be organised with rules in the following order:

1. Error messages
2. Quick-fix redirects
3. Restructured site redirects
4. Rewrite engine rules

However, bear in mind that the rules cascade: rules further down the file will overrule directives further up.


### 6.2 Redirect rules

Redirect rules MUST be created using the following format:

```
Redirect 301 path/to/old/url http://www.st-andrews.ac.uk/path/to/new/url
```

* Use only the 301 moved permanently redirect. This is used for permanent URL redirection, meaning current links or records using the URL that the response is received for should be updated.
* You MUST separate each component within the direct rule with a single space, not a tab.
* You MUST NOT include a slash at the end of the URIs or URLs.


### 6.3 Comments

When working with .htaccess, it's helpful (and encouraged) to leave descriptive comments along with your various directives. To do so, simply prepend a hashsymbol `#`` to the beginning of the line, like so:

```
# this is a helpful comment
# that continues on this line
    # you may indent comments
    # whenever you would like
        # and as much as you'd like
```

Comments in .htaccess files MUST exist on their own line

and you may add as many comments as needed. If you place a comment on the same line as a directive, Apache will throw the dreaded 500 — Internal Server Error•. You can indent your comments too, because Apache ignores any white space and blank lines that may appear before a directive." p.13


### 6.4 Add rules


### 6.5 Delete rules