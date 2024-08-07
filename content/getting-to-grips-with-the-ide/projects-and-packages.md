## Projects and packages

The first toolbar goes hand in hand with the projects pane.
It has an input field for the projects directory that has already been mentioned in the previous chapter.
Just to recap, you can change the projects directory at any time by typing a fully qualified path into this input field and hitting return or clicking the refresh button.
Note that all open documents will be closed when you do this.
They will also all be closed if you hit the refresh button even without changing the projects directory.
In effect the IDE does not differentiate between the two cases.

Aside from the projects directory input field the projects toolbar has several buttons and a recycle bin for the project pane's files and directories.
The button next to the recycle bin with the two arrows synchronises the active document, that is the one that is open in the editor.
Synchorising just means selecting the corresponding file in the projects pane.
The pencil button allows you to edit the name of the currently selected file or directory.
The next botton along allows you to show and hide packages.
This is useful because packages do not live in their own directory but alongside projects.
Hiding them temporarily is therefore often desirable.
Lastly, the rightmost two buttons allow you to create files and directories, respectively.
These will be created in the currently selected directory, if there is one, otherwise in the projects directory.

As for the projects pane itself, you can mostly drag files and directories around freely.
Bear in mind, however, that packages are immutable in the sense that their file and directory names cannot be changed.
Also you cannot drag files into the projects directory, because only projects and packages are loaded.
Remember also that the topmost directories of packages are shown with a padlock.
One other thing to bear in mind is that only what are known as recognised files are shown in the projects pane by default.
Thus a file may seem to disappear if you drag it into a sub-directory, for example.
Recognised files are those that go into packages, with other files being ignored.

* `README.md` 
* `meta.json`
* `*.fls `
* `type.ptn`
* `symbol.ptn`
* `operator.ptn`
* `term.bnf`
* `statement.bnf`
* `metastatement.bnf`

There are some other files that are not ignored, mostly to do with Highmark:

* `*.md`
* `*.mds`
* `index.json`

Note that all but `\*.fls` and `\*.md` files belong strictly in the topmost directories of projects and packages.
As already mentioned, by default they will not shown in the projects pane if placed elsewhere.
There is no such restriction on `.fls` or `\*.md ` files and you are encouraged to create sub-directories for them.
