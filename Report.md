## Udacity Deep Reinforcement Learning Nanodegree 
## Project 1: Navigation

### Learning Algorithm

In this project the environment is solve by using the DQN Reinforcement Learning Algorithym. The DQN takes the state as input and predicts  the action value as per the current policy in order to maximize the expected reward for all future states with the current policy. 
Then the agent takes the action and receives a reward and the next state from the environment. This information is used to update the weights in the DQN to better match predictions with observations and the iteration continues and the target average reward is reached. 
This algorithym is also enhanced with experience replay to randomize state-action-reward tuples in order to prevent biasing the DQN towards correlated state-action pairs. This also enables to benefit from rare occurances. 


### Deep Q-Network Architecture

Since 37 discrete states are present in the environment in contrast to raw pixel data, convolutional layers were not necessary in the nural network. Only two fully connected hidden layers with ReLu activation were used in the nural network. 
Each hidden layer consists of 64 neurons each. 

#### Hyperparameters

- `BUFFER_SIZE = 10000` is the number of experience tuples `(state, action, reward, next_state, done)` that are stored in the replay buffer and avaiable for learning
- `BATCH_SIZE = 64` is the number of tuples that are sampled from the replay buffer for learning, i.e. the minibatch size.
- `GAMMA = 0.99` is the discount factor that controls how far-sighted the agent is with respect to rewards. `GAMMA = 0` implies that only the immediate reward is important and `GAMMA = 1.0` implies that all rewards are equally important, irrespective whether they are realised soon and much later
- `TAU = 0.001` controls the degree to which the target Q-network parameters are adjusted toward those of the local Q-network. `TAU = 0` implies no adjustment (the target Q-network does not ever learn) and `TAU = 1` implies that the target Q-network parameters are completelty replaced with the local Q-network parameters
- `LR = 0.0001` is the learning rate for the gradient descent update of the local Q-network weights
- `UPDATE_EVERY = 4` determines the number of sampling steps between rounds of learning (Q-network parameter updates)
- `epsilon` controls the degree of exploration vs exploitation of the agent in selecting its actions. `epsilon = 0` implies that the agent is greedy with respect to the Q-network (pure exploitation) and `epsilon = 1` implies that the agent selects actions completely randomly (pure exploration). In this project, `epsilon` was initially starts from 1.0 and decays by a factor of 0.995 after each episode until the min. epsilon of 0.01 is reached.


#### Results

The environment isolved by reaching +13 average scores over 100 episodes after less than 600 episodes. The accumulation of rewards are given in the figure below:

![830D65CC-DF64-46FE-92FD-008A2B585E89_4_5005_c](https://user-images.githubusercontent.com/66205537/159553514-faa7c9c1-d637-44f2-b4e1-0ecee45c21fb.jpeg)

The average scores for every 100 episodes are as follows:

![0465E05E-CE57-4B20-B90C-C4BB9F53F23E_4_5005_c](https://user-images.githubusercontent.com/66205537/159553629-049b3b2a-05a6-4067-a78c-7233d01e016e.jpeg)


#### Future Improvements

Although the results are quite satisfactory they can still be improved :
1. Further variation and optimization of hyperparameters. Expecially the learning rate is quite effective and it can be varied to see some quicker results can be optained.
2. Employing a prioriterized experience replay. This provides more learning from experience tuples which has TD error close to zero. 
3. Employing a duelling network. That would combine to estimotrs, i.e. one for the state value function and one for the state advantage function
