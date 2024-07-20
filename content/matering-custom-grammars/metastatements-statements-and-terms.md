## Metastatements, statements and terms

Metastatements are covered first because they are probably the least familiar, then statements and lastly terms.
The ties between custom grammars and verification are also introduced, because the former cannot be fully understood in isoluation from the latter.
Verification is mostly a syntactic process, and grammars define syntax of course.

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
Metavariables are meta level variables, that is variables the values of which are instances of meta level concepts such as statements.
To arrive formally at the inference above you would substitute "it's raining" for `A` and "i'll get wet" for `B` and then apply the rule.
There is a slight indirection here because the usual natural language equivalent of implication is "if ... then"`.
But clearly you could use the word 'implies' rather than the implication character and everything would tie together nicely.

As mentioned in the motivating example, this rule is useless unless the `A ⇒ B` metastatement is not just parsed as nonsense.
And, as also mentioned already, this requires two additions to a custom grammar:

1. The operator regular expression pattern must be augmented with the `⇒` character.
2. The `metastatemt` rule must be augmented with the `metavariable ⇒ metavariable` definition.

Moving on from the motivating example somewhat, the requisite files are to be found in the `minimal-propositional-logic` package.
The contents of the `operator.ptn` file are as follows.
Note that the implication `⇒` operator is supported along with several others:

```
iff|⇔|⇒|∧|∨|¬
```

And the contents of the `metastatement.bnf` file are the following.
Note that the second definition effectively encompases the `metavariable ⇒ metavariable` definition:

```
metastatement  ::=  "¬"<NO_WHITESPACE>metastatement
    
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

This time the rule is derived rather than just stated.
The proof is a short derivation that utilises the premises and ends with the conclusion.
It is worth some time getting to grips with the reasoning and also following the references, which can be clicked, to the other rules.
This is meta level resasoning.

Such rules can be employed at the object or intrinsic level, too, with statements being substituted for metavariables.
Thus changes which impact the parsing of metastatements also impact statements, as will be seen next.

### Statements

Staying with the `minimial-propositional-logic` package for the moment, here are the contents of the `statement.bnf` file:

```
statement  ::=  "¬"<NO_WHITESPACE>metaArgument

             |  metaArgument ( "∧" | "∨" | "iff" | "⇒" | "⇔" ) metaArgument

             ;
```

The overall pattern is identical to that for metastatements.
However, rather than the `statement` rule being referenced in the defintions there is a reference to the `metaArgument` rule.
Here is the BNF for this rule and the `argument` rule to boot:

```
metaArgument  ::=  statement ( ) 

                |  metaType ( ) 
                
                ;

argument      ::=  term ( ) 

                |  type ( )
                
                ;
```

In passing, note that the precedence of the definitions is see-thtough, so to speak.
Moving on, one of the ways that syntax is tied to verification is by way of combinators.
These restrict statements to be of a certain form, indeed all statements must match either user defined or built in combinators.
Here are the contents of the `combinators.fls` file in the `minimal-propositional-logic` package, for example.
The relation to the custom grammar should be clear:

```
Combinator ¬Statement

Combinator Statement ∧ Statement
Combinator Statement ∨ Statement
Combinator Statement ⇒ Statement
Combinator Statement ⇔ Statement
Combinator Statement iff Statement
```

Now copy the first of these combinator declarations into the sandbox and also set the start rule name to `combinatorDeclaration`.
The following parse tree should appear:

```
                                               combinatorDeclaration [0]                                    
                                                           |                                                
                --------------------------------------------------------------------------------------      
                |                                             |                                      |      
"Combinator"[primary-keyword] [0]                       statement [0]                          <END_OF_LINE>
                                                              |                                             
                                          ----------------------------------------                          
                                          |                |                     |                          
                                  "¬"[operator] [0] <NO_WHITESPACE>    metaArgument [0] ( )                 
                                                                                 |                          
                                                                           metaType [0]                     
                                                                                 |                          
                                                                    "Statement"[meta-type] [0]              
```

Thus combinators are themselves statements, but with `metaType` nodes where `statement` nodes would otherwise be.
And verifhing a statement essentially entails traversing its parse tree side by side with the parse tree of a combinator.
If a `metaType` node is encountered in the combinator's parse tree then the verifier expects a `statement` node in the statement's parse tree.
It then verifies this statement recursively by the same means.

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

Note that the `argument` rule is referenced here in a similar vein to the treaement of metastatements above.
This is because at an intrinsic level, it is terms that are combined to form statements rather than other statements.
Here are the combinators corresponding to the above custom grammar, which should clarify:
The type here is the real number `ℝ` type, defined in the `numbers` package:

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
"Combinator"[primary-keyword] [0]                     statement [0]                   <END_OF_LINE>
                                                            |                                      
                                          ------------------------------------                     
                                          |                |                 |                     
                                  argument [0] ( ) "⩾"[operator] [0] argument [0] ( )              
                                          |                                  |                     
                                      type [0]                           type [0]                  
                                          |                                  |                     
                                    "ℝ"[type] [0]                      "ℝ"[type] [0]               
```

In this case, when the verifier encounters the `type` node in the combinator it would expect to find a `term` node in the corresponding statement.
If it did so then it would verify this term recursively,  resulting in a type.
It would then match this type again the child node of the `type` node in the combinator.

### Terms

