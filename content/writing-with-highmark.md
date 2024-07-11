# Writing with Highmark

Highmark is a document preparation system inspired by Markdown[^markdown] and TeX[^tex].
It is supported by Occam, as will been seen.     
As a matter of fact both this book and the Foundations book are written in Highmark.

What motivated Highmark's development was the need to make clear the distinctxion between style and content.
This is essential for controlled natural languages, indeed Highmark could be seen as an intermediate step towards Occam's CNL support.

As an example of the need to distinguish style from content, consider the following HTML.
Here the `b` and `i` elements stand for bold and italic, respectively:

```
<p>
This is meant to be communicated <b>strongly</b> whereas this is meant to be <i>emphasised</i>.
</p>
```

These days such elements, the ones that intimate style that is, have been deprecated in favour of elements that convey meaning.
Here is the HTML that would be used today.
Here `em` here stands for emphasis, by the way:

```
<p>
This is meant to be communicated <strong>strongly</strong> whereas this is meant to be <em>emphasised</em>.
</p>
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

Or the aural CSS:

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

In fact this latter approach, namely using the `aural` medai type, was never widely adopted, but nonetheless the point about separation of style and content holds.

Markdown does not have an attendant style language in the way HTML has CSS, and therefore Highmark includes a new language imaginatively called Markdown Style.
This is very much like CSS and indeed compiles down to CSS just as Markdown compiles down to HTML.

@include content/writing-with-highmark/installation-and-publishing.md
@include content/writing-with-highmark/project-and-published-structure.md
@include content/writing-with-highmark/markdown-elements.md
@include content/writing-with-highmark/markdown-style.md

[^tex]: https://en.wikipedia.org/wiki/TeX

[^markdown]: https://en.wikipedia.org/wiki/Markdown

@footnotes

@pageNumber