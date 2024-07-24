## Metastatements, statements and terms

Metastatements are covered first because they are probably the least familiar, then statements and lastly terms.
The default custom grammar is covered last of all.
Some of the ties between custom grammars and verification, specifically combinators and constructors, are also introduced, because the two cannot be understood in isolation.
With Occam verification is for the most part a syntactic process, and grammars define syntax of course.

### Metastatements

Perhaps the best way to explain metastatements is look again at the inference rule given in the motivating example.
Here the metavariable declarations have been included, too:

```
Metavariable A:Statement
Metavariable B:Statement

Rule (ModusPonens)
  Premises
    A ⇒ B
    A
  Conclusion
    B
```

Now consider the two statements "If it's raining then I'll get wet" and "It's raining".
If you were to say these two statements then it would be reasonable to infer that you might subsequently say "I'll get wet".
Such an inference is used often even in day to day argumentation and Modus Ponens, the rule given above, is its formal form.

The premises and conclusions of inference rules consist of metastatements, each made up of metavariables and optionally operators.
Metavariables are meta level variables.
That is, variables the values of which are instances of meta level concepts such as statements.
To arrive formally at the inference above you would substitute "it's raining" for the metavariable `A` and "i'll get wet" for the metavariable `B` and then apply the rule.
There is a slight indirection here because the usual natural language equivalent of implication is "if ... then"`.
But clearly you could use the word 'implies' rather than the implication character and everything would tie together nicely.

As mentioned in the motivating example, this rule is useless unless the `A ⇒ B` metastatement is not just parsed as nonsense.
And, as also mentioned already, this requires two additions to the requisite custom grammar:

1. The operator regular expression pattern must be augmented with the `⇒` character.
2. The `metastatement` rule must be augmented with the `metavariable ⇒ metavariable` definition.

Moving on from the motivating example somewhat, files containing these additions are to be found in the `minimal-propositional-logic` package.
The contents of the `operator.ptn` file are as follows.
Note that the implication `⇒` operator is supported along with several others:

```
iff|⇔|⇒|∧|∨|¬
```

And the contents of the `metastatement.bnf` file are the following.
Note that the second definition effectively encompases the required `metavariable ⇒ metavariable` combination:

```
metastatement  ::=  "¬"&lt;NO_WHITESPACE&gt;metastatement
    
                 |  metastatement ( "∧" | "∨" | "iff" | "⇒" | "⇔" ) metastatement
     
                 ;   
```

In order to begin to tie in verification with such changes, consider the following rule, also found in the `minimal-propositional-logic` package:

```
Metavariable P:Statement
Metavariable Q:Statement

Rule (ModusTollens)
  Premises
    P ⇒ Q 
    ¬Q
  Conclusion
    ¬P
  Proof
    Premise
      P
    Then
      ¬Q
    P ⇒ ¬Q by ImplicationIntroduction
    P ⇒ Q
  Therefore
    ¬P by NegationIntroduction
```

This time the rule is derived rather than simply stated.
Proofs are derivations that utilise premises and end with conclusions.
It is worth some time getting to grips with the reasoning here and also following the references, which can be clicked, to the other rules.
This is meta level resasoning.

Such rules can also be employed at the object or intrinsic level, with statements being substituted for metavariables as discussed above.
Thus changes to custom grammars which impact the parsing of metastatements also have a bearing statements, as will be seen next.

### Statements

Staying with the `minimial-propositional-logic` package for the moment, here are the contents of the `statement.bnf` file:

```
statement  ::=  "¬"&lt;NO_WHITESPACE&gt;metaArgument

             |  metaArgument ( "∧" | "∨" | "iff" | "⇒" | "⇔" ) metaArgument

             ;
```

Note that the overall pattern is identical to that for metastatements.
However, rather than the `statement` rule being referenced in the defintions there is a reference to the `metaArgument` rule.
Here is the BNF for this rule and the `argument` rule to boot.
In passing, note that the precedence of the definitions is see-thtough, so to speak:

```
metaArgument  ::=  statement ( ) 

                |  metaType ( ) 
                
                ;

argument      ::=  term ( ) 

                |  type ( )
                
                ;
```

Moving on, one of the ways that syntax is tied to verification is by way of combinators.
These restrict statements to be of a certain form, indeed all statements must match either user defined or built in combinators.
Here are the contents of the `combinators.fls` file in the `minimal-propositional-logic` package, for example.
The relation to the package's custom grammar should be clear:

```
Combinator ¬Statement

