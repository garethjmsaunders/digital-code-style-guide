# Sublime Text standards guide

<!-- MarkdownTOC -->

- [1. Version](#1-version)
- [2. Package Control](#2-package-control)
	- [Batch install packages](#batch-install-packages)
	- [Package Control.sublime-settings file](#package-controlsublime-settings-file)
	- [Package descriptions](#package-descriptions)
- [3. User Preferences](#3-user-preferences)

<!-- /MarkdownTOC -->




## 1. Version

We recommend using **Sublime Text 3 beta**.

All the plugins work with Sublime Text 2 so it's up to user preference.




## 2. Package Control

Plugins for Sublime Text are called 'packages'.

Perhaps the most useful plugin we use is [Package Control](https://packagecontrol.io/). This makes it very simple to find, install and keep packages (plugins) up to date.

Install via the console (`Ctrl + '` or `View > Show Console`). Copy and paste the appropriate [install script](https://packagecontrol.io/installation) then press Enter.

Packages can be searched via `Preferences > Browse Packages...`.


### Batch install packages

To speed up getting started, when you first install Sublime Text you can batch import all the plugins required.

First make sure that Package Control is installed, then create a JSON file called `Package Control.sublime-settings` and save it to the following location:

**Windows**
`C:\Users\[YOUR_USERNAME\]\AppData\Roaming\Sublime Text 3\Packages\User`


**Mac OS X**
`PATH`

Or you can access this file from Sublime Text in `Preferences > Package Settings > Package Control > Settings - User`.


### Package Control.sublime-settings file

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


### Package descriptions

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




## 3. User Preferences

The following user preferences settings, found at `Preferences > Settings — User`, offers a very usable coding environment:

```
{
	"always_show_minimap_viewport": true,
	"bold_folder_labels": true,
	"caret_extra_bottom": 1,
	"caret_extra_top": 1,
	"caret_extra_width": 1,
	"caret_style": "phase",
	"default_encoding": "UTF-8",
	"default_line_ending": "LF",
	"dictionary": "Packages/Language - English/en_GB.dic",
	"draw_white_space": "selection",
	"fade_fold_buttons": false,
	"font_size": 20,
	"highlight_line": true,
	"highlight_modified_tabs": true,
	"hot_exit": true,
	"ignored_packages":
	[
		"Vintage"
	],
	"indent_guide_options":
	[
		"draw_normal",
		"draw_active"
	],
	"line_padding_bottom": 1,
	"line_padding_top": 1,
	"remember_open_files": true,
	"rulers":
	[
		80
	],
	"save_on_focus_lost": true,
	"show_encoding": true,
	"show_line_endings": true,
	"tab_size": 4,
	"translate_tabs_to_spaces": true,
	"trim_trailing_white_space_on_save": true,
	"wordwrap": true
}
```
