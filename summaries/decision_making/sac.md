Contributions:
1.	Proposes an automatic gradient-based temperature tuning method that adjusts the expected entropy over the visited states to match a target value.
2.	Evaluates SAC over popular RL benchmarks and improves average reward along with sample efficiency.  
3.	Evaluates the algorithm on real-world locomotion tasks (four-legged robot) and hand manipulation and demonstrates end to end learning for the first time.

The paper addresses the problem of poor sample efficiency of deep RL model-free methods.  An algorithm in the actor-critic architecture is introduced which has separate policy and value function networks, which works in an off-policy way by reusing the samples and maximizes entropy to have better generalization and stable training.  The framework learns maximum entropy policies in continuous action spaces with discounted infinite horizons.

The objective of the policy is to learn a policy which maximizes the expected reward and the entropy of the policy weighted by a parameter, a hyperparameter.  Using entropy maximization has many benefits, as it encourages exploration and helps to find multiple modes of near optimal behavior.

The soft policy iteration is a combination of two steps: soft policy evaluation and soft policy improvement.  The evaluation steps involve the learning the Q function which accounts of entropy terms too.  In the policy improvement step, the learn Q function is used in the exponential form to determine the policy steps. To limit the policy space to tractable set, the learnt policy is projected into gaussians based family of distributions by minimizing the KL divergence. 

Both the steps are run alternately, optimizing the networks with SGD.  The hyperparameter temperature is hard to set and therefore, the framework is modified to optimize under constraints to keep the average entropy bounded. The dual of the problem is optimized for all the parameters of the network and entropy temperature. 

The experiments show that the algorithm is both sample efficient and the learnt policies have higher average reward.  The approach outperforms other state of the art by a huge margin.  Moreover, the paper demonstrates real-life use case and probably is the first one to showcase.

The paper is well written, but sometime obtuse to understand given a lot of previous work it refers to.  The mathematical proofs seem sound to me, but the purpose of all of it got lost because the function approximators (neural networks) do not have the assumptions made. So, I did not understand the need of the extensive mathematical analysis in the first place, because we are banking on the empirical results to prove the efficacy. 

Questions:
1.	The paper mentions that previous works use entropy maximization as a regularizer, and the current work uses it as an objective to optimize for. How is regularization different from maximization(optimization)?
2.	How multiple modes discovered using Gaussians? The mean of a single gaussian has a peak so do not understand, how multiple modes are modelled as Gaussian.
3.	How H, entropy bound chosen? Would not this be like temperature parameter?
4.	The paper claims that the harder tasks have a small basin of good hyperparameters. I do not understand this claim. What is the intuition behind this?
