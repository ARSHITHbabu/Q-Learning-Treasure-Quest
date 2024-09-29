This repository showcases a Q-Learning implementation where two competitive agents compete to find the treasure in a grid-based environment. The project demonstrates the application of reinforcement learning using Q-Learning algorithms for agents to learn and adapt based on their interaction with the environment.


# **GETTING STARTED**


## ***Introduction :***

The concept of reinforcement learning allows agents to learn their optimal behaviors through interacting with an environment. The project has implemented the Q-learning algorithm for two competing agents who try to attain a treasure within a grid world. During their turns in moving around within the grid, they update their Q-values based on the reward that each of them receives after every move. The winner of the game is he whose reward at the end of the game is the largest.

---

## ***Objective :***

### *The main objective of this project is to*:

    Environment SetUp:Design a grid environment with agents moving, interacting, and competing.
    
    Ensure the environment is customizable to test various scenarios and settings.
    
    State Representation:We then develop a proper state representation for the agents that capture the critical features of the environment, such as agent and target positions.
    
    Reward Structure: Define a reward structure strongly that supports desired behaviors, such as reaching the target, avoiding obstacles, or penalizing unnecessary moves.
    
    Agent Cooperation/Conflict:This discusses the dynamics of cooperation and competition between agents by bringing support to mutual adaptation in strategy basing on an opponent's move.
    
    Exploration Techniques:Implement other exploration strategies (e.g., ε-greedy, softmax) and analyze how they affect the learning efficiency and effectiveness of the agents.
    
    Policy Recommendation:Analyze how the Q-Learning algorithm allows agents to improve their policies over time through iterative learning and experience.
    
    Parameter Fine-tuning:Experiment with various hyperparameters: namely, learning rate, discount factor, and exploration rate, to enhance agents' learning process and speed of convergence. 
    
    Performance Measures: Define and evaluate performance metrics to assess the agents' learning progress, including average rewards, number of episodes to convergence, and success rates.
    
    Visualization:Create visualizations of the agents’ learning process, including heatmaps of Q-values, reward distributions, and agent trajectories to better understand their strategies.
    
    Comparison with Other Algorithms: Compare Q-Learning to other reinforcement learning algorithms, such as SARSA and Deep Q-Networks, to point out strengths and weaknesses.
    
    Scalability:Investigate how the algorithm scales with an increasing number of agents or a more complex environment, analyzing computational efficiency and performance. 
    
    Real-World Applications: Discuss potential real-world applications of the developed algorithm, such as robotics, game AI, and resource management in multi-agent systems. 
    
    Learning Curve Analysis: Analyze the learning curve of each agent and describe how it relates the exploration-exploitation trade-off to overall performance. 
    
    Game Theory Aspects: Deduce from the strategies of agents some game-theoretic implications concerning ideas like Nash equilibrium for their mutual play.

---

## ***Methodology :***

1. ### *Q-Learning Algorithm :*
   
     Q-Learning is a model-free reinforcement learning algorithm. It trains agents to learn the value of being at a particular state and taking a particular action. Q-values are updated based on the Bellman equation.

     $$