Combinator Statement ∧ Statement
Combinator Statement ∨ Statement
Combinator Statement ⇒ Statement
Combinator Statement ⇔ Statement
Combinator Statement iff Statement
```

Now copy the first of these combinator declarations into the grammars sandbox and set the start rule name to `combinatorDeclaration`.
The following parse tree should appear:

```
                                               combinatorDeclaration [0]                                    
                                                           |                                                
                --------------------------------------------------------------------------------------      
                |                                             |                                      |      
"Combinator"[primary-keyword] [0]                       statement [0]                          &lt;END_OF_LINE&gt;
                                                              |                                             
                                          ----------------------------------------                          
                                          |                |                     |                          
                                  "¬"[operator] [0] &lt;NO_WHITESPACE&gt;    metaArgument [0] ( )                 
                                                                                 |                          
                                                                           metaType [0]                     
                                                                                 |                          
                                                                    "Statement"[meta-type] [0]              
```

Thus combinators are themselves statements, but with `metaType` nodes where `statement` nodes would otherwise be.
In fact verifhing a statement essentially entails traversing its parse tree in tandem with with the parse tree of a combinator.
If a `metaType` node is encountered in the combinator's parse tree then the verifier expects a corresponding `statement` node in the statement's parse tree.
It then verifies this statement recursively and carries on.

Custom grammars also have a bearing on statements at an intrinsic level.
To see an example, open the `inequalities` package and reload.
Here are the contents of the `operators.ptn` file:

```
<|⩽|⩾|>
```
 
And the contents of the `stsatement.bnf` file:

```
statement  ::=  argument ( "<" | "⩽" | "⩾" | ">" ) argument ;
```

Note that the `argument` rule is referenced here in a similar vein to the `metaArgument` rule above.
This is because at an intrinsic level, it is terms that are combined to form statements, not than other statements.
Here are the combinators corresponding to the above custom grammar, for example, which should clarify:
The real number `ℝ` type here is defined in the `numbers` package, by the way:

```
Combinator ℝ < ℝ
Combinator ℝ > ℝ
Combinator ℝ ⩽ ℝ
Combinator ℝ ⩾ ℝ
```

Copying the last of these into the grammars sandbox results in the following parse tree.

```
                                          combinatorDeclaration [0]                                
                                                      |                                            
                -----------------------------------------------------------------------------      
                |                                           |                               |      
"Combinator"[primary-keyword] [0]                     statement [0]                   &lt;END_OF_LINE&gt;
                                                            |                                      
                                          ------------------------------------                     
                                          |                |                 |                     
                                  argument [0] ( ) "⩾"[operator] [0] argument [0] ( )              
                                          |                                  |                     
                                      type [0]                           type [0]                  
                                          |                                  |                     
                                    "ℝ"[type] [0]                      "ℝ"[type] [0]               
```

In this case, if the verifier encountered the `type` node in the combinator's parse tree then it would expect to find a corresponding `term` node in the statement's parse tree.
If it did so then it would verify this term, which would result in a type.
It would then match this type against the child node of the `type` node in the combinator.

### Terms

A good example of a custom grammar relating to terms can be found in the `strings` package.
Open this package now and export its custom grammars to the grammars sandbox.
There is little in the way of changes to the regular expression patterns, with only the `+` and `|` operators being defined:

```
\\+|\|
```

Note that the `+` operator is defined elsewhere, in the `arithmetic` package for example.
The term BNF is more interesting:

```
term  ::=  argument&lt;NO_WHITESPACE&gt;( ( "[" "..." argument "]" ) 

                                  | ( "[" argument "..." argument "]" ) 

                                  | ( "[" argument "..." "]" ) 
      
                                  ) (20)

        |  argument "+" argument

        |  "|" argument "|"

        |  [string-literal] 

        ;
```

Just as statements are matched against combinators, terms are matched against constructors.
Here are the constructor definitions in the `strings` package:

```
Constructor |String|:ℕ

Constructor String[ℕ...]:String
Constructor String[ℕ...ℕ]:String
Constructor String[...ℕ]:String
  
Constructor String + String:String
```

If you copy the first of these into the grammars sandbox then the following parse tree should result:

```
                                                           constructorDeclaration [0]                                                 
                                                                        |                                                             
                 ---------------------------------------------------------------------------------------------------------------      
                 |                                            |                                   |              |             |      
"Constructor"[primary-keyword] [0]                        term [0]                        ":"[special] [0]   type [0]    &lt;END_OF_LINE&gt;
                                                              |                                                  |                    
                                           --------------------------------------                          "ℕ"[type] [0]              
                                           |                  |                 |                                                     
                                   "|"[operator] [0]  argument [0] ( )  "|"[operator] [0]                                             
                                                              |                                                                       
                                                          type [0]                                                                    
                                                              |                                                                       
                                                     "String"[type] [0]                                                               
