## Markdown Style

Highmark's main contribution to Markdown is the introduction of a dedicated style language, called Markdown Style.
This is akin to CSS, indeed it complies down to CSS.
Markdown Style's relation to published divisions is covered first, after that its syntax is covered.

1. There is a default Markdown Style[^defajlt-markdown-style] that is applied to all divisions. 
Although it cannot be removed, it can be completely overridden if need be.
Its purpose is to provide a consistent style in the abscence of any other.
The idea is similar to a browser's default CSS.
This may not be apparent but is always present.
There is no such thing as an unstyled web page shown in a browser.
2. After this there is the `default.mds` file in the root of the project.
This is applied not just to the `default.md` file's corresponding division but to all divisions.
Here is part of this book's default style:

```
padding: 6vh;

blockListing,
inlineListing {
  colour: \#000;
  background-colour: transparent;
}

inlineListing {
  padding: 0;
}

blockListing {
  border: 1PX solid \#333;
  padding: 12pt 18pt;
  line-height: 19pt;
  box-shadow: 3pt 3pt 0 \#999;
}
```

3. Laslly individual Markdown Style files are only applied to the divisions of their correspondoing Markdown files.
For example there is a `cover.mds` Markdown Style file in the `front-matter` directory corresponding to the `cover.md` file.

Properties outside of any rule, such as the `padding` property above, are applied to all the elements in a division.
On the other hand properties inside of rules are applied to their correspondoing Markdown elements.
Here is a complete list of the element names that can be used in Markdown Style files:

#### Headings

* primaryHeading
* secondaryHeading
* tertiaryHeading
* quaternaryHeading
* indexHeading

#### Lists

* orderedList
* orderedItem
* unorderedList
* unorderedItem
* indexList
* indexItem
* contentsList
* contentsItem
* footnotesList
* footnotesItem

#### Links

* anchor
* emailLink
* hyperlink
* indexLink
* contentsLink
* footnoteLink

#### Tables

* table
* tableHead
* tableHeadRow
* tableHeadCell
* tableBody
* tableBodyRow
* tableBodyCell

#### Listings

* blockLine
* blockListing
* inlineListing

#### Text elements

* line
* paragraph
* strongText
* emphasisedText
* stronglyEmphasisedText

#### Miscellaneous

* error
* pageNumber

All element names aside from these those above are ignored.

Here are some other things to bear in mind about Markdown Style and in particular its relation to CSS:

1. Rules can be nested but there is no need for a SASS-liike ampersand:

```
paragraph {
  line {
    font-weight: bold;
  }
}
```

2. The properties themselves are a strict subet of CSS properties but most common functionality is supported.
Native English speakers can use `colour` rather than `color` and it will be translated to the americanism:

```
background-colour: red;
```

3. Pseudo-elements  and ombinators are not supported but pseudo-classes are.
For example, from the default Markdown Style file:

```
table,
...
tertiaryHeading,
quaternaryHeading {
  :first-child {
    margin-top: 0;
  }
  
  :last-child {
    margin-bottom: 0;
  }
}
```

Lastly, there are five Computer Modern Unicode[^cmb-fonts] or CMU fonts available:

* Computer Modern Serif
* Computer Modern Sans
* Computer Modern Bright
* Computer Modern Concrete
* Computer Modern Typewriter

Each comes in the four variants of regular, bold, italic and bold italic, making twenty files in all.
As mentioned earlier, these are copied to the `font` directory during publishing.
The `@font-face` CSS at-rules are automatically added to the CSS embedded in the `index.html` file, making these fonts easily avaiable.
Here is an example from the default style:

```
primaryHeading,
secondaryHeading,
tertiaryHeading,
quaternaryHeading {
  line-height: 1;
  font-weight: normal;
  font-family: "Computer Modern Sans";
}
```

[^cmb-fonts]: https://github.com/djalbat/highmark-fonts/tree/master

[^defajlt-markdown-style]: https://github.com/djalbat/highmark-markdown/blob/master/src/defaultMarkdownStyle.js
