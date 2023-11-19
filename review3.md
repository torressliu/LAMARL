# Response
Thanks for your valuable advice on robot learning. Hope that our answers will address your concerns. 
## As the main motivation of the method is to address a practical issue in the real-world robot learning environment. The paper only contains a short section about the snake robot experiment. 2. （除了机器人场景外，我们也在虚拟做，因为FIMDP在虚拟也很多，比如NPCcontorl,例如游戏中，云端服务器对终端NPC进行实时控制，一旦NPC中间卡顿，则会大幅度降低用户体验。因此我们follow eval scan of related works, e.g.[1][2].我们使用主流虚拟场景模拟远程控制NPC任务。）
We apologize for the confusion caused by the robot experiment section and we will reconstruct this part writing. Please allow us to provide a clear explanation. Our primary objective is to introduce a novel general algorithm that contributes to the deep reinforcement learning community. Similar to the contribution of PDQN[1] and PADDPG[2] to the hybrid action control field. Hybrid control problems exist in both virtual scenarios and robot scenarios, and these papers are mainly verified in mainstream simulation tasks in the field of DRL. 

We use representational reinforcement learning to solve FIMDP in real-time control. This problem is not limited to robot scenarios, but also exists in many virtual scenarios (such as game NPC control highlighted in the introduction). FIMDP is suitable for all periodic or low-frequency interaction tasks, not just for packet loss and delay. Therefore, our main contribution lies on mainstream simulation task verification, similar to the other DRL algorithm papers. We are willing to provide adequate experimental videos after the review. Because we have institution logos on our robot and hardware. In order to make the task as clear as possible, we take several frames from the demo video and mask our logo. [This is the anonymous link.](https://anonymous.4open.science/r/MARS-frame/task_frame.png).

The reinforcement learning method proposed in this paper is aimed at the deep reinforcement learning algorithm community. It is one of the main parts of the snake robot control system. The complete robot control system and diverse experimental analysis will be expanded into a journal submission for the robot learning community.

[1] Xiong, Jiechao, et al. "Parametrized deep q-networks learning: Reinforcement learning with discrete-continuous hybrid action space." arXiv preprint arXiv:1810.06394 (2018).

[2] Hu, Zhejie, and Tomoyuki Kaneko. "Hierarchical advantage for reinforcement learning in parameterized action space." 2021 IEEE Conference on Games (CoG). IEEE, 2021.
## Details of snake robot experiment.
## If the snake fails to receive any commands, simply stopping by doing nothing and waiting for the new commands is acceptable.
Snake robot point tracking is a periodic information acquisition task. The reason for this phenomenon is not packet loss or delay, but the unique rolling gait of the snake robot. The rolling gait of the snake robot is the most efficient gait for outdoor work at present, which includes the rolling of the head sensor. However, this gait causes the next observation to be acquired only when the head sensor rolls to a position parallel with the ground. If the rolling motion is interrupted midway, the next state cannot be obtained, leading to agent ineffective shaking.  Our control system is the first to complete the rolling gait tracking task. We describe the snake robot tracking task in detail and provide several [visualization results](https://anonymous.4open.science/r/ICLR2024-173C) in the new version.

In addition to robot scenarios, fragmented interactions also exist in many virtual scenarios. For example, remote control of NPCS: In the game, the cloud server needs to control the terminal NPC in real time. NPC stalling can significantly degrade user experience. So we follow works with related evaluation scenarios (e.g.RTAC[1]RDAC[2]). We used mainstream virtual scenarios (Mujoco, D4RL) to simulate remote control of NPC tasks. Our method outperforms in these tasks.

[1] Chris Pal, et al. "Real-time reinforcement learning." Advances in neural information processing systems 32 (2019).
[2] Ramstedt, Simon, et al. "Reinforcement learning with random delays." arXiv preprint arXiv:2010.02966 (2020).
## It is usually good to include demo videos.
Thanks for your advice. We are willing to provide the visualization results, we provide a [demo video and several visual description](https://anonymous.4open.science/r/ICLR2024-173C) of the task in the new version. 

If our reply address your concerns, we would appreciate it if you could kindly consider raising the score.