```

The verification of terms is almost entirely analogous to the verification of statements. 
In fact the behaviour of the verifier when `type` nodes are encountered in constructors is exactly the same as when they are encountered in combinators.

In passing it is worth noting that types are defined in custom grammars, and that they are defined at the token level.
For example, the `String` type is defined in the `type.tpn` file.
Another example can be found in the `numbers` package.
Note that Unicode characters can be used directly in regular expression patterns:

```
[ℝℚℤℕ]\\\{0\}|[ℝℚℤℕ]
```

Terms can be formed not just from variables and operators but also from symbols.
Furthermore, sometimes terms are formed from standalone constructurs without additional arguments or operators.
This is the case for the `zero` term, for example, which can be found in the `numbers` package.
A parallel from natural language is useful here.
Terms can be thought of as akin to syllables, which may be concatenated to form words or may be words by themselves, standalone so to speak.

There are also parallels with natural language in the way that terms can be formed.
Open the `natural-numbers` package and export its custom grammars to the grammars sandbox.
The `successor` and `predecessor` symbols are defined in the `symbols.ptn` file:

```
successor|predecessor
```

The term BNF is also defined therein:

```
term  ::=  "successor"&lt;NO_WHITESPACE&gt;"(" argument ")"

        |  "predecessor"&lt;NO_WHITESPACE&gt;"(" argument ")"

        ;
```

Note the use of the `&lt;NO_WHITESPACE&gt;` token, which disallows whitespace between tokens. 
In a simiilar vein, syllables are usually concatenated without any space between them in order to form words, but this is not always the case.
Email used to be e-mail, for example.
Whitespace between tokens is tolerated by Occam by default.
However, the above example shows that it can be precluded if thought necessary.

### The default custom grammar

This is best viewed in the grmmars sandbox, appearing as it does at the foot of any list of custom grammars.
It cannot be bypassed and therefore provides something of a window into the more pointed aspects of verification.

Looking at the regular exprssion patters firstly, there is one built-in `Object` type;
no built in symbols, which is perhaps not surprising;
and an array of operators:

```
⊧|is|for|omits|contains|undefined
```

It is arguable whether they should have been included in the default cusotm garmmar or should have found their way into the Florence grammar itself.
In the end they stayed in the default custom grammar because they are not referenced in the Florence BNF.

Speaking of which, here is the term BNF, the least daunting of the three:

```
term  ::=  "(" argument ")"

        |  variable 
        
        ;
```

The verifier has a built in constructor that we return the type of a term enclosed in parentheses.
This is the default behaviour, however, this consutructor is always tries last, and can therefore be overridden.

The statement BNF is also not too daunting:

```
statement                            ::=   "(" metaArgument ")" 
                                                  
                                       |   equality

                                       |   typeAssertion 
                                                  
                                       |   undefinedAssertion

                                       ;
                                       
equality                             ::=   argument "=" argument ;

typeAssertion                        ::=   term... ":" type ;

undefinedAssertion                   ::=   variable "is" "undefined" ;
```

Note that statements can also be parenthesised.
The verifier has a built in combinator to handle parenthesised statements, in fact.
Also note that equality is present in the grammar.
Again this is handled internally by the verifier.
Incidentally there is no need for a combinator for equality, the verificer simply picks out the `equality` node.
The utility of the remaining two assertions should be clear.

Lastly, the BNF for metastatements.
It is nothing if not daunting and is given here mainly for the sake of completeness:

```
metastatement                        ::=   "(" metastatement ")" 
           
                                       |   ruleSubproofAssertion         
                                        
                                       |   contextDefinition 
           
                                       |   proofAssertion
       
                                       |   metavariable ( inclusion | substitution )?

                                       |   metavariable substitution?

                                       ;

ruleSubproofAssertion                ::=   "[" metastatement ( "," metastatement )\* "]" "..." metastatement ;

contextDefinition                    ::=   context "=" ( judgement | context ) ( "," ( judgement | context ) )\* ;

proofAssertion                       ::=   context "⊧" judgement ;
 
judgement                            ::=   reference "::" metastatement ;

inclusion                            ::=   ( "omits" | "includes" ) variable ;

substitution                         ::=   "[" term... "for" variable "]" ;
```

Again note that parentheses are essentially internatlised by the verifier at a meta level.
Aside from this observation, nothing more will be added here as all of these concepts will be covered in the later chapters/ 
