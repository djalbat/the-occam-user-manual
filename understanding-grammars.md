# Understanding Grammars

Occam's grammars functionality is one of its strong points but what exactly is a grammar, at least in Occam's parlance?
A grammar can loosely be described as that which is needed in order to describe and work with a language.
More specifically, it can be comprised of three parts:

1. A collection of symbols or characters that are the smallest elements of the language. 
These symbols or characters are more often than not considered synonymous with the glyphs that represent them.
In our case a sequence of such characters is what comprises the content of a document or file.

2. A set of rules, usually based on regular expressions,[^3] to collect these characters into larger elements, called tokens or lexemes.
We tend to envisage a sequence of characters as continuous rather than discrete and therefore tend to think of these rules as chopping up the content, so to speak.
This process is called lexing or tokenising and we stick to the latter.

3. Another set of rules, more high level, that are responsible for organising these tokens into larger elements.
In the case of natural language these would be phrases, sentences, paragraphs and so on.
This process is called parsing the tokens or, by extension, the content
The resulting structure is usually called an abstract syntax tree or AST for short.
We call it a parse tree, however.

Lastly, not part of this list but equally important is the way in which the parse tree and the tokens themselves are utilised and sometimes maninpulated.
We cover this practice in this chapter, too.

## Language flexibility and extensibility

Consider the following variable declaration written in Occam's default language, called Florence:

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

Now consider the same variable declaration but written in a controlled natural language, or CNL for short.
Occam does not natively support this language as yet but will do so in the future.
It can be created using the grammars sandbox that is the subject of the next chapter, however:

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

Note that exactly the same information can be extracted from this parse tree as from the previous one, even though the language has changed.
The verifier would be able to ascertain that this is indeed a variable declaration from the topmost `variableDeclaration` node, for example, just as before.
Similarly it could also ascertain that the variable is called `n` and that its type is `ℕ`.

In essence, in fact, the parse trees would appear to be identical to the verifier, since it ignores elements that were not pertinent.
The `Variable` keyword in the Florence parse tree would be ignored, for example, or the `Let`, `be` and `a` keywordds in the CNL parse tree.

In summary, for all intents and purposes the Flroence and CNL languages will appear to be identical to the verifier and not just for varaible declarations but everything.
Furthermore, it should be clear that the natural language parts of CNL can be akin to any natural language, it does not have to be English.
This flexibility with languages is an important feature of Occam.

Occam also allows languages to be extended.
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
This is the fallback or last resort of the grammar, so to speak, if the metastatement cannot be parsed in a more meaningful way.

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

Next, we augment the `metastatement` rule in the grammar to include metastatements of the requisite form:

```
metastatement ::= metavariable "⇒" metavariable ;
```

As a result of these changes we get a `metastatement` node, not just a `nonsense` one:

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

What this means in practice is not just a more sensical parse tree.
With this rule now working, so to speak, its premises and conclusion can be matched to other metastatements and statements in derivations by the verifier.
This means that whereas before augmenting the grammar the verifier would have fallen over when encountering this rule, now it would be able to continue.

Indeed it could be said that about half the job of verification is getting content to parse by way of extening Occam's in-built grammars.
As mentioned earlier, there is a grammars sandbox to help you with this work.
Therefore like Occam's flexibility with languages, extensibility is also an important feature.

## Unicode

The first of the points at the beginning of this chapter suggested that any grammar needs a collection of characters or symbols.
In Occam's case this is Unicode, a near ubiliquitous standard that encompasses close to 150,000 characters to date and has the potential to support over a million.
These characters are organised across various planes, namely the basic multilingual plane, or BNP for short, and sixteen so-called astral planes.
For example, the aforementioned double-struck `ℕ` character, being regularly used in mathematical texts, can be found in the basic multilingual plane.
On the other hand the `𝔸` character, being far less common, is relegated to an astral plane.
In practice the position of a Unicode character, called its code point, is immaterial.
As mentioned in the previous chapter, the Occam IDE has a Unicode picker to enable you to pick from a large selection of Unicode characters without knowing their code points.
Finally mention should go the JuliaMono typeface,[^1] which is used in the editor and which has support for thousands of Unicode characters.

## Tokenising content with lexers

There are several lexers to be found in the Occam grammars package.[^2]
In reality these are all the same lexer but configured slightly differently.

In essence the lexer is a state machine having two states, namely 'in comment' and 'not in comment'.
Depending on these states it uses a different sequence of both in-b⨶and optionally user defined rules in order to tokenise content.
The order in which the rules are executed matters.
Comments must be picked out before string literals, for example.

In fact, it is more apt to say that there really is only one lexer, it is just that it is more handily configured at a low level when compared to the parser.
To be precise, a `CommonLexer` class is extended with divers static properties which essentially dictate its behaviour.
For example, a particular lexer might pick out C-style comments as opposed to Perl-style ones, or it might not pick out comments at all.
Simiarly it might pick out string literals or, again, it might not.

