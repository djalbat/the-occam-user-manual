## Tokenising content with lexers

There are several lexers to be found in the Occam grammars package.[^occam-grammars]
In fact these are all the same lexer but configured slightly differently.

In essence Occam's lexer is a state machine having two states, namely 'in comment' and 'not in comment'.
Depending on these states it uses a different sequence of both in-built and user defined rules in order to tokenise content.
The order in which the rules are executed matters.
Comments must be picked out before string literals, for example.

For each of the grammars a `CommonLexer` class is extended with divers static properties which essentially define the lexer's in-built rules.
For example, a particular lexer might pick out C-style comments as opposed to Perl-style ones, or it might not pick out comments at all.
Simiarly it might pick out string literals or, again, it might not.

As well as picking out verious types of tokens, lexers distinguish between two kinds of token, namely significant and non-significant.
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

Lexers resort to user defined rules should their in-built rules fail to match content and they are tried in order from top to bottom.
Note that all of hte regular expression patterns start with the `^` caret character which matches the start of the content.
Thus it is reasonable to envisage the lexer as consuming the content from left to right.

One other thing to note is that the last user-defined rule will match anything but whitespace.
Given that a prior in-built rule will have already matched any whitespace this guarantees that the plain text lexer will cope with any content.
We call this robustness and come back to this important property of both lexers and parsers in a later section.

[^occam-grammars]: https://github.com/djalbat/occam-grammars
