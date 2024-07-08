## Installation and publishing

The requirements for Highmark are the same as those for Occam so it is assumed that you have both Node and Git installed.
The Occam IDE is also essential.
As mentioned in the introduction, it does not matter if you have no interest in verification and only intend to use Occam for Highmark.
In that case this chapter is for you.

The first thing to do is to get the Highmark CLI tool installed.
This is straightforward enough:

```
sudo npm install --global highmark-cli\@latest
```

You can test the installation with the follwoing command:

```
highmark --version
```

The next thing to do is to clone this book's repository, which will serve as an example:

```
git clone git@github.com:djalbat/the-occam-user-manual.git
```

It is recommanded that you create a `Books` directory or some such to clone into.
Next, cd into this directory and run the following command:

```
highmark initialise
```

Now run the following commmand:

```
highmark --server --watch --port=7777 the-occam-user-manual
```

This will start a small web server for viewing the book.
The choice of 7777 for the port is chosen because you may be running Occam on port 8888, by the way.
You can now view the entire book at the following URL:

```
http://localhost:7777
```

It is not unreasonable to ask why it is necessary to run a web server in order to view an HTML file.
This is because web fonts are used and they cannot be viewed statically.
There is no good reason for this.
Web fonts hardly pose no more of a security threat than images, say, but historically they were singled out for this treatment and there appears to be no way around other then serving them dynamically.
The only recompense is that as a result of running a web server the browser can be refreshed when the book is published.
This is the purpose of the `watch` option.

Moving on, running the CLI tool as a web server will lock the terminal.
To stop the web server and unlock the terminal, press the command or control key together with the 'C' key in the usual manner.
Leave it running for the time being, however, and open another terminal at the some place.
In this terminal type the following command to publish the book:

```
highmark --client the-occam-user-manual
```

As already mentioned, once the book has been published the browser should refresh.
The `client` option will cause a JavaScript client to be bundled with the output HTML file in order to improve the end user experience.

