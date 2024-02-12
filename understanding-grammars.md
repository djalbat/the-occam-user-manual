# Understanding Grammars

Occam's grammars functionality is one of its strongest suits but what exactly is a grammar, at least in Occam's parlance?
A grammar can loosely be described as that which is needed to describe and work with a language.
More specifically, it can be thought of as comprising three parts:

1. A collection of symbols or characters that are the smallest elements of the language. 
These symbols or characters are usually viscerally synonymous with the glyphs that represent them.
In our case a sequence of such characters is what comprises the content of a document or file.

2. A set of rules, usually based on regular expressions,[^3] to collect these characters into larger elements, called tokens or lexemes.
We tend to envisage a sequence of characters as continuous rather than discrete, however, and therefore tend to think of these rules as chopping up the content rather than gathering it.
This process is called lexing or tokenising and we stick with the latter.

3. Another set of rules, written in BNF,[^4] that are responsible for organising these tokens into larger elements.
In the case of a natural language these would be phrases, sentences, paragraphs and so on.
This process is called parsing the tokens or, by extension, the content
The resulting structure is usually called an abstract syntax tree or AST for short.
We call it a parse tree, however.

## Language flexibility and extensibility

Consider the following variable declaration written in Occam's default language, called Florence:

```
Variable n:ℕ
```

Here we are declaring a variable named `n` to be of natrual number type, represented by the double-struck `ℕ` character.
Now look at the parse tree.
This is what what the verifier would see, so to speak.

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
It is not too hard to imagine that the verifier can extract this information from the parse tree by traversing it somehow, and this is indeed the case.

Now consider the same variable declaration but written in a controlled natural language, or CNL for short.
Occam does not natively support this language as yet but will do so in the future.
For the moment it can be created using the grammars sandbox that is the subject of the next chapter:

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
The verifier would be able to ascertain that this is indeed a variable declaration from the topmost `variableDeclaration` node, for example.
Similarly it could also ascertain that the variable is called `n` and that its type is `ℕ`, just as before.

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
                 nonsense [0]                   <END_OF_LINE>
                       |                                     
      -----------------------------------                    
      |                |                |                    
