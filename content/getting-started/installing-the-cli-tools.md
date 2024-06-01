## Installing the CLI tools

CLI stands for command line interface.
CLI tools are the ones that do not have a GUI, instead running directly inside a terminal or command prompt.
Occam has two, namely a package manager and called `open`; and a verifier called simply `verify`.
Installing them both is done by way of `npm` and is easy enough, although there are caveats.

The first caveat is that if you are using a unixy operating system, and this includes MacOS, then you will probably need to prepend `sudo` to the installation commands.
The reason for this is that the tools are installed globally and the directory for globally installed npm packages is restricted.
Prepending `sudo` to the install commands therefore ensures that the installation can go ahead.
There is an argument that says that you should not use such a directory and instructions can be found on the Internet to configure `npm` to use others.
However, in all honesty, if you trust the package in question then it is not worth the bother.
It is far easier to just prepend `sudo` and have done with it.

Moving on, in order to install the `open` package manager execute the following command in a terminal or command prompt, leaving off the `sudo` as necessary:

```
sudo npm install --global occam-open-cli\@latest
```

Similarly for the verifier:

```
sudo npm install --global occam-verify-cli\@latest
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
Occam Open-CLI version 6\.0\.9
```

If you do then you can safely skip to the next section.
Otherwise, if you see an error then the second caveat applies to you and you will have to read on.

An error occurs when there is another application called `open` that takes precedence over the `open` npm package that you have just installed.
One workaround is to create a symbolic link to the package in order to ensure that it takes precedence.
This may render the other application useless, but in practice this is rarely an issue.
It is worth briefly mentioning what kinds of applications are likely to be pushed aside by this workaround, however.
In the case of MacOS, the native `open` CLI tool can be used to open files with their registered applications.
For example, you could open a PDF file with the system's default PUF viewer.
On other unixy systems the native `open` application is likely to be a legacy graphics utility.
In either case, temporarily pushing it to one side will do no lasting harm.

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
