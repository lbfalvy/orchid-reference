# Introduction

Orchid is an embeddable declarative programming language. It can be thought of as an extension of a configuration format that supports functions and complex logic. In this regard it occupies a similar niche to Lua.

Because the language is fully sandboxed and all interaction with the external world is defined by the embedder, standard I/O is rather unimportant, so this guide focuses on demonstrating the internal logic of the language and I/O facilities are only explained as and when they are needed to demonstrate a concept.