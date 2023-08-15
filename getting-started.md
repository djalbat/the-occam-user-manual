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

It goes without saying then that in order to use Occam you will need to have Node installed on your local machine.
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

The only other software that needs to be installed in order to use Occam is Git.
Git is version control software and was invented by Linus Torvalds, of Linux fame.
It revolutionised version control and indeed developer and team workflows and thereby productivity immediately upon release and has become ubiquitious since.
Alongside Git came the GitHub website that enabled developers to share their code with the wider community and, as an aside, along with Markdown could be said to have reinvgurated readme files.
If they were ever vigorous in the first place, that is.
You can at a pinch get away without installing Git, at least initially, but if you are going to do any serious work with Occam then you will need it.
Occams own package manager leverages Git, for example, and the Open Mathematics site allows for GitHub integration.