As well as picking out verious types of token, the lexer distinguishes between two kinds of token, namely significant and non-significant.
Significant tokens will be picked up by the parser further down the line whereas non-significant tokens are largely ignored.
There are subtleties in this, however, which we will come to later on.
One worth mentioning now however is that end of line tokens can be either significant or non-significant depending on the particular lexer's configuration.

Thus the configuration of any lexer comprises a number of in-built properties to do with comments, literals and the like together with an optional sequence of user defined rules.
These rules are defined by so-called lexical entries in JSON form, where are mappings of token types to the regular expression patterns that pick them out.
For example, here are the entries for the plain text lexer:

```
[
  {
    "alpha-numeric": "^[a-zA-Z0-9]+"
  },
  {
    "punctuation": "^[@,\\.\"'`]+"
  },
  {
    "unassigned": "^[^\\s]+"
  }
]
```

The rules that result are used to attempt to tokenise the content should all the plain text lexer's in-built rules fail to do so and they are tried in order from top to bottom.
Note that all of hte regular expression patterns start with the `^` caret symbol which matches the start of the content.
Thus we envisage the lexer as eating up the content from left to right, so to speak.
This is always the case.

One other thing to note is that the last user-defined rule will match anything but whitespace.
Given that a prior in-built rule will have already matched any whitespace this all but guarantees that the plain text lexer will cope with just about anything.
We call this robustness and come back to this important property of both lexers and pareers in a later section.

Perhaps this is too much detail but what is important to stress is that there are in-built rules which come first and that the configuration of any lexer can be augmented with user-defined rules defined by what we call lexical entries.
To make this all a bit more concrete, recall that we augmented Occam's Florence grammar in order to pick out the `⇒` implication symbol as an operator token.
This would have meant an addtional lexical entry along the lines of the following:

```
{
  "operator": "^⇒"
}
```

This is in fact exactly what happens under the hood.

## Parsing tokens with parsers

Like the lexers, there are several parsers to be found in the Occam grammars package.[^2]
And again like the lexers, these are all in fact the same common parser but configured differently in each case. 
Specifically, a `CommonParser` class is extended for each grammar although, unlike the lexers, there are no other specific properties or in-built rules.
Effectively the only thing that differentiates these parsers is the BNF[^4] associated with each, in fact.

It is worth a moment to look at BNF in more detail.
Imagine you want to parse an arithmetic expression.
You would require something like the following rules at least.

An arithmetic expression can be...

1. another arithmetic expression enclosed in brackets,
2. two other arithmetic expressions separated by a binary operator,
3. a number.

Furthermore we would have to define two other rules:

4. An operator is an addition, subtraction, division or multiplication symbol.
5. A number is a series of one or more decimal digits.

Such natural language specifications are both cumbersome and ambiguous.
All BNF does is make this all precise:

```

  expression :: "(" expression ")"

              | expression operator expression

              | number

              ;

   operator ::= "+" | "-" | "÷" | "×" ;

     number ::= /\d+/ ;

```

There are a couple of further to note.
Firstly, the `number` rule makes use of a regular expression in its definition.
Secondly, two of the definitions in the `expression` rule are recursive, in fact the second is what is called left recursive.
We shall come back to this later.

It is not going too far to claim that not only is this specification clearer than the natural language one by far but that it could have been given with no prior explanation at all.
Such is BNF's great utility, if employed with common sense.

We end this section with a brief description of how Occam's parser works.
There is no need for a deep understanding but having at least a passing familiarity with the process may avoid frustration later on.
So, Occam's parser is what is known as a top-down parser.
Its goal is to evaluate the starting rule, which by default is usually the first rule, parse all of the tokens it is given and then terminate.
It evaluates a rule by evaluating each of its definitions in turn.
If one of a these definitions evaluates then rule evaluates and we are done.
In order to evaludate a definition all of its parts must evaluate.
Parts are generally either non-terminal, that is they simply point to a rule; or terminal, in which case they match a token.
There is a third category of parts called complex parts which are best described as in-ine rules.

It is worth a moment to imagine a top down parser, configured with the BNF above, parsing an arithmetic expression such as `(1+2)÷3`.
It should become clear why the second definition of the `expression` rule is going to create problems.
When the parser encounters this definition it will try to evaluate the `expression` rule again and if the first definition cannot be evaluated then the parser will loop indefinitely.
This problem can be alleviated by rewriting the BNF under the hood, so to speak, but it is reasonable to ask why another parser achtiteture cannot be adopted, one that is not susceptible to left recursion.
The answer is that all parser architectures are susceptible to one form of recursion or another and top down parsers are generally by far the simplest and fastest.

## The Florence grammar







[^1]: https://juliamono.netlify.app/
[^2]: https://github.com/djalbat/occam-grammars
[^3]: https://en.wikipedia.org/wiki/Regular_expression
[^4]: https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form
[^5]: https://github.com/djalbat/occam-parsers/blob/master/src/bnf/bnf.js
