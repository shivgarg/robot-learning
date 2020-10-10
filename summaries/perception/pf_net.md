Contributions: -
1.	Encodes the particle filter algorithm as a neural network for e2e learning.
2.	Demonstrates the efficacy of the architecture on visual localization in a simulator environment.
3.	Shows the applicability of the method to multiple sensors input.

The paper proposes a way to run particle filter algorithm as a neural network.  The approach involves two stages, the first modelling the transition function. The transition function is modelled to convert action to global action space and a gaussian noise is added to the final state to mimic the sampling behaviour. The observation stage is also modelled as a neural network which takes as input, the state representation, 2D map, RGB image and other sensory data and applies CNN, LFC and FC layers to output a score about the likelihood of the state given the 2D map and sensory input.  

Another technique that is introduced is the soft resampling, to enable flow of gradients when the particles are resampled and need to be uniformly weighted. So instead of uniform weighing, a weighted score is chosen between uniform 1/K and wk. 

The loss function is the L2-distance of the ground truth x, y, and pose from the predicted values. 
The overall writing of the paper is clear, and the PF net architecture is explained clearly by referring to all the existing work.  The results are good when to compared to existing work.  The approach beats the previous work on tracking, global localization, and semi global localisation task, by just training the network on the tracking task, depicting the approach robustness towards varied level of noises. The soft resampling leads to mixed results with poor performance on tracking task but better performance on global localization which is inherently noisier and intuitively requires resampling for better results. 

Some concerns:
1. Loss function is L2-norm, which is sensitive to outliers. Probably use Huber loss
2. No experiments with real robot.
3. Try to present some results without a 2D map, or a map learnt on the fly.
4. Choice of 4 timesteps seems arbitrary to me for gradient backpropagation.

Future Work
1.	Consider the setup in a multi-agent problem, by forming graph nets to coordinate actions.
2.	Apply the formulation to object tracking in videos.