"A"[name] [0] "⇒"[unassigned] [0] "B"[name] [0]              
```

Note that it does indeed parse, but that it is being parsed as nonsense.
This is the fallback if the metastatement cannot be parsed in a more meaningful way.

To make sense of this metastatement, we first augment the grammar with a regular exprssion pattern that picks out the `⇒` implication character as an operator token.
The following parse tree shows that the metastatement still parses as nonsense but that this character is at least being recognised as an operator:

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

Next, we augment the `metastatement` rule in the BNF to include metastatements of the requisite form:

```
metastatement ::= metavariable "⇒" metavariable ;
```

As a result of these changes we get a `metastatement` node instead of a `nonsense` one:

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
With this rule now working its premises and conclusion can be matched to other metastatements and statements in derivations by the verifier.
This means that whereas before augmenting the grammar the verifier would have fallen over when encountering this rule, now it would be able to continue.

Indeed it could be said that about half the job of verification is getting content to parse by way of extening Occam's in-built grammars.
As mentioned earlier, there is a grammars sandbox to help you with this work.
So like Occam's flexibility with languages, extensibility is an important feature.

## Unicode

The first of the points at the beginning of this chapter suggested that any grammar needs a collection of characters or symbols.
In Occam's case this is Unicode, a near ubiliquitous standard that encompasses close to 150,000 characters to date and has the potential to support over a million.
These characters are organised across various planes, namely the basic multilingual plane, or BNP for short, together with sixteen so-called astral planes.
For example, the aforementioned double-struck `ℕ` character, being regularly used in mathematical texts, can be found in the basic multilingual plane.
On the other hand the `𝔸` character, being far less common, is relegated to an astral plane.
In practice the position of a Unicode character, called its code point, is immaterial.
As mentioned in the previous chapter, the Occam IDE has a Unicode picker to enable you to pick from a large selection of Unicode characters without knowing their code points.
Mention should also go the JuliaMono typeface,[^1] which is used in the editor and which has support for thousands of Unicode characters.

## Tokenising content with lexers

There are several lexers to be found in the Occam grammars package.[^2]
In fact these are all the same lexer but configured slightly differently.

In essence Occam's lexer is a state machine having two states, namely 'in comment' and 'not in comment'.
Depending on these states it uses a different sequence of both in-built and user defined rules to tokenise content.
The order in which the rules are executed matters.
Comments must be picked out before string literals, for example.

For each of the grammars a `CommonLexer` class is extended with divers static properties which essentially define its in-built rules.
For example, a particular lexer might pick out C-style comments as opposed to Perl-style ones, or it might not pick out comments at all.
Simiarly it might pick out string literals or, again, it might not.

As well as picking out verious types of token, lexers distinguish between two kinds of token, namely significant and non-significant tokens.
Significant tokens will be picked up by the parser further down the line whereas non-significant tokens are largely ignored.
There are subtleties in this, however, which we will come to later on.
One worth mentioning now however is that end of line tokens can be either significant or non-significant depending on the particular lexer's configuration.

Unlike a lexer's in-built rules, its user defined rules are defined by so-called lexical entries in JSON form.
These are essentially mappings of token types to the regular expression patterns that match them.
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

User defined rules are tried should the lexer's in-built rules fail to match the content and they are tried in order from top to bottom.
Note that all of hte regular expression patterns start with the `^` caret character which matches the start of the content.
Thus it is reasonable to envisage the lexer as consuming the content from left to right.

One other thing to note is that the last user-defined rule will match anything but whitespace.
Given that a prior in-built rule will have already matched any whitespace this guarantees that the plain text lexer will cope with any input.
We call this robustness and come back to this important property of both lexers and pareers in a later section.

## Parsing tokens with parsers

Like the lexers, there are several parsers to be found in the Occam grammars package.[^2]
And again like the lexers, these are all in fact the same common parser but configured differently in each case. 
Specifically, a `CommonParser` class is extended for each grammar although, unlike the lexers, there are no other specific properties or in-built rules.
The only thing that differentiates each parser is its associated BNF.

It is worth a moment to look at BNF in more detail.
Imagine you want to parse an arithmetic expression.
You would require something like the following rules at least...

An arithmetic expression can be:

1. Another arithmetic expression enclosed in brackets,
2. two other arithmetic expressions separated by a binary operator,
3. a number.

Furthermore we would have to define two other rules:

4. An operator is an addition, subtraction, division or multiplication character.
5. A number is a series of one or more decimal digits.

Such natural language specifications are both cumbersome and ambiguous, however.
All BNF does is make all of this precise:

```
expression :: "(" expression ")"

            | expression operator expression

            | number

            ;

 operator ::= "+" | "-" | "÷" | "×" ;

   number ::= /\d+/ ;
```

It is not going too far to claim that not only are the above rules clearer than their natural language counterparts but that they could have been given with no prior explanation at all.
Such is BNF's great utility, if employed with common sense.

We end this section with a brief description of how Occam's parser works.
There is no need for a deep understanding but having at least a passing familiarity with the process may avoid frustration later on.
So, Occam's parser is what is known as a top-down parser.
Its goal is to evaluate the start rule, which is usually the first rule, during the process of which all of the tokens should be consumed.
It evaluates a rule by evaluating each of its definitions in turn.
If one of a these definitions evaluates then rule evaluates and we are done.
In order to evaludate a definition all of its parts must evaluate.
Parts are generally either non-terminal, that is they simply point to a rule; or terminal, in which case they match a token.
There is a third category of parts called complex parts which are perhaps best described as in-ine rules.

It is worth a moment to imagine a top down parser, configured with the BNF above, parsing an arithmetic expression such as `(1+2)÷3`.
It should become clear why the second definition of the `expression` rule is going to create problems.
When the parser encounters this definition it will try to evaluate the `expression` rule again and if the first definition cannot be evaluated then the parser will loop indefinitely.
This problem can be alleviated by rewriting the BNF under the hood but it is reasonable to ask why another parser achtiteture cannot be adopted, one that is not susceptible to left recursion.
The answer is that all parser architectures are susceptible to one form of recursion or another and top down parsers are generally by far the simplest and fastest.
We come back to this particular form of recursion, called left recursion, later on.

## The Florence grammar

Some familiarity with the Florence grammar is helpful and so we look at its constituent parts now. 
Here is the definition of the `FlorenceLexer` class:

```
class FlorenceLexer extends CommonLexer {
  ...
  static EndOfLineToken = EndOfLineSignificantToken;

  static WhitespaceToken = WhitespaceToken;

  static RegularExpressionToken = null;

  static EndOfLineCommentToken = EndOfLineCommentSignificantToken;

