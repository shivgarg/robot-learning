Contributions: 

1.    Proposed a new operation namely EdgeConv to learn local dependencies for classification and segmentation tasks: This layer improves upon previous implementation treating the points independently, is permutation invariant, plus easily integrable in a 3d point cloud processing model 

2.    Experiments with dynamic updates to graph: In contrast with previous fixed graph approaches, they demonstrate the benefit of dynamic updates to graph in each layer. 

3.    Perform ablation studies as compared to previous work and give some qualitative results for better understanding and justification for their new layer. 

 

The paper builds upon the idea of PointNet, by using 3D point cloud as in in deep learning models and extending it adding an EdgeConv layer to learn local geometric relations in contrast to independent handling in PointNet. The PointNet/PointNet++ operator, CNN operator is a special case of the edge conv operator.  The Edge Conv is permutation invariant but is not translation invariant.  The graph is computed at each layer using kNN algorithm. The distance is measured in the Euclidean space. The k is a hyperparameter. It is mentioned that large k leads to degradation performance.  I found the use of Euclidean not well motivated. Though in the initial layer it is intuitive to use it to capture local geometry, but this may not hold for higher layers since the vectors start encoding certain semantic information. Some experiments with a different metric function would have been nice.  

The approach has SOTA results on ModelNet40 dataset. The qualitative results show good patterns with the semantic alignment. And the runtime of the model is much better as compared to previous approaches with similar accuracy measure. But I found it to be counterintuitive why the model performs worse when compared to existing approaches on part segmentation/segmentation. The whole hypothesis is that the local information is helpful in 3d vision tasks and it should help the part segmentation task too. Probably some analysis of failure cases would have given some insight.  

A good extension would be to construct a weighted graph (weights as a function of distance) instead of the hard graph currently used in the implementation. Also, the O(N^2) implementation is slow at each layer and I have read about some optimizations made in NLP (transformer attention head mechanism) and probably they could be ported here too.  

 

 