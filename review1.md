# Response
We appreciate your valuable and inspiring comments. Hope that our response can address your concern. 
## Why is clustering representations of actions that have similar environmental effects better than clustering action sequences with similar values or rewards? 
The in-depth explanation is as follows (Section 1 of the new version, highlight) :
-	 Get accurate Q value is difficult: In sparse reward environments (such as FIMDP), reward and Q are difficult to obtain and the evaluation of Q values in the early stage of training is inaccurate. In contrast, environmental dynamic is more reliable and accessible.
-	Environmental dynamic contains more information: The same reward or Q value may correspond to different environmental changes, but the same environmental change must have the same reward or Q value.
-	Environmental dynamic is reward-agnostic: In FIMDP, rewards are sparse. Environment dynamics do not require a per-step reward. Therefore, environmental dynamic representation is more robust in FIMDP.

Further, in the experimental analysis, we compare these three representational learning methods (1. cluster by Env dynamic 2. cluster by Q 3. cluster by reward). We only changed the clustering representations to ensure experimental fairness (buffer size is $1e6$. Average of the 10 runs).

| Method      | Halfcheetah | Walker | maze-hard |
| :-----------: | :-----------: | :------------: | :-----------: |
| Env dynamic (ours) |$7012.1\pm 131.4$|$4821.6\pm 427.6$|$311.4\pm 16.3$|
| Q  |$6386.1\pm 412.7$|$4021.6\pm 313.7$|$275.2\pm 13.7$|
| reward  |$6618.1\pm 372.7$|$4188.3\pm 185.5$|$253.9\pm 21.5$|
## In the random FIMDP tasks mentioned in the paper, is the number of decision steps fixed within one trial or randomly decided during execution? 
The number of decision steps is fixed. In FIMDP, the executor must maintain a high frequency of motion when it cannot interact. Thus, the number of decision steps should be longer than the maximum interaction interval.
## How will the method perform if trained with longer action sequences but executed with a shorter interval, compared with training with shorter action sequences?
we perform an experiment of different length decision steps. The following results show that reducing the number of steps as much as possible can improve scores (Average of the 10 runs. Interval is 6). As the number of steps increases, both the sequence dimension and the reward sparsity increase. These lead to an explosion of action space dimensions and difficulty in exploration, respectively.
| task      | 6 step| 12 step| 18 step|
| :-----------: | :-----------: | :------------: | :-----------: |
| Walker |$4715.6\pm 343.1$|$4613.2\pm 362.7$|$4215.9\pm 428.3$|
| maze-hard  |$271.2\pm 11.4$|$258.3\pm 15.2$|$246.5\pm 21.3$|
## In a real-time RL setting, where it's not guaranteed that the actions actually executed by the executor strictly match the policy's output, do the collected trajectory samples inherently lack stationarity? 
Section 3.2 of the new version covers our method to guarantee training stability in detail (a common low-level method used in real-time control). We use the physical clocks on both devices to align. If the actions are obsolete, lose them. We retain the time stamp and execution flag of each action, which makes actions executed in strict accordance with the timestamp order. When the new sequence arrives at the executor, the previous sequence will be replaced, and the execution flag of the unexecuted action will be False. The subsequent rewards will be accumulated into the new sequence. Thus, each latent space action reward is the sum of the executed action reward in the corresponding sequence. Following results show the effect of the alignment method (average of the 10 runs, Interval is 6). 

| Method      | Walker| maze-hard|
| :-----------: | :------------: | :-----------: |
| Ours |$4463.2\pm 362.7$|$311.4\pm 16.3$|
| without alignment |$4168.3\pm 372.6$|$213.1\pm 16.7$|
## Why MARS has a more pronounced advantage over frame-skips in simpler tasks than in more complex tasks?
Compared to frameskip, MARS does have a reduced advantage on several difficult tasks, e.g. Maze_hard,HalfCheetah. This is because the VAE hyperparameters of MARS are not optimized in difficult tasks, but keep the same settings as those in simple tasks. We adjust the VAE hyperparameters while keeping the remaining hyperparameters unchanged for both methods （following table). By doing this MARS has a more pronounced advantage on complex tasks . (Old score of MARS in maze-Hard:$315.2\pm 13.9$, old score of MARS in maze-Hard:$6417.3\pm 317.3$)

| method     |  maze-hard| HalfCheetah|
| :-----------: | :-----------: | :------------: | 
| Ours |$356.4\pm 16.3$|$8631.5\pm 265.2$|
| TD3- frameskip |$285.7\pm 12.5$|$5842.3\pm 306.7$|
## Does the decoder need to be run on the execution device? Does this mean that latent representations will also be lost?
We do not deploy the decoder to the executor. Although there is an interval between interactions, the agent will make a c step decision based on each timestep information, so each time step (t+i) will receive c times in the future. In addition, our decision sequences are set at maximum intervals to ensure that the executor receives the next sequence before the previous sequence is completed.
## The paper mentions that MARS has better stationarity.  
Section 1 of the new version provides a detailed analysis: Our method is more stable than frameskip and Advance decision. 
- The essence of frameskip is the repetition of an action, which leads to internal homogeneity of the action sequence and the inability to change the action at key states. Thus, the policy is unstable.
- Advance decision needs to output the whole action sequence (concatenate c steps), and the long action sequence will increase the output dimension (output_dim= c * single_action_dim). This increases the difficulty of the action space exploration. Thus, the agent cannot learn the optimal policy.
- Our method represents diverse action sequences in low-dimensional space. RL algorithms only need to learn policies in the latent action space. Our method reduces the difficulty of exploration and performs better.

Further, in the experimental analysis, we compare the policy stability of these three methods for sequence length. Ours provides high stability.
| method     | 6 step| 12 step| 18 step|
| :-----------: | :-----------: | :------------: | :-----------: |
| Ours |$4715.6\pm 343.1$|$4613.2\pm 362.7$|$4215.9\pm 428.3$|
| TD3- frameskip |$3714.7\pm 252.1$|$941.6\pm 603.2$|$195.7\pm 72.5$|
| TD3- advanced decision |$2368.2\pm 316.4$|$913.2\pm 592.1$|$718.3\pm 176.8$|
## Should the "Musar" be referred to as "MARS"?
Correct this in the new version.

If our reply addresses your concerns, we would appreciate it if you could kindly consider raising the score.
