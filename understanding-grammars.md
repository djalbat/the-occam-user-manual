# Understanding Grammars

Occam's grammars functionality is one of its strong points but what exactly is a grammar, at least in Occam's parlance?
A grammar can loosely be described as that which is needed in order to describe and work with a language.
More specifically, it can be comprised of three parts:

1. A collection of symbols or characters that are the smallest elements of the language. 
These symbols or characters are more often than not considered synonymous with the glyphs that represent them.
In our case a sequence of such characters is what comprises the content of a document or file.

2. A set of rules, usually based on regular expressions, to collect these characters into larger elements, called tokens or lexemes.
We tend to envisage a sequence of characters as continuous rather than discrete and therefore tend to think of these rules as chopping up the content, so to speak.
This process is called lexing or tokenising and we stick to the latter.

3. Another set of rules, more high level, that are responsible for organising these tokens into larger elements.
In the case of natural language these would be phrases, sentences, paragraphs and so on.
This process is called parsing the tokens or, by extension, the content
The resulting structure is usually called an abstract syntax tree or AST for short.
We call it a parse tree, however.

Lastly, not part of this list but equally important is the way in which the parse tree and the tokens themselves are utilised and sometimes maninpulated.
We cover this practice in this chapter, too.

This chapter is somewhat long and involved but nonetheless the material must be covered, because understanding grammars is essential when using Occam.
In order to justify this statement we give some examples of their utility.

## Language flexibility and extensibility

Consider the following variable declaration, written in Occam's default language, called Florence:

```
Variable n:ℕ
```

Here we are declaring a variable named `n` to be of natrual number type, represented by the double-struck `ℕ` character.
Now look at the parse tree.
This is what Occam sees or, more importantly, what the verifier would see.

```
                                      variableDeclaration [0]                             
                                                 |                                        
               ---------------------------------------------------------------------      
               |                      |               |              |             |      
"Variable"[primary-keyword] [0] variable [0]  ":"[special] [0]   type [0]    <END_OF_LINE>
                                      |                              |                    
                                "x"[name] [0]                  "ℕ"[type] [0]              
```

It should be clear from this parse tree that we have a variable declaration to hand, with the aforementioned `n` varaible and `ℕ` type.
We imagine that the verifier can extract this information from the parse tree by traversing it somehow, and this is indeed the case.

Now consider the same variable declaration but written in a different kind of language, called controlled natural language, or CNL for short.
Occam does not natively support this language as yet but will do so in the future.
It can be created using the grammar sandbox that is the subject of the next chapter, however:

```
Let x be a variable of type ℕ.
```

Here is the resultant parse tree:

```
                                                            variableDeclaration [0]                                                              
                                                                       |                                                                         
       ---------------------------------------------------------------------------------------------------------------------------------         
       |              |              |             |                 |                 |               |              |                |         
"Let"[name] [0] variable [0]  "be"[name] [0] "a"[name] [0] "variable"[name] [0] "of"[name] [0] "type"[name] [0]   type [0]    "."[unassigned] [0]
                      |                                                                                               |                          
                "x"[name] [0]                                                                                   "ℕ"[type] [0]                    
```

Note that exactly the same information can be extracted from this parse tree as from the previous one, even though the language is completely different.
The verifier would be able to ascertain that this is indeed a variable declaration from the topmost `variableDeclaration` node, for example.
Similarly it could also ascertain that the variable is called `n` and that its type is `ℕ`.

In fact, the parse trees would appear to be identical to the verifier, since it simply ignores elements that were not pertinent.
The `Variable` keyword in the Florence parse tree, for example, or the `Let`, `be` and `a` keywordds in the CNL parse tree.

In summary, for all intents and purposes the Flroence and CNL languages appear to be identical to the verifier and not just for varaible declarations but for all elements of the languages.
Furthermore, it should be clear that the natural language parts of CNL can be akin to any natural language, it does not have to be English.
This flexibility with languages is one of the things that sets Occam apart.

Occam also allows languages to be extended.
Consider the following inference rule.
Quite what an inference rule is or what this one is useful for are not important at this stage.
It is enough to know that inference rules are the building blocks of reasoning in Occam's case and that they are always user defined, never in-built:

```
Rule (ModusPonens)
  Premises
    A ⇒ B
    A
  Conclusion
    B
```

Now consider the parse tree of the first of the premises:

```
                         unqualifiedMetastatement [0]        
                                       |                     
                       --------------------------------      
                       |                              |      
                 nonsense [0]                   <END_OF_LINE>
                       |                                     
      -----------------------------------                    
      |                |                |                    
"A"[name] [0] "⇒"[unassigned] [0] "B"[name] [0]              
```

Note that it does indeed parse, but that it is being parsed as `nonsense`.
This is the fallback or last resort of the grammar, so to speak, if the statement cannot be parsed in a more meaningful way.
More details on this mechanism will follow.

To make sense of this metastatement, we first augment the grammar with a regular exprssion to pick out the `⇒` implication symbol as an operator token.
The following parse tree shows that the statement is still parses as nonsense but that this symbol is at least being recognised as an operator:

```
                       unqualifiedMetastatement [0]        
                                     |                     
                      -------------------------------      
                      |                             |      
                nonsense [0]                  <END_OF_LINE>
                      |                                    
      ---------------------------------                    
      |               |               |                    
"A"[name] [0] "⇒"[operator] [0] "B"[name] [0]              
```

Now we augment the `metastatement` rule in the grammar to include metastatements of the requisite form:

```
metastatement ::= metavariable "⇒" metavariable ;
```

Now the parse tree is more what we might expect:

```
                            unqualifiedMetastatement [0]         
                                          |                      
                          ---------------------------------      
                          |                               |      
                  metastatement [0]                 <END_OF_LINE>
                          |                                      
        ------------------------------------                     
        |                |                 |                     
metavariable [0] "⇒"[operator] [0] metavariable [0]              
        |                                  |                     
  "A"[name] [0]                      "B"[name] [0]               
```

As a result of these changes we get a `metastatement` node, not just nonsense:

```
                            unqualifiedMetastatement [0]         
                                          |                      
                          ---------------------------------      
                          |                               |      
                  metastatement [0]                 <END_OF_LINE>
                          |                                      
        ------------------------------------                     
        |                |                 |                     
metavariable [0] "⇒"[operator] [0] metavariable [0]              
        |                                  |                     
  "A"[name] [0]                      "B"[name] [0]               
```

What this means in practice is not just less nonsensical parse trees.
With this rule now working, so to speak, its premises and conclusions can be matched to other metastatements and statements in derivations by the verifier, with suitable substitutions.
This means that whereas before augmenting the grammar the verifier would have fallen over when encountering this rule, now it would be able to continue.
This extensibiliy means that not just new inference rules can be defined, but new terms, statements and so on.
Indeed it could be said that about half the job of verifying is getting the content to parse in the first place by way of extening Occam's default grammars.










