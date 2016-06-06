---
layout: post
title:  "GitHub Pages now faster and simpler!"
categories: jekyll
---

### Updates to Markdown filter and syntax highlighters

Github recently adopted Kramdown as their only Markdown processor, which
will go into effect after May 1.

And instead of Pygments, Rouge will be now the only syntax highlighter
supported by Github Pages. Github announced these changes in a recent
[blog
post](https://github.com/blog/2100-github-pages-now-faster-and-simpler-with-jekyll-3-0):

GitHub Pages now *only* supports
[Rouge](https://github.com/jneen/rouge), a pure-Ruby syntax highlighter,
meaning you no longer need to install Python and Pygments to preview
your site locally. If you were previously using Pygments for
highlighting, the two libraries are feature compatible, so we'll swap
Rouge in for Pygments when we build your site, to ensure a seamless
transition.

Traditionally, highlighting in Jekyll has been implemented via [the
](http://jekyllrb.com/docs/templates/#code-snippet-highlighting)[ **\{ % highlight % }**  ](http://jekyllrb.com/docs/templates/#code-snippet-highlighting)[
Liquid tag](http://jekyllrb.com/docs/templates/#code-snippet-highlighting),
forcing you to leave a pure-Markdown experience. With kramdown and Rouge
as the new defaults, syntax highlighting on GitHub Pages should work
like you'd expect it to work anywhere else on GitHub, with native
support for [backtick-style fenced code
blocks](https://help.github.com/articles/creating-and-highlighting-code-blocks/)
right within the Markdown.

> You can create fenced code blocks by placing triple backticks *\`\`\`*
> before and after the code block.

How to make the updates to use Kramdown and Rouge
--------------------------------------------------------------------------

If you were using redcarpet and Pygments, and you want to switch to
Kramdown and Rouge, you need to make an update in your configuration
file. For example, if you previously had this:

> *highlighter: pygments*   
> *markdown: redcarpet*    
> *redcarpet:*    
> > *extensions: \["no\_intra\_emphasis", "fenced\_code\_blocks", "tables", "with\_toc\_data"\]*

Just change it to this:

> *highlighter: rouge*   
> *markdown: kramdown*    
> *kramdown:*   
>> *input: GFM*   
> *auto\_ids: true*     
> *syntax\_highlighter: rouge*

Make sure you specify the Github Flavored Markdown parser by adding
*input: **GFM***. Otherwise backticks won’t be processed.

### Test

*\{ % highlight css % }*   
  body {   
   margin: 0;   
  }   
*\{ % endhighlight % }*   
 
Output:
{% highlight css %}   
  body {   
   margin: 0;   
  }    
{% endhighlight %}    
 
 


*\`\`\`css*   
*body {*   
* margin: 0;*   
*}*   
*\`\`\`*
 
Output:

```css
body {      
 margin: 0;      
}
```

### References    
- <http://idratherbewriting.com/2016/02/21/bug-with-kramdown-and-rouge-with-github-pages/#updates-to-markdown-filter-and-syntax-highlighters>
- <https://github.com/blog/2100-github-pages-now-faster-and-simpler-with-jekyll-3-0>
- <https://help.github.com/articles/creating-and-highlighting-code-blocks/>
- <https://github.com/pawelgrzybek/pawelgrzybek.github.io>
