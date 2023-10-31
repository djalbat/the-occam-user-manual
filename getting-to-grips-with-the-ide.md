# Getting to grips with the IDE

As mentioned in the getting started chapter, Occam has its own IDE. 
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

## Projects and packages,

The first toolbar goes hand in hand with the projects pane.
It has an input field for the projects directory that was mentioned earlier.
Just to recap, you can change the projects directory at any time by typing a fully qualified path into this field and hitting return or clicking the refresh button.
Note that all open documents will be closed when you do this.
They will also all be closed if you hit the refresh button even without changing the projects directory.
In effect the IDE does not differentiate between the two cases.

Aside from the projects directory input field the projects toolbar has several buttons and a recycle bin for the project pane's files and directories.
The button next to the recycle bin with the two arrows synchronises the active document, that is selects its corresponding file in the pane.
The pencil button allows you to edit the name of the currently selected file or directory.
Lastly, the rightmost two buttons allow you to create files and directories, respectively.
They will be created in the currently selected directory, if there is one, otherwise in the root projects directory.

As for the projects pane itself, you can mostly drag filea and directories around freely.
Bear in mind however that packages are immutable in the sense that their file and directory names cannot be changed.
Also you cannot drag files in the projects directory, because only projbects and packages are loaded.
Remember also that the topmost directories of packages are shown with a padlock.
One other thing to bear in mind is that only what are known as recognised files are shown in the proejcts pane by default.
Thus a file may seem to disappear if you drag it into a child directory, for example.
Recognised files are those that go into packages, with other files being ignored.
The one exception are `*.md` files of which only `README.md` files in the topmost directories of projects make it into packages.
Here is the list:

* `*.fls `
* `*.md `
* `meta.json`
* `type.ptn`
* `symbol.ptn`
* `operator.ptn`
* `term.bnf`
* `statement.bnf`
* `metastatement.bnf`

All but `*.fls` and `*.md` files belong strictly in the topmost directories of projects and packages.
As already mentioned, by default they will not show in the projects pane if placed elsewhere.
There is no such restriction on `.fls` files and you are encouraged to cretae sub-directories for them.

## Sessions

The second toolbar goes with the sessions pane. 
It has a rubbish bin and an input for session keys.
There are also three buttons for creating, joining and leaving sessions, as well as a button to copy the session key to the clipboard.

Clicking the button for creating a session when the session key input is left blank will create a seesion with a random key.
It is recommended that you do this and then pass the session key to other session users by way of email or whatever.
They can paste the session key into the session key input and then click the join session button in order to join the session.
Anyone can leave a sesssion at any time, including the creator.
In fact the session will persist on the server for half a minute or so even when everyone has left during which time it can be re-joined.

Once a session is created you can drag files and folders into it from the projects pane.
These can then be removed from the session by dragging them into the rubbish bin to the left of the session key input.
Anyone can add and remove files to and from a session, by the way, the session creator has no special privileges.
Also bear in mind that if someone drags a file into a session that already exists in one of your projects then this file will be altered concurrently regardless of whether you have it open in the editor or not.
Finally, bear in mind that adding package files to sessions can cause problems, because if another session user has the file as a project file then they will be able to alter it.
Consequently your package file will be altered concurrently and this is unlikely to be the desired behaviour.
