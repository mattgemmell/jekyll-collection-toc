# Collection Table of Contents - an include for Jekyll

By [Matt Gemmell](https://mattgemmell.scot/) - https://mattgemmell.scot/

Jekyll include which generates a hierarchical table of contents list for a given collection.

(This file is for use with the [Jekyll static web site generator](https://jekyllrb.com), which is written in Ruby, and is free.)

This include assumes you have a Jekyll collection whose documents are stored hierarchically in the filesystem, and whose order is specified in your site's `_config.yml` file.

When invoked, this include will generate a simple HTML list (`OL` or `UL`) reflecting the hierarchical nature of the ordered documents, with each entry being the relevant document's title, linked to that document's URL. If the current page is one of the entries, that entry will not be linked. The list itself has CSS class "`toc`", and will be an ordered list (`OL`) by default. There is an optional parameter to generate an `UL`-type list instead.

## Installation

Place the include into your Jekyll site's `_includes` folder.

## Usage

`{% include collection_toc.html collection_name="your-collection-name-here" %}`

## Notes

1. The "`collection_name`" parameter is the name of the collection as a string; it is NOT a collection object, array of collection entries, or anything else.

2. There's an optional "`unordered`" parameter, which if specified and set to "`true`" will cause the HTML list to be of the unordered (`UL`) type. The actual ordering of the list's entries is unaffected by this setting; it only affects the resulting HTML markup. Typically, browsers render an ordered list with ascending numbered items, and render an unordered list as bulleted items, but CSS may of course change this behaviour.	

3. This include assumes a certain reasonable rationale regarding your collection's files on disk and their ordering as specified in the `_config.yml` file, as follows. When a subsequent entry in the order is at a deeper level of nesting in the filesystem than the prior entry, the subsequent entry is assumed to be the child of the prior one. An example order is below.

		- crew.markdown
		- red-shirts.markdown
		- red-shirts/picard.markdown
		- red-shirts/riker.markdown
		- yellow-shirts.markdown
		- yellow-shirts/data.markdown
		- yellow-shirts/laforge.markdown
		- yellow-shirts/worf.markdown
		- blue-shirts.markdown
		- blue-shirts/troi.markdown
		- blue-shirts/crusher.markdown
		
	This would generate an HTML list which, when rendered in a browser, visually resembles the plain-text equivalent list below. The filenames are assumed to correspond to the file's titles (in their YAML front matter) in the conventional manner.
		
		1. Crew
		2. Red Shirts
			1. Picard
			2. Riker
		3. Yellow Shirts
			1. Data
			2. LaForge
			3. Worf
		4. Blue Shirts
			1. Troi
			2. Crusher

4. There's also an optional "`collated`" parameter, which if specified and set to "`true`" will cause the links to be to anchors on the same page, rather than to each document's own URL. The anchors will be the slugified form of the corresponding document's own (root-relative) URL, i.e. `#{{ doc.url | slugify }}` in Liquid. This is useful for collated versions of a collection, where a single page contains the content of all documents within a collection, for example as a convenience for printing or saving. See the "`example-collated-page.markdown`" file in this repository for an example of a Jekyll page which will create a collated view of a given collection, rewriting any inter-document links to still work properly.

## Why this is useful

Collections have the handy property of having an order, such that each page can have a link to the previous and/or next entries. Jekyll allows storing the corresponding content files hierarchically in the filesystem, and hierarchy often has semantic significance, such as for sub-sections or topics.

This very simple include allows generating a linked Table of Contents which reflects the implicit hierarchical nature of a collection's files on disk, exposing those semantics, without sacrificing the convenience of having a conceptually linear overall order. This is especially useful for lengthy guides, reviews, tutorials, theses, documentation, and so forth.
