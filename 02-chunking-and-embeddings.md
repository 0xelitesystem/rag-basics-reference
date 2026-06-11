# Chunking and embeddings

Before you can retrieve relevant pieces of your documents, you have to break the documents into pieces and make those pieces searchable by meaning. These two steps, chunking and embedding, are the preparation phase of RAG, and the choices you make here shape how well retrieval works later. Poor chunking is one of the most common reasons a RAG system retrieves the wrong thing.

## Why you chunk

You split documents into chunks for two reasons. First, you can only fit so much into a prompt, so you need pieces small enough that several fit alongside the question. Second, retrieval is more precise on smaller pieces: a whole document is about many things, so matching a question to it is coarse, while a focused paragraph matches a specific question cleanly. The aim is chunks that are each about one coherent thing, large enough to carry meaning on their own but small enough to be specific.

## How chunk size matters

Chunks that are too large dilute relevance, because a big chunk contains both the relevant sentence and a lot of unrelated text, which weakens the match and wastes prompt space. Chunks that are too small lose context, because a sentence pulled from its surroundings may not make sense or may match on a word while missing the meaning. The right size depends on your content, and it is worth tuning rather than guessing. Overlapping chunks slightly, so each shares a little text with its neighbors, helps avoid splitting a relevant idea across a boundary where neither half matches well.

## Respect the structure of the document

The best chunk boundaries follow the document's own structure rather than cutting at a fixed character count. Splitting on headings, sections, or paragraphs keeps each chunk about a single topic, which is exactly what makes retrieval precise. Cutting blindly every so many characters tends to slice through the middle of an idea, leaving chunks that each carry half a thought. Where documents have clear structure, use it; where they do not, paragraph and sentence boundaries are better cut points than arbitrary lengths.

## What an embedding is

An embedding is a list of numbers that represents the meaning of a piece of text, produced by an embedding model. The key property is that texts with similar meaning produce embeddings that are close together in this numerical space, even when they share few exact words. This is what lets retrieval match a question to a relevant chunk by meaning rather than by keyword: a question about resetting a password can match a chunk about account recovery, because their embeddings are near each other, despite the different wording.

## Storing them for search

Each chunk's embedding is stored, usually in a vector store, alongside the chunk's text and any metadata you want, such as its source document, section, or date. The vector store's job is to take a query embedding and quickly return the stored chunks whose embeddings are closest to it. Metadata stored with each chunk lets you filter, for example to recent documents or to a particular source, and lets you tell the model and the user where a retrieved piece came from. Getting chunking and embedding right is most of what makes the retrieval step return useful material rather than near-misses.
