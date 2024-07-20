## Terms, statements and metastatements

Metastatements are covered first because they are probably the least familiar, then statements and lastly terms.

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
If you were to say these two statements then it would be reasonable to infer that you would subsequently say "I'll get wet".
Such an inference is used often even in day to day argumentation and Modus Ponens is its formal expression.

Its premises and conclusion consist of metastatements, with each on made up of metavariables and optionally operators.
Metavariables are meta level variables, that is variables the values of which are statements.
To arrive at the inference above you would substitute "it's raining" for `A` and "i'll get wet" for `B` and then apply the rule.
There is a slight indirection here because the usual natural language equivalent of implication is "if ... then"`.
But clearly you could use the word 'implies' rather than the implication character and everything would tie together nicely.

As mentioned in the motivating example, this rule is useless unless the `A ⇒ B` metastatement is parsed as such as not as nonsense.
And, also as mentioned already, this requires two additions to the custom grammar:

1. The operator pattern must match the `⇒` character.
2. The `metastatemt` rule must be augmented with the `metavariable ⇒ metavariable` definition.

Rather than the home made custom grammar created in the motivating example, have a look at the requisite files in the `minimal-propositional-logic` package.

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

Before moving on to statements it is worth becoming a little more familier with reasoning at a meta or extrinsic level.
Consider the following rule, therefore, also to be found in the `minimal-propositional-logic` package:

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

Here the rule is derived rather than just stated.
The proof is a short derivation that utilises the premises and ends with the conclusion.
It is worth some time getting to grips with the reasoning and also following the references, which can be clicked, to the other rules.

Such rules are utilised at the object or intrinsic level, too, with statements being substituted for metavariables when rules are utilised.
Thus the means to augment metastatements also have a bearing on statements, as will be seen next.

### Statements

Staying with the `minimial-propositional-logic` package for the moment, here are the contents of the `statement.bnf` file:

```
statement  ::=  "¬"<NO_WHITESPACE>metaArgument

             |  metaArgument ( "∧" | "∨" | "iff" | "⇒" | "⇔" ) metaArgument

             ;
```

The overall pattern for statements is identical to that for metastatements.
However, rather than the `statement` rule being referenced in the defintions there is a reference to the `metaArgument` rule.
Here is the BNF for this rule and the `argument` rule to boot:

```
metaArgument                         ::=   statement ( ) 

                                       |   metaType ( ) 
                                       
                                       ;

argument                             ::=   term ( ) 

                                       |   type ( )
                                       
                                       ;
```

Note firstly that the precedence of all of their definitions is see-thtough, so to speak.
Other than that, note that a meta-argument can be either a statement or a meta-type.
The only meta-type encountered so far is `Statement` and in fact there is only one other, namely `Context`.
The the need for these intermediate rules is related to Occam's type system.
Most of the detail will be left for later chapters concerned with verification.
However, as in the case of the proof of the Modus Tollens, some understanding is helpful now.

One of the ways that syntax is tied to verification is by way of combinators.
These restrict statements to be of a certain form, indeed all statements must match either a user defined or built in combinator.
For, here are the contents of the `combinators.fls` file in the `minimal-propositional-logic` package:

```
Combinator ¬Statement

Combinator Statement ∧ Statement
Combinator Statement ∨ Statement
Combinator Statement ⇒ Statement
Combinator Statement ⇔ Statement
Combinator Statement iff Statement
```

The relation to the custom grammars should be clear, with statements being defined as combinations of other statements.
Again it is worth stressing that no statement verifies unless it matches a combinator.

Custom grammars also have a bearing on statements at an intrinsic level.
To see an example, open the `inequalities` package and reload.
Here are the contents of the `operators.ptn` file:

```
<|⩽|⩾|>
```
 
Hopefully the contents of the `stsatement.bnf` will come as no surprise:

```
statement  ::=  argument ( "<" | "⩽" | "⩾" | ">" ) argument ;
```

One thing to note, however, is that the `argument` rule is referenced here rather than the `metaArgument` rule.
That is because the various inequality operators relate terms rather than statements.
Put another way, statements are formed by combining terms in this instance rather than other statements.
Here are the requisite combinators, which should clarify:

```
Combinator ℝ < ℝ
Combinator ℝ > ℝ
Combinator ℝ ⩽ ℝ
Combinator ℝ ⩾ ℝ
```

The type here is the real number `ℝ` type, defined elsewhere.

The use of references to the `metaArgument` and `argument` rules as opposed to refrences to the `statement` and `term` rules, respectively, is because combinators are statements themselves.
Returning to the meta level for a moment, here is the parse tree for the `¬Statement` statement combinator, for example:

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

And here is the parse tree for the `Combinator ℝ ⩾ ℝ` combinator:

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

It is worth spending the time to get both of these parse trees showing in the grammars sandbox.
In the latter case you will need to import a different set of custom grammars for the `inequalities` package.

With the proviso once again that this is not a chapter on verification, it is worth pointing out exactly what goes on when statements are verified.
When the verifier encounters a statement, it tries to match each of the ocmbinators that it has to hand in turn.
Imagine the parse tree for a particular combinator on one side and the parse tree for the statement at hand on the other.
The verifier traverses both in tandem, matching node for node until it comes across a `type` or `metaType` node in the combinator.
In the case of a `type` node it expects to find a corresponding `term` node in the statement and verifies that.
The process of doing so will return a type, which can then be matches against the type attained by verifying the `type` node in the combviantor's parse tree.
On the other hand if it encounters a `metaType` node then it will expect to find a `statement` node at the corresponding position in the statement's parse tree, in which case it will be able to continue.







