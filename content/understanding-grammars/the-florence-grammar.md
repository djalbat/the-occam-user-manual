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
In fact again we make the point, as we did with the plain text lexer that, since a prior in-built rule will have already matched any whitespace, this guarantees that the Florence lexer will cope with any content.

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

verticalSpace                        ::=   \&lt&lt;END_OF_LINE&gt;&gt;+ ;

error                                ::=   . ;
```

There are some points to note here, too.
Firstly, the `verticalSpace` rule matches one or more end of line tokens.
Recall that the Florence lexer is configured to treat such tokens as significant, hence they can be referenced here.
Also, the `document` rule's definition has a complex part which stipulates one or more of a choice of three parts.
These will be evaluated in sequence and therefore the `error` rule provides the required fallback functionality.
Its single definition has only one wildcard part `.` that will match any significant token, as its name suggests.
Thus Occam's parsers can be said to be robust, in a similar vein to its lexers, in the sense that they will cope with any content.

Here is part of the BNF about half way down:

```
unqualifiedMetastatement..           ::=   metastatement... <END_OF_LINE> 

                                       |   nonsense... <END_OF_LINE> 
                                       
                                       ;

qualifiedMetastatement..             ::=   metastatement... qualification <END_OF_LINE> 

                                       |   nonsense... qualification <END_OF_LINE> 
                                        
                                       ;

...

qualification                        ::=   ( "by" | "from" ) reference ;

...

nonsense                             ::=   ( [type] | [symbol] | [operator] | [special] | [secondary-keyword] | [meta-type] | [name] | [unassigned] )+ ;
```

Since ambiguity is being treated later we will pass over the fact that each of the first two rules have two definitions and the use of the double period modifiers after these rules' names.
Instead we focus on the ellipsis `...` modifier on each of the rule name parts.
This switches the parser into what is called a look-ahead mode, in which it takes note of the part that follows the look-ahead part when evaluating the look-ahead part itself.
To see why this is needed, consider the `nonsense` rule which, if left to its own devices, will parse a qualification since it parses one or more tokens of pretty much any type.
If it can be made to look ahead, however, it will stop before the qualification thus allowing the parser to continue to evaluate the `qualification` part of the definition.

It is not unreasonable to ask why this look-ahead mode is not the default mode of the parser, given its obvious utility.
Ths answer is that it can slow the parser down enornously.
On the one hand in its usual mode the parser will parse a sequence of tokens in time roughly linearly proportional to the sequence's length.
On the other hand in its look-ahead mode, although no detailed profiling has ever been done, it seems that the time is if not expoenentially then at least polynomially proportional to sequence length.
Thus although a look-ahead mode was a necessity when designing the parser, it is used throughout all of Occam's grammars with considerable caution.
