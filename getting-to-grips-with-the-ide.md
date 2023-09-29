# Getting to grips with the IDE

As mentioned in the getting started section, Occam has its own IDE. 
Actually Occam's CLI tools are not integrated with it as of yet and therefore it is really just a glorified collaborative text editor.
Nonetheless it has it uses. 
It supports Occam's own vernacular, for example, called Florence. 
It will also unpack Occam's pac=kages in its projects pane so that you can effectively browse them as projects. 
And it has useful indexing and navigation features.
All told it is worth the effort of downloading and installing it and will only improve with time.

It has been made as useable as possible and most of its functionaoity should be discoverable.
However, some functionality is more hidden and so all of it is covered in what follows.
To begin then, note that there are severral toolbars along the top as well as the several panes.
All of the toolbars with input fields are sizeable.
Most of hte panes can be minimised in the obvious way, moreover the vertical splitter bars can be double clicked to minimise the left and right areas.

The first toolbar goes hand in hand with the projects pane and has a recylce bin for its files and directories.
The button with the two arrows will synchronise the active document with the projects pane, in other words select its corresponding file therein.
The pencil button allows you to edit the name of the currently selected file or directory.
The next two buttons allow you to create files and directories, respectively.
Either will be created in the currently selected directory, if there is one, otherwise in the root projects directory.

As for the projects pane itself, you can drag filea and directories around freely but bear in mind that packages are immutable.
Remember that the topmost directories of packages are shown with a padlock.
One other thing to bear in mind is that by defualt only recognised files are shown in the proejcts pane.
Thus a file may seem to disappear if you drag it into a child directory, for example.
In fact here is a list of recognised files:

* *.fls
* meta.json
* type.ptn
* symbol.ptn
* operator.ptn
* term.bnf
* statement.bnf
* metastatement.bnf

You can correct this easily enough in the settings, which we will come to in a while.
