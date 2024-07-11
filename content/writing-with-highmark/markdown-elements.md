## Markdown elements

Highmark supports a number of Markdown elements.
In keeping with Markdown their syntax can be somewhat proprietary.

Block elements are delimited by empty lines and are covered first.

### Headings

```
\# Primary heading
\#\# Secondar heading
\#\#\# Tertiary heading
\#\#\#\# Quaternary heading
```

Note that underlining words and phrases with equality symbols or dashes does not result in headings, only the above syntax works.

### Tables

```
| First head cell | Second head cell |
--------------------------------------
| First body cell | .                |
```

Note that a period denotes an empty cell.

### Lists

```
\* An unordered list item
\* Another unordered list item

\2. An ordered list item
\4. Another ordered list item
... spread over two lines.
```

Note that the numbering for ordered lists can be completely arbitrary.

### Block listings

```
\`\`\`

A block listing.

 Whitespace is reproduced faithfully.

\`\`\`
```

### Footnotes

```
\[^occam]: A footnote ...
pertaining to Occam.
```

Footnotes can be placed anywhere in a division but they always appear in a list at its foot and then only if they have been referenced.

### Paragraphs

Paragraphs have no specific syntax, being just one or more contiguous non-empty lines.

Inline elements are covered next.

### Emphasised text

```
\*\* emphasised text, conventially shown in italic \*\*
\*\*\* strong text, conventially shown in bold \*\*\*
\*\*\*\* strongly emphasised text, conventially shown in both bold and italic \*\*\*\*
```

Note that the syntax here starts with two asterisks and ends with four. 
Single asterisks are reserved for unordered list items and reusing them would result in ambiguity.

### Inline listings

```
This \`listing\` will appear inline.
```

### Links

Email links and hyperlinks can, in keeping with other Markdown variants, take two forms.
Shorthand links appear verbatim whereas the use of brackets allows a separate name to be rendered:

```
james.smith@djalbat.com

[James Smith](james.smith@djalbat.com)

https://djalbat.com

[James Smith](https://djalbat.com)
```

Footnote links are also supported:

```
Occam \[^occam].
```

Footnote references have already been covered.
They begin footnotes:

```
\[^occam]: A footnote ...
pertaining to Occam.
```

Note also that the only difference betwween a footnote link and its reference is that the latter has a semi-colon appended.

### Images

Image syntax is similar to hyperlinks but with a prepended exclamation mark:

```
![A cat](image/cat.svg) 
```

Alternative text must always be provided and therefore there is no shorthand syntax for images.

@pageNumber
