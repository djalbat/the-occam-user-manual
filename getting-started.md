# Getting started

Occam comprises divers sites, services and applications, the documentation for which is somewhat disparate.
This chapter aims to bring it all together.
It also provices some background on the tools and technologies behind Occam, for the curious.

All of Occam is written in JavaScript, which was invented in the mid-nineties. 
It could be said to have languished until the advent of Node.js, hereafter called just Node, in the late naughties.
Node brought several innovations:

* It enabled developers to write web application servers almost almost trivially.
* It provided a straightforward package manager and a site where packages could be published for free and for all of the community to use.
* As well as server side code, developers could write client side code on Node which could be made to run on broswers by way of a process called bundling.

Allied with continued improvements to JavaScript itself, most notably the ES6 and ES7 releases, Node resulted in an explosion in its use.
This was especially evidient in, but by no means restricted to, Internet appcliations.
Both JavaScript and Node continue to evolve and although both have their detractors, it is safe to say that they will be with us and in a healthy state for the foreseeable future.

## Prerequisites

It almost goes without saying then that in order to use Occam you will need to have Node installed.
In fact the chances are that it already is.
To check this, run the following command in a terminal or command prompt:

```
node --version
````

If something like the following is returned...

```
v18.16.1
```

...then you are in good shape and need do nothing more.
Any major version of Node will do to run Occam, down to major version 12.
If the version that you have installed is older than that or if you just want to install the latest version then go to the Node site here...

[https://nodejs.org/](https://nodejs.org/)

...and follow the instructions for your operating system.

Installing Node will also install Node's package manager, called `npm`.
Again you can easily check that it is installed with the following command:

```
npm --version
```

If you have a relatively recent version of Node installed then the version of `npm` will also be recent enough, too.

The only other prerequisite is Git.
Git is version control software invented by Linus Torvalds, of Linux fame.
It revolutionised version control almost instantly upon its release and, as a consequence, revolutiionised developer and team workflows.
Alongside Git came the GitHub website.
GitHub enabled developers to share their code with the wider community and, as an aside, along with Markdown it brought readme files to the fore.
You can at a pinch get away without installing Git, at least initially, but if you are going to do any serious work with Occam then you will need it.
Occam's own package manager leverages Git, for example, and the Open Mathematics site allows for GitHub integration.

Git may well already be installed on your system.
In order to check, run the following command:

```
git --version
```

Any version will do since Git has been more than adequate since its initial release.
If you do not have Git installed or want the latest version then go to the Git website:

[https://git-scm.com/](https://git-scm.com/)

Installation should be straightforward and no further guidance is given here.

## Installing the IDE

Occam has its own IDE, or integrated development environment.
There are two variants available, for desktop and browser.
The desktop variant currently only runs on MacOS and the browser variant is therefore provided for everyone else.
You must use Google Chrome in order to run it, however.
Other browsers may work but they are not supported.
If you really have an issue with Chrome then use Chromium which, although still Google's, is at least open source:

[https://www.chromium.org/Home/](https://www.chromium.org/Home/)

It is worth mentioning that there is effectively no difference between the two variants and you are not missing out if you can only install the browser variant.
The desktop variant is in fact simply the aforementioned Chromium configured so as to hide the usual browser functionality and present only the embedded application.
If you get the chance to run the two variants side by side then will be able to see for yourself that they are identical.

Both variants are available from the Occam website:

[https://occam.science](https://occam.science)

Click on the 'I am not a robot' checkbox and download your preference.

Installing the browser variant will be covered first.
Simply unzip the downloaded zip file and move the unzipped 'Occam' directory to a location of your choice.
Your home directory is advised but it does not really matter as long as you have access to the directory from a terminal or command prompt.
Now open a terminal or command prompt, `cd` into the Occam directory and execute the following command:

```
npm start
```

Lastly, open a browser with the following URL:

[http://localhost:8888](http://localhost:8888)

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
If you have two instances and change the projects directory in one of them, for example, you will effectivley be changing it in the other.
Perhaps the settings can be sandboxed to particular instances in some later release but this is not the case presently so beware.

## Installing the CLI tools

CLI stands for command line interface and CLI tools are the ones that do not have a GUI, instead running directly inside a terminal or command prompt.
Occam has two, namely a package manager and called `open`; and a verifier called simply `verify`.
Installing them both is done by way of `npm` and is easy enough, although there are caveats.

The first caveat is that if you are using a unixy operating system, and this includes MacOS, then you will probably need to prepend `sudo` to the installation commands.
The reason for this is that the tools are installed globally and the directory for globally installed npm packages, is restricted.
Prepending `sudo` to the install commands therefore ensures that the installation can go ahead.
There is an argument that says that you should not use such a directory and instructions can be found on the Internet to configure `npm` to use others.
However, in all honesty, if you trust the package in question then it is not worth the bother.
It is far easier to just prepend `sudo` and have done with it.

Moving on, in order to install the `open` package manager execute the following command in a terminal or command prompt, leaving off the `sudo` as necessary:

```
sudo npm install --global occam-open-cli@latest
```

Similarly for the verifier:

```
sudo npm install --global occam-verify-cli@latest
```

You can immediately check that the verifier is installed by running the following command:

```
verify --version
```

You should see something like this:

```
Occam Verify-CLI version 0.0.645
```

You can also try the `open` package manager with the following command:

```
open --version
```

And you may, if you are fortunate, see something like this:

```
Occam Open-CLI version 6.0.9
```

If you do then you can safely skip to the next section.
Otherwise if you see an error then the second caveat applies to you and you will have to read on.

An error occurs when there is another application called `open` that takes precedence over the `open` npm package that you have just installed.
One workaround, therefore, is to create a symbolic link to the package that ensures it takes precedence.
This may render the other application useless, however in practice this is rarely an issue.
It is, however, worth just mentioning what kinds of applications are likely to be pushed aside, so to speak, by this workaround.
In the case of MacOS the `open` CLI tool can be used to open files with their registered applications.
For example, you could open a PDF file with the system's default PUF viewer.
On other unixy systems the `open` application is likely to be a legacy graphics utility.
In either case pushing it aside will do no lasting harm.

To continue, in order to create a symbolic link you first need to know the fully qualified path to the npm global installation directory.
This is easily recovered as the first line of the output from the following command:

```
npm list --global
```

Once you have the directory to hand, you need to add an alias to your terminal or command promopt's configuration file.
Exactly what this file is depends on your system.
On MacOS it will be either the `.bashrc` or `.bash_profile` file in your home directory.
If you are not using MacOS then hopefully you will have enough knowledge of your system to know which file to edit.
Moving swiftly on, assuming that the fully qualified path of the npm global installation directory is `/usr/local/bin`, add the following line to the requisite terminal or command prompt configuration file:

```
alias open='/usr/local/lib/node_modules/occam-open-cli/open.js'
```

Obviously adjust this to match your own npm global installation directory.
Save the file and if you open a new terminal or command prompt then the `open` package manager should now be ready to use.

With hindsight perhaps `open` was not the best name to choose for Occam's package manager.
Hopefully the above workaround has not caused too many difficulties.

## Opening, viewing and verifying packages and projects

With the IDE and `open` package manager to hand you are ready to start looking at some Occam packages and projects.
To begin with, create a projects directory.
You can call it what you like but here it will be called 'Projects'.
By the way, projects and packages tend to sit side by side in the same diretory with Occam.
To continue, when you have created the projects directory, open a terminal or command prompt and `cd` into it:

```
cd Projects
```

Then initialise the `open` package manager with the following command:

```
open initialise
```

This creates a hidden configuration file which under normal circumstances you should not need to touch.

Next, open some packages with the following command:

```
open material-conditional
```

Several packages will be opened, in fact, the last of which will be the `material-conditional` package.
Next, in order to find out the fully qualified path of the projects directory use the following command, which stands for present working dfirectory:

```
pwd
```

Make a note of the fully qualified path and launch the IDE.
Near to the top left you will see a projects path input field.
Type in the fully qualified path of the projects directory and hit return or click on the refresh button immediately to the right of the input field.
You will see the packages appear in the projects pane on the left.
Note the small padlocks on the folder icons, which tell you that these are packages and not project directories.
It is perhaps not worth going into too much detail in this chapter about what the various files and directories contain, but do at least take a few moments to click around, so to speak.
One thing you will notice is that all of the files are read only.
This is to be expected given that these are packages and not projects.

Before opening any projects, delete the existing packages.
In order to do so, from within the projects directory run the following command if you are on Windows...

```
del /S *
```

...or the followinog command if you are on unixy systems:

```
rm -rf *
```

Double check that all of the packages have been removed by returning to the IDE and clicking the refresh button.

Now run the following command in the projects directory:

```
open clone peano-axioms
```

This time you will be prompted to clone all of the depdencies.
If you type 'y' and hit return then `open` will clone the underlying projects for the packages rather than just downloading the packages themselves.
It leverages Git in order to do this, which is why you need Git installed even at this relatively early stage.
Return to the IDE and click the refresh button again.
You will see the newly created project directories, without padlocks this time.
You will also note that all of the files are editable.

Lastly, have a go at verifying the `peano-axioms` project.
Because it has already been published and because you have downloaded all of the dependencies as well as the project itself, it should verify without a hitch.
To check this, run the following command:

```
verify peano-axioms
```

If all goes well then you should see the last ten lines of the output, something like this:

```
INFO: peano-axioms/theorems.fls (91) - Verified the 'successor(n) = zero' supposition.
INFO: peano-axioms/theorems.fls (93) - Verified the 'zero = successor(n)' statement as an equality.
INFO: peano-axioms/theorems.fls (93) - Verified the 'zero = successor(n)' unqualified statement.
INFO: peano-axioms/theorems.fls (95) - Verified the 'zero:NonZeroNaturalNumber' qualified statement.
INFO: peano-axioms/theorems.fls (96) - Verified the '(successor(n) = zero) ⇒ zero:NonZeroNaturalNumber' qualified statement.
INFO: peano-axioms/theorems.fls (97) - Verified the '¬(zero:NonZeroNaturalNumber)' qualified statement.
INFO: peano-axioms/theorems.fls (99) - Verified the '¬(successor(n) = zero)' qualified statement.
INFO: peano-axioms/theorems.fls (82-99) - Verified the 'P8' theorem.
INFO: Verified the 'peano-axioms/theorems.fls' file.
INFO: Verified  'peano-axioms'.
```

To see the last one hundred lines of output, run the following command:

```
verify --tail=100 peano-axioms
```

Lastly, if you would like to follow the output as the verifier does its work, run the following command:

```
verify --follow peano-axioms
```

There will be several hundred lines of output in this case because the verifier has to verify not just the `peano-axioms` project but all the projects it depends on.
To bring this chapter to a close, therefore, remove all but the `peano-axioms` project and open its dependencies as packages rather than projects.
Afterwards, when you verify the `peano-axioms` project the verifier will work much more quickly.
