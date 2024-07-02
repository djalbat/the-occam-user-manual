## Sessions

The second toolbar goes with the sessions pane. 
It has a rubbish bin and an input field for session keys.
There are also three buttons for creating, joining and leaving sessions, as well as a button to copy the session key to the clipboard.

Clicking the button for creating a session when the session key input field is left blank will create a seesion with a random key.
It is recommended that you do this and then pass the session key to other session users by way of email or whatever.
They can paste the session key into the session key input field and then click the join session button in order to join the session.
Anyone can leave a sesssion at any time, including the creator.
In fact the session will persist on the server for half a minute or so even when everyone has left, during which time it can be re-joined.

Once a session is created you can drag files and directories into it from the projects pane.
These can then be removed from the session by dragging them into the rubbish bin to the left of the session key input field.
Anyone can add files to and remove files from a session. 
The session creator has no special privileges in this respect.
Also bear in mind that if someone drags a file into a session that already exists in one of your projects then this file will be altered concurrently regardless of whether you have it open in the editor or not.
Finally, bear in mind that adding package files to sessions can cause problems, because if another session user has the file as a project file then they will be able to alter it.
Consequently your package file will be altered concurrently and this is unlikely to be the desired behaviour.
