# Working with Highmark

As mentioned in the introduction, Occam supports Highmark as well as formal reasoning.
In fact, over time it is likely that the majority of Occam's users will be Highmark users.
If you are one of these users then this chapter is for you.

Highmark is a document preparation system inspired by Markdown[^markdown] and TeX[^tex].
Aside from blending variants of these two technologies it unique selling point is the clear separation of style and content.
In a sense Markdown already does this because it does not include any style information.
It is usually converted to HTML with the assumption being that styling will be added with CSS.
Highmark goes one step further, however, and provides a separate language akin to CSS for the purposes of stying, called Markdown Style.
Highmark's variant of Markdown together with Markdown style are converted to HTML and CSS, respectively, as expected.
And in future it is hoped that they will be converted to Open Document format and from there to PDF.

@embed content/working-with-highmark/getting-started.md
@embed content/working-with-highmark/markdown.md
@embed content/working-with-highmark/markdown-style.md

[^tex]: https://wikipedia.org/tex

[^markdown]: https://wikipedia.org/markdown

@footnotes
