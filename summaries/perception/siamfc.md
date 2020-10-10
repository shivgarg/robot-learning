Contributions:
1.	Proposes a method to learn similarity metric using deep CNNs from labelled data.
2.	The deployment is completely online, without requiring any expensive backpropagation steps during inference time.
3.	The proposed network runs in real time.

The paper works on Visual Object tracking problem where a single object demarcated in the first frame is tracked in the video. The paper proposes a deep learning-based approach based on Siamese networks.  It is the first approach DL based approach which works in real time. The approach Is straightforward. A fully convolutional network is learnt which embeds the object in an embedding space. The function f (z, x) compares an exemplar image z to an image x and return a score quantifying the level of similarity.

f (z, x) =g(φ(z),φ(x))

The φ is a network which when given an image as input, outputs a representation of the image. The function g is a measure of similarity, can be L1, L2 distance, correlation etc. The exemplar can be the features extracted from the first frame or updated with new features for prediction made in each frame.  Thus, for each location in the search image, a score is output quantifying the similarity to the object being tracked. The one with the maximum score is selected as the position of the object.  The network is trained using a logistic loss with data coming from ILSRVC video object detection. The paper gives detailed results on the VOT benchmarks. The method is competitive on all the three benchmarks, consistently having metrics beating or comparable to the top performing tracker. Among the top performing methods only SiamFC runs in real time, 86fps for 3 scale version, 56 fps for 5 scale version. Demonstrates that ImageNet dataset provides sufficient variety to achieve top line results on varied benchmarks. The 3-scale version outperforms 5 scale one on all benchmarks.

Limitations:
1.	The method struggles with disambiguation as shown in the qualitative results.
2.	There are a lot of tunable parameters for e.g.:
    *	R, radius for positive examples
    *	Scale choice to accommodate size change.
    *	Positive example mining from T frames apart.
3.	This method scales linearly with objects to be detected. For multi-object tracking, this method may lose real-time nature.

Future Work:
1.	Use ranking losses since relative score is important not the absolute ones.
2.	Add bounding box regression to the approach for better fine-tuned boxes for better results.