  static SingleLineCommentToken = PythonStyleSingleLineCommentToken;

  static EndOfMultiLineCommentToken = PythonStyleEndOfMultiLineCommentToken; 

  static StartOfMultiLineCommentToken = PythonStyleStartOfMultiLineCommentToken; 

  static MiddleOfMultiLineCommentToken = PythonStyleMiddleOfMultiLineCommentToken; 

  static SinglyQuotedStringLiteralToken = null;

  static DoublyQuotedStringLiteralToken = DoublyQuotedStringLiteralToken;
}
```

Note that end of line tokens are significant, like YAML or Python but unlike JSON or Java. 
Note also that both single and multiple line Python style comments are supported. 
And lastly note that doubly quoted string literals are preferred to singly quoted ones and that regular expression literals are not supported.
These properties define the in-built rules and in addition to these we have the following lexical entries for the user defined rules.
The regular expression pattern for the `primary-keyword` entry has been abridged, by the way:

```
[
  {
    "special": "^(?:,|::|:|=|\\(|\\)|\\[|\\]|\\.\\.\\.)"
  },
  {
    "primary-keyword": "^(?:Rule|Axiom|Theorem|Lemma|Conjecture|Metalemma|Metatheorem|Premises|Premise|Conclusion|Proof...)\\b"
  },
  {
    "secondary-keyword": "^(?:from|by)\\b"
  },
  {
    "meta-type": "^(?:Statement|Context)\\b"
  },
  {
    "name": "^[A-Za-zΑ-Ωα-ω][A-Za-zΑ-Ωα-ω_0-9]*"
  },
  {
    "unassigned": "^[^\\s]+"
  }
]
```

Note that the regular expression pattern for the last `unassigned` token type will match anything but whitespace.
In fact again we make the point, as we did with the plain text lexer, that since a prior in-built rule will have already matched any whitespace this guarantees that the Florence lexer will cope with any input.

Here is the abridged top-level part of the BNF for the parser:

```
document                             ::=   ( topLevelDeclaration | verticalSpace | error )+ ;

topLevelDeclaration                  ::=   typeDeclaration 
                                           
                                       |   variableDeclaration 

                                       ...                                           
                                           
                                       |   rule 

                                       |   axiom 

                                       |   lemma 

                                       |   theorem 

                                       |   conjecture 

                                       |   metalemma 

                                       |   metatheorem 

                                       ;

verticalSpace                        ::=   <END_OF_LINE>+ ;

error                                ::=   . ;
```

There are some points to note here, too.
Firstly, the `verticalSpace` rule matches one or more end of line tokens.
Recall that the Florence lexer is configured to treat such tokens as significant, hence they can be referenced here.
Also, the `document` rule's definition has a complex part which stipulates one or more of a choice of three parts.
These will be evaluated in sequence and therefore the `error` rule provides the required fallback functionality.
Its single definition has only one wildcard part `.` that will match any significant token, as its name suggests.
Thus Occam's parsers can be said to be robust, in a similar vein to its lexers, in the sense that they will cope with any input.
Robustness is picked up again in the later section on ambiguity.

Here is part of the mid-level BNF:

```
unqualifiedMetastatement!            ::=   metastatement... <END_OF_LINE> 

                                       |   nonsense... <END_OF_LINE> 
                                       
                                       ;

qualifiedMetastatement!              ::=   metastatement... qualification <END_OF_LINE> 

                                       |   nonsense... qualification <END_OF_LINE> 
                                        
                                       ;

...                                       

qualification                        ::=   ( "by" | "from" ) reference ;

nonsense                             ::=   ( [type] | [symbol] | [operator] | [special] | [secondary-keyword] | [meta-type] | [name] | [unassigned] )+ ;
```

Since ambiguity is being treated later we will pass over the fact that each of the first two rules have two definitions and the use of the exclamation mark after these rules' names.
Instead we focus on the ellipsis `...` modifier on each of the rule name parts.
This switches the parser into what is called a look-ahead state, where it takes note of the part that follows the look-ahead part when evaluating the look-ahead part itself.
This is useful because the `nonsense` rule if left to its own devices would parse a qualification, since it parses one or more tokens of pretty much any type.
If it can be made to look ahead, however, it will stop before the qualification thus allowing the parser to continue to evaluate the `qualification` part of the definition.

It is not unreasonable to ask why this look-ahead state is not the default state of the parser, given its obvious utility.
Ths answer is that it slows the parser down considerably.
On one hand in its normal state the parser will parse a sequence of tokens in time roughly linearly proportional to the sequence's length.
On the other hand in its look-ahead state, although no detailed profiling has ever been done, it seems most likely that the time is likely to be if not expoenentially then at least polynomially proportional.
Thus although a look-ahead state was a necessity when designing the parser, it is used throughout all of Occam's grammars with considerable caution.

We bring this section to a close with mention of custom grammars.
These are the subject of the next chapter but because they augment the Florence grammar, it makes sense to at least mention the default custom grammar here.
This grammar completes the Florence grammar with additional regular expression patterns for the lexer and additional rules for the parser.
Here are the regular expression patterns, for the `type` and `symbol` and `operator` token types, with the second of these being empty:

```
typePattern = "Object";

