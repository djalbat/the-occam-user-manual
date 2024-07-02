## Editing

Hopefully little explanation of the editor's functionality is needed and it should feel familiar to anyone who has used such tools before.
There are two toolbars that go along with it, namely the find and the Unicode toolbars.
These will be covered below.

There is also a menu in the bottom-right corner of the editor itself, which remains hidden until you mouse over it.
It has buttons to increase and decrease font size as well as buttons to toggle the presentation mode.
There is also a button that toggles a preview pane when Markdown or Markdown Style documents are being edited.
A button also appears when the screen is split between editor and preview pane in order to allow you to swicch their relative positions.

Moving on to the fold functionality, folds can of course be expanded or collapsed by clicking on their buttons with the mouse.
The corresponding keyboard shortcuts are the command or control key together with the plus and minus keys which will expand or collapse any folds enclosing the selections, respectively.
Holding down the shift key at the same time will expand or collapse all the folds.
   
There are two kinds of find functionality, namely what might be calling finding and grouping.
For finding, both in the file being currently edited and in all the files in the loaded projects and packages, the keyboard shortcut is the command or control key together with the 'F' key.
This moves the input focus to the content input field in the find toolbar from where you can type in the content you wish to find.
Clicking the first of buttons to the right of this input field will find the content in the file being edited, or you can hit the enter key.
In either case the focus will return to the editor with the content to be found under the sole selection.
On the other hand if you click the second button then a list of links to occurences of the content to be found in all of the loaded projects and packages will be given in the console.
Bear in mind that these link are shown as 'info' level messages and therefore if you have the log level set at a higher level then you will not see them.

The second kind of find functionality is grouping and this happens in the editor without its focus being taken away.
The requisite keyboard shortcut is the command or control key together with the 'G' key.
If nothing is selected, that is only carets are showing, then the token underneath the first caret will be selected.
If there is already a selection then the next occurrence of the selected content will be selected.
This process can be repeated until all occurrences have been found, or hold down the shift key to group all occurences at once.

The editor fully supports Unicode but of course no keyboard can.
In order to get around this the Unicode toolbar has been provided.
The keyboard shortcut is the command or control key together with the 'U' key, which moves the input focus to the Unicode character input field.
Typing into this input field will reveal a drop down list of filtered Unicode characters, one of which will always be selected.
Hitting the enter key will paste this character into and return the focus to the edited document or copy it to the clipboard, depending on the setting.
Or you can click on any character in the dropdown list to give the same result.

Lastly, the keyboard shortcut to undo the last group of operations is the usual command or control key together with the 'Z' key.
For redoing, hold the shift key down at the same time.
