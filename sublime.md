# Sublime Text standards guide

<!-- MarkdownTOC -->

- [1. General](#1-general)
	- [Version](#version)
	- [Package Control](#package-control)
- [2. Batch install packages](#2-batch-install-packages)
	- [Package Control.sublime-settings](#package-controlsublime-settings)
- [3. Package descriptions](#3-package-descriptions)

<!-- /MarkdownTOC -->




## 1. General


### Version

We recommend using Sublime Text 3, but all the plugins work with Sublime Text 2 so it's up to user preference.


### Package Control

Plugins for Sublime Text are called 'packages'.

Perhaps the most useful plugin we use is [Package Control](https://packagecontrol.io/). This makes it very simple to find, install and keep packages (plugins) up to date.

Install via the console (`Ctrl + '` or `View > Show Console`). Copy and paste the appropriate [install script](https://packagecontrol.io/installation) then press Enter.

Packages can be searched via `Preferences > Browse Packages...`.




## 2. Batch install packages

To speed up getting started, when you first install Sublime Text you can batch import all the plugins required.

First make sure that Package Control is installed, then create a JSON file called `Package Control.sublime-settings` and save it to the following location:

**Windows**
`C:\Users\[YOUR_USERNAME\]\AppData\Roaming\Sublime Text 3\Packages\User`


**Mac OS X**
`PATH`

Or you can access this file from Sublime Text in `Preferences > Package Settings > Package Control > Settings - User`.


### Package Control.sublime-settings

You may use this curated JSON file of recommended Sublime Text plugins.

Simply copy and paste it into your `Package Control.sublime-settings` file, remove any that look redundant (e.g. if you don't do any WordPress development), save it to the correct location, then restart Sublime Text.

	{
		"bootstrapped": true,
		"in_process_packages":
		[],
		"installed_packages":
		[
			"Alignment",
			"Autoprefixer",
			"Bootstrap 3 Snippets",
			"BracketHighlighter",
			"Color Highlighter",
			"CSScomb",
			"DevDocs",
			"Emmet",
			"GitGutter",
			"jQuery",
			"JSHint Gutter",
			"Markdown Preview",
			"MarkdownEditing",
			"MarkdownTOC",
			"Package Control",
			"Placeholders",
			"Sass",
			"SideBarEnhancements",
			"SyncedSideBar",
			"Theme - Minimal",
			"TodoReview",
			"Tomorrow Color Schemes",
			"View In Browser",
			"WordPress",
			"WordPress Developer Resources",
			"WordPress Generate Salts",
		]
	}




## 3. Package descriptions

* [Alignment](https://packagecontrol.io/packages/Alignment) - A key-binding for aligning multi-line and multiple selections.
* [Autoprefixer](https://packagecontrol.io/packages/Autoprefixer) - This auto-add's Vendor prefixes.
* [Bootstrap 3 Snippets](https://packagecontrol.io/packages/Bootstrap%203%20Snippets) - Able to autocomplete bootstrap 3 plugins.
* [BracketHighlighter](https://packagecontrol.io/packages/BracketHighlighter) - Highlights the content between [ ], ( ), { }, " ", ' '
* [CSScomb](https://packagecontrol.io/packages/CSScomb) - Coding style formatter for CSS.
* [DevDocs](https://packagecontrol.io/packages/DevDocs) - allowing you to easily search the DevDocs documentation.
* [Emmet](https://packagecontrol.io/packages/Emmet) - Emmet has many options for autocompleting code or programmatically generating code.
* [GitGutter](https://packagecontrol.io/packages/GitGutter) - A plugin to show an icon in the gutter area indicating whether a line has been inserted, modified or deleted.
* [jQuery](https://packagecontrol.io/packages/jQuery) - This is a Sublime Text bundle to help with jQuery functions. It has syntax highlighting and almost all of the jquery methods as snippets.
* [JSHint Gutter](https://packagecontrol.io/packages/JSHint%20Gutter) - A plugin allowing you to check your JavaScript code for nasty errors, coding conventions and other goodies.
* [Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview) - Preview and build your markdown files quickly in your web browser from sublime text 2/3.
* [MarkdownEditing](https://packagecontrol.io/packages/MarkdownEditing) - Markdown plugin for Sublime Text. Provides a decent Markdown color scheme, with syntax highlighting.
* [MarkdownTOC](https://packagecontrol.io/packages/MarkdownTOC) - This plugin search headings in document and insert TOC (Table Of Contents) to it.
* [Placeholders](https://packagecontrol.io/packages/Placeholders) - This package contains basic HTML placeholder content for Sublime Text e.g. lorem ipsum text, forms, images etc.
* [Sass](https://packagecontrol.io/packages/Sass) - This add-on adds syntax highlighting and tab/code completion for Sass and SCSS files.
* [SideBarEnhancements](https://packagecontrol.io/packages/SideBarEnhancements) - Provides enhancements to the operations on Sidebar of Files and Folders for Sublime Text.
* [SyncedSideBar](https://packagecontrol.io/packages/SyncedSideBar) - Plugin to sync project sidebar (folder view) with currently active file.
* [TodoReview](https://packagecontrol.io/packages/TodoReview) - A SublimeText plugin for reviewing todo (and other) comments within your code.
* [Tomorrow Color Schemes](https://packagecontrol.io/packages/Tomorrow%20Color%20Schemes) - Tomorrow Color Schemes for SublimeText.
* [View In Browser](https://packagecontrol.io/packages/View%20In%20Browser) - Open the contents of your current view/tab in a web browser.
* [WordPress](https://packagecontrol.io/packages/WordPress) - Sublime Text WordPress Package is a collection of WordPress snippets and autocompletions for Sublime Text.
* [WordPress Developer Resources](https://packagecontrol.io/packages/WordPress%20Developer%20Resources) - Sublime Text 2/3 Plugin to search the new Wordpress Developer Resources (developer.wordpress.org).
* [WordPress Generate Salts](https://packagecontrol.io/packages/WordPress%20Generate%20Salts) - A Sublime Text 3 Plugin for generating new WordPress salt keys.
