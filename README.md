EDown - EDoc Extension for generating Github-flavored Markdown
==============================================================

<ulf.wiger@erlang-solutions.com>

Status:
------
More-or-less readable Markdown can be generated.
A doclet needs to be written that also creates 
a markdown-based index and overview. Currently, the 
edoc_doclet creates an index.html and overview.html,
which do not point to the .md files.

To generate markdown edoc, run:

`edoc:application(App, [{doclet, edown_doclet} | OtherOpts]).`

The `edown_xmerl` module is used as an xmerl export module.
It converts xmerl's "simple xml" to Markdown syntax. Note that
GH-flavored Markdown allows HTML markup (at least common tags),
but doesn't expand markdown markup inside HTML markup, so the 
`edown_xmerl` module has to know the context in which it operates.

NOTE
====
EDoc provides a plugin structure, so that one may specify own 
layout modules, export modules, and doclets. However, there is 
some overlap esp. between the layout and doclet modules, and 
several functions are expected to produce files on their own.
This causes a problem for EDown, since it cannot handle frames.
Instead, it would probably like to create one overview file with
different sections. It would have been better to have a framework
where some plugin functions identify the different files to be 
written, and the outline of each, other plugins convert to suitable
content representation (e.g. HTML or Markdown), and EDoc then 
writes the files necessary.

For now, EDown focuses on producing reasonable Markdown, rather
than complying fully with the plugin framework. That is, the 
edown_doclet module will not go out of its way to function together
with any other layout module than edown_layout, and vice versa.

markedoc
========

The sed script bin/markedoc works in the opposite direction and converts your README.md to an EDoc file. 

See bin/MARKEDOC-README.md.

**FreeBSD, Mac OS X**
	$ sed -E -f markedoc.sed <markdown file> > <edoc file>

**Linux**
	$ sed -r -f markedoc.sed <markdown file> > <edoc file>


