## A motivating example

Getting custom grammars right can often seem like the most taxing part of verification.
Fortunately there is a grammars sandbox to help you on the Occam website:

https://occam.science/

Probably the best way to begin to master custom grammars is by example, which will be developed using the grammars sandbox.
Quite what an inference rule is or what this one is useful for does not matter quite yet but consider the following rule:

```
Rule (ModusPonens)
  Premises
    A ⇒ B
    A
  Conclusion
    B
```

If you copy and paste this rule into the pretty printer in the grammars sandbox then you will see a parse tree appear below it.
Here is part of it for the first of the premises:

```
                        unqualifiedMetastatement.. [0]        
                                       |                     
                       --------------------------------      
                       |                              |      
                 nonsense [0]                   <END_OF_LINE>
                       |                                     
      -----------------------------------                    
      |                |                |                    
"A"[name] [0] "⇒"[unassigned] [0] "B"[name] [0]              
```

Note that it does indeed parse, but that it is being parsed as nonsense.
This is the fallback if the unqualified metastatement cannot be parsed in a more meaningful way.

If you want then you can copy just the premise itself into the pretty printer and set the start rule to `unqualifiedMetastatement`.
If you do so then be sure to include a carriage return after the `A ⇒ B` since the rule requires it.
Here is the rule from the Florence grammar again, in fact.
Note that the definition with a reference to the `metastatement` rule will be evaluated before the `nonsense` definition:

```
unqualifiedMetastatement..           ::=   metastatement... <END_OF_LINE> 

                                       |   nonsense... <END_OF_LINE> 
                                       
                                       ;
```

To continue, the first thing to do in order to make sense of this metastatement is to add a custom grammar.
To do so, type 'modus-ponens' or some such into the input field in the custom grammars panel.
Now click the 'Add' button and a new item representing the custom grammar will appear.
As well as a button for the name itself it has three additional buttons, the utility of which should be obvious.
Click on the name button now to activate the custom grammar.
This will enable the input field and textarea for the patterns and BNF, respectively.

Next, select 'operator' from the pattern drop down, then copy and paste the implication symbol from the pretty printer into the input field.
Immediately the parse tree should change, albeit only slightly:

```
                       unqualifiedMetastatement [0]        
                                     |                     
                      -------------------------------      
                      |                             |      
                nonsense [0]                  &lt;END_OF_LINE&gt;
                      |                                    
      ---------------------------------                    
      |               |               |                    
"A"[name] [0] "⇒"[operator] [0] "B"[name] [0]              
```

Note that the first child node of the `unqualifiedMetastatement` node is still called `nonsense`  but at least the implication symbol is now being picked out as an operator.

Finally, select 'metastatement' from the BNF drop down and type the following into the textarea immediately below.
This will augment the `metastatement` rule with a definition for parsing the implication:

```
metastatement ::= metavariable "⇒" metavariable ;
```

As a result of these changes the `nonsense` node should have changed to a `metastatement` node:

```
                            unqualifiedMetastatement [0]         
                                          |                      
                          ---------------------------------      
                          |                               |      
                  metastatement [0]                 &lt;END_OF_LINE&gt;
                          |                                      
        ------------------------------------                     
        |                |                 |                     
metavariable [0] "⇒"[operator] [0] metavariable [0]              
        |                                  |                     
  "A"[name] [0]                      "B"[name] [0]               
```

This may seem like an innocuous example but it is difficult to overstate its importance.
Without the ability to augment Occam's Florence and controlled natural language grammars in this way this rule would never be of any use.
Once it parses its premises and conclusion can be matched to other metastatements and statements in derivations.
And whereas before the verifier would have fallen over when encountering this rule, now it will be able to continue.
