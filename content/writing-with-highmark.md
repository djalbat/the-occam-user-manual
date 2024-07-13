# Writing with Highmark

Highmark is a document preparation system inspired by Markdown[^markdown] and TeX[^tex].
It is supported by Occam, as will been seen.     
As a matter of fact both this book and the Foundations book are written in Highmark.

What motivated Highmark's development was the need to make clear the distinctxion between style and content.
This is essential for controlled natural languages, indeed Highmark could be seen as an intermediate step towards Occam's CNL support.

As an example of the need to distinguish style from content, consider the following HTML.
Here the `b` and `i` elements stand for bold and italic, respectively:

```
&lt;p&gt;
This is meant to be communicated &lt;b&gt;strongly&lt;/b&gt; whereas this is meant to be &lt;i&gt;emphasised&lt;/i&gt;.
&lt;/p&gt;
```

These days such elements, the ones that intimate style that is, have been deprecated in favour of elements that convey meaning.
Here is the HTML that would be used today.
The `em` element signifies emphasis, by the way:

```
&lt;p&gt;
This is meant to be communicated &lt;strong&gt;strongly&lt;/strong&gt; whereas this is meant to be &lt;em&gt;emphasised&lt;/em&gt;.
&lt;/p&gt;
```

And now the attendant visual CSS:

```
b {
  font-weight: bold;
}

em {
  font-style: italic;
}
```

And the equivalent aural CSS:

```
\@media aural {
  strong {
    voice-volume: x-loud;
  }

  em {
    voice-rate: slow;
  }
}
```

In fact the latter approach of using the `aural` medai type has never widely adopted, but nonetheless the point about separation of style and content holds.

Markdown does not have an attendant style language in the way HTML has CSS, and therefore Highmark includes a new language imaginatively called Markdown Style.
This is very much like CSS and indeed compiles down to CSS just as Markdown compiles down to HTML.

@include content/writing-with-highmark/installation-and-publishing.md
@include content/writing-with-highmark/project-versus-published-structure.md
@include content/writing-with-highmark/markdown-elements.md
@include content/writing-with-highmark/markdown-style.md

[^tex]: https://en.wikipedia.org/wiki/TeX

[^markdown]: https://en.wikipedia.org/wiki/Markdown

@footnotes

@pageNumber