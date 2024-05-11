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
