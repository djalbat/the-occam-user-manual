# Getting to grips with the IDE

As mentioned in the getting started section, Occam has its own IDE. 
Actually Occam's CLI tools are not integrated with it as of yet and therefore it is really just a glorified collaborative text editor.
Nonetheless it has it uses. 
It supports Occam's own vernacular, for example, called Florence. 
It will also unpack Occam's packages in its projects pane so that you can browse them as projects. 
And it has useful indexing and navigation features.
All told it is worth the effort of downloading and installing it and will only improve with time.
Some effort has been made in order to make it as usable as possible and most of its functionaoity should therefore be discoverable.
However, some functionality is subtle or hidden and so all of it is covered in what follows.

To begin then, note that there are severral toolbars along the top as well as the several panes.
All of the toolbars with input fields are sizable.
Note that if you hover over the buttons then tooltips will appear.
You can turn this feature off in the settings.
Also note that most of the panes can be minimised in the obvious way, moreover the vertical splitter bars can be double-clicked in order to minimise the left and right areas.

## Projects and packages, files and directories

The first toolbar goes hand in hand with the projects pane.
It has an input field for the projects directory that was mentioned in the getting started chapter.
Just to recap, you can change the projects directory at any time by typing a fully qualified path into this field and hitting return or clicking the refresh button.
Note that all open documents will be closed when you do this.
They will also all be closed if you hit the refresh button even without changing the projects directory.
In effect the IDE does not differentiate between the two cases.

Aside from the projects directory input field the projects toolbar has several buttons and a recylce bin for the project pane's files and directories.
The button next to the recycle bin with the two arrows synchronises the active document, that is selects its corresponding file in the pane.
The pencil button allows you to edit the name of the currently selected file or directory.
Lastly, the rightmost two buttons allow you to create files and directories, respectively.
They will be created in the currently selected directory, if there is one, otherwise in the root projects directory.

As for the projects pane itself, you can drag filea and directories around freely.
Bear in mind however that packages are immutable in the sense that their file and directory names cannot be chnaged and the contents of their files can be viewed in the editor but not altered.
Remember also that the topmost directories of packages are shown with a padlock.
One other thing to bear in mind is that only what are known as recognised files are shown in the proejcts pane by default.
Thus a file may seem to disappear if you drag it into a child directory, for example.
Recognised files are those that go into packages, with other files being ignored.
Here is the list:

* `*.fls `
* `meta.json`
* `type.ptn`
* `symbol.ptn`
* `operator.ptn`
* `term`
* `statement.bnf`
* `metastatement.bnf`

All but `*.fls` files belong strictly in the topmost directories of projects and packages.
As already mentioned, by default they will not show in the projects pane if placed elsewhere.
There is no such restriction on `.fls` files and you are encouraged to cretae sub-directories for them.
