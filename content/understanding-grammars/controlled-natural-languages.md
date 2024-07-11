## Controlled natural languages

Consider the following variable declaration written in Florence:

```
Variable n:ℕ
```

Here a variable named `n` is declared to be of natrual number type, represented by the double-struck `ℕ` character.
Here is the parse tree, which is what what the verifier would see, so to speak:

```
                                      variableDeclaration [0]                             
                                                 |                                        
               ---------------------------------------------------------------------
               |                      |               |              |             |      
"Variable"[primary-keyword] [0] variable [0]  ":"[special] [0]   type [0]    &lt;END_OF_LINE&gt;
                                      |                              |                    
                                "x"[name] [0]                  "ℕ"[type] [0]              
```

It should be clear from this parse tree that we have a variable declaration to hand, with the aforementioned `n` variable and `ℕ` type.
It is not too hard to imagine that the verifier can extract this information from the parse tree by traversing it somehow, and this is indeed the case.

Now consider the same variable declaration but written in a controlled natural language:

```
Let n be a variable of type ℕ.
```

Here is the resultant parse tree:

```
                                                            variableDeclaration [0]                                                              
                                                                       |                                                                         
       ---------------------------------------------------------------------------------------------------------------------------------
       |              |              |             |                 |                 |               |              |                |         
"Let"[name] [0] variable [0]  "be"[name] [0] "a"[name] [0] "variable"[name] [0] "of"[name] [0] "type"[name] [0]   type [0]    "."[unassigned] [0]
                      |                                                                                               |                          
                "n"[name] [0]                                                                                   "ℕ"[type] [0]                    
```

Note that exactly the same information can be extracted from this parse tree as from the previous one, even though the language has changed.
The verifier would be able to ascertain that this is indeed a variable declaration from the topmost `variableDeclaration` node, for example.
Similarly it could also ascertain that the variable is called `n` and that its type is `ℕ`, just as before.

In essence the parse trees would appear to be identical to the verifier, in fact, since it ignores elements that are not pertinent.
The `Variable` keyword in the Florence parse tree would be ignored, for example, or the `Let`, `be` and `a` keywordds in the controlled natural language parse tree.

In summary, for all intents and purposes the Florence language and controlled natural languages will appear to be identical to the verifier.
And not just for variable declarations but every language element.
Furthermore, it should be clear that the natural language parts of the latter could be given in any natural language, it does not have to be English.
This flexibility with languages is an important feature of Occam.
