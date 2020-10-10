Contributions:
1.	Introducing NOCS coordinate space for objects, a concept of having shared normalized 3d space for objects of a particular type. 
2.	A new dataset creation procedure, by taking real background images and placing synthetic objects based on game engines and context awareness.  A new dataset is collected using real images and released for evaluation of such systems.
3.	SOTA results by using NOCS, semantic mask and object label to estimate the size of object along with orientation and location.

The paper proposes a method to do 6D Object Pose and Size estimation on unseen objects. It improves over the existing work by doing away with the need to CAD models.  A CNN is proposed which takes in RGB image and outputs object class, instance mask and a NOCS mask. The NOCS mask is a normalized 3D representation in a unit cube of the object. The CNN predicts a perspective transformation of the NOCS. The CNN architecture is borrowed from MaskRCNN and three heads to estimate NOCS map are added to it. This NOCS is used in conjunction with depth map to estimate the pose and size of the object. This NOCS map estimation does away with the need of CAD models.

Smoothed L1 loss is used to optimize the NOCS map head of the network if the problem is formulated as a regression, or a SoftMax as a classification.  The symmetry in objects is handled by creating multiple ground truth NOCS maps by rotating on the axis about which the object is symmetric, and the minimum loss is used for optimization.

The paper also proposes a new synthetic dataset generation technique by leveraging real background images and placing synthetic objects based on context.  They use Unity game engine and add the plane detection algorithm to identify tabletops and sample randomly to place an object on the surface. A couple of virtual light sources are placed to mimic shadows. 

The paper is written well, but I hope it could have been written better explaining the NOCS in detail. It took me a while to understand it. The work is original as far as my knowledge is concerned and the results are good. The absolute value of metrics shows a lot of work that still needs to be done.  The ablation studies are extensive, comparing all the moving parts of the network and giving insights into how different components improve the system. 

Questions:
1.	Why focus on table objects? The authors mention a couple of times about using only table-top objects, did not understand why they emphasized this fact.
2.	Why didn’t the authors use depth information from the starting, depth would have helped in better determination of NOCS maps? Though they say about using COCO for supervision, but they could have used a multimodal thing, ignoring depth input in COCO case.
3.	I did not understand how symmetric NOCS maps help to handle symmetric objects. Since symmetric objects after rotation would have same ground truth NOCs maps, why the extra maps needed?
