Contributions: 

1.    Transporter architecture to learn visual features and keypoints for RL tasks. 

2.    Demonstrates using keypoints are input leads to sample efficient RL with policies having better returns on Atari games. The learnt keypoints are well aligned spatially, temporally, and geometrically. 

3.    Demonstrates on using keypoints for exploration leads to efficient exploration. Exploration using most controllable keypoints gives better results than random exploration. The learnt skills over keypoints are task agnostic and can be used for any task. 

 

The paper presents a method to learn representation of a state alongwith learning keypoints of objects. The keypoints are coordinates in the input 2D image depicting locations of object keypoints in an image.  The method to learn keypoints uses a KeyNet which generates K feature maps and they are aggregated using fixed variance isotropic gaussian. The main idea is for two frames at time s and t, s<t, the network learns a representation for the frames and interpolates the frame by removing the features at keypoint at time s and adding the feature values at keypoints at step t. The learning objective is the pixelwise L2 reconstruction loss.  

For learning options grounded in the keypoints, the paper defines kx4 q functions learning to maximize the return, where the return is defined as the distance travelled in a up, down, left, and right directions, respectively. The search space is then reduced to choosing from the set of kx4 q function space and rolling out the policy for n steps before making an update. All the q-functions are trained from the accumulating replay buffer. The paper introduces concept of controllability policy where the keypoint having max difference in the Q return values is used for exploration. These learnt options are task agnostic and can be applied to any task. 

The authors justify their hypothesis/claims through various ablation experiments. The approach is evaluated for 5 games in Atari ALE and Manipulator domains. The method outperforms the baselines in keypoint tracking. Also, the using keypoints as input leads to faster convergence with highest reward values demonstrating that keypoints are better than raw pixel values for input. Also, the random exploration average reward is higher when using the options action space instead to random exploration using actions. 

The paper is well explained barring the section on exploration mechanism. It could have been written more clearly. The works seems to me to be quite like CSWMs, since there instead of keypoints, object maps are used. The reconstruction loss there is the contrastive loss as opposed to l2 loss here. Like CSWMs, there is little motivation as to why thing approach works, like k maps produce just one keypoint. Do not see any inductive bias here to do so. 

Questions/Limitations: 

1.    Why target frame up to 20 frames away is chosen for learning the network weights? 

2.    The keypoint selection dependent on the domain, the max number of keypoints needs to be predetermined. 

3.    The authors mention that the network needs to be retrained for each domain. This retraining may offset any benefit of sample efficient RL or better exploration strategies. 

  

 