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

To summarise this approach, precedence is enforced by way of splitting the operators into two separate rules.
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

There are two problems with this cumbersome approach:

1. The increased depth and complexity of the parse tree. Arguably extraneous nodes such as the `multiplicativeTerm` and `additionalOperator` nodes are an inevitable consequence of the elaborate BNF, for example.

2. The BNF itself is flawed. Note that the `multiplicativeTerm` rule references the `number` rule, the reason being that there must be some rule at the foot of the hierarchy, so to speak. If we try to replace this with a reference to the `term` rule then we get a form of left recursion that cannot be eliminated. Thus if someone else wants to add additional rules to the `term` rule then they would be unable to do so independently.

In order to tackle these problems a new way of treating precedence was devised.
The BNF below shows how it can be utilised:

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
And if look-ahead is enabled then the parser will have the chance to all possible parse trees until it finds one that satisfies this criteria, thus enforcing precedence.

One other thing to note is that both the definitions of the `argument` rule, the need for which will be explained in a later chapter, are given what might be called empty or see-through precedence.
This ensures that precedence is enforced between nodes that are to be found directly above and below them.
Here is the parse tree that results:

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
Finally, note that it is possible to add further definitions to the `term` rule independently without introducting forms of left recursion that cannot be eliminated.

