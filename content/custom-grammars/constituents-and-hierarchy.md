## Constituents and hierarchy

The grammars sandbox is an invaluable tool for working with custom grammars but it is also necessary to work with them from within the IDE.
The constituent parts of custom grammars are optionally defined for each project and package and their files are viewable from within the IDE by default. 
The list has been given in an earlier chapter but here it is again:

* `type.ptn`
* `symbol.ptn`
* `operator.ptn`
* `term.bnf`
* `statement.bnf`
* `metastatement.bnf`

Thus Occam's lexers' rules for picking out type, symbol and operator tokens can be extended whilst its parsers' BNF rules for terms, statements and metastatements can also be extended.

The IDE has the facility for exporting custom grammars to the grammars sandbox.
To see it in action, open the `material-conditional` package in a fresh directory, making sure to open all of the dependencies as well:

```
open initialise
open material-conditional
```

The following packages will be opened:

* `material-conditional`
* `de-morgans-laws`
* `classical-propositional-logic`
* `intuitionistic-propositional-logic`
* `minimal-propositional-logic`

Returning to the IDE, set the projects directory to the directory containing these packages and reload.
Now click on the toolbar button second from the right in order to export the custom grammars and then go to the grammars sandbox and click the import button in the custom grammars panel.
You will see the custom grammars for these five packages imported.
Note that if you have any custom grammars already defined, such as the one needed for the motivating example, then importing will overwrite them.
Be mindful of this as there is no way of recovering them.

The order in which these custom grammars are imported is the topological ordering determined by their dependency relations.
Specifically, dependencies will always appear below their dependents.
For example, the `minimal-propositional-logic` package is a dependency of the `intuitionistic-propositional-logic` package and therefore appears below it.
By the way, if you had clicked the button to export the custom grammars with a package selected in the projects pane then only the custom grammar for that particular package together with its dependencies would have been exported.

To continue, all of these packages define meta-level concepts and so the type and symbol input fields will be empty for each of them.
Similarly for the term BNF.
On the other hand the statement and metastatement BNF will be non-empty for some of them, as will the operator pattern.
It does not matter if these concepts mean nothing to you at this stage, what is important is that you gain some fluency in clicking around, so to speak.
Speaking of unknown concepts, the default custom grammar is probably best avoided altogether at this stage.
