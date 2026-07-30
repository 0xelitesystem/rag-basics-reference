# RAG Basics Reference

Retrieval-augmented generation, or RAG, is a pattern for giving a language model relevant information at the moment it answers, instead of relying only on what the model learned during training. You store your documents, find the pieces most relevant to a question, and put those pieces into the prompt so the model answers from them. It is how you make a model answer about your own content, recent information, or anything too large or private to put in the prompt wholesale.

This reference explains the pattern in plain language, end to end.

## What is inside

- [01-what-rag-is.md](01-what-rag-is.md) the problem it solves and the basic loop
- [02-chunking-and-embeddings.md](02-chunking-and-embeddings.md) splitting documents and turning them into searchable vectors
- [03-retrieval-and-ranking.md](03-retrieval-and-ranking.md) finding and ordering the most relevant pieces
- [04-grounding-and-citations.md](04-grounding-and-citations.md) making the model answer from the sources and cite them
- [05-when-rag-helps-and-when-it-doesnt.md](05-when-rag-helps-and-when-it-doesnt.md) choosing RAG over the alternatives

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright (c) 2026 0xelitesystem.
