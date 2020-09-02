Contributions:
1.	Introduced a new layer RoIAlign, improving upon previous version RoIPool and RoIWrap
a.	Leads to significant improvement in the existing object detection system 
2.	Demonstrated a multi-task system to do object detection, classification, instance segmentation and keypoint detection together.
a.	Implementation to leverage multiple tasks for improved individual task performance.
3.	An end to end trainable system, with a short training time.
a.	Released code and with a smaller training time, the experimentation with instance segmentation is made quicker.

This paper builds upon Faster RCNN by introducing a parallel mask prediction branch in addition to existing classification and object detection branch. The RoIPool layer in the network is replaced by RoIAlign layer which extracts the feature map without quantizing the feature map indexes. The implementation beats the 2016 COCO contest winners.  A multitask loss combining classification, object detection and instance segmentation in equal proportions is used. The mask branch only predicts the segmentation mask for each of the K classes thereby offloading the classification task on to the object classification branch.  The authors performed a lot of ablation studies evaluating different parameters.  I would have preferred more qualitative results for Class-specific vs class-agnostic case.  The results here are close. Maybe class specific masks are not needed at all, some results about masks predicted by different class masks would have helped. My hunch is that most of the class specific masks may be predicting similar mask boundaries, just the class specific is one more fine.
The paper is well written, with a lot of experiments to support their decision/claims. The code has been released along with pretrained models. The paper is easy to read and well written. For future work, I think there should be a focus on smaller objects since the performance gap is huge between small and medium objects. 

