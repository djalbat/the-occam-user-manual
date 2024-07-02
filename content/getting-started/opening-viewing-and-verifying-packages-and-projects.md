## Opening, viewing and verifying packages and projects

With the IDE and `open` package manager to hand you are ready to start looking at some Occam packages and projects.
To begin with, create a projects directory.
You can call it what you like but here it will be called 'Projects'.
By the way, projects and packages tend to sit side by side in the same directory with Occam.
In particular there is no separate directory for packages.
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
Next, use the following command to find out the fully qualified path of the projects directory on Windows:

```
cd
```

...or the following on unixy systems:

```
pwd
```

Make a note of the fully qualified path and launch the IDE.
Near to the top left you will see a projects path input field.
Type in the fully qualified path of the projects directory and hit return or click on the refresh button immediately to the right of the input field.
You will see the packages appear in the projects pane on the left.
Note the small padlocks on the directory icons, which tell you that these are packages and not project directories.
It is perhaps not worth going into too much detail in this chapter about what the various files and directories contain, but do at least take a few moments to click around, so to speak.
One thing you will notice is that all of the files are read only.
This is to be expected given that these are packages and not projects.

Before opening any projects, delete the existing packages.
In order to do so, from within the projects directory run the following command if you are on Windows...

```
del /S \*
```

...or the followinog command if you are on unixy systems:

```
rm -rf \*
```

Double check that all of the packages have been removed by returning to the IDE and clicking the refresh button.

Now run the following command in the projects directory:

```
open clone peano-axioms
```

This time you will be prompted to clone all of the dependencies.
If you type 'y' and hit return then `open` will clone the underlying projects for the dependencies rather than just downloading the packages themselves.
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
Afterwards, if you verify the `peano-axioms` project then the verifier will work much more quickly.
