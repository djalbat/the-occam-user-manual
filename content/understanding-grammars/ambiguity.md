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
