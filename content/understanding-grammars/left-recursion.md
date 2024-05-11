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
