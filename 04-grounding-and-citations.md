# Grounding and citations

Retrieving the right chunks is only half the job. The model still has to answer from them rather than from its own prior knowledge, and ideally it should show which chunk each claim came from. Grounding is the practice of tying the answer to the supplied sources, and it is what makes a RAG answer trustworthy and checkable rather than just plausible.

## The grounding problem

Given relevant chunks in the prompt, a model may still answer from its training rather than from the chunks, blend the two, or state something the chunks do not support. This is the central failure mode of RAG: a confident answer that the supplied sources do not actually back. The model is good at producing fluent text, and fluency is not the same as faithfulness to the sources. Grounding techniques push the model to use the supplied material and to be honest when the material does not contain the answer.

## Instructing for grounding

The prompt should tell the model to answer using only the supplied sources, to say clearly when the sources do not contain the answer rather than guessing, and not to rely on outside knowledge for factual claims. This does not guarantee faithfulness, but it meaningfully shifts behavior, especially the instruction to admit when the answer is not in the sources. A model that will say the provided material does not cover this is far more useful than one that fabricates a confident answer, because the first is honest about the gap and the second hides it.

## Citations and attribution

Asking the model to cite which source each part of its answer came from serves two purposes. It lets the user verify the answer against the original, which is the only reliable check on faithfulness, and it tends to improve faithfulness itself, because attributing each claim to a source nudges the model to actually base claims on the sources. Carrying source metadata through retrieval so each chunk can be identified, and asking the model to reference those identifiers, gives an answer a user or a downstream check can trace back. An answer you can verify is worth far more than one you have to trust blindly.

## Verifying faithfulness

For systems where correctness matters, you can add a check that the answer is actually supported by the retrieved chunks, rather than assuming it is. This can be a separate step that compares the claims in the answer against the sources and flags unsupported ones. It catches the case where the model produced a fluent answer that drifted from the material. This is more work, and not every application needs it, but for anything where a wrong answer is costly, verifying that the answer is grounded in what was retrieved is the difference between a demo and a dependable system.

## Honesty about gaps is a feature

The most underrated grounding behavior is the model declining to answer when the sources do not support one. It feels like a worse product to return the material does not cover this rather than a confident guess, but it is far better, because a wrong confident answer erodes trust in every answer the system gives. A RAG system that reliably says when it does not know, and grounds and cites when it does, earns the user's trust in a way that a system which always answers, sometimes wrongly, never can. Design and prompt for that honesty rather than against it.
