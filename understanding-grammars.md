# Understanding Grammars

Occam's grammars functionality is one of its strong points but what exactly is a grammar, at least in Occam's parlance?
A grammar can loosely be described as that which is needed in order to describe and work with a language.
More specifically, it can be comprised of three parts:

1. A collection of symbols or characters that are the smallest elements of the language. 
These symbols or characters are more often than not considered synonymous with the glyphs that represent them.
In our case a seuquence of such characters is what comprises the content of a document or file.

2. A set of rules, usually based on regular expressions, to collect these characters into larger elements, called tokens or lexemes.
We instinctively view a sequence of characters as continuous rather than discrete and therefore tend to think of these rules as chopping up the content, so to speak.
This process is called lexing or tokenising the content.
We stick to the latter.

3. Another set of rules, more high level, that are responsible for organising these tokens into larger elements.
In the case of natural language these would be phrases, sentences, paragraphs and so on.
This process is called parsing the tokens or, by extension, the content
The resulting structure is usually called an abstract syntax tree or AST for short.
We cell it a parse tree, however.

Lastly, not part of this list but equally important is the way in which the parse tree and sometimes the tokens themselves are interpreted and sometimes maninpulated.
We cover this practice in this chapter, too.

This chapter is somewhat long and involved but nonetheless it must be mastered because understanding grammars is crucial to using Occam.
Why is this? 
Why are grammars such an integral part of Occam?
Consider the following variable declaration, written in Occam's default language, called Florence:

```
Variable n:ℕ
```

It should be clear that we are declaring a variable named `n` to be of natrual number type, represented by the double-struck `ℕ` character.
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

Note that exactly the same information can be extracted from this parse tree as the previous one, even though the language is completely different.
The verifier would be able to ascertain that this is indeed a variable declaration from the topmost `variableDeclaration` node, for example.
Similarly it could also ascertain that the variable is called `n` and that its type is `ℕ`.

But this is not all.
Aside from the horizontal positions of the pertinent elements, the parse trees are essentially the same.
Both contain elements that are not ;ertinent and are thus ignored by the verifier.
The `Variable` keyword in the Florence parse tree, for example, or the `Let`, `be` and `a` keywordds in the CNL parse tree.
In fact the means by which the verifier extracts pertinent information do not change from one language to the next at all.
In summary, for all intents and purposes the Flroence and CNL languages appear to be identical to the verifier and not just for varaible declarations but for all elements of the language.
Furthermore, it should be clear that the CNL language could have been written in French, or Chinese.
This agnosticism to language is one of the things that sets Occam apart.