symbolPattern = "";

operatorPattern = "⊧|is|for|omits|contains|undefined";
```

Note that the `operatorPattern` regular expression pattern would have been augmented with the implication character earlier.

And here are the abridged BNF rules:

```
term!                                ::=   variable ;

statement!                           ::=   "(" metaArgument ")" 
                                                  
                                       |   equality

                                       |   typeAssertion 
                                                  
                                       |   undefinedAssertion

                                       ;
                                       
equality                             ::=   argument "=" argument ;

typeAssertion                        ::=   term ":" type ;

undefinedAssertion                   ::=   variable "is" "undefined" ;

metastatement!                       ::=   "(" metastatement ")" 
           
                                       ...
                                        
                                       ;

...
```

These are a bit more convoluted but note the presence of the `metastatement` rule which again would have been augmented earlier.

## Ambiguity

Recall that all of both Occam's lexers and parsers are configured to be robust in the sense that they will cope with any input.
In the case of the lexers, robustness is guaranteed by an in-built rule that matches whitespace together with a last user defined `unassigned` rule that matches anything but whitespace.
In the case of the parsers, robusteness is guaranteed by an `error` rule that is always given as the last choice in the singular definitions of start rules.

Thus robustness is guaranteed by ambiguity.
Under normal circumstances there should be no unassigned tokens or error nodes, but nonetheless all of the content can be tokenised as whiteapce and unassigned tokens and parsed as error nodes.
So there are always at least two sequences of tokens and two parse trees for any input.

Ambiguity is considered unacceptable from a theoretical standpoint but what would happen were it not built in to all of Occam's grammars?
If we wanted to guarantee robustness for the lexers then we would have to hard code an in-built rule to run after the user defined rules expressly for the purposes of catching any content not matched beforehand.
But this is precisely what the `unassinged` rule does.
Simimlarly, if we wanted to guarantee robustness for the parsers then we would have to engineer them in such a way as to default to an error node somehow should no other nodes be possible.
This approach was attempted early on in development, in fact, but it was abandoned as it compllicated the parser enormously.
In the end any attempt to solve the problem of robustness programmatically simply simulates these `unassigned` and `error` rules, often at considerable programmatic cost.
Thus the kind of ambiguity brought about by unassigned tokens and error nodes is unavoidable in lexers and parsers that have to work in practice.

The other use for ambiguity has already been touched upon, namely the `nonsense` rules.
Because these rules are referenced in definitions that come after the ones that reference the `statement` and `metstatement` rules, the latter should always be evaluated first.
The need for nonsense nodes is not as pressing as error nodes and they do not contribute to robustness overall.
Their utility lies in permitting high level nodes such as theorem nodes to remain intact whilst a user finishes typing a statement in the IDE, say.
Furtherfmore, nonsense nodes allow documents to be parsed with only the default custom grammar which makes indexing in the IDE much faster.

The exclamation mark `!` modifier on the `statement` and `metastatement` rules, amongst others, deserves mention at this point.
These modifiers flag rules as potentially ambiguous but they are not used consistently throughout.
The topmost `document` rule is deliberately ambiguous, for example, but it is not flagged as such.
The reason is that in practice this modifier is used to tell the incremental algorithm not to recurse into the rule during its parsing stage since this can cause problems.
An exception has to be made for the topmost rule, however, since instructing the incremental algorithm not to recurse into it would defeat its purpose entirely.

Finally on the subject of ambiguity, the astute reader may well also ask whether the order of definitions can be relied upon givevn that the BNF may be rewritten in order to eliminate left recursion.
The answer is that it is assumed that the rules where ambiguity happens are not left recursive.
This is indeed an assumption, but in practice it holds.

## Precedence

Another of Occam's grammar features is precedence.
Consider the following arithmetic expression:

```
1+2/3-4
```

We would like this to parse whilst respecting the precedence of the operators.
The following BNF will achieve this in the standard way:

```
            expression ::= additionalTerm... "." ;


        additionalTerm ::= additionalTerm additionalOperator multiplicativeTerm

                         | multiplicativeTerm

                         ;

    multiplicativeTerm ::= multiplicativeTerm multiplicativeOperator number

                         | number

                         ;


    additionalOperator ::= "+" | "-" ;

