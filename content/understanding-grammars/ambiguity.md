## Ambiguity

Recall that all of Occam's lexers and parsers are configured in such a way as to be robust, in the sense that they will cope with any content.
In the case of the lexers, robustness is guaranteed by an in-built rule that matches whitespace together with a last user defined `unassigned` rule that matches anything but whitespace.
In the case of the parsers, robustness is guaranteed by an `error` rule that is always given as the last choice in the singular definitions of start rules.
In theory perhaps there should be no unassigned tokens or error nodes but practice they do regularly come about.

To reiterate this point, as a last resort all content can be tokenised as whiteapce together with unassigned tokens; and parsed as error nodes.
So there are always at least two sequences of tokens and two corresponding parse trees for any content.
Thus robustness is effectively guaranteed by ambiguity.

Now contrast this state of affairs with the theoretical standpoint that ambiguity is unacceptable.
What would happen then were it not built in to all of Occam's grammars?
If we wanted to guarantee robustness for the lexers then we would have to hard code an in-built rule to run after the user defined rules expressly for the purposes of catching any content not matched beforehand.
But this is precisely what the `unassinged` rule does.
Simimlarly, if we wanted to guarantee robustness for the parsers then we would have to engineer them in such a way as to default to an error node somehow should no other nodes be possible.
This approach was attempted early on in development, in fact, but it was abandoned as it compllicated an already complex piece of software even more.
In the end any attempt to solve the problem of robustness programmatically simply simulates these `unassigned` and `error` rules, often at considerable programmatic cost.
Thus it can be argued that the kind of ambiguity brought about by unassigned tokens and error nodes is unavoidable in lexers and parsers that have to work in practice.

Another use for ambiguity has already been touched upon, namely the `nonsense` rules.
The need for nonsense nodes is not as pressing as error nodes and they do not contribute to robustness overall.
Their utility lies in permitting high level nodes such as theorem nodes to remain intact whilst a user finishes typing a statement in the IDE, say.
Furtherfmore, nonsense nodes allow documents to be parsed with only the default custom grammar, which makes indexing in the IDE much faster.

The double period modifier for the `unqualifiedMetastatement` and `qualifiedMetastatement` rules deserves mention at this point.
In fact there is also a single period modifier, an example of its use being the `error` rule.
In order to understand their utility it is necessary to delve into Occam's internals a little.
As well as the lexers and parsers covered in this chapter, which are called batch lexers and parsers because they act on the content as a whole, Occam also has incremental lexers and parsers.
It is not helpful to go into too much detail here but the general idea is that they process the content from a high level, so to speak, and utilise the batch lexers and parsers only on parts of the content that change.
What the single and double period modifiers do is force these incremental lexers and parsers to behave in a certain way.

Specifically, the single period modifier will stop the incremental parser in its tracks.
When it encounters a rule thus modified it will stop travsering down the parse tree and utilise the batch parser immediately.
It behaves similarly if it encounters a rule modified with a double period modifier, however if the batch parser succeeds once utilised then it will at least try to refine the result further by a certain means.

Both of these modifiers are needed when dealing with ambiguity at a medium to low level, so to speak.
To see this, suppose that the batch parser parses part of the content as nonsense and suppose also that subsequently the user makes an incremental change to that part of the content that allows it to be parsed as a statement.
If the incremental parser were to be allowed to traverse down the parse tree indefinitely, however, it would perhaps make a change only to a child node of the nonsense node, leaving the parse nonsense node otherwise intact.
By stopping the incremental parser at the higher level, however, it is forced to try to evaluate the `statement` fule every time and in particular before the `nonsense` rule.
Thus if that part of the content can indeed be parsed as a statment then this will be the outcome.

These modifiers are of singular use when dealing with the ambiguity purposely added to the Flroence grammar and indeed others.
We call rules modified with single and double period modifiers semi-opaque and opaque, respectively, hopefully for obviously reasons.
