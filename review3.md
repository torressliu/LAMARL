# Response
Thanks for your valuable advice on robot learning. We will modify the presentation to improve the readability of the work. Hope that our answers will ease your concerns.
## The paper only contains a short section about the snake robot experiment with simple proprioceptive observations.  
We apologize for the confusion caused by the robot experiment section and we will reconstruct this part writing. Please allow us to provide a clearer explanation. Our primary objective is to introduce a novel general algorithm that contributes to the deep reinforcement learning community (e.g. PDQN[1], PADDPG[2] in hybrid action space control field. Hybrid control problems exist in both virtual scenarios and robot scenarios, and these papers are mainly verified in mainstream simulation tasks in the field of DRL.). 
We use representational reinforcement learning to solve FIMDP in real-time control. This problem is not limited to robot scenarios, but also exists in many virtual scenarios (such as game NPC control highlighted in the introduction). FIMDP is suitable for all periodic or low-frequency interactions, not just for packet loss and delay (these are two of the common causes of FIMDP. Low-frequency reception of robotic sensors can also cause FIMDP , which we will highlight in the new version). In order to make the task as clear as possible, we take a frame from the video and mask our logo. [This is the anonymous link.]()
Therefore, our main contribution lies on mainstream simulation task verification, similar to the other DRL algorithm papers. We are willing to provide adequate experimental videos after the review. Because we have institution logos on our robot and hardware. 
[1] Neunert, Michael, et al. "Continuous-discrete reinforcement learning for hybrid control in robotics." Conference on Robot Learning. PMLR, 2020.
[2] Hu, Zhejie, and Tomoyuki Kaneko. "Hierarchical advantage for reinforcement learning in parameterized action space." 2021 IEEE Conference on Games (CoG). IEEE, 2021.
## If the snake fails to receive any commands, simply stopping by doing nothing and waiting for the new commands is acceptable.
We selected the task of the robot snake due to its unique rolling gait. The rolling gait of the robot snake is the most efficient gait for outdoor work at present, which includes the rolling of the head sensor. This gait causes the next observation to be acquired only when the head sensor rolls to a position parallel with the ground (this periodic acquisition observation results in FIMDP). If this rolling motion is interrupted midway, the next state cannot be obtained, leading to ineffective shaking. It is for this reason that our approach was the only one able to successfully accomplish the task. This control system is the first in the field of robot snake to realize the task of rolling gait tracking.
## The bandwidth should be enough for transmitting the small amount of data consisting of only 54-dimensional vectors
This suggestion is very meaningful. We will describe the real world robot scenario in more detail in the new version. Although the observation of a single step of the robot snake is 54-d, the decision sequence of each step is 20, so the dimension is 1.08k. the control frequency of real interaction is 20 Hz.
## It is usually good to include demo videos.
Thank you very much for your advice. We are willing to provide the video, but our robot is pinted with the logo of the institution and was warned in the early stage of submission. Adequate experimental videos will be provided after the review. In order to make the task as clear as possible, we take a frame from the video and mask our logo. [This is the anonymous link.]()