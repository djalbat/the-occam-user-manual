# Introduction

I have tried to make Occam[^1] as useable as possible but there are limits.
At the end of the day it is an expert system and some of its parts, not least the verifier, need detailed explanations.
It is the purpose of this book is to provide these explanations.

It also goes into consdierable depth on the subject of Occam's approach to language.
Occam has what might be called a default language or vernacular, called Florence,[^2] but it will also support what is called Controlled Naatural Language in the near future.
Indded, the verifier cannot distinguish between these languages at all.
This book explains how this is possible as well.

AFter explaining Occam's approach to language, which basically boils down to grammars, this book gives a very detailed explanation of how the verifier works.
Some may find this interminable but I thought that since it, like the rest of Occam, is written in JavaScript, this explanation was essential.
Indeed the whole idea behind Occam is to facilitate human reasoning, not to supplant it.
I hope htat the verifier's implenentation is both transparent and readable, especially augmented with the detailed explanation here, and you are strongly encouraged to get to grips with it.
Apart from anything else this will save a good deal of frustration when you begin implementating mathematics, logic or whatever with Occam.

In fact on this subject I would like to make a few points clear about what Occam is rea

[^1]: The word Occam is used somewhat nebulously here.
It is most often associated with Occam's IDE but in fact it encompasses a range of software and services.
This book explains these divers parts and there is a companion book, called The Foundations of Symbolic Reasoning, that covers the underlying theory.
[^2]: Occam was originally called Florence but the former seemed more apt.