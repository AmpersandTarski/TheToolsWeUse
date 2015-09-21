# Test page for math in markdown
This page is [a copy from another page on github](https://github.com/cben/mathdown/wiki/math-in-markdown). It is there only to get an idea what we could do with math in our documentation. Please feel free to delete anything in this page that doesn't add to that purpose. 

# Survey of syntaxes for math in markdown #

> TODO: This is becoming useful as a cheatsheet => rearrange this page to be user-oriented before being developer-oriented.

> TODO: [notepag.es](https://github.com/fivesixty/notepages) if it's up again; [Discourse plugin](https://meta.discourse.org/t/mathjax-plugin-supports-math-notation-using-latex/12826/25); **[Madoko](http://research.microsoft.com/en-us/um/people/daan/madoko/doc/reference.html#sec-overview-of-madoko) - great new entrant**!

It'd be nice if everybody could agree on the same syntax(es) to denote math fragments in Markdown; alas, as every extension to Markdown, it's a mess :-(
If you're adding math support to your markdown tool, I have one plea: please consider supporting [a subset of] standard LaTeX delimiters before inventing your own.  Also see [discussion on CommonMark](http://talk.commonmark.org/t/mathjax-extension-for-latex-equations/698/4).

I'm taking for granted that the *content* of the math fragments is LaTeX syntax.  Arguably syntaxes like AsciiMath (MMD used to do this), are a better match for Markdown's philosophy, but most people who care about non-trivial math support already know [some] LaTeX syntax (which is why MMD 3 switched to LaTeX).

  * [CoffeeTeX](https://github.com/kasperpeulen/CoffeeTeX) is an intriguing new option, based on a lot of unicode.  It's a superset of latex math, so could be used harmlessly(?) with these proposals.  TODO: take a deeper look.

Multiple syntaxes exist:

 1. dollars: `$inline$` and `$$display$$`.
    Pro: same as LaTeX (`$$` is deprecated TeX syntax but never mind), easiest to write.
    Con: prone to false positives like `$20` — confusing to users who don't write math.
    There are frequently restrictions on when this is recognized.

 2. single backslash: `\(inline\)` and  `\[display\]`
    Pro: same as LaTeX.
    Con: interferes with ability to escape parens and brackets e.g. `\[this is not]\(a link)`

 3. double backslash: `\\(inline\\)` and  `\\[display\\]`
    Pro: doesn't interfere with escaping parens and brackets (introduced by MultiMarkdown for this reason).
    Con: non-standard, ugly.

 4. Literal-based syntaxes.  Their upside is they are interpreted as literal text by engines that don't understand the syntax.  This avoids runaway misformatting due to `_` or `*`.  I'd say this backward compatibility is not that important for *converters* (if you have a math-rich document, you'll not be happy with a converter that merely doesn't choke on it, you want the math to actually render) but a considerable win for *editors*.

 5. naked latex environment `\begin{foo}...\end{foo}`.
    Pro: simple way to include (almost) arbitrary raw latex.

 6. standalone sub/superscript outside math — unique to [Pandoc](http://johnmacfarlane.net/pandoc/README.html#superscripts-and-subscripts) AFAIK.  Not worth the a separate syntax IMHO.

TODO: arrange this by goals, not syntaxes.
TODO: discuss macros.

## Convertor Engines ##

### reminder: LaTeX
Just a reminder: LaTeX itself supports `$inline$`, `\(inline\)`, `$$display$$` ([deprecated](https://tex.stackexchange.com/questions/503/why-is-preferable-to)), `\[display\]`.
Also some environments enter math mode e.g. `\begin{equation}...\end{equation}`.

Escaping these is possible (with occasional complications) via `\$` and [`\backslash` / `\textbackslash`](http://tex.stackexchange.com/q/9363).

Macro definition appear outside math mode but usually affect math.

### [MultiMarkdown](http://fletcher.github.io/MultiMarkdown-4/math.html)
MultiMarkdown 2 used ASCIIMathML syntax within (only?) double backslashes.

MultiMarkdown 3 and 4 switched to LaTeX/MathJax syntax, within double backslashes (`\\(inline\\)`, 
`\\[ display \\]`) as well as dollars ( `$inline$` , `$$display$$`).
For `$inline$`, in order to be correctly parsed as math, there must not be any space between the $ and the actual math on the inside of the delimiter, and there must be space on the outside.

It also support Pandoc-style superscript (`y^(a+b)^`) and subscript (`x~y,z~`).  The trailing ^ or ~ delimiter is optional in simple cases.

### [Pandoc](http://johnmacfarlane.net/pandoc/README.html#math)
By default dollars; optional support for single and/or double backslashes.
`$...$` constrained by heuristic: [opening dollar not followed by space, closing not followed by number](https://groups.google.com/forum/#!msg/pandoc-discuss/KiyMZn1wFHg/lPUzI8U-KukJ).

Smart enough to parse nested $y = x^2 \hbox{ when $x > 2$}$ as single formula.

Recognizes `\begin{foo}...\end{foo}` and `\foo{...}` without any extra delimiters.
[Supports macros](http://johnmacfarlane.net/pandoc/README.html#latex-macros) — recognizes `\def...`, `\newcommand...` without any extra delimiters, pre-expands macros for non-latex output formats.

Also supports [free-standing sub/superscripts](http://johnmacfarlane.net/pandoc/README.html#superscripts-and-subscripts): `H~2~O is a liquid.  2^10^ is 1024.`

### [Scholdoc](http://scholarlymarkdown.com/Scholarly-Markdown-Guide.html#math) fork of pandoc

[Scholdoc](http://scholdoc.scholarlymarkdown.com/)/[ScholarlyMarkdown](http://scholarlymarkdown.com/) is notable as the most ambitious effort for science-friendly markdown, adding not just math but also numbered references, figures and other stuff.  Note: it's an experiment in progress, ["a stop-gap measure to quickly test out ideas"](https://news.ycombinator.com/item?id=9204352).

As for math, it supports same dollar syntaxes as Pandoc, as well as literal-based syntaxes:

  * *Exactly 2* backticks for inline math: ``` ``a+b=c`` ```.  Recall that markdown allows any number of surrounding backticks, to delimit literals containing lesser sequence(s) of backticks.  It's almost backward compatible (usage of 2 backticks is quite rare), and you still can use 3 or more to write non-math literals containing backticks.

    The ScholarlyMarkdown use of literal inline delimiters allows for math expressions to prepend numbers, such as ``\approx``5 meters. In contrast, $\approx$5 meters will fail to be recognized as math (as in Pandoc).

  * Fenced literal of `math` "language" for display blocks, also supporting optional label which [can be refernced](http://scholarlymarkdown.com/Scholarly-Markdown-Guide.html#numbered-internal-references):

        ```math #yourmathlabel
        a + b = c
        ```

        Can be referenced with [#yourmathlabel] — rendered as 1, or (#yourmathlabel) — rendered as (1).

      * Display math is automatically wraped in `gathered` [`aligned`] environment if it contains `\\` (and `&`) symbols.  If you want to disable this behavior, use the `math_plain` "language".

  * Fenced block of `math_def` "language" for macro definitions (and I presume other stuff legal in latex preamble?) — whereever it appears in the markdown source, it will be parsed first in the output (nice e.g. if you want to use the macro in the document's title):

        ```math_def
        \newcommand{\foo}{Foo}
        ```

### [kramdown](http://kramdown.gettalong.org/syntax.html#math-blocks)
Rather clever single syntax: `$$ ... $$` is display math if alone in a paragraph, inline if on same line with other content; `$$\begin{foo}...\end{foo}$$` outputs raw `\begin{foo}...\end{foo}` without wrapping in math delimiters.

**Criticism:** https://github.com/GitbookIO/kramed/issues/3
This syntax has no way to express display math in middle of paragragh:
> That sounds contradictory, but due to the fact that it is accepted to treat mathematics as part of sentences, it totally makes sense for mathematical equations, even display/block mathematics, to be inside a paragraph.

### [kramed](https://github.com/GitbookIO/kramed/blob/master/test/tests/math.text)
Fork of marked.
Same as kramdown: dual use of `$$...$$` for inline and display.

### [supermarked](https://github.com/ForbesLindesay/supermarked#katex)
Another fork of marked.
Dollars *within literals*: `` `$inline$`, `$$display$$` `` — but also in literal blocks:

```
    $inline typesetting but on its own line?$

and:

    $$display$$
```
[[source](https://raw.githubusercontent.com/ForbesLindesay/supermarked/master/examples/math.md) ->
 [output](https://rawgit.com/ForbesLindesay/supermarked/master/examples/math.html)]

(My personal opinion is that this is not such a great idea because it makes it hard to use the dialect to describe its own math syntax — in general it breaks the "literals are never processed" axiom.
But that applies to some other literal-based syntaxes, and must be weighed against the tool-compatibility benefit...)

### [Hoedown](https://github.com/hoedown/hoedown/blob/master/test/Tests/Math.text)
With `HOEDOWN_EXT_MATH` (`--math`), supports `\\(inline\\)`, `\\[display\\]`, and Kramdown style `$$dwim$$` syntax automatically interpreted as inline or display.
With `HOEDOWN_EXT_MATH_EXPLICIT` added (`--math --math-explicit`), also parses `$inline$` and double dollars become `$$always block$$`.
[I might be wrong, has no docs]

### [Maruku](https://github.com/bhollis/maruku/blob/master/docs/math.md)

Off by default, math extension has to be [enabled](https://github.com/bhollis/maruku/blob/master/docs/math.md#enabling-the-extension).

`$inline$`, `$$display$$`, `\[display\]`.
Supports a unique nicer syntax for referencing equations:

    Consider (eq:a):

    $$ \alpha = \beta $$        (a)

(`\label` and `\eqref` also work)

### [MathJax](http://docs.mathjax.org/en/latest/options/tex2jax.html)
[Not a converter in itself but powers math in most online apps.]

Configurable delimiters — by default `\(inline\)`, `$$display$$`, `\[display\]`.
Smart enough to parse `$y = x^2 \hbox{ when $x > 2$}$.` as one expression.
Supports backslash-escaping to prevent parsing as math.

Recognizes `\begin{foo}...\end{foo}` without any extra delimiters.
Supports macros — recognizes `\def...`, `\newcommand...` without any extra delimiters.

Can also support MathML and AsciiMath — depends on configuration. 

### [KaTeX](https://khan.github.io/KaTeX/)
Much faster (and smaller) than MathJax but supports considerably less constructs so far.
Doesn't yet recognize math by any delimiter, need to call function per math fragment. 
Notable for outputting stable HTML+CSS+webfont that work on all modern browsers, so can run during conversion and work without javascript on client.  (MathJax 2.5 also has "CommonHTML" output but it's bad quality, only usable as preview; the closest server-side option is MathJax-node outputing SVG.)

Not yet used much with markdown. 

### ikiwiki with [mathjax plugin](https://github.com/bk/ikiwiki-plugin-mathjax)

Both display ($$...$$ or \[...\]) and inline ($...$ or \(...\)) math are supported. Just take care that inline math must stay on *one line in your markdown source. A single literal dollar sign in a line does not need to be escaped, but two do.

(alternatively there is a [pandoc plugin](https://ikiwiki.info/plugins/contrib/pandoc/))

### [Jekyde](https://zohooo.github.io/jekyde/latex.html)
Dollars. (although their MathJax config also allows `\(` and `\[`?)

### [Softcover](http://manual.softcover.io/book/softcover_markdown#sec-embedded_math)
Single backslashes.  Supports labels, `\ref` and `\eqref`.

Also [supports but discourages](http://manual.softcover.io/book/softcover_markdown#sec-terrible_math) Leanpub's `{$$}...{/$$}` syntax.

### Markdown-it with [markdown-it-math](https://github.com/runarberg/markdown-it-math) plugin
[Markdown-it](https://github.com/markdown-it/markdown-it) is JS CommonMark-compatible parser.  markdown-it-math supports configurable delimiters, with some the restriction that block delimiters must stand on their own line; the defaults are notably unique:

    $$inline$$

    $$$
    display
    $$$

More importantly, the inner syntax is configurable (by passing alternative convertor) but **defaults to [AsciiMath](https://runarberg.github.io/ascii2mathml/), not TeX**!

### [FSharp.Markdown library](http://tpetricek.github.io/FSharp.Formatting/sideextensions.html)
`$inline$`, apparently also allows `$$inline$$`(?).
Has unique syntax for display math with no closing delimiter:

    $$$
    A_{m,n} = \begin{pmatrix}
      ...
    \end{pmatrix}

Lots of examples [here](http://www.aleacubase.com/cudalab/cudalab_usage-math_formatting_on_markdown.html).

### Python-markdown with [Python-markdown-math extension](https://github.com/mitya57/python-markdown-math#math-delimiters)
`\(inline\)`, `$$display$$`, `\[display\]`.  `$inline$`. 
And some support for `\begin{foo}...\end{foo}`.
`$inline$` disabled by default, but can be enabled by passing enable_dollar_delimiter=True in the extension configuration.

### Pelican with [`render_math` plugin](https://github.com/barrysteyn/pelican_plugin-render_math#markdown)

`$inline$` as long as the closing `$` is not preceded by space;
`$$display$$`; `\begin{foo}...\end{foo}`.

## Sites / Online Editors ##

To a large degree these rely on one of the above converters for math support.

### Stack Exchange scientific sites such as mathoverflow, [Physics.SE](https://physics.stackexchange.com/editing-help#latex) and [Mathematics.SE](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)

`$inline$`, `$$display$$`.  Also (undocumented?) recognizes `\begin{foo}...\end{foo}` without any delimiters but only for some environments, e.g. `\begin{equation}` works but `\begin{matrix}` requires surrounding dollars.  Recognizes `\newcommand` and friends inside dollars.

  * [Electrical Engineering.SE](https://electronics.stackexchange.com/editing-help#LaTeX) has a weird exception: single `$` does not delimit inline math, `\$...\$` does!?!  (`$$display$$` works as usual.)

### [Stackedit](https://stackedit.io/#mathjax)
Dollars.  Smart enough to parse `$y = x^2 \hbox{ when $x > 2$}$.` as one expression.
`\begin{foo}...\end{foo}` outside dollars also works.
Also recognizes `\\\\(inline\\\\)` (yep, that's 4 backslashes) and `\\[display\\]` but I'm not sure they're intentional.

### [Marxi.co](http://marxi.co/#latex-expression)  (Based on Stackedit; uses SVG to store HTML with math in Evernote.)
Dollars.  Smart enough to parse `$y = x^2 \hbox{ when $x > 2$}$.` as one expression.
`\begin{foo}...\end{foo}` outside dollars also works.

### [SageMathCloud](https://plus.google.com/115360165819500279592/posts/NCsfZzjMDrD)
Dollars and backslashes.
Powered by MathJax (with printing powered by pandoc) so also recognizes stuff like `\begin{foo}...\end{foo}` outside math delimiters.

### [Authorea](https://authorea.com)
The site supports (via pandoc) multiple input formats from AsciiDoc to Texile.
In markdown it uses single backslash: `\(inline\)` and  `\[display\]`.  [discussion](https://www.authorea.com/issues/5)

### [Penflip](https://www.penflip.com/blog/mathjax-integration)
Mixed: `\(inline, only on one line\)`, and `$$display, can be multi-line$$`.

### [Markx](https://markx.herokuapp.com)
Dollars, double backslashes.

### Beegit
Undocumented but seems to support `\\(inline\\)`, `$$display$$`, `\\[display\\]` as well as `\begin{foo}...\end{foo}`.

### [Leanpub](https://leanpub.com/help/manual#leanpub-auto-mathematical-equations)
`{$$}...{/$$}`.  Used for both inline and display (if the math stands alone in a paragraph).

### Draft [Markua](https://leanpub.com/markua/read) spec
[Markua](http://markua.com/) is a successor to Leanpub Flavored Markdown but published as a neutral spec; independent implementations are beginning e.g. https://github.com/dshafik/markua.

[Inline math](https://leanpub.com/markua/read#math-span) is represented using `{math: mathml}...{/math: mathml}` and `{math: latex}math here too!{/math: latex}`.  
There is also the `{$$}...{/$$}` shorthand which uses the default math language (see below).

[Display math](https://leanpub.com/markua/read#math-blocks) is represented using `{math: latex}` or `{math: mathml}` attributes before a code block:

    {math: latex}
    ```
    \left|\sum_{i=1}^n a_ib_i\right|
    \le
    \left(\sum_{i=1}^n a_i^2\right)^{1/2}
    \left(\sum_{i=1}^n b_i^2\right)^{1/2}
    ```

There is also a shorthand — starting a code block with ```` ```math ```` will use the default math language.

The default math language in a Markua document is determined by the value of the `math` attribute which is set in the [metadata](https://leanpub.com/markua/read#settings); if unset it's latex.

### Gitbook
Math support not clearly documented.  Can come via https://github.com/GitbookIO/plugin-mathjax or https://github.com/GitbookIO/plugin-katex plugins, or possibly now builtin via kramed?

In any case, uses kramdown-style double-duty `$$inline$$` (among other text) and `$$display$$` (alone in paragragh).
I tried Gitbook's online editor and it seems to treat every line as a paragraph for the purpose of deciding what's display math; not sure if that's specific to the editor or the format.

### http://tex.s2cms.ru/page/
kramdown-style double dollars for both inline and display.

### [Gingko](https://gingkoapp.com/faq#card364224844d1c4451ba000051)
Dollars.  `$$display math$$` delimiters only recognized at start/end of line (can be combined with markdown constructs e.g. `> - $$quoted listed math$$` but not `text $$math$$.`).  Both kinds of math can be split across lines.

(Need to choose "Enable LaTeX" from gear menu)

### [Gitter](http://blog.gitter.im/maths-geeks-take-note/)
Only `$$inline$$` — yep, only inline math in double dollars.
Uses KaTeX so fast but less math constructs are supported.

### [Instiki](https://golem.ph.utexas.edu/wiki/instiki/show/Syntax)
`$inline$`, `$$display$$`, `\[display\]`.  The internal math syntax is [itex2MML — has some intentional differeces from TeX](https://golem.ph.utexas.edu/~distler/blog/itex2MMLcommands.html). 

Also supports [theorem-like environments](https://golem.ph.utexas.edu/wiki/instiki/show/Theorems) and references to numbered equations as `(eq:label)` or `\eqref{label}` and embedded SVG as `\begin{svg}<svg...</svg>\end{svg}`.  See https://golem.ph.utexas.edu/wiki/instiki/edit/Sandbox for details.

### [Logdown](http://logdown.com/demo)
Literal-based syntax:

    Display:
    ```mathjax
    x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a}
    ```
    
    Inline: `$a^2 + b^2 = c^2$`.  AFAICT, there is no way to write a literal starting and ending in dollars that won't be interpreted as math.

This resembles Scholdoc's syntax, but I'd say Scholdoc's is better thought out.

### [Editor.md](https://pandao.github.io/editor.md/examples/katex.html)
Kramdown-style `$$...$$` for both inline and display — centered if alone on the line.
Also ```` ```math ```` or ```` ```latex ```` or ```` ```katex ```` (all equivalent) literal blocks for display.
(There are still [some bugs](https://github.com/pandao/editor.md/issues/120) with centering != displaystyle.)

### [Mathdown](https://mathdown.net/?doc=help) by yours truly
Dollars and backslashes.
Tries to recognize LaTeX without delimiters like Pandoc but not very robust: `\begin{foo}...\end{foo}`, `\[re]newcommand...}` (greedy till last `}` on the line).

All this only works when the delimiters & math are written on a single line, but I consider that [a bug](https://github.com/cben/CodeMirror-MathJax/issues/3).

## Desktop editors

### R Studio [R Markdown v2](http://rmarkdown.rstudio.com/#embedding-equations)
Based on Pandoc.
`$inline$` (without space between the $s and the math), `$$ display $$`.
Also supports raw MathML (`<math>...</math>`).
Also `superscript^2^` syntax is mentioned in [v1->v2 migration doc](http://rmarkdown.rstudio.com/authoring_migrating_from_v1.html), so I presume pandoc's `subscript~2~` is also supported.

I didn't test this but I have a suspicion the "no space between $ and math" rule was quoted from [pandoc doc](http://rmarkdown.rstudio.com/authoring_pandoc_markdown.html#math) which is not exactly what pandoc actually implements.

#### [R Markdown v1](https://web.archive.org/web/20140721030657/https://support.rstudio.com/hc/en-us/articles/200486328-Equations-in-R-Markdown)
Backslashes, dollars, and WordPress-inspired `$latex ...$` and `$$latex ... $$` syntaxes.
Also supports raw MathML.

### [Retext when configured for math](http://sourceforge.net/p/retext/wiki/MathJax/)
Based on [pymarkups](http://pythonhosted.org//Markups/standard_markups.html#markdown-markup).
`$inline$`, `\(inline\)`, `$$display$$`, `\[display\]` as well as `\begin{foo}...\end{foo}`.

### [MacDown](http://macdown.uranusjr.com/features/)
Uses Hoedown.  Math support is optional, has 2 modes:

  - `\\(inline\\)`, `\\[display\\]`, `$$dwim$$` (either inline or display depending on context).
  - `\\(inline\\)`, `\\[display\\]`, `$inline$`, `$$display$$`.

Also documented to support MathML [this simply follows from markdown's *ML pass-through plus MathJax (`TeX-AMS-MML_HTMLorMML` config) rendering MathML even on browsers that don't support it].

### [Haroopad](https://github.com/rhiokim/haroopad#enhanced-markdown-syntax)
Has to be enabled in Preferences (General tab > Enable Mathematics Expression).
Can choose between `$$$inline$$$` or `$inline$` syntax; either way supports `$$display$$`.
Also supports pandoc-like `^superscript^`, `~subscript~`.

See also [Korean doc about math](http://pad.haroopress.com/page.html?f=mathematics-expression) and [examples](http://pad.haroopress.com/page.html?f=sample-mathematics).

### [Uberwriter](https://bazaar.launchpad.net/~w-vollprecht/uberwriter/quickly_trunk/view/head:/help/stump/help.md#L666)
Uses pandoc for export, so supports `$inline$` (with heuristic of no spaces on inside of the dollars), `$$display$$` and raw `\foo{...}` and `\begin{bar}...\end{bar}`.  Plus standalone `~subscript~` and `^superscript^` syntaxes.

The regular preview doesn't render math, but you can preview an individual formula by right-clicking it (Esc to close).  This only works for dollar(s)-delimited math, not the other syntaxes pandoc recognizes.

### Remarkable
Didn't find clear documentation of math support.
[Changelog](http://remarkableapp.net/change_log.md) mentions pandoc-like `^superscript^`, `~subscript~` and new "MathJax support (slightly buggy)".
It seems `$inline$`, `$$display$$` are the supported syntaxes.
All the above work equally in preview, HTML and PDF export and are not confused by chars significant to markdown (like `*`) inside the math.

`\\[display\\]` and `\begin{foo}...\end{foo}` also work (preview and export) but content that look like markdown markup breaks the rendering — I suppose these are incidental side effect of MathJax running on the full output. (I'll report the issue)

### Atom with [markdown-preview-plus][] / [markdown-preview-katex][] plugins
`$inline$`, `$$display$$`, `\[display\]`.

[markdown-preview-plus]: https://github.com/Galadirith/markdown-preview-plus/blob/v1.4.0/LATEX.md#syntax
[markdown-preview-katex]: https://github.com/abejfehr/markdown-preview-katex/blob/master/LATEX.md#syntax

### [Texts.io](http://www.texts.io/support/0020/)
Dollars.  Conversion is Pandoc-powered.
It's a semi-WISYWIG editor: IIUC editing happens on a document model, which is then [exported](http://www.texts.io/support/0009/) back into markdown.  Most markdown syntaxes can be manually entered and are then [auto-converted](http://www.texts.io/support/0018/) into the internal model — including `$inline$` followed by <kbd>Space</kbd> and `$$display$$` followed by <kbd>Enter</kbd>.

### TODO: Typora
Not sure without trying (don't have a Mac).
[`$$` opens display math block](https://twitter.com/Typora/status/560811438332080128) and from [the in-place formatting goals](https://abnerlee.github.io/typora/2015/03/11/why-typora/) I *suppose* you can just type `$$math$$` without any mouse clicks and it will render, but not sure.  Also unclear if [`$inline$` is supported yet](https://twitter.com/search?q=typora%20math).

### Emacs with [markdown-mode.el](http://jblevins.org/projects/markdown-mode/) with `markdown-enable-math` turned on
Highlights (and doesn't parse as markdown) `$..$`, `$$..$$`, or `\[..\]`.  But that's all.

### Qute
Apparently anything MathJax would recognize — dollars, backslashes, some latex constructs without math delimiters...

Qute is no longer developed, but I mention it fondly as its per-paragraph source/rendered toggling was one of the inspirations for Mathdown's in-place formatting and math rendering (the other was Emacs with preview-mode).

## Mobile apps

### [EQ Writer](http://www.eqeditor.com/writer/)
Double backslashes (powered by MultiMarkdown).

## Testing ##

Testing `It costs between $10 and $20.`:
http://johnmacfarlane.net/babelmark2/?normalize=1&text=It+costs+between+%2410+and+%2420.
Only Maruku (Math-Enabled) recognized it as math.

Testing various syntaxes:
http://johnmacfarlane.net/babelmark2/?normalize=1&text=Inline%3A+%24dollar+%5Csqrt%7Bx%7D%24%2C+%5C(single+backslash+%5Csqrt%7Bx%7D%5C)%2C+%5C%5C(double+backslash+%5Csqrt%7Bx%7D%5C%5C).%0A%0ADisplay%3A+%24%24double+dollar+%5Csqrt%7Bx%7D%24%24%2C+%5C%5Bsingle+backslash+%5Csqrt%7Bx%7D%5C%5D%2C+%5C%5C%5Bdouble+backslash+%5Csqrt%7Bx%7D%5C%5C%5D.%0A

## See also MathType's "Works With..." database ##

They mention every tool/site under the sun, e.g.
http://www.dessci.com/en/products/mathtype/works_with.asp#!target=beegit
although some entries are placeholders, and they don't go into much detail on the exact syntax.

---

## Appendix: notable non-markdown tools ##

  - [Jemdoc](http://jemdoc.jaboc.net/latex.html) (you probably want its [MathJax variant](https://github.com/wsshin/jemdoc_mathjax)): `$inline$` and `\(display\)`.

    > Yes, round brackets instead of square brackets---this is to avoid a conflict with ordinary square brackets that are escaped to avoid being a link.  Sorry.

  - [Mathflowy](https://github.com/thricedotted/mathflowy) chrome extension for math in Workflowy: `\(inline\)`, `\[display\]`.


