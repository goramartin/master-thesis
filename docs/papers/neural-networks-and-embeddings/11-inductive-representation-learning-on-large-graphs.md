# Inductive Representation Learning on Large Graphs

[Link](https://arxiv.org/abs/1706.02216)

## Mostly ideas

Learn ebeddings with the graphSage on wikidata with a bit different graph structure.
The node features would contain the embeddings of textual representations for the nodes.
The question would be how to create an embedding of the query?
Maybe one could find the entities represented in the query.
And then compute final similarity with the found entities and the entities in candidate set based on the graph sage embeddings?