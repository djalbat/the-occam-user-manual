# Writing with Highmark

Highmark is a document preparation system inspired by Markdown[^markdown] and TeX[^tex].
It is supported by Occam, as will been seen.     
As a matter of fact both this book and the Foundations book are written in Highmark.

The core concept that underlies Highmark is the distinctxion between style and content.
To give an example, in the early days of the web often no such distinction was made.
Consider the following HTML:

```
<p>
This is meant to be communicated <b>strongly</b> whereas this is meant to be <i>emphasised</i>.
</p>
```

Here the `b` and `i` elements stand for bold and italic, respectively.
What if the reader is visually impaired, however? 
To cover such cincumstances thnew elements were deprecated and new elements invented to encapsulate the **meaning** of parts of the document whilst their **presentation** was defined in CSS.
Thus the above became:

```
<p>
This is meant to be communicated <strong>strongly</strong> whereas this is meant to be <em>emphasised</em>.
</p>
```

Note that `em` here stands for emphasise.
Now the attendant visual CSS:

```
b {
  font-weight: bold;
}

em {
  font-style: italic;
}
```

And the aural CSS:

```
\@media speech {
  strong {
    voice-volume: x-loud;
  }

  em {
    voice-rate: slow;
  }
}
```

In fact this approach was never widely adopted, but nonetheless the point has been made.



[^tex]: https://en.wikipedia.org/wiki/TeX

[^markdown]: https://en.wikipedia.org/wiki/Markdown

@footnotes
