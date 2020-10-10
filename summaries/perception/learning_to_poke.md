Contributions:
1.	Proposes an approach to model the dynamics of robot’s interactions directly from images, by proposing two models forward and backward, one for both dynamics.
2.	The joint model generalizes to unseen scenes and objects by achieving goals in situations having significantly different visual appearances
3.	The experiments show the role of forward model in regularizing the inverse model. 

The paper approaches the problem of learning intuitive physics model of the world without using any prior information/modelling of the environment. The input to the model is the RGB image of the current state and the rgb image of the goal state and the output is the poke vector (p, angle, l). 

To achieve this, the problem is modelled as two models, forward and inverse models, where the inverse model takes in two images and outputs a poke to achieve the goal state. The forward model takes in the poke vector and the current state image and outputs the latent representation of the next state.  The forward model is trained to output the latent representation since predicting the pixel wise image is quite hard and exact reconstruction is not always needed for downstream tasks. Having the inverse model adds constraints to the optimization problem of the forward model. The images are passed through AlexNet to get a vector representation for each image. 

The evaluation is done by asking the inverse model to predict the poke vector to displace the object from a start frame to the position as shown in the goal frame. The evaluation is done over unseen objects, thus signifying generalizability of the process.  The inference process is sequential with the most likely poke vector chosen at each step and is applied to the simulator.  This has its limitations of being unable to move around the objects, The baseline is a simple blob model , which detects the object based on object detector and calculates the poke vector based on the vector difference of the position. 

The results are pretty good as they tell that the model learnt to detect position and pose of the objects. The joint and inverse model both outperform in the pose error metric, and the joint model has performance equivalent to the baseline model in the relative location error.  

Questions
1.	Why poke vector space discretized? Could have been formulated as a regression problem. 
2.	Why couldn’t the model learn to go around obstacles?
3.	I would like some clarification/insights about why the model performs at par with the simple baseline on position error.
4.	The modelling has a markovian assumption. So, can using n frames from history help to increase precision of poke vector. 
