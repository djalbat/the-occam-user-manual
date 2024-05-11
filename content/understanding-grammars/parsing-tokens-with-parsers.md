## Parsing tokens with parsers

Like the lexers, there are several parsers to be found in the Occam grammars package.[^occam-grammars]
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
expression ::= "(" expression ")"

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

