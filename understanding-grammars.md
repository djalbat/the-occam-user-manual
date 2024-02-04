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
Why is this, and why are grammars such an integral part of Occam?
Consider the following variable declaration, written in Occam's default language, called Florence:

```
Variable n:ℕ
```

It should be clear that we are declaring a variable named `n` to be of natrual number type, represented by the double-struck `ℕ` character.
Now look at the parse tree:

```
                                      variableDeclaration [0]                             
                                                 |                                        
               ---------------------------------------------------------------------      
               |                      |               |              |             |      
"Variable"[primary-keyword] [0] variable [0]  ":"[special] [0]   type [0]    <END_OF_LINE>
                                      |                              |                    
                                "x"[name] [0]                  "ℕ"[type] [0]              
```

This is what Occam sees or, more importantly, what the verifier will see.
We can see from this parse tree that we have a variable declaration, and that this declares the aforementioned `n` varaible with type `ℕ`.
We imagine that the verifier can extract this information from the parse tree by traversing it somehow, and this is indeed the case.



