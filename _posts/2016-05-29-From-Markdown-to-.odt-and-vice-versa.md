---
layout: post
title: From Markdown to .odt and vice-versa
category: Markdown .odt
---



I wanto to convert complex documents for Markdown so they can be used
here **to write this blog**. There are lots of ways, but i choose the following
one.

We need to have LibreOffice, pandoc, and a text editor.

The process is this.

1.  Create a .odt file in LibreOffice, using the following. The first
     three items in the list *must* be applied using styles, i.e. from
     "Styles and Formatting" &gt; "Paragraph Styles":
 
     -   Headings—*not* Titles,
     -   Preformatted Text (only works for block elements),
     -   Quotations,
     -   ordered and unordered lists,
     -   hyperlinks,
     -   italics and bold,
     -   footnotes.
 
 
2. Run   **`pandoc -s file.odt -t markdown -o file.md`**
3. Edit the markdown **file.md** and correct every thing that seems wrong!!!
     There is some markdown editors, i like to use [MarkdownPad2].




Test:

Here is a heading
=================

Here is some text. *Here is some italics*. **Here is some bold**. [Here
is a link4](http://suttacentral.net/). Here is a footnote.[^1]

Here is some text. *Here is some italics*. **Here is some bold**. [Here
is a link4](http://suttacentral.net/). Here is a footnote.[^2]

Here is some text. *Here is some italics*. **Here is some bold**. [Here
is a link4](http://suttacentral.net/). Here is a footnote.[^3]

Here is a subheading
--------------------

### Here is a subsubheading

#### Here is a subsubsubheading

-   Here is an unordered list.
-   Here is an unordered list.
-   Here is an unordered list.

Here is some text. *Here is some italics*. **Here is some bold**. [Here
is a link4](http://suttacentral.net/). Here is a footnote.[^4]

1.  Here is an ordered list.
2.  Here is an ordered list.
3.  Here is an ordered list.

*Here is some monospace text.*

> Here is a blockquote. Here is a blockquote.


## Pandoc

Pandoc is a general markup converter that can convert from one markup
format to another. It can read [Markdown], [CommonMark], [PHP Markdown
Extra], [GitHub-Flavored Markdown], and (subsets of) [Textile],
[reStructuredText], [HTML], [LaTeX]),[MediaWiki markup],
[TWiki markup], [Haddock markup], [OPML], [Emacs Org
mode], [DocBook], [txt2tags]), [EPUB], [ODT] and [Word
docx];

and it can write plain text, [Markdown], [CommonMark], [PHP Markdown
Extra], [GitHub-Flavored Markdown], [reStructuredText], [XHTML],
[HTML5], [LaTeX] (including [*beamer*] slide shows),
[ConTeXt], [RTF], [OPML], [DocBook], [OpenDocument], [ODT], [Word docx],
[GNU Texinfo], [MediaWiki markup], [DokuWiki markup]), [Haddock markup],
[EPUB] (v2 or v3), [FictionBook2], [Textile], [groff man] pages, [Emacs Org mode], [AsciiDoc], [InDesign ICML], [TEI Simple], and [Slidy], [Slideous],
[DZSlides], [reveal.js] or [S5] HTML slide shows. It can also
produce [PDF] output on systems where LaTeX, ConTeXt, or *wkhtmltopdf* is installed.

<http://pandoc.org/README.html>

### Using Pandoc ###

By default, pandoc produces a document fragment, not a standalone
document with a proper header and footer. To produce a standalone
document, use the **-s** or ***--standalone*** flag:


To convert from markdown to Word docx:

```ruby
pandoc -s -S input.md -o output.docx
```

To convert from Word docx to markdown:

```ruby
pandoc -f docx -t markdown foo.docx -o foo.markdown
```

To convert markdown to PDF:

```ruby
pandoc input.md -o output.pdf
```

**To convert from .odt to markdown:**

```ruby
pandoc -s file.odt -t markdown -o file.md
```

**To convert from markdown to .ODT (OpenDocument Text):**

```ruby
pandoc input.md -o output.odt
```


See: *[*http://pandoc.org/demos.html*](http://pandoc.org/demos.html)



### References   


- <https://writers.stackexchange.com/questions/9056/from-markdown-to-odt-and-vice-versa-a-possible->      
- [distraction-free-writing-workfl](https://writers.stackexchange.com/questions/9056/from-markdown-to-odt-and-vice-versa-a-possible-distraction-free-writing-workfl)   
- <http://extensions.libreoffice.org/extension-center/texmaths-1>   
- <http://extensions.libreoffice.org/extension-center/writer2latex-1>   
- <https://discourse.suttacentral.net/t/converting-from-word-processor-to-markdown/21>   
- [Markdown instead of Word Processors](https://www.garron.me/en/blog/switching-to-markdown-no-word-processors-anymore.html)   



[MarkdownPad2]: http://markdownpad.com/
[Markdown]: http://daringfireball.net/projects/markdown/
[CommonMark]: (http://commonmark.org/
[PHP Markdown Extra]: https://michelf.ca/projects/php-markdown/extra/
[GitHub-Flavored Markdown]: https://help.github.com/articles/github-flavored-markdown/
[Textile]: http://redcloth.org/textile
[reStructuredText]: http://docutils.sourceforge.net/docs/ref/rst/introduction.html
[HTML]: http://www.w3.org/html/
[LaTeX]: http://latex-project.org/
[MediaWiki markup]: https://www.mediawiki.org/wiki/Help:Formatting
[TWiki markup]: http://twiki.org/cgi-bin/view/TWiki/TextFormattingRules
[Haddock markup]: https://www.haskell.org/haddock/doc/html/ch03s08.html
[OPML]: http://dev.opml.org/spec2.html
[Emacs Org mode]: http://orgmode.org/
[DocBook]: http://docbook.org/
[txt2tags]: http://txt2tags.org/
[EPUB]: http://idpf.org/epub
[ODT]: http://en.wikipedia.org/wiki/OpenDocument
[Word docx]: http://www.microsoft.com/interop/openup/openxml/default.aspx
[Markdown]: http://daringfireball.net/projects/markdown/
[CommonMark]: http://commonmark.org/
[PHP Markdown Extra]: https://michelf.ca/projects/php-markdown/extra/
[GitHub-Flavored Markdown]: https://help.github.com/articles/github-flavored-markdown/
[reStructuredText]: http://docutils.sourceforge.net/docs/ref/rst/introduction.html
[XHTML]: http://www.w3.org/TR/xhtml1/
[HTML5]: http://www.w3.org/TR/html5/
[LaTeX]: http://latex-project.org/
[*beamer*]: https://ctan.org/pkg/beamer
[ConTeXt]: http://contextgarden.net/
[RTF]: http://en.wikipedia.org/wiki/Rich_Text_Format
[OPML]: http://dev.opml.org/spec2.html
[DocBook]: http://docbook.org/
[OpenDocument]: http://opendocument.xml.org/
[ODT]: http://en.wikipedia.org/wiki/OpenDocument
[Word docx]: http://www.microsoft.com/interop/openup/openxml/default.aspx
[GNU Texinfo]: http://www.gnu.org/software/texinfo/
[MediaWiki markup]: https://www.mediawiki.org/wiki/Help:Formatting
[DokuWiki markup]: https://www.dokuwiki.org/dokuwiki
[Haddock markup]: https://www.haskell.org/haddock/doc/html/ch03s08.html
[EPUB]: http://idpf.org/epub
[FictionBook2]: http://www.fictionbook.org/index.php/Eng:XML_Schema_Fictionbook_2.1
[Textile]: http://redcloth.org/textile
[groff man]: http://developer.apple.com/DOCUMENTATION/Darwin/Reference/ManPages/man7/groff_man.7.html
[Emacs Org mode]: http://orgmode.org/
[AsciiDoc]: http://www.methods.co.nz/asciidoc/
[InDesign ICML]: https://www.adobe.com/content/dam/Adobe/en/devnet/indesign/cs55-docs/IDML/idml-specification.pdf
[TEI Simple]: https://github.com/TEIC/TEI-Simple
[Slidy]: http://www.w3.org/Talks/Tools/Slidy/
[Slideous]: http://goessner.net/articles/slideous/
[DZSlides]: http://paulrouget.com/dzslides/
[reveal.js]: http://lab.hakim.se/reveal-js/
[S5]: http://meyerweb.com/eric/tools/s5/
[PDF]: https://www.adobe.com/pdf/


[^1]: Here is a footnote.
[^2]: Here is a footnote.
[^3]: Here is a footnote.
[^4]: Here is a footnote.