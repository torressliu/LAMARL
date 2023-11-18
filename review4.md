# Response
Thank you for your comments. Hope that our answers can address your concerns. If so, we would appreciate it if you could kindly consider raising the score.
## The experiemnt part may not fully match with the motivation of the paper. Generally speaking, simulation environments such as Mujoco do not require the use of framentary control. 
This question is valuable. Instead of using Mujoco directly, we built several FIMDP tasks based on mujoco and D4RL to mimic remote control of virtual NPC. The details of constructing FIMDP simulation tasks is described in the experiment section Sec 4.2: In real-world tasks, an execution time for one step is about 0.05s to 0.25s. And most of the prohibited interaction duration is 0.5s to 2s. Thus, we set the interval step length as 8 to simulate the real-world setting.  We will highlight the task settings in the new version. And put it at the top of the experiment section.
## Why does the method significantly outperform TD3 with advanced decision? Please explain the comparison between the baselines in more details.
- Td3-advance decision needs to output the whole action sequence (concatenate c steps), and the long action sequence will increase the output dimension (output_dim= c * single_action_dim). This increases the difficulty of the action space exploration. Thus, the agent cannot learn the optimal policy (mentioned in the introduction).
- Our method represents diverse action sequences into low-dimensional space. RL algorithms only need to learn policies in the latent action space. Our method reduces the difficulty of exploration and performs better.
- Our algorithm is a plug-in method and can be applied to all major reinforcement learning methods. To ensure experimental fairness, all methods use Td3. This eliminates the framework advantages that Td3 brings to advance deisicion.
- Following results show the sensitive of two methods to action sequence dimension. The first table runs on Walker (Mujoco) and the second runs on Maze-hard (average of the 10 runs). It can be found that the exploration ability of Td3-advance decision decreases significantly with the increase of sequence length. We will add analysis in the new version.

| method     | 18 dim| 36 dim| 54 dim|
| :-----------: | :-----------: | :------------: | :-----------: |
| Ours |$4715.6\pm 343.1$|$4613.2\pm 362.7$|$4215.9\pm 428.3$|
| TD3- advanced decision |$2368.2\pm 316.4$|$913.2\pm 592.1$|$718.3\pm 176.8$|

| method     | 12 dim| 24dim| 36 dim|
| :-----------: | :-----------: | :------------: | :-----------: |
| Ours |$271.2\pm 11.4$|$258.3\pm 15.2$|$246.5\pm 21.3$|
| TD3- advanced decision  |$83.5\pm 5.7$|$31.9\pm 7.4$|$85.1\pm 2.8$|
## What is the interaction pattern between the executor and the agent in the real-world experiment?
The agent is arranged in the cloud server, and the executor interacts fragmentally through the LAN. All data is transmitted through data packets.
## The real-world robotic control experiment lack important details, including the interaction pattern between the executor and the agent in the real-world experiment.
We will provide a detailed description of the experiment in the new version. The 21-joints snake robotic uses a rolling gait. The algorithm is arranged in the cloud server, and the decision end interacts with the snake robot through the local area network. The snake robot needs to scroll from the starting point to the target point in a scene with a size of 5 square meters. Each observation step is 54d, the action sequence time step is 20, so the action sequence dimension is 1.08k. And the control frequency of the real interaction is 20 Hz. We will attach the experiment video after the review. Because we have institution logos on our robot and hardware. In order to make the task as clear as possible, we take a frame from the video and mask our logo. [This is the anonymous link.](https://anonymous.4open.science/r/MARS-frame/task_frame.png)
