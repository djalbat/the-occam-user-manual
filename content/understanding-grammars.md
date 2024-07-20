# Understanding Grammars

Occam's grammars functionality is one of its strongest suits but what exactly is a grammar, at least in Occam?
It can be thought of as comprising three parts:

1. A collection of symbols or characters that are the smallest elements of a language. 
These symbols or characters are usually conflated with the glyphs that represent them. 
In our case a sequence of such characters is what comprises the content of a document or file. 
2. A set of rules, usually based on regular expressions,[^regular-expressions] to collect these characters into larger elements, called tokens or lexemes. 
A sequence of characters tends to be envisaged as continuous rather than discrete and therefore it is more usual to think of these rules as chopping up the content rather than gathering it. 
This process is called lexing or tokenising, with the latter being preferred here.
3. Another set of rules, written in BNF,[^bnf] that are responsible for organising tokens into larger elements. 
In the case of a natural language these would be phrases, sentences, paragraphs and so on. 
This process is called parsing the tokens or, by extension, the content 
The resulting structure is usually called an abstract syntax tree or AST for short. 
However, the phrase parse tree is used throughout this book and in the code itself.

Each of these points has its own dedicated section in what follows.
After that there is a brief section on controlled natural languages follwed by a section on Florence, Occam's default language.
The important subject of custom grammars has its own chapter, which comes next.

@embed content/understanding-grammars/unicode.md
@embed content/understanding-grammars/tokenising-content-with-lexers.md
@embed content/understanding-grammars/parsing-tokens-with-parsers.md
@embed content/understanding-grammars/controlled-natural-languages.md
@embed content/understanding-grammars/the-florence-grammar.md
@embed content/understanding-grammars/ambiguity.md
@embed content/understanding-grammars/precedence.md
@embed content/understanding-grammars/left-recursion.md

[^bnf]: [https://en.wikipedia.org/wiki/Backus-Naur_form](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form)

[^regular-expressions]: https://en.wikipedia.org/wiki/Regular_expression

@footnotes

@pageNumber
