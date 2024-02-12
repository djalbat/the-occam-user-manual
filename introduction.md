# Introduction

I have tried to make Occam[^1] as useable as possible but there are limits.
At the end of the day it is an expert system and some of its parts, not least the verifier, need detailed explanations.
It is the purpose of this book is to provide these explanations.

It also goes into consdierable detail on the subject of Occam's approach to language, which basically boils down to its use of grammars.
Occam has what might be called a default language or vernacular, called Florence,[^2] but it will also support what is called Controlled Natural Language in the near future.
Indded, the verifier cannot distinguish between these languages at all.
This book explains how this is possible.

After explaining Occam's approach to language this book gives a very detailed explanation of how the verifier works.
Some may find this explanation nauseating but I maintain that it is essential.
The whole idea behind Occam is to facilitate human reasoning and not to supplant it, and it is the verifier that reasons on your behalf.
So you must understand how it does this.
In fact I recommend that you read the introduction together with the first four chapters of the Foundations book before going much further with this one.
They are neither very long nor very deep and will provide the necessary background for understanding the verifier in particular.

I hope that the verifier's implenentation is both transparent and readable, and therefore understandable, especially augmented as it is with the explanation here.
Apart from anything else any genuine understanding of it will likely save a good deal of frustration when you begin to work seriously with Occam.
The other need for a genuine understanding is that the verifier and is therefore not verifiable itself.
So you cannot simply press a button and have confidnece in it, that is not the idea at all.

In fact, at the risk of courting controversy, I would argue that it should not be the idea with any verifier.
All are failible regardless of what their proponents may claim and therefore I do not believe that their results should ever be trusted without some level of human oversight.
Indeed in my opinion verification should be an aid to clarity and rigour and never a substitute for it.
The idea of a proof as a black box in particular is anathema to me.

Moving on, the standpoint that software should be an aid to human reasonibg and not a substitute for it must these days be tempered by a consideration of artificial intelligence as a tool for reasoning.
What kept me going over the near decade of work that it took to get Occam to its first viable release was a firm belief in what I call the four elephants, expounded in the aforementtioned first four chapters of the Foundations book.
I had not heard of large language models when I started out and they were never a motivating factor, but as I came to my first milestone after those many years, they began to loom large.
Their emergence has hardly changed my view on the relationship between software and humans apropos of reasoning, however.

Admittedly of late there has been some progress in the direction of coupling artificial intelligence models with formal inference systems and the results have been promising.
For its part Occam only has a bearing on the right hand side of this coupling, so to speak.
It is much more flexible and extensible than a tool where the inference rules are hard-coded, however.
Moreover, on the left hand side, so to speak, the output of any large language model or similar system can serve as input for Occam.

Thus the panacea of using computers as tools for symbolic reasoning, be that devising algorithms or protocols; mathematics or logic; or whatever, is almost upon us.
And it is worth pointing out that this panacea has been anticipated for around seventy five years now.
There is no doubt that artificial intelligence is on the verge of bringing of all this about, but without tools such as Occam the output of these systems will always be clouded in doubt.
So there is nothing to fear from artificial intelliegence, at least in this realm of human endeavour.
I hope and expect Occam to become a potential tool for anyone working in any field of symbolic reasoning in the coming years.
It will enable them to leverage artificial intelligence to aid their own enquiries but never, at least for the foreseeable future, is it going replace them.

[^1]: The word Occam is used somewhat nebulously here.
It is most often associated with Occam's IDE but in fact it encompasses a range of software and services.
This book explains these divers parts and there is a companion book, called The Foundations of Symbolic Reasoning, that covers the underlying theory.
[^2]: Occam was originally called Florence but the former seemed more apt.