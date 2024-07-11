## Custom grammars

Occam allows languages to be extended by way of custom grammars.
Consider the following inference rule.
Quite what an inference rule is or what this one is useful for are not important at this stage:

```
Rule (ModusPonens)
  Premises
    A ⇒ B
    A
  Conclusion
    B
```

Now consider the parse tree for the first of the premises:

```
                         unqualifiedMetastatement [0]        
                                       |                     
                       --------------------------------      
                       |                              |      
                 nonsense [0]                   &lt;END_OF_LINE&gt;
                       |                                     
      -----------------------------------                    
      |                |                |                    
"A"[name] [0] "⇒"[unassigned] [0] "B"[name] [0]              
```

Note that it does indeed parse, but that it is being parsed as nonsense.
This is the fallback if the metastatement cannot be parsed in a more meaningful way.

To make sense of this metastatement, we first augment the grammar with a regular exprssion pattern that picks out the `⇒` implication character as an operator token.
The following parse tree shows the result, with the metastatement still being parsed as nonsense but with this character at least being recognised as an operator:

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

Next, we augment the `metastatement` rule in the BNF to include metastatements of the requisite form:

```
metastatement ::= metavariable "⇒" metavariable ;
```

As a result of these changes we now get a `metastatement` node instead of a `nonsense` one:

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

What this demonstrates in practice is not just a more sensical parse tree.
With this rule now working, its premises and conclusion can be matched to other metastatements and statements in derivations.
This means that whereas before augmenting the grammar the verifier would have fallen over when encountering this rule, now it would be able to continue.

Indeed it could be said that about half the job of verification is getting content to parse by way of extending Occam's in-built grammars.
As mentioned earlier, there is a grammars sandbox to help you with this work.
So, like Occam's flexibility with languages, extensibility is an important feature.
