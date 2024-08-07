# Introduction

I have tried to make Occam[^occam] as useable as possible but there are limits.
At the end of the day it is an expert system and some of its parts, not least the verifier, need detailed explanation.
It is the purpose of this book is to provide these explanations.

This book also goes into considerable detail on the subject of Occam's approach to language, which largely boils down to its use of grammars.
Occam has its own language, called Florence,[^florence] but it will also support controlled natural languages in the near future.
Indeed, the verifier cannot distinguish between these languages at all.
This book explains how this is possible.

After explaining Occam's approach to language this book will give a very detailed explanation of how the verifier works.
Some may find this nauseating but I maintain that it is essential.
The whole idea of Occam is not to replace human reasoning but to facilitate it, and it is the verifier that reasons on your behalf.
In fact I recommend that you read the introduction together with the first four chapters of the Foundations book before going much further with this one.
They are neither very long nor very deep and will provide the necessary background for understanding the verifier in particular.

I hope that the verifier's implenentation is both transparent and readable, and therefore understandable, especially augmented as it is with the explanation here.
Apart from anything else even a partial understanding will likely save a good deal of frustration when you begin to work seriously with Occam.
The other reason for understanding the verifier is that it has not been verified itself.
So you cannot simply press a button and have confidence in it, that is not the idea at all.

In fact, at the risk of courting controversy, I would argue that it should not be the idea with any verifier.
All are failible regardless of what their proponents may claim and therefore I do not believe that their results should ever be trusted without some level of human oversight.
Indeed in my opinion verification should be an aid to clarity and rigour and never a substitute for it.
The idea of a proof as a black box in particular is anathema to me.

Moving on, the standpoint that software should be an aid to human reasoning and not a substitute for it must these days be tempered by a consideration of artificial intelligence as a tool for reasoning.
What inspired me over the near decade of work that it took to get Occam to its first viable release was a firm belief in what I call the four elephants, expounded in the first four chapters of the aforementioned Foundations book.
I had not heard of large language models when I started out and they were never a motivating factor, but as I came to my first milestone after those many years, they began to loom large.

The resurgence of artificial intelligence in recent years has hardly changed my views on automated reasoning, however.
Admittedly of late there has been some progress in the direction of coupling artificial intelligence with formal reasoning systems.
Occam's role in all of this seems to be that the output of any large language model or such like can potentially serve as its input.

Thus the panacea of using computers as tools for symbolic reasoning, be that devising algorithms or protocols; discovering new mathematics or logic; or whatever, is almost upon us.
And it is worth pointing out that this panacea has been eagerly anticipated for around seventy five years now.
There is no doubt that artificial intelligence is on the verge of bringing all of this about, but without tools such as Occam the output of artificial intelligence models will be clouded in doubt.

Changing the subject, I should mention Highmark, wihch is a new document preparation system developed in tandem with Occam.
It was a necessary intermediate step in working towards Occam's support for controlled natural languages but I hope that in the long run it will succeed in its own merits.
Both this book and the Foundations book were written using Highmark and it may well turn out that more people use Occam for working with it than for reasoning.
There is therefore a chapter dedicated to it immediately after the chapter on getting to grips with the IDE.
And if you are using Occam to work exclusively with Highmark then please do not be daunted by the formal reasoning side of things, you can safely ignore it, and rest assured that support for Highmark will always be included.

To conclude, I hope that in the coming years at least some people will come to see Occam as an indispensible tool for symbolic reasoning.
Amongst other things it will enable them to leverage artificial intelligence to aid their own intellectual enquiries.
However artificial intelligence will not, at least not in the foreseeable future, supplant them.

[^occam]: The word Occam is used somewhat nebulously here.
It is most often associated with Occam's IDE but in fact it encompasses divers software and services.
This book explains these practical parts and there is a companion book, called The Foundations of Symbolic Reasoning, that covers the underlying theory.

[^florence]: Occam was originally called Florence but the former seemed more apt.

@footnotes

@pageNumber
