## The console and settings

At present the console is not interactive and only logs 'error', 'warning', 'info', 'debug' and 'trace' level messages.
The log level can be adjusted in the settings pane on the right.
The recommended level is 'info', which will ensure that you see all pertinent messages in the sense that you will see nothing at all unless something goes wrong.
All messages are sent to the console but may not be shown if the log level precludes them.
So if something does go wrong then the relevant debug and trace messages will still be avaialble if the log level is subsequently set appropriately.

Of the other settings, hopefully most will be self explanatory.
Here is a list of short explanations of those that might not be:

* Auto save is not immediate but can take up to three seconds to save changes. 
There is a setting to save files upon closing them, which is strongly recommended.
* Single click explorers means that the single-click and double-click actions are combined when clicking on files and directories. 
This is worth a try but is a matter of taste.
* If you choose not to copy Unicode characters to the clipboard then they will pasted directly into the active document, otherwise they will be discarded. 
Again this is a matter of personal taste.
* If you enable the loading of hidden files and directories then be aware that Git creates a hidden directory in cloned projects and that this can potentially contain thousands of entries. 
Enable this setting at your peril, therefore.
* Going straight to singular labels and references means that if you click on a label, say, and if there is only one corresponding reference then you will be taken straight to it rather than a link to it being given in the console. 
And vice versa if you click on a reference, of course.
