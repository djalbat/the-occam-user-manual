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
I had not heard of large language models when I started out and they were never a motivating factor but as I came to my first milestone after those many years, they began to loom large.
Their emerenge has not changed my view on the relationship between software and humans apropos of reasoning, however.




In fact on this subject I would like to make a few points clear about what Occam is good for.

[^1]: The word Occam is used somewhat nebulously here.
It is most often associated with Occam's IDE but in fact it encompasses a range of software and services.
This book explains these divers parts and there is a companion book, called The Foundations of Symbolic Reasoning, that covers the underlying theory.
[^2]: Occam was originally called Florence but the former seemed more apt.