Q(s, a) \leftarrow Q(s, a) + \alpha \left[ r + \gamma \max_{a'} Q(s', a') - Q(s, a) \right]
$$

Where:
- $Q(s, a)$ is the current estimate of the action value for action $a$ in state $s$.
- $\alpha$ is the learning rate (0 < $\alpha$ ≤ 1).
- $r$ is the reward received after taking action $a$ from state $s$.
- $\gamma$ is the discount factor (0 ≤ $\gamma$ < 1).
- $s'$ is the next state after taking action $a$.


2. ### *Environment Setup :*
   
  The environment for this project shall be designed as a grid where two competing agents are engaged in the task of locating treasure. The grid is structured with a predefined layout that consists of various cells representing the following states:

    Treasure Cell: The ultimate goal for both agents, represented as the cell containing the treasure. When an agent reaches this cell, it receives a reward of +100 points.

    Wall Cells: These are obstacles that agents cannot pass through. If an agent attempts to move into a wall cell, it incurs a penalty of -10 points. This encourages agents to learn and avoid invalid moves.

    Empty Cells: There is no treasure within. When an agent moves to an empty cell, it incurs a slight penalty of -1 point. It is an inhibition of unnecessary movement to encourage the agents to find the treasure in optimal time. During the agent's turn, it may take any one of the four possible actions: up, down, left, or right. The movement mechanics allow for giving each agent feedback in the form of rewards or penalties resulting from the action it chose, so that over time, it can adapt to optimise the strategy.


3. ### *Agents :*
   
   The agents compete against each other, and each has its own Q-table. Over time, they learn the optimal path to the treasure based on the rewards they receive for different actions. The agent with the best reward is deemed the winner.
​
---

## ***Code Structure :***

The project code is divided into 4 cells for modularity and ease of understanding:

  ### **1) Cell 1: Environment Setup**
  This cell defines the environment for the agents, establishing the foundational framework for their interactions. It includes:

          1.Defining the Grid Layout:

               The grid is represented as a two-dimensional array where each cell can either be empty, contain a wall, or contain the treasure. The dimensions of the grid can be adjusted to modify the complexity of the environment.

          2.Setting Up the Positions:

                Walls: Randomly positioned to create obstacles that agents must navigate around.
                Agents: Each agent starts at designated positions on the grid, ensuring they are not placed in walls or on the treasure initially.
                Treasure: The treasure is placed randomly on the grid, serving as the target for both agents.
                
          3.Rewards and Penalties: The environment is designed to provide feedback based on the agents’ actions:

                Treasure Found: Agents earn +100 points for successfully reaching the treasure.
                Invalid Move: Agents incur a penalty of -10 points for attempting to move through walls.
                Empty Cell: Moving to an empty cell results in a -1 point penalty, encouraging agents to strategize toward finding the treasure rather than aimlessly exploring.

                
  ### **2) Cell 2: Q-Learning Algorithm Implementation :**
  This cell implements the Q-Learning algorithm, which enables agents to learn and, over time, change their strategies.

          1.Initialization of Q-TABLES: 
                The methods maintain a different Q-table for different agents. Q-table is initialized to zeros. Every entry is the expected utility of taking a certain action in a given state.

          2.Defining Learning Parameters:
                Learning rate (α) : controls how much of the new information is incorporated into the Q-values. With a higher value, the learning is faster, but this causes instability as well.
                Discount Factor (𝛾): Indicates the importance of future rewards. A value close to 1 emphasizes rewards in the long run, and the value closer to 0 emphasizes immediate rewards.
                Balance Exploration-Exploitation (epsilon): This parameter controls the probability of choosing a random action (exploration) versus choosing the best-known action (exploitation). The value of epsilon usually decreases with time, favoring exploitation as learning increases. 

          3.Major Logic for updating Q-values and choosing an action:
                Agents, using the ε-greedy strategy, choose their actions. An action having the highest value in Q is chosen most of the time and sometimes an arbitrary action is chosen.


  ### **3) Cell 3: Running the Simulation :**
  This cell orchestrates the competition among agents within the multi-episodes, ensuring that the learning environment is dynamic. It consists of

          1.Initialize the Agents: 
          Place every agent on the grid such that it is ready to race.

          2.Running Episodes: 
          There are several running episodes in the simulation where,

                Agent cycles: Agents alternate turns to carry out their respective actions, thus learn from the environment in a cycle.
                
                Learning and Updating Q-Tables: After each action, the agents get feedback where after updating their Q-table based on the outcome of their moves.
                
                Reward Tracking: This involves cumulative reward tracking for each agent along the episode to understand their learning process.

          3.Showing the Winner: 
          The total reward for both agents at the end of each episode is compared in order to establish the agent with the higher total as the winner, reflecting the effectiveness of their learned strategies.


  ### **4) Cell 4: Visualization and Results :**
  This cell visualizes the results of the simulation it gained for the agents' performance and behavior during learning. It comprises:

          1.Movements of Agents on the Grid:
          A graphical representation of the paths that the agents have followed in all episodes, showing how strategies change with time.
          
          2.Cumulative Rewards Over Time: 
          A plot displaying the cumulative rewards of each agent over episodes with trends and learning efficiency. Performance Comparison: Comparative graphics showing how the performance of the agents changes with episodes, giving an overview of which strategies perform better.
          
          3.Analysis of Learning: 
          The visualizations allow an analysis of the learning curves of the agents, whether they are indeed able to optimize their strategies based on the received rewards.

---

## ***Results and Observations :***


  ### **1) Learning Progress :**

  Both agents significantly improved their performance over time in navigating the grid. They initially moved randomly because they had to study the environment for information. However, as rewards and penalties were received, they adjusted their strategy to maximize their path to the treasure.
  
  The Q-tables of the two agents were updated dynamically based on their interactions with the environment, reflecting their evolving understanding of best actions to take in the different states.
  

   ### **2) Performance Improvement :**
   
   Over the course of the simulation, both agents improved their performance in terms of how many cumulative rewards they would earn. Initially, the rewards were variable owing to how exploratory these agents' behaviors were, but by regulating their strategies, they were later seen to be capable of getting higher rewards.
   
  Specifically, agents began to favor certain paths that consistently led to the treasure, illustrating their learning curve in identifying optimal routes.
  

   ### **3) Exploration vs. Exploitation :**

   Initially, both agents roam the grid with a highly random nature to explore as many actions as possible without really having any policy. It is at these early explorations when information about the environment can be gathered and the implications of their actions may be understood.
   
  During episodes, agents tend more towards exploitation rather than exploration and favor the action that can be computed to yield the higher reward so far. Therefore, a prominent hallmark of reinforcement learning-the balance between exploration and exploitation-is very well demonstrated by the evolution of the strategies adopted by the agents.


  ### **4) Dynamic Strategies :**

  This competition generated interesting dynamics among the agents because they sometimes employed alternative strategies to outmaneuver one another in their race for the treasure. For instance, the agent could take a more direct route while the other opted for a longer route that previously had higher rewards.
  
  These lively interactions demonstrated not only the flexibility of the agents but, above all, exposed the complexity of competitive environments where agents should not only learn optimal strategies but also predict the actions of their opponent.


### **5) Final Outcomes :**

  The final result of the simulation presented that both had learned very different strategies from one another to navigate the grid efficiently. The most effective strategy was declared the winner based on the agent's higher cumulative rewards.

  Path visualizations of the agents over the episodes depict learning in that the transitions of their movements also seem to appear purposeful as they consistently move towards the treasure.

---

## ***Conclusion :***

  This is an excellent project showing reinforcement learning principles, specifically Q-Learning, applied to competitive multi-agent scenarios. It demonstrates that by learning through trial and error, agents can identify optimal behaviors when competing for rewards within the same environment. As users exercise different parameters of learning and the configuration setup of the grid, they will see different types of competitive dynamics between agents.

  Feel free to open the code and play with the environment, the agent behavior, or the learning parameters to understand the strength of Q-Learning in reinforcement learning tasks!!!

---

## ***Future Improvements :***

  Adding more complex environments with multiple treasures or obstacles.
  
  Introducing more agents to create a multi-agent Q-Learning system.
  
  Experimenting with advanced reinforcement learning techniques like Deep Q-Networks (DQN).

---

## ***Contact :***

For any inquiries or feedback, feel free to reach out:

    Arshith Babu Sankar Deepa
    arspersbabu@gmail.com





  

  


  

  


          

          
                
                      











