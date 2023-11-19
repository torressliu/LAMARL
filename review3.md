# Response
Thanks for your valuable advice on robot learning. Hope that our answers will address your concerns. 
## Details of snake robot experiment.
Snake robot point tracking is a periodic information acquisition task. The reason for this phenomenon is not packet loss or delay, but the unique rolling gait of the snake robot. The rolling gait of the snake robot is the most efficient gait for outdoor work at present, which includes the rolling of the head sensor. However, this gait causes the next observation to be acquired only when the head sensor rolls to a position parallel with the ground. If the rolling motion is interrupted midway, the next state cannot be obtained, leading to agent ineffective shaking.  Our control system is the first to complete the rolling gait tracking task. We describe the snake robot tracking task in detail and provide several [visualization results](https://anonymous.4open.science/r/ICLR2024-173C) in the new version. The snake robot needs to scroll from the starting point to the target point in a scene with a size of 5 square meters. Each observation step is 54d, the action sequence time step is 20, so the action sequence dimension is 1.08k. And the control frequency of the real interaction is 20 Hz.

In addition to robot scenarios, fragmented interactions also exist in many virtual scenarios. For example, remote control of NPCS: In the game, the cloud server needs to control the terminal NPC in real time. NPC stalling can significantly degrade user experience. So we follow works with related evaluation scenarios (e.g.RTAC[1]RDAC[2]). We used mainstream virtual scenarios (Mujoco, D4RL) to simulate remote control of NPC tasks. Our method outperforms in these tasks.

[1] Chris Pal, et al. "Real-time reinforcement learning." Advances in neural information processing systems 32 (2019).

[2] Ramstedt, Simon, et al. "Reinforcement learning with random delays." arXiv preprint arXiv:2010.02966 (2020).
## It is usually good to include demo videos.
Thanks for your advice. We are willing to provide the visualization results, we provide a [demo video and several visual description](https://anonymous.4open.science/r/ICLR2024-173C) of the task in the new version. 

If our reply address your concerns, we would appreciate it if you could kindly consider raising the score.
