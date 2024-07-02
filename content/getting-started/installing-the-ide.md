## Installing the IDE

Occam has its own IDE, or integrated development environment.
There are two variants available, for desktop and browser.
The desktop variant currently only runs on MacOS and the browser variant is therefore provided for everyone else.
You must use Google Chrome in order to run it, however.
Other browsers may work but they are not supported.
If you really have an issue with Chrome then use Chromium which, although still Google's, is at least open source:

It is worth mentioning that there is effectively no difference between the two variants and you are not missing out if you can only install the browser variant.
The desktop variant is in fact simply the aforementioned Chromium configured so as to hide the usual browser functionality and present only the embedded application.
If you get the chance to run the two variants side by side then will be able to see for yourself that they are identical.

Both variants are available from the Occam website:

https://occam.science

Click on the 'I am not a robot' checkbox and download your preference.

To install the browser variant, simply unzip the downloaded zip file and move the unzipped 'Occam' directory to a location of your choice.
Your home directory is advised but it does not really matter as long as you have access to it from a terminal or command prompt.
Now open a terminal or command prompt, `cd` into the Occam directory and execute the following command:

```
npm start
```

Lastly, open a browser with the following URL:

http://localhost:8888

You will be presented with the Occam IDE.
Beyond bookmarking the URL there is nothing more to do.

To install the desktop variant, again unzip the downloaded zip file and this time drag it into the Applications directory, which should be accessible from the finder.
Now, most importantly, do not double click on the icon.
Instead, right click on it and choose 'Open'.
Doing this ensures that you have the opportunity to configure MacOS to execute the iDE even though it is not from a trusted source.
If you simply go ahead and double click on the icon then you will have to configure the security settings after the event and this can be fiddlesome to say the least.
Once the IDE is running, right click on the icon in the dock and choose the option to keep it there.

One last thing to bear in mind is that opening more than one instance of either the browser or indeed the desktop variant of the IDE will almost certainly lead to problems and possibly even lost work.
This is because the IDE stores its settings in the browser's local storage, remember that the desktop version is really just a browser in disguise, and this storage is shared across instances.
If you have two instances and change the projects directory in one of them, for example, you will effectively be changing it in the other.
Perhaps the settings can be sandboxed to particular instances in some later release but this is not the case presently so beware.