multiplicativeOperator ::= "*" | "/" ;


                number ::= /\d+/ ;
```

To summarise the approach quickly, precedence is enforced by way of splitting the operators into two separate rules.
The exact details are not important, however we give the parse tree in passing:

```
                                                                                                                                expression [0]                                       
                                                                                                                                       |                                             
                                                                                                  --------------------------------------------------------------------------         
                                                                                                  |                                                                        |         
                                                                                         additionalTerm [0]                                                       "."[unassigned] [0]
                                                                                                  |                                                                                  
                                              ---------------------------------------------------------------------------------------------------------                              
                                              |                                                                                |                      |                              
                                     additionalTerm [0]                                                             additionalOperator [0] multiplicativeTerm [0]                    
                                              |                                                                                |                      |                              
           -----------------------------------------------------------------------                                    "-"[unassigned] [0]        number [0]                          
           |                      |                                              |                                                                    |                              
  additionalTerm [0]   additionalOperator [0]                         multiplicativeTerm [0]                                                 "4"[unassigned] [0]                     
           |                      |                                              |                                                                                                   
multiplicativeTerm [0]   "+"[unassigned] [0]             -------------------------------------------------                                                                           
           |                                             |                        |                      |                                                                           
      number [0]                              multiplicativeTerm [0] multiplicativeOperator [0]     number [0]                                                                       
           |                                             |                        |                      |                                                                           
  "1"[unassigned] [0]                               number [0]           "/"[unassigned] [0]    "3"[unassigned] [0]                                                                  
                                                         |                                                                                                                           
                                                "2"[unassigned] [0]                                                                                                                  
```

There are two problems with this approach.
Firstly, the increased depth and complexity of the parse tree.
Arguably extraneous nodes such as the `multiplicativeTerm` and `additionalOperator` nodes are an inevitable consequence of the elaborate BNF, for example.
Seconldly, the BNF itself is flawed.
Note that the `multiplicativeTerm` rule references the `number` rule, the reason being that there must be some rule at the foot of the hierarchy, so to speak.
If we try to replace this with a reference to the `term` rule then we get a form of left recursion that cannot be eliminated.
This is not a fault of the algorithm to eliminate left recusrion but a fault of the BNF itself.
Thus is someone else wants to add additional rules to the `term` rule then they would be unable to do so independently.

In order to tackle these problems a new way of treating precedence was devised.
The BNF below shows all that is needed with the solution to hand:

```
expression ::= term... "." ;


     term  ::=  argument ( "/" (4)
                            
                         | "*" (3)
                                            
                         | "+" (2)
               
                         | "-" (1) ) argument

             |  number

             ;
             
  argument ::= term ( ) 
  
             | type ( )
             
             ;

      
   number  ::=  /\d+/ ; 
```

Here each of the choices in the second part of the `term` rule's first definition has been augmented with a number in parenthesis.
These numbers will be inherited by the nodes during parsing with the proviso that nodes with lower numbers are not allowed to appear directly below those with higher ones.
And if look-ahead is enabled then the parser will have the chance to try likely several parse trees until it finds one that satisfies this criteria, thus enforcing precedence.

One other thing to note is that both the definitions of the `argument` rule, the need for which will be explained in a later chapter, are given what might be called empty or see-through precedence.
This ensures that precedence is enforced between nodes that are to be found directly above and below them.
Here is the parse tree:

```
                                                                                                              expression [0]                                   
                                                                                                                     |                                         
                                                                                    ------------------------------------------------------------------         
                                                                                    |                                                                |         
                                                                              term [0] (1)                                                  "."[unassigned] [0]
                                                                                    |                                                                          
                                       -------------------------------------------------------------------------------------------                             
                                       |                                                                     |                   |                             
                               argument [0] ( )                                                     "-"[unassigned] [0]  argument [0] ( )                      
                                       |                                                                                         |                             
                                 term [0] (2)                                                                                term [0]                          
                                       |                                                                                         |                             
         -------------------------------------------------------------                                                      number [0]                         
         |                   |                                       |                                                           |                             
 argument [0] ( )   "+"[unassigned] [0]                      argument [0] ( )                                           "4"[unassigned] [0]                    
         |                                                           |                                                                                         
     term [0]                                                  term [0] (4)                                                                                    
         |                                                           |                                                                                         
    number [0]                                   -----------------------------------------                                                                     
         |                                       |                   |                   |                                                                     
