# Response
Thanks for your recognition of our work and your willingness to improve score. We hope our reply can answer your questions.
## The questions are also related to weakness, what are the differences between FIMDP and POMDP, or MDP with reward delays?
We compare FIMDP with other delayed MDPS and POMDP in the new version for increased readability:
-The main difference between FIMDP and delayed MDP: FIMDP requires the decision end to maintain continuous motion while controlling the executor to complete the task through low-frequency interaction, and cannot stop. However, the goal of previous delayed MDP was to address reward and action delay, allowing the agent to stall.
-The main difference between FIMDP and POMDP: Agents in FIMDP can obtain global information when interacting, while agents in POMDP has no access to global state.

## 2.	If we have/learned a world model for the environment, can we do the model-based predictions, like model predictive control to solve the FIMDP? (this might be the most straightforward method that first came into my mind.) How does this compare to learning the multi-step representations?
This question is valuable. In fact, we originally wanted to build a world model to achieve comprehensive environmental perception. However, the interval of FIMDP is too long and there are random interval scenes, the construction of world model is very difficult. It can be summarized that the sampling of data is unstable and does not meet the quality standards for constructing the world model). Instead, we construct a motion latent space. To prove this conclusion, Following results shows the performance of the original MBPO[1] based world model method (Average of the 10 runs. Interval is 10). In the future, we will further think about how to make Model-based methods effective in FIMDP tasks

| Methods     | Walker| maze-hard| HalfCheetah|
| :-----------: | :-----------: | :------------: | :-----------: |
| MBPO-based |$3781.2\pm 217.5$|$203.6\pm 15.8$|$6153.1\pm 381.2$|
| Ours  |$4715.6\pm 343.1$|$271.2\pm 11.4$|$7012.1\pm 131.4$|

[1] Janner, Michael, et al. "When to trust your model: Model-based policy optimization." Advances in neural information processing systems 32 (2019).
