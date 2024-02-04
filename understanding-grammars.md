# Understanding Grammars

Occam's grammars functionality is one of its strong points but what exactly is a grammar, at least in Occam's parlance?
A grammar can loosely be described as that which is needed in order to describe and work with a language.
More specifically it can be comprised of three parts:

1. A collection of symbols or characters that are the smallest elements of the language. 
These symbols or characters are more often than not considered as essentially synonymous with the glyphs that are used to represent them.
In our case a seuquence of such characters is what commprises the content of a document or file.

2. A set of rules, usually based on regular expressions, to collect these characters into larger elements, called tokens or lexemes.
We often consider a sequence of characters as continuous rather than discrete and therefore tend to think of these rules as chopping up the content, so to speak.
This processing is called lexing or tokenising the content.
We stick to the latter.

3. Another set of rules, more high level, that are responsible for organising these tokens into larger semantic blocks.
In the case of natural language these would be phrases, sentences, paragraphs and the like.
This process is called parsing the tokens or, by extension, the content and the resulting structure is usually called the abstract syntax tree, or AST for short.
We cell it the parse tree, however.

Lastly, not part of this list but equally important is the way that the parse tree and sometimes the tokens themselves are interpreted and sometimes even maninpulated.
We cover this practice in this chapter, too.

