# Understanding Grammars

Occam's grammars functionality is one of its strongest suits but what exactly is a grammar, at least in Occam's parlance?
A grammar can loosely be described as that which is needed to describe and work with a language.
More specifically, it can be thought of as comprising three parts:

1. A collection of symbols or characters that are the smallest elements of the language. These symbols or characters are usually conflated with the glyphs that represent them. In our case a sequence of such characters is what comprises the content of a document or file.

2. A set of rules, usually based on regular expressions,[^regular-expressions] to collect these characters into larger elements, called tokens or lexemes. We tend to envisage a sequence of characters as continuous rather than discrete and therefore tend to think of these rules as chopping up the content rather than gathering it. This process is called lexing or tokenising and we stick with the latter.

3. Another set of rules, written in BNF,[^bnf] that are responsible for organising these tokens into larger elements. In the case of a natural language these would be phrases, sentences, paragraphs and so on. This process is called parsing the tokens or, by extension, the content The resulting structure is usually called an abstract syntax tree or AST for short. We call it a parse tree, however.

There are two main parts to Occam's grammars functionality.
Firstly, there is Occam's default language, Florence, together controlled natural languages.
Secondly there are custom grammars.
We touch briefly on these in the first section of this chapter but a detailed treatement is saved for next.
Aside from this brief excursion, the remainder of this chapter is dedicated to Florence, controlled natural languages and grammars in general.

@embed content/understanding-grammars/language-flexibility-and-extensibility.md
@embed content/understanding-grammars/unicode.md
@embed content/understanding-grammars/tokenising-content-with-lexers.md
@embed content/understanding-grammars/parsing-tokens-with-parsers.md
@embed content/understanding-grammars/the-florence-grammar.md
@embed content/understanding-grammars/ambiguity.md
@embed content/understanding-grammars/precedence.md
@embed content/understanding-grammars/left-recursion.md

[^bnf]: [https://en.wikipedia.org/wiki/Backus-Naur_form](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form)

[^juliamono]: https://juliamono.netlify.app/

[^occam-grammars]: https://github.com/djalbat/occam-grammars

[^regular-expressions]: https://en.wikipedia.org/wiki/Regular_expression

@footnotes
