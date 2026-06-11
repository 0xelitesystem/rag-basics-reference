# What RAG is

A language model knows what it learned during training and what you put in its prompt. It does not know your private documents, anything published after its training, or details too specific to have been learned. RAG solves this by fetching relevant information when a question arrives and placing it into the prompt, so the model answers from material it would not otherwise have. The model still does the writing; RAG supplies the facts.

## The problem it addresses

Two limits drive the need for RAG. First, a model's knowledge is fixed at training time and has a cutoff, so it cannot know recent events or your specific data. Second, prompts have a size limit, so you cannot simply paste an entire knowledge base into every request. RAG addresses both by selecting only the relevant pieces for each question and including just those. It is the practical answer to: how do I make this model answer accurately about content it was never trained on, without stuffing everything into the prompt?

## The basic loop

RAG has two phases. The first happens once, ahead of time: you take your documents, split them into manageable pieces, convert each piece into a numerical representation that captures its meaning, and store those in a way you can search. The second happens on every question: you convert the question into the same kind of representation, find the stored pieces most similar to it, and place those pieces into the prompt alongside the question, instructing the model to answer using them. The model reads the supplied pieces and writes an answer grounded in them.

## Why not just fine-tune the model

A common alternative is to train the model further on your data, called fine-tuning. Fine-tuning changes how the model writes and can teach it patterns, but it is a poor way to inject facts you need to keep current or to cite. Facts baked in through training are hard to update, hard to attribute to a source, and prone to being blended or misremembered. RAG keeps the facts in a store you control, so you can update them by changing documents rather than retraining, and you can point at exactly which document an answer came from. For factual, changing, or citable knowledge, retrieval usually beats baking it into weights.

## What RAG does and does not give you

RAG gives the model access to relevant, current, specific information at answer time, and a basis for citing where an answer came from. It does not make the model smarter, and it does not guarantee a correct answer, because the model can still misread or ignore the supplied pieces, and because the retrieval can fetch the wrong pieces. RAG is a way to put the right material in front of the model; the quality of the answer still depends on whether the right material was retrieved and whether the model used it faithfully. The rest of this reference is about getting both of those right.
