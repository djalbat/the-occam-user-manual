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
Also note that most of the panes can be minimised in the obvious way.
Moreover the vertical splitters, that is the draggable elements between the panes, can be double-clicked in order to minimise the left and right panes.

## Projects and packages

The first toolbar goes hand in hand with the projects pane.
It has an input field for the projects directory that was mentioned earlier.
Just to recap, you can change the projects directory at any time by typing a fully qualified path into this field and hitting return or clicking the refresh button.
Note that all open documents will be closed when you do this.
They will also all be closed if you hit the refresh button even without changing the projects directory.
In effect the IDE does not differentiate between the two cases.

Aside from the projects directory input field the projects toolbar has several buttons and a recycle bin for the project pane's files and directories.
The button next to the recycle bin with the two arrows synchronises the active document, that is selects its corresponding file in the pane.
The pencil button allows you to edit the name of the currently selected file or directory.
The next botton allows you to show and hide packages.
This is useful because packages do not live in their own directory but alongside projects.
Hiding them temporarily is therefore often desirable.
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

## The console and settings

At present the console is not interactive and only logs 'error', 'warning', 'info', 'debug' and 'trace' level messages.
The log level can be adjusted in the settings pane on the right.
The recommended level is 'info', which will ensure that you see all pertinent messages.
All messages are sent to the console but may not be shown if the log level has been set to preclude them.
So if something appears to have gone wrong then the relevant debug and trace messages will still be avaialble if the log level is subsequently set appropriately.
Note that the IDE has been designed so that if you keep the log level at 'info' then during normal operation you will not see any messages at all.

Of the other settings, hopefully most will be self explanatory.
Of the ones that perhaps need an explanation, showing only recognised files has already been touched upon in the projects and packages section above.
If you choose not to copy Unicode characters to the clipboard then they will pasted directly into the active document, otherwise being discarded.
If you enable the loading of hidden files and directories then be aware that Git creates a hidden directory in cloned projects and that it can potentially contain thousands of entries.
In fact this setting was added precisely to stop the hidden Git directory from being loaded.
Disable it at your peril, therefore.
Lastly, going straight to singular labels and references means that if you, click on a label, say, then if there is only one corresponding reference then you will be taken straight to it rather than a link to it being givem in the console.
And vice versa if you click on a reference.

## Editing

Little explanation of the editor's functionality is needed and it will hopefully feel familiar to anyone who has used such tools before.
There are two toolbars that go along with it, namely the find and Unicode toolbars.
These are tied up with the keyboard shortcuts, which is perhaps the only thing that requires further explanation aside from the menu in the bottom-right corner of the editor itself.
This remains hidden until you mouse over it.
It has buttons to increase and decrease the editor's font size as well as buttons to toggle the presentation mode.

Starting with the fold functionality, folds can of course be expanded or collapsed by clicking on their buttons with the mouse.
The corresponding keyboard shortcuts are the command or control key together with the plus and minus keys which will expand or collapse any folds enclosing the selections, respectively.
Holding down the shift key at the same time will expand or collapse all the folds.
   
There are two kinds of find functionality, namely what might be calling finding and grouping.
For finding, both in the file being currently edited and in all the files in the loaded projects and packages, the keyboard shortcut is the command or control key together with the 'F' key.
This moves the input focus to the content input field of the find toolbar from where you can type in the content you wish to find.
Clicking the first of buttons to the right of this field will find the content in the file being edited, or you can hit the enter key.
In either case the focus will return to the editor with the content to be found under the sole selection.
On the other hand if you click the second button then a list of links of occurences of the content to be found in all of the loaded projects and packages will be given in the console.
Bear in mind that these link are shown as 'info' level messages and therefore if you have the log level set at a higher level then you will miss them.

The second kind of find functionality is grouping and this happens in the editor without its focus being taken away.
The requisite keyboard shortcut is the command or control key together with the 'G' key.
If nothing is selected, that is only carets are showing, then the token underneath the first caret will be selected.
If there is already a selection then its next occurrence of the selected content will be selected.
This process can be repeated until all occurrences have been found, or hold down the shift key to group all occurences at once.

The editor fully supports Unicode but of course no keyboard can.
In order to get around this the Unicode toolbar has been provided.
The keyboard shortcut is the command or control key together with the 'U' key, which moves the input focus to the Unicode character input field.
Typing into this field will reveal a drop down list of filtered Unicode characters, one of which will always be selected.
Hitting the enter key will paste this character into and return the focus to the edited document.
Or you can click on any character in the dropdown list to give the same result.

Lastly, a word or two about undo and redo functionality.
The keyboard shortcut to undo the last group of operations is the usual command or control key together with the 'Z' key.
For redoing, hold the shift key down.
Unlike other text editors if you partically traverse the redo buffer and then make a fresh operation then the partial remains of the redo buffer are not obliterated.
Instead they are transformed using the same operational trnasformations that are employed in sessions.
Thus the redo buffer will appear to degrade over time rather than immediately disappearing altogether and this can be disconcerting.
If this explanation does not entirely make sense or if you encounter this mechanism unexpectedly then the best advice is probably to pick a toy example file and familiarise yourseif with the mechasnim by way a few operations either way.
Finally, on the subject sessions, bear in mind that concurrent user's operations are not added to your own undo and redo buffers because they cause a blow up in their size.

## Exporting custom grammars

The very last toolbar to mention is the grammars toolbar, which only has one button to export the custom grammars.
If a project or package is selected at the time then clicking this button will export the corresponding custom grammar together with custom grammars on which it depends.
Otherwise the custom grammars for all of the loaded projects and packages will be exported.



