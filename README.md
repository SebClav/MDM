<h1 align="center"> MDM (Mask Development Model) </h1>

<p align="center">
  <img src="https://github.com/user-attachments/assets/9b959d90-1988-429d-b4f1-ee88285ffa36" width="100" alt="Project Grampus MDM">
</p>


<p align="center">
Compile your domain knowledge into an executable mask, instead of retraining a model.
</p>



## What is MDM?

MDM is a file format and a small toolchain for serving deterministic domain knowledge without invoking a language model.


The idea is simple. For a query whose answer is a known, formally established fact, a language model is the wrong tool: it spends computation and can still answer incorrectly, because its output is governed by statistical likelihood rather than by verification. MDM takes the deterministic knowledge of a domain, written by a human in a readable source file, and compiles it into a mask: a unit that answers those queries directly, retrieving the fact instead of generating it.

A mask does three things for the queries it covers:

- **Retrieves** the answer directly from compiled knowledge, without a model and without consuming tokens.
- **Vetoes** explicitly listed wrong statements, so a known incorrect answer is never emitted.
- **Keeps sensitive values local**, resolving them against the mask instead of sending them to a model.


Queries the mask does not cover, such as open problems with no settled answer, are routed to a language model, which remains responsible for everything that genuinely requires reasoning or generation.

## What MDM is not


MDM does not replace language models, and it does not improve their reasoning. It only removes the model from the path for the fraction of queries that are factual and deterministic. Its usefulness scales with how much of that kind of traffic a system handles.

- The retrieval guarantee is exact match.
- Paraphrased errors are not caught.
- Masks are authored by hand.


## Why it matters


In settings where data must stay private, such as hospitals, small and medium businesses, and public institutions, sending every query to a cloud model is not always acceptable. MDM lets the deterministic part of the workload be answered locally, on ordinary hardware, without a GPU and without sending data to a third party.


## Part of Project Grampus


MDM is a component of Project Grampus, a broader effort exploring how to decide when a language model should be involved at all. MDM provides the deterministic foundation: the layer that answers what is already known, so the model is reserved for what is not.


<p align="center">
  <em>"Attention is just your last resort."</em>
</p>
