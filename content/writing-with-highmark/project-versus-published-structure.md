## Project versus published structure

There are a few types of input file in the cloned repository:

* Several Markdown `*.md` files including a `default.md` file.
* Several Markdown Style `*.mds` files including a `default.mds` file.
* An `index.json` file for the indexer's options.

These files are all visible in the Occam IDE's projects pane.
Note that the paths of the Markdown and Markdown Style files often correspond.
This will be fully explained later on.

Additionally the following files will be present.
You will need to uncheck the 'Show only recognised files' checkbox in the Occam IDE's settings pane in order to see them.
They are all output files in the sense that they are produced by publishing:

* An `index.html` file.
* Web font `*.woff2` files in a `font` directory.
* A bundled `client.js` file and a `checkmark.svg` file that it uses.

Lastly there are some adjunct files:

* A `license.txt` file.
* Image files in an `image` directory.
* A `README.md` file and a `README.mds` file.

At the very least a project must have a `default.md` file in its root directory and an `index.html` file will be written to this directory when publishing.
The location of the `font` directory is also written in stone.
Aside from these constraints, however, you are free to organise files and directories as you see fit.
In particular a project's directory structure has no bearning on publishing at all.

One concept that needs explanation before going any further is that of a division.
Highmark can be used for writing not just books but also papers, presentations and so on.
Each of these formats comprises different elements such as chapters, sections, slides and the like.
What therefore should Highmark use as its standard element?
Any of the aforementioned elements would likely cause confusion out of context and therefore the standard element is called a division.
This comes from `div` elements in HTML and although awkward at first it has the advantage of being generic.
So each Markdown file in a Highmark project results in a division, albeit with some exceptions.

Although publishing is unaffected by the project's directory structure there are some Markdown elements, called directives, which do have an effect or are otherwise related.
They are:

* `@index`
* `@ignore`
* `@embed <path>`
* `@include <path>`
* `@contents`
* `@footnotes`
* `@pageNumber`

With these directives and the concept of divisions in mind, open the `default.md` file.
This has two kinds of directive, namely a single `@ignore` directive, which tells Highmark not to include the corresponding division when publishing; and several `@include` directives.
During publishing Highmark keeps an array of divisions corresponding to the Markdown files that it processes by way of `@include` directives.
As it encounters each one it immediately processes the corresponding Markdown file and adds the resulting division to this array, provided there is no `@ignore` directive.
Thus in effect the `@include` directives define a tree structure of nested divisions that is flattened out during publishing.

If you mouse over the `@incloude` directives in the `default.md` file then you will see that their paths are clickable.
Click on the first of them now in order to open up the `front-matter/cover.md` file.

As mentioned briefly in the earlier chapter on getting to grips with the IDE, an additional button will appear in the editor menu when Markdown or Markdown Style documents are active.
You can click on this button now in order to bring up the preview pane to show the cover.
When you do so yet another button will appear in the editor menu to enable you to change the relative positions of the preview pane and the pretty printer.
The icon on the other button will also change, signfifying that you can show just the preview pane, hiding the pretty printer altogether.
There is also an invisible splitter between the preview pane and the pretty printer which can be dragged in order to alter the relative amount of space they take up.
Lastly it is worth reminding you of the presentation mode and the extra space that it admits.

Return now to the `front-matter.md` file and click on the `front-matter/contents.md` include path.
Aside from the title this file only has a `@contents` directive.
During publishing this results in the gathering of any headings present in the remaining divisions into a nested list of links.
There is little else to say about the list of contents for now except that it can be styled independently of other lists.

Now use the clickable paths in the `@include` directives to navigate your way to the `content/introduction.md` file.
This has two further directives at its foot, namely the `@footnotes` and `@pageNumber` directives.
Both do as their names suggest.
The Markdown elements needed to create the footnotes themselves will be covered later.

Next, navigate to the `content/getting-started.md` file.
This has several `@embed` directives, which behave much like `@include` directives except that no new divisions are created.
Instead the sub-divisions of each division are embedded directly in the containing division, as the name suggests.

The last directive is the `@index` directive, which can be found in the `back-matter/index.md` file.
As the name suggests this creates an index, the process of which is worth its own section, which comes later on.

Lastly, returning to publishing, try the following command:

```
highmark set-options
```

Three prompts will be given:

1. ***Contents depth***, which determines which headings are gathered into the contents lists. 
The default contents depth is 2, which corresponds to only the primary and secondary headings being shown.
2. ***Lines per page***, the default being infinity, in which case no pagination takes place.
There is no ideal but around 50 seems workable.
More on this point in a moment.
8. ***Characters per line***, with around 80 being workable.
If the lines per page is set to infinity then this option is ignored.

On the subject of pagination it is important to understand the limits of what can be done.
Currently Highmark only publishes to HTML and there is no way to accurately gauge how many lines make up any particular page.
Therefore, unfortunately, pagination does not result in pages of equal height.
Best practice seems to be to choose settings which feel comfortable and accept that the user will do some scrolling.
Given that the Highmark client allows for the font size to be changed, this is almost inevitable.
