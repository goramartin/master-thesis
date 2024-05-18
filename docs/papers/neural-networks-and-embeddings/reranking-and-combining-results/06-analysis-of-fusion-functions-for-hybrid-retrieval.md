# An Analysis of Fusion Functions for Hybrid Retrieval

- [Link](https://dl.acm.org/doi/10.1145/3596512) (late 2023)
 
We study hybrid search in text retrieval where lexical and semantic search are fused together with the intuition that the two are complementary in how they model relevance. 

In particular, we examine fusion by a convex combination of lexical and semantic scores, as well as the reciprocal rank fusion (RRF) method, and identify their advantages and potential pitfalls. 

Contrary to existing studies, we find RRF to be sensitive to its parameters; that the learning of a convex combination fusion is generally agnostic to the choice of score nor- malization; that convex combination outperforms RRF in in-domain and out-of-domain settings; and finally, that convex combination is sample efficient, requiring only a small set of training examples to tune its only parameter to a target domain.

Previous things with hybrid:
    - [Leveraging Semantic and Lexical Matching to Improve the Recall of Document Retrieval Systems: A Hybrid Approach](https://arxiv.org/pdf/2010.01195) (2019)
    - [Out-of-Domain Semantics to the Rescue! Zero-Shot Hybrid Retrieval Models](https://arxiv.org/pdf/2201.10582) (2022)
      - contains a good references for hybrid
      - they use reciprocal rank fusion
      - Our findings show that the performance of a deep retrieval model is significantly deteriorated when the target domain is very different from the source domain that the model was trained on. On the contrary, lexical models are more robust across domains.
      - They say it outperforms convex combination.

They want to find out how fusion is done.

Results:
- They find out that convex combination is not necessarily shortcomed with normalization choise. And is a good choise for across domains.
- They find out that rrf generalizes poorly to out od domain datasets. They intuit that because rrf is a function of ranks, it disregards distribution of scores and discards usefull information. Observe that the distance between raw scores plays no role in determining their hybrid score - which is counter intuitive.
- Tuning alpha in convex combination is extremely sample efficient, requiring just a handful of labaled queries to arrive at a value suitable for a target doomain. RRF is less sample efficient and converges to relatively less effective retrieval system.

Our analysis leads us to believe that the convex combination formulation is theoretically sound, empirically effective, sample-efficient, and robust to domain shift. Moreover, unlike the parameters in RRF, the parameter(s) of a convex function are highly interpretable and, if no training samples are available, can be adjusted to incorporate domain knowledge.