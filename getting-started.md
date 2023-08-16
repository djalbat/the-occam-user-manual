# Getting started

Occam comprises several applications, sites and services, the installation instructions and further documentation for which are spread across several sites, readme files, etc.
This chapter aims to bring all this information into one place, therefore.
It is a one stop shop for getting started with Occam, so to speak.
It also provices some background on the tools and technologies behind Occam, for the curious.

All of Occam is written in JavaScript, which was invented in the mid-nineties. 
JavaScript could be said to have languished until the advent of Node.js, hereafter called just Node, in the late naughties.
Node brought several innovations to JavaScript:

* It enabled JavaScript developers to write web application servers almost trivially.
* It provided an easy to use package manager and a site where packages could be puclibhed for free and for all of the community to use.
* As well server side code, devel9pers could make use of client side libraries and write code to run in the broswer by way of a process called bundling.

Allied with continued improvements to JavaScript itself, most notably the ES6 and ES7 releases, Node resulted in an explosion in the use of JavaScript.
This was especially evidient in, but by no means restricted to, Internet appcliations.
Both JavaScript and Node continue to evolve and although both have their detractors, it is safe to say that they will be with us, and in a healthy state, for the foreseeable future.

## Prerequisites

It almost goes without saying then that in order to use Occam you will need to have Node installed on your local machine.
In fact, the chances are that it is already installed.
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
If the version that you have installed is older than this, or if you just want to install the latest version, to to the Node site here:

[https://nodejs.org/](https://nodejs.org/)

Follow the instructions for your operating system.
Node should be easy to install and no futher guideance is given here.

Installing Node will also install Node's package manager, called `npm`.
Again you can easily check that it is installed with the following command:

```
npm --version
```

If you have a relatively recent version of Node installed then the version of `npm` will also be recent enough.

The only other prerequisite is Git.
Git is version control software and was invented by Linus Torvalds, of Linux fame.
It revolutionised version control almost instantly upon its release and, as a consequence, revolutiionised developer and team workflows and thereby productivity, too.
Alongside Git came the GitHub website.
GitHub enabled developers to share their code with the wider community and, as an aside, along with Markdown it reinvgurated readme files, too.
If they were ever vigorous in the first place, that is.
You can at a pinch get away without installing Git, at least initially, but if you are going to do any serious work with Occam then you will need it.
Occam's own package manager leverages Git, for example, and the Open Mathematics site allows for GitHub integration.

Git may well already be installed on your system.
In order to check, run the following command:

```
git --version
```

Any version will do since Git has been remarkably stable since its initial release.
If you do not have Git installed or want the latest version, go to the Git website:

[https://git-scm.com/](https://git-scm.com/)

Installation should be straightforward and no further guidance is given here.

## Installing the IDE

Occam has its own IDE, or integrated development environment.
In fact Occam's CLI tools are not integrated with it as of wrirting, and therefore it is really what could be described as just a glorified collaborative text editor.
It has it uses as-is, however.
It supports Occam's vernacular, called Florence, for example, and its collaborative features are second to none.
They are based on an algorithm that is partly formalised in Occam, in fact.
It will also expand Occam's packages in its projects pane so that you can effectively browse them as projects, and it has a useful index.
All told it is worth the effort of downloading and installing it and will only improve with time.

There are two variants available, for desktop and browser.
The desktop variant currently only runs on MacOS and the browser variant is therefore provided for everyone else.
It will also run on MacOS, of course.
You must use Google Chrome or Chromium to run the browser version.
Other browsers may work but they are not supported.
If you really have an issue with Chrome then download and install Chromium which, although still Google's, does at least has the virtue of being open source:

[https://www.chromium.org/Home/](https://www.chromium.org/Home/)

It is worth pointing out that there is effectively no difference between the two variants and you are not missing out if you cannot install the desktop version.
They genuinely are the exact same application, albeit packaged in two different ways.
The desktop verion is in fact simply the aforementioned Chromium browser configured so as to hide the usual browser functionality and present only the embedded application.
If you get the chance then you can run the two side by side and will be able to see for yourself that they are identical.

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
Beyond bookmarking the URL there is nothing else to do.

To install the desktop variant, again unzip the downloaded zip file and this time drag it into the Applications directory, which should be accessible from the finder.
Now, most importantly, do not double click on Occam the icon.
Instead, right click on it and choose 'Open'.
Doing this ensures that you have a chance to configure MacOS to execute the iDE even though it is not from a trusted source.
If you simply go ahead and double click on the icon then you will have to configure MacOS manually and this process can be fiddlesome to say the least.
Once the IDE is running, right click on the icon in the dock and choose the option to keep it there.

## Installing the CLI tools

CLI stands for command line interface and CLI tools are the ones that do not have a GUI, instead running directly inside a terminal or command prompt.
Occam has two, namely a package manager modelled largely on Node's `npm` package manager and called `open`; and a verifier called simply `verify`.
Installing them both is done by way of `npm` and is easy enough, although there are caveats.

The first caveat is that if you are using a unixy operating system, and this includes MacOS, then you will probably need to prepend `sudo` to the installation commands.
The reason for this is that the tools are installed globally and the directory for globally installed npm packages, whcih is what both of these tools are, is restricted.
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
Occam Verify CLI version 0.0.645
```

You can also try the `open` package manager with the following command:

```
open --version
```

And you may, if you are fortunate, see something like this:

```
Occam Open CLI version 6.0.9
```

If you do then you can safely skip to the next section.
Otherwise if you see and error then the second caveat applies to you and you will have to read on.

Put simply, an error occurs when there is another application called `open` that takes precedence over the `open` npm package that you have just installed globally.
One workaround, therefore, is to create a symbolic link to the `open` npm package that ensures it takes precedence instead.
This effectively renders the other application useless, however in practice this is rarely an issue.
It is, however, worth just mentioning what kinds of applications are likely to be pushed aside, so to speak, by this workaround.
In the case of MacOS the `open` program can be used to open files with their registered applications.
For example, you could open a PDF file with the system's default PUF viewer.
On other unixy systems the `open` application is likely to be a legacy graphics utility.
In either case pushing it aside will do no lasting harm.

To continue, in order to create a symbolic link you first need to know the fully qualified path to the npm global installation directory.
This is easily recovered as the first line of the output from the following command:

```
npm list --global
```

Once you have the directory to hand, you need to add an alias to your terminal or command promopt's configuration file.
Exactly what this file is dependes on your system.
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

## Opening and viewing packages and projects

With the IDE and `open` package manager to hand you are ready to start looking at some Occam packages and projects.
To begin with, create a dedeicated directory.
You can call it what you will but for the sake of an example it will be called 'Projects' here.
By the way, projects and packages tend to sit side by side in the same diretory with Occam.
When you have created the directory, open a terminal or command prompt and `cd` into it:

```
cd Projects
```

Then initialise the `open` package manager with the following command:

```
open initialise
```

This creates a hidden configuration file which under normal circumstances you should not need to touch.

Next, download some packages with the following command:

```
open material-conditional
```

Several packages will be opened, in fact, the last of which will be the `material-conditional` package.
Next, you need to find out the fully qualified path of the projects directory.
On Winodws systems the following command will return it:

```
cd
```

On unixy systems, includimg MacOS, the following command, which stnads for present working dfirectory, will do:

```
pwd
```

Make a note of this path and run the IDE.
Near to the top left you will see a projects input field.
Type the path in here and hit return or click on the refresh button immediately to the right.
