# .htaccess style and standards guide

Version 0.3.0
Last updated: Monday 8 August 2016

The terms MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are used in this document with the meanings found in [RFC 2119: Key words for use in RFCs to indicate requirement levels](https://www.ietf.org/rfc/rfc2119.txt).

<!-- MarkdownTOC -->

- [1. About .htaccess](#1-about-htaccess)
- [2. What we use .htaccess for](#2-what-we-use-htaccess-for)
- [4. Version controlled](#4-version-controlled)
- [5. Filenames](#5-filenames)
- [6. Style](#6-style)
    - [6.1 General layout](#61-general-layout)
    - [6.2 Redirect rules](#62-redirect-rules)
        - [6.2.1 Format](#621-format)
        - [6.2.2 Order of rules](#622-order-of-rules)
    - [6.3 Comments](#63-comments)
        - [6.3.1 File title](#631-file-title)
        - [6.3.2 Section titles](#632-section-titles)
- [7. Adding new redirects](#7-adding-new-redirects)
- [8. Example file](#8-example-file)

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

This short guide outlines how .htaccess files MUST be organised and managed.

As .htaccess directives apply to all sub-directories, we want as few rules as possible in the root folder. Remember that the web server reads the .htaccess for _every_ visit to the server.

.htaccess files SHOULD only be used for the following use-cases:

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

If the .htaccess file at the root of the server is not configured properly then redirects will not work which may result in at best broken links and at worst an unusable web server, which will obviously also create a poor user-experience and introduce reputational risk.

Impact:     3/3
Likelihood: 3/5
Total risk  9/15

Following this guide will reduce the likelihood of errors being introduced and reduce the risk associated with editing the .htaccess file.




---

## 4. Version controlled

The .htaccess file MUST be version controlled in a _private_ Git repository (e.g. Bitbucket), so that there is always a working version that can be rolled back to.

Commits MUST be made only after the file has been tested on the server; in other words, only commit verifiably working .htaccess files.

Commit messages MUST follow the [commit message style guide](https://github.com/standrewsdigital/digital-code-style-guide/blob/master/commit-messages.md).

You MAY tag commits, but there is no need to unless it marks a significant event.




---

## 5. Filenames

The .htaccess filename SHOULD be named `.htaccess`: a nameless file with a `.htaccess` extension.

Because of how the server is configured, you MAY name the file `htaccess.acl`, although the strong preference is for `.htaccess`.

Files MUST be saved with Unicode (UTF-8) encoding; saving with the byte-order mark (UTF-8 with BOM) is optional, but recommended.




---

## 6. Style

### 6.1 General layout

The .htaccess SHOULD be organised with rules in the following order:

1. Error messages
2. Quick-fix redirects
3. Restructured site redirects
4. Rewrite engine rules

However, bear in mind that in a few places with a .htaccess file rule-order is important, so you may need to break this order.


### 6.2 Redirect rules

#### 6.2.1 Format

Redirect rules MUST be created using the following format:

```
Redirect 301 /path/to/old/url http://www.st-andrews.ac.uk/path/to/new/url
```

* Use only the 301 (moved permanently) redirect. This is used for permanent URL redirection, meaning current links or records using the URL that the response is received for should be updated.
* You MUST separate each component within the direct rule with a single space, not a tab.
* You MUST NOT include a slash at the end of the URIs or URLs.


#### 6.2.2 Order of rules

Because of the cascade, if you need to redirect a parent directory as well as a number of its sub-directories, you must list the parent directory _after_ the sub-directories. For example:

```
Redirect 301 /path/to/old/sub-1 https://www.st-andrews.ac.uk/parent/sub-1
Redirect 301 /path/to/old/sub-2 https://www.st-andrews.ac.uk/parent/sub-2
Redirect 301 /path/to/old/sub-3 https://www.st-andrews.ac.uk/parent/sub-3
Redirect 301 /path/to/old https://www.st-andrews.ac.uk/parent
```




### 6.3 Comments

As with all code endeavours, you are encouraged to leave descriptive comments for whoever comes after you (that may even be you).

Comments in .htaccess files are prepended with a hash (`#`) symbol.

```
# This is a helpful comment
# that continues on this line.
```

* Comments MUST exist on their own line. If you place a comment on the same line as a directive, Apache httpd will throw a 500 Internal Server Error.
* Comments SHOULD be written as complete, grammatical sentences with an initial capital and a full-stop at the end.
* You MUST keep comments up-to-date when code changes.


#### 6.3.1 File title

The .htaccess file MUST begin with a general introductory block that records the following:

```
# ==========================================================================
#  FILE TITLE (IN ALL CAPS)
# ========================================================================== 
# Description of what the file is used for. You SHOULD also include a simple 
# table of contents, e.g.
#
#     TABLE OF CONTENTS
#
#     1. Error messages
#     2. Quick-fix redirects
#     3. Restructured sites redirects
#     4. Rewrite engine rules
#
# @version     1.2.0  2016-07-04
# @owner       Name, School or unit <email@st-andrews.ac.uk>
```


#### 6.3.2 Section titles

Every new major section and sub-section of a .htaccess file MUST be prefixed with a section title and meta information.

```




# ==========================================================================
#  NAME OF MAIN SECTION (IN ALL CAPS)
# ========================================================================== 


# Name of sub-section (in sentence case)
# --------------------------------------------------------------------------
# @owner        Name, School or unit <email@st-andrews.ac.uk>
# @description  Reason for creating this 
# @since        1.2.0
# @added        2016-08-08
# @review       2016-11-08

Redirect 301 /path/to/old/url/1 https://www.st-andrews.ac.uk/path/to/new/url/1
Redirect 301 /path/to/old/url/2 https://www.st-andrews.ac.uk/path/to/new/url/2
Redirect 301 /path/to/old/url/3 https://www.st-andrews.ac.uk/path/to/new/url/3
```

* The main section title MUST be in all capitals, and indented by one space.
* There MUST be four blank lines before the main section name.
* The sub-section title MUST be in sentence case.
* There MUST be two blank lines before the sub-section name. 
* Horizontal rules (`=` and `-`) MUST contain 75 symbols.

Each block MUST contain the following information:

**Name of sub-section**
This should be a meaningful name to describe the block, e.g. School of Economics website redesign.

**@owner**
The name, and school or unit, and email address of the person who requested the redirects to be created. This allows us to contact them in the future should we have any questions.

**@description**
General description about the reason why the redirect was created, e.g. Created because an email went out to alumni with an outdated URL.

It can be helpful if you record here whether this redirect is linked to an email or print campaign.

If you find an answer online (for example, on Stack Overflow, or a blog) then you SHOULD add the link to the description so future developers know what's up.

**@since**
Which version of the .htaccess this was added; the version number can be found in the file title. This can help us track when changes were made.

**@added**
The date that these directives were added to the .htaccess file. This MUST be in ISO date format, i.e. `yyyy-mm-dd`.

**@review**
The date that these directives should be reviewed and potentially removed from the .htaccess file. This MUST be in ISO date format, i.e. `yyyy-mm-dd`.

By default this should be 3 months after the date they were added, with a maximum of 6 months. If this is longer than 6 months then these redirects MUST be put into the main server config. Send them to the IT systems team via Unidesk (<itservicedesk@st-andres.ac.uk>)

Before adding redirects you MUST ask the owner how long they should remain in place, for example, if this is linked to a specific email or print campaign.

If this section does not expire then mark it as permanent.




---

## 7. Adding new redirects

Assuming that the redirect cascade allows it, new rules SHOULD always be added beneath previous rules within a section.

This means that the oldest redirect rules will appear at the top of each section, which makes it easier to see which rules need to be reviewed/removed next.




---

## 8. Example file

```
# ==========================================================================
#  LIVE SERVER <www.st-andrews.ac.uk>
# ========================================================================== 
# Primary .htaccess file for the production server (live). Version 
# controlled in Bitbucket (Git), published via T4.
#
#     TABLE OF CONTENTS
#
#     1. Error messages
#     2. Quick-fix redirects
#     3. Restructured sites redirects
#     4. Rewrite engine rules
#
# @version     1.2.0  2016-08-08
# @owner       Digital communications team <itservicedesk@st-andrews.ac.uk>




# ==========================================================================
#  1. ERROR MESSAGES
# ========================================================================== 


# Apache custom error responses
# --------------------------------------------------------------------------
# @owner        Digital communications team <itservicedesk@st-andrews.ac.uk>
# @description  Customised error response documents for 4xxx status. See
                https://httpd.apache.org/docs/2.4/custom-error.html
# @since        1.0.0
# @added        2015-01-01
# @review       Permanent

ErrorDocument 401 /path/to/error/document/401/
ErrorDocument 403 /path/to/error/document/403/
ErrorDocument 404 /path/to/error/document/404/




# ==========================================================================
#  2. QUICK-FIX REDIRECTS
# ========================================================================== 


# Alumni email URL fix
# --------------------------------------------------------------------------
# @owner        Jane Doe, Development <email@st-andrews.ac.uk>
# @description  Email sent out with wrong URL. This redirects to the correct
                one. Email campaign is expected to last 2 months, but we will
                keep this live for three.
# @since        1.1.0
# @added        2016-05-31
# @review       2016-08-31

Redirect 301 /path/to/old/url/1 https://www.st-andrews.ac.uk/path/to/new/url/1




# ==========================================================================
#  3. RESTRUCTURED SITES REDIRECTS
# ========================================================================== 


# School of Economics redesign
# --------------------------------------------------------------------------
# @owner        Adam Smith, School of Economics <email@st-andrews.ac.uk>
# @description  Moved from secondary account to T4. These redirects will 
                ensure that old URLs still work while bookmarks and search
                engine results are updated.
# @since        1.1.0
# @added        2016-06-08
# @review       2016-09-08

Redirect 301 /path/to/old/url/1 https://www.st-andrews.ac.uk/path/to/new/url/1
Redirect 301 /path/to/old/url/2 https://www.st-andrews.ac.uk/path/to/new/url/2
Redirect 301 /path/to/old/url/3 https://www.st-andrews.ac.uk/path/to/new/url/3


# School of English redesign
# --------------------------------------------------------------------------
# @owner        Robert Burns, School of English <email@st-andrews.ac.uk>
# @description  Significant restructure of IA. This will catch old URLs whil
                bookmarks and search engine results are updated.
# @since        1.2.0
# @added        2016-08-08
# @review       2016-11-08

Redirect 301 /path/to/old/url/1 https://www.st-andrews.ac.uk/path/to/new/url/1
Redirect 301 /path/to/old/url/2 https://www.st-andrews.ac.uk/path/to/new/url/2
Redirect 301 /path/to/old/url/3 https://www.st-andrews.ac.uk/path/to/new/url/3




# ==========================================================================
#  4. REWRITE ENGINE RULES
# ========================================================================== 


# Rewrite engine rules
# --------------------------------------------------------------------------
# @owner        Systems team, IT Services <itservicedesk@st-andrews.ac.uk>
# @description  mod_rewrite rules
# @since        1.0.0
# @added        2007-01-01
# @review       Permanent

RewriteEngine on

RewriteCond %{HTTP_HOST} subdomain.st-andrews.ac.uk [NC]
RewriteRule ^.*$ https://www.st-andrews.ac.uk/subdomain/ [R] [L]

RewriteCond %{HTTP_HOST} subdomain [NC]
RewriteRule ^.*$ https://www.st-andrews.ac.uk/subdomain/ [R] [L]

RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)/$ /$1 [L,R=301]
```
