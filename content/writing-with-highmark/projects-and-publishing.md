## Projects and publishing

You will find several types of input file in the cloned repository's directory.
Specifically:

* Other Markdown `*.md` files including a `default.md` file.
* Other Markdown style `*.mds` files including a `default.mds` file.
* An `index.json` file for the indexer's options.

These files are all visible in the Occam IDE's projects pane.
Additionally the following files will be present but unless you uncheck the 'Show only recognised files' option in the Occam IDE's settings you will not see them:
They are all output files in the sense that they are produced by publishing:

* An `index.html` file.
* Web font `*.woff2` files in a `font` directory.
* A bundled `client.js` file and a `checkmark.svg` file that it uses.

Lastly there are some adjunct files:

* A `license.txt` file.
* Image files in an `image` directory.
* A `README.md` file and a `README.mds` file.

The locations of the input files must always be as stated above and the names and locations of the output files cannot currently be changed.
At the very least a project must have a `default.md` file in the project root and the `index.html` file will also be written to the project root when publishing.
The `font` directory name and location is also written in stone if you want to use the web fonts that Highmark provideds.
Aside from these constraints, however, you are free to create files and folders as you see fit.
In particular, aside from the `font` diretory, the directory structure has no bearning on publishing at all.

One concept that needs explanation before going much further is the concept of a division.
Highmark is suitable for creating not just books but papers, presentations and son on.
Each of these formats encompass different elements such as chapters, sections, slides and the like?
What therefore should Highmark use as its standard element?
Any of the aforementioned elements would likely cause confusion and therefore the standard organisation element is called a division.
This comes from `div` elements in HTML and although awkward at first has the advantage of being generic.

Generally speaking, each Markdown file in a Highmark project results in a division, however there are two exceptions to this rule.
The first is when files are embedded and the second is when the divisions are paginated.
Both of these exceptions will be covered in what follows.

With the concept of divisions in mind, open the `default.ms` file.
This has two kinds of directives:

1. The `@ignore` directive, which tells Highmark not to include the corresponding division when publishing.
2. The `@include` directive, which tells Highmark to process the given file and create a separate division when publishing.

If you mouse over the `@incloude` directives then you will see that the paths are clidkable.