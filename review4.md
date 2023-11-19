# Response
Thank you for your comments. Hope that our answers can address your concerns.
## The experiment part may not fully match the motivation of the paper. Generally speaking, simulation environments such as Mujoco do not require the use of fragmentary control. 
Fragmented interactions exist in many virtual scenarios. For example, remote control of NPCS: In the game, the cloud server needs to control the terminal NPC in real time. NPC stalling can significantly degrade the user experience. So we follow works with related evaluation scenarios (e.g.RTAC[1]RDAC[2]). We used mainstream virtual scenarios (Mujoco, D4RL) to simulate remote control of NPC tasks instead of using Mujoco directly. The details of constructing fragmented interactions simulation tasks are described in the experiment section Sec 4.2: In real-world tasks, an execution time for one step is about 0.05s to 0.25s. And most of the prohibited interaction duration is 0.5s to 2s. Thus, we set the interval step length as 8 to simulate the real-world setting.  We will highlight the task settings in the new version. And put it at the top of the experiment section.

[1] Chris Pal, et al. "Real-time reinforcement learning." Advances in neural information processing systems 32 (2019).

[2] Ramstedt, Simon, et al. "Reinforcement learning with random delays." arXiv preprint arXiv:2010.02966 (2020).
## The real-world robotic control experiment lacks important details, including the interaction pattern between the executor and the agent in the real-world experiment.
The 21-joint snake robotic uses a rolling gait. The algorithm is arranged in the cloud server, and the decision end interacts with the snake robot through the local area network. [This is the interaction pattern figure.](https://anonymous.4open.science/r/ICLR2024-C0F6/interaction_pattern.png)

Snake robot point tracking is a periodic information acquisition task. The reason for this phenomenon is not packet loss or delay, but the unique rolling gait of the snake robot. The rolling gait of the snake robot is the most efficient gait for outdoor work at present, which includes the rolling of the head sensor. However, this gait causes the next observation to be acquired only when the head sensor rolls to a position parallel to the ground. If the rolling motion is interrupted midway, the next state cannot be obtained, leading to ineffective shaking of the robot. 

The snake robot needs to scroll from the starting point to the target point in a scene with a size of 5 square meters. Each observation step is 54d, and the action sequence time step is 20, so the action sequence dimension is 1.08k. The control frequency of the real interaction is 20 Hz. We describe the snake robot tracking task in detail and provide several [visualization results](https://anonymous.4open.science/r/ICLR2024-C0F6/) in the new version. 
## Why does the method significantly outperform TD3 with advanced decision? Please explain the comparison between the baselines in more detail.
Explanation:
- Td3-advance decision needs to output the whole action sequence (concatenate c steps), and the long action sequence will increase the output dimension (output_dim= c * single_action_dim). This increases the difficulty of the action space exploration. Thus, the agent cannot learn the optimal policy (mentioned in the introduction).
- Our method represents diverse action sequences in low-dimensional space. RL algorithms only need to learn policies in the latent action space. Our method reduces the difficulty of exploration and performs better.
- Our algorithm is a plug-in method and can be applied to all major reinforcement learning methods. To ensure experimental fairness, all methods use Td3. This eliminates the framework advantages that Td3 brings to advance deisicion.

Verified by experiment:
- Following results show the sensitivity of three methods (Ours, TD3-advanced decision, TD3-frameskip) to the action sequence dimension. The first table runs on Walker (Mujoco) and the second runs on Maze-hard (average of the 10 runs).
- It can be found that the exploration ability of Td3-advance decision decreases significantly with the increase of sequence length.
- TD3-frameskip has better exploration ability than TD3- advanced decision. This is because frameskip reduces the spatial dimension of exploration by sacrificing action variety (repeating the same action).
- Our method has the best performance by reducing the dimension of exploration space and ensuring the diversity of action through the representation of action space.

| method     | 12 dim| 24dim| 36 dim|
| :-----------: | :-----------: | :------------: | :-----------: |
| Ours |$271.2\pm 11.4$|$258.3\pm 15.2$|$246.5\pm 21.3$|
| TD3- frameskip |$231.2\pm 14.6$|$112.1\pm 3.2$|$88.7\pm 2.5$|
| TD3- advanced decision  |$83.5\pm 5.7$|$31.9\pm 7.4$|$85.1\pm 2.8$|

| method     | 18 dim| 36 dim| 54 dim|
| :-----------: | :-----------: | :------------: | :-----------: |
| Ours |$4715.6\pm 343.1$|$4613.2\pm 362.7$|$4215.9\pm 428.3$|
| TD3- frameskip |$3714.7\pm 252.1$|$941.6\pm 603.2$|$691.3\pm 122.4$|
| TD3- advanced decision |$2368.2\pm 316.4$|$913.2\pm 592.1$|$718.3\pm 176.8$|

##If our reply addresses your concerns, we would appreciate it if you could kindly consider raising the score.
