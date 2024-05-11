## Language flexibility and extensibility

Consider the following variable declaration written in Occam's default language, called Florence:

```
Variable n:ℕ
```

Here we are declaring a variable named `n` to be of natrual number type, represented by the double-struck `\ℕ` character.
Now look at the parse tree. This is what what the verifier would see, so to speak:

```
                                      variableDeclaration [0]                             
                                                 |                                        
               ---------------------------------------------------------------------
               |                      |               |              |             |      
"Variable"[primary-keyword] [0] variable [0]  ":"[special] [0]   type [0]    &lt;END_OF_LINE&gt;
                                      |                              |                    
                                "x"[name] [0]                  "\ℕ"[type] [0]              
```

It should be clear from this parse tree that we have a variable declaration to hand, with the aforementioned `n` varaible and `\ℕ` type.
It is not too hard to imagine that the verifier can extract this information from the parse tree by traversing it somehow, and this is indeed the case.

Now consider the same variable declaration but written in a controlled natural language, or CNL for short.
Occam does not natively support this language as yet but will do so in the future.
For the moment it can be created using the grammars sandbox that is the subject of the next chapter:

```
Let x be a variable of type \ℕ.
```

Here is the resultant parse tree:

```
                                                            variableDeclaration [0]                                                              
                                                                       |                                                                         
       ---------------------------------------------------------------------------------------------------------------------------------
       |              |              |             |                 |                 |               |              |                |         
"Let"[name] [0] variable [0]  "be"[name] [0] "a"[name] [0] "variable"[name] [0] "of"[name] [0] "type"[name] [0]   type [0]    "."[unassigned] [0]
                      |                                                                                               |                          
                "x"[name] [0]                                                                                   "\ℕ"[type] [0]                    
```

Note that exactly the same information can be extracted from this parse tree as from the previous one, even though the language has changed.
The verifier would be able to ascertain that this is indeed a variable declaration from the topmost `variableDeclaration` node, for example.
Similarly it could also ascertain that the variable is called `n` and that its type is `\ℕ`, just as before.

In essence the parse trees would appear to be identical to the verifier, in fact, since it ignores elements that were not pertinent.
The `Variable` keyword in the Florence parse tree would be ignored, for example, or the `Let`, `be` and `a` keywordds in the CNL parse tree.

In summary, for all intents and purposes the Flroence and CNL languages will appear to be identical to the verifier and not just for varaible declarations but every pertinent language element.
Furthermore, it should be clear that the natural language parts of CNL can be akin to any natural language, it does not have to be English.
This flexibility with languages is an important feature of Occam.

Occam also allows languages to be extended.
Consider the following inference rule.
Quite what an inference rule is or what this one is useful for are not important at this stage, by the way:

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

To make sense of this metastatement, we first augment the grammar with a regular exprssion pattern that picks out the `\⇒` implication character as an operator token.
The following parse tree shows that the metastatement still parses as nonsense but that this character is at least being recognised as an operator:

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
metastatement ::= metavariable "\⇒" metavariable ;
```

As a result of these changes we get a `metastatement` node instead of a `nonsense` one:

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

What this means in practice is not just a more sensical parse tree.
With this rule now working its premises and conclusion can be matched to other metastatements and statements in derivations by the verifier.
This means that whereas before augmenting the grammar the verifier would have fallen over when encountering this rule, now it would be able to continue.

Indeed it could be said that about half the job of verification is getting content to parse by way of extening Occam's in-built grammars.
As mentioned earlier, there is a grammars sandbox to help you with this work.
So like Occam's flexibility with languages, extensibility is an important feature.
