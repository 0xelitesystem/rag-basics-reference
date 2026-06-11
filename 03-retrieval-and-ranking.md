# Retrieval and ranking

When a question arrives, the system has to find the chunks most likely to help answer it and decide which ones to actually include. This is the retrieval step, and how well it works determines the ceiling on answer quality, because the model can only use what it is given. A model with perfect reasoning still answers badly if retrieval handed it the wrong chunks.

## The basic retrieval

The straightforward approach embeds the question with the same model used for the chunks, then asks the vector store for the chunks whose embeddings are closest to the question's. Closeness in the embedding space approximates relevance of meaning, so this returns chunks that are about what the question is about, even when the wording differs. You take the top several and place them in the prompt. This semantic search is the heart of retrieval and works well when chunking and embeddings are sound.

## Why semantic search alone is not enough

Pure semantic matching has blind spots. It can miss exact terms, like a specific product code or name, because those carry meaning through their exact characters rather than their semantic neighborhood. It can also return chunks that are topically similar but do not actually contain the answer. Combining semantic search with traditional keyword search, so that exact-term matches are also caught, covers both kinds of relevance and is a common improvement. This hybrid approach retrieves on both meaning and exact terms, then merges the results.

## Ranking and re-ranking

The order of the chunks matters, both because you may only have room for a few and because models attend more to some positions than others. After an initial retrieval that favors recall, fetching a generous set of candidate chunks, a re-ranking step can score those candidates more carefully for how well each actually answers the question, and keep only the best. Re-ranking trades a little extra work for noticeably better precision, because the first pass is tuned to not miss anything while the second is tuned to pick the genuinely best, and the two goals are different.

## How many chunks to include

There is a balance in how much to retrieve. Too few chunks risk missing the piece that holds the answer. Too many dilute the prompt with irrelevant text, which can distract the model, push out the relevant chunk's influence, and cost more. The right number depends on your content and your prompt budget, and it is worth testing rather than assuming. A smaller set of highly relevant chunks usually beats a larger set padded with marginal ones, because the model's attention is finite and noise competes with signal.

## Use metadata and filters

Retrieval improves when you narrow the field before matching. If a question is clearly about recent information, filter to recent documents. If it names a product or section, filter to that source. Metadata stored with each chunk lets you cut the search space to the relevant subset before semantic matching runs, which both speeds retrieval and removes whole categories of wrong answers. The combination of filtering on metadata, retrieving on meaning and keywords, and re-ranking the candidates is what separates a RAG system that usually finds the right chunk from one that often does not.