"1"[unassigned] [0]                      argument [0] ( )   "/"[unassigned] [0]  argument [0] ( )                                                              
                                                 |                                       |                                                                     
                                             term [0]                                term [0]                                                                  
                                                 |                                       |                                                                     
                                            number [0]                              number [0]                                                                 
                                                 |                                       |                                                                     
                                        "2"[unassigned] [0]                     "3"[unassigned] [0]                                                            
```

In fairness it is deeper than the previous parse tree but this is only because of the requisite `argument` nodes.
Other than that, note that precedence has been enforced with hardly any compromises on readability either of the parse tree or the BNF.
Finally, note that it is possible to add further definitions to the `term` rule independently without introducting left recursion that cannot be eliminated.

## Left recursion

It helps to know what left recursion is because the algorithm to eliminate it will occasionally throw up an error that will appear spurious without context.
We recall the following BNF:

```
expression ::= "(" expression ")"
 
             | expression operator expression
 
             | number
 
             ;

  operator ::= "+" | "-" | "÷" | "×" ;

    number ::= /\d+/ ;
```

The second of the definitions of the `expression` rule is left recursive, as previously pointed out.
Here is the adjusted BNF with the left recursion eliminated.
It is certainly not necessary to understand how this can come about:

```
expression            ::= expression_ expression~* ;

operator              ::= "+" | "-" | "÷" | "×" ;

number                ::= /\d+/ ;

expression_           ::= "(" expression ")"

                        | number

                        ;

expression~expression ::= operator expression ;

expression~           ::= expression~expression ;
```
 
However, we draw attention to one of the adjustments in order to justify the kinds of errors that result when certain forms of left recursion cannot be eliminated.
Suppose then that the second definition is abridged:

```
expression ::= "(" expression ")"

             | expression
 
             ...

             ;

...
```

A little thought should convince that this will make the BNF untenable.
The algorithm cannot be expected eliminate such forms of left recursion and therefore it will throw an error.
The exact wording of the error may confuse, however:

```
The 'expression~' directly repeated rule is effectively empty.
```

Notice that the parts previously found after the `expression` part in the `expression` rule's second definition found their way verbatim into the single definition of the `expresssion~expression` rule.
But with these parts removed, this rule becomes empty.
And since the `expression~` rule references it, the former is described as being effectively empty.
Thus a concrete feature of the adjusted BNF, in this case an empty rule, signifies a form of left recursion that cannot be eliminated.
This is typical but fortunately there are only a handful of such forms and the errors that arise all follow along these lines.
Furthermore, a little practice is all that suffices before it becomes straightforward to work out where problems lie.

Lastly, the other type of error that arises is when complex parts cannot be rewritten.
Again we alter the second definition of the `expression` rule to demonstrate:

```
expression ::= "(" expression ")"

             | ( expression | number ) operator expression

             ...

             ;
 
...
```

The first part of the second definition is a complex part and these cannot be rewritten.
To see what this is so, simply ask yourself what the names of the rewritten rules would be.
Here is the error:

```
The '( expression | expression ) operator expression' definition of the 'expression' rule is complex.
```

In these cases there is no choice but to pull the offending complex part out into its own rule:

```
      expression ::= "(" expression ")"

                   | expressionNumber operator expression

                   ...

                   ;

expressionNumber ::= expression | number ;

...
```

Now rules such as `expressionNumber~` can be created by the algorithm.
Finally on this subject it is worth noting that When complex part errors arise experience suggests that they can often be replaced with something better rather than pulling them out into another rule.

[^1]: https://juliamono.netlify.app/
[^2]: https://github.com/djalbat/occam-grammars
[^3]: https://en.wikipedia.org/wiki/Regular_expression
[^4]: https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form
[^5]: https://github.com/djalbat/occam-parsers/blob/master/src/bnf/bnf.js
