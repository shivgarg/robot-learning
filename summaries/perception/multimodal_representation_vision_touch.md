Contributions: 

1.    Propose a neural network to learn state representation from multi-modal data. 

2.   Show that the learnt representation from visual, haptic, and proprioceptive data helps to learn policies in a sample efficient way. 

3.    Demonstrate that the learnt representations and policy transfer to different peg shapes and the learn representation are robust perturbations and sensor noise. 

 

The paper main contribution is to leverage multi-modal data to learn control policy. The problem is divided into two parts: learning state representation and using the state representation to learn the policy. The control problem is modelled as finite-horizon discounted MDP  

The state representation network uses four networks to encode visual, haptic, proprioceptive, and next action data into vectors. The networks are trained in a self-supervised way by using three loss functions: 1. Optical flow: Available from robot geometry, kinematics, and proprioception. 2. Contact or not: Heuristics on Force sensor readings. 3. Alignment of input space.: sampling procedure in the data.   

The environment is model-free, i.e. no model of the environment I used which helps to account for uncertainty and eliminates the need for an accurate model. The policy is learnt by using TRPO and the output of policy is the 3D vector of displacement. The policy net takes in the learnt state representation and the model weights of the state encoders are frozen to assist faster training of the policy.  A set of four staged reward functions are used to learn the policy. The paper evaluates on 5 variations of peg insertion, each differing in shape of peg. The experiments were run in simulator for the ablation study to show the importance of visual and haptic input.  

The paper is well written, with well-motivated decisions and extensive experiments both in simulator and real robot.  The results of the paper are promising that the learnt representation make the RL training part sample efficient and the features tend to transfer to similar environments and are robust to slight perturbations. This work precedes the CSWNs and Object Keypoint detector, but in the qualitative results in those papers, the features maps learn to localize to an object, maybe something similar is happening here. 

Avenues for improvement are to extend to larger DOF’s and maybe with different types of noises, like changing background/ changing lighting/ randomly masking data in vision and haptic data streams. 

Questions/Concerns: 

1.    Why optical flow loss is used, instead of maybe pixel wise reconstruction loss or contrastive loss? 

2.    For the PD impedance controller, why acceleration is modelled as au =ades-kp(x-xdes)-kv(v-vdes). I have little background in robotics hardware.  

3.    Details about how the constants in the reward formulation are chosen. 

4.    Details about the perturbations applied/sensor noise introduced missing. 

5.    Why other techniques like VAE etc. not considered with for state representation learning? 

 