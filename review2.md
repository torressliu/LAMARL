# Response
Thanks for your recognition of our work. We hope our reply can address all your concerns.
## The questions are also related to weakness, what are the differences between FIMDP and POMDP, or MDP with reward delays?
We compare FIMDP with other delayed MDPS and POMDP in the new version:
- The main difference between FIMDP and delay MDP: In FIMDP All environmental information is delayed (observation, action sequence, reward). Besides, agents are not allowed to pause midway. However, in reward delay MDP agent just need address the reward delay. And reward delay MDP does not consider the harm caused by the agent stalled in the middle.
- POMDP does not involve delay, but the agent gets a local observation at each step. In contrast, the FIMDP has a delay in obtaining observations, but the agent can obtain global observations

## 2.	If we have/learned a world model for the environment, can we do the model-based predictions, like model predictive control to solve the FIMDP? (this might be the most straightforward method that first came into my mind.) How does this compare to learning the multi-step representations?
This question is valuable. In fact, we originally wanted to build a world model to achieve comprehensive environmental perception. However, the interval of FIMDP is too long and some tasks have random interval and the training of world models is very complex. It is difficult to construct effective dynamics models and reward models under delayed conditions, which can be summarized as we cannot model random delays effectively. Therefore, we chose a method that is easier to train and robust to delay: construct a action latent space. To prove that our approach is more efficient than model-based approach in FIMDP tasks. Following results shows the performance of the original MBPO[1] based world model method (Average of the 10 runs. Interval is 10). In the future, we will further think about how to make Model-based methods effective in FIMDP tasks.

| Methods     | Walker| maze-hard| HalfCheetah|
| :-----------: | :-----------: | :------------: | :-----------: |
| MBPO-based |$3781.2\pm 217.5$|$203.6\pm 15.8$|$6153.1\pm 381.2$|
| Ours  |$4715.6\pm 343.1$|$271.2\pm 11.4$|$7012.1\pm 131.4$|

[1] Janner, Michael, et al. "When to trust your model: Model-based policy optimization." Advances in neural information processing systems 32 (2019).
## If you think the above response address your concerns, we would appreciate it if you could kindly consider raising the score.

