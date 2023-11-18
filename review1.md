# Response
We appreciate your valuable and inspiring comments. Hope that our response can address your concern. If so, we would appreciate it if you could kindly consider raising the score.
## Why is clustering representations of actions that have similar environmental effects better than clustering action sequences with similar values or rewards? 
The in-depth analysis is as follows (we will add to the new version of the paper) :
-	 Get accurate Q value is difficult: In sparse reward environments (such as FIMDP), reward and Q are difficult to obtain and the evaluation of Q values in the early stage of training is inaccurate. In contrast, environmental dynamic is more reliable and accessible.
-	Environmental dynamic contains more information: The same reward or Q value may correspond to different environmental changes, but the same environmental change must have the same reward or Q value.
-	Environmental dynamic is reward-agnostic: i.e. this information/knowledge can be shared and transferred to different tasks in the same environment.
-	The following results confirm this conclusion. All methods only change the representation module, and the data and architecture are consistent (average of the 10 runs).

| Method      | Halfcheetah | Walker | maze-hard |
| :-----------: | :-----------: | :------------: | :-----------: |
| Env dynamic (ours) |$7012.1\pm 131.4$|$4821.6\pm 427.6$|$311.4\pm 16.3$|
| Q  |$6386.1\pm 412.7$|$4021.6\pm 313.7$|$275.2\pm 13.7$|
| reward  |$6618.1\pm 372.7$|$4188.3\pm 185.5$|$253.9\pm 21.5$|
## In the random FIMDP tasks mentioned in the paper, is the number of decision steps fixed within one trial or randomly decided during execution? 
The number of decision steps is fixed. In FIMDP, executor must maintain a high frequency of motion when it cannot interact. Thus, the number of decision steps should be longer than the maximum interaction interval.
## How will the method perform if trained with longer action sequences but executed with a shorter interval, compared with training with shorter action sequences?
we performe an experiment of different length decision steps. Following results show that reducing the number of steps as much as possible can improve scores (Average of the 10 runs. Interval is 10). As the number of steps increases, both the sequence dimension and the reward sparsity increase. These lead to an explosion of action space dimensions and difficulty in exploration, respectively.
| task      | 6 step| 12 step| 18 step|
| :-----------: | :-----------: | :------------: | :-----------: |
| Walker |$4715.6\pm 343.1$|$4613.2\pm 362.7$|$4215.9\pm 428.3$|
| maze-hard  |$271.2\pm 11.4$|$258.3\pm 15.2$|$246.5\pm 21.3$|
## In a real-time RL setting, where it's not guaranteed that the actions actually executed by the executor strictly match the policy's output, do the collected trajectory samples inherently lack stationarity? 
The new version will cover our method to guarante the training stability in detail. FIMDP is divided into consistent FIMDP and random FIMDP. In consistent FIMDP, the decision end and the executor are strictly aligned. In the random FIMDP, to ensure stable training and execution, we retain the time stamp and execution flag of each action, which are executed in strict accordance with the timestamp order. When the new sequence arrives at the executor, the previous sequence will be replaced, and the execution flag of the unexecuted action will be False. The subsequent rewards will be accumulated into the new sequence. Thus, each latent space action reward is the sum of the executed action reward in the corresponding sequence. Following results shows the effect of alignment method (average of the 10 runs, Interval is 6).

| Method      | Walker| maze-hard|
| :-----------: | :------------: | :-----------: |
| Ours |$4463.2\pm 362.7$|$311.4\pm 16.3$|
| without aligment |$4168.3\pm 372.6$|$213.1\pm 16.7$|
## Why MARS has a more pronounced advantage over frame-skips in simpler tasks than in more complex tasks?
Because the simple tasks does not require too much action change, the demand for internal diversification of the action sequence is not high. So frameksip can learn suboptimal policies.
## Does the decoder need to be run on the execution device? 
The question is instructive. We do not need to deploy the decoder to the executor. Thus avoid a series of problems. We will highlignt this in the new version to improve readability.
## The paper mentions that MARS has better stationarity.  
We apologize for the misleading wording. "stationarity" means that MARS can ensure the effectiveness of the policy in multiple tasks. To verify this conclusion, we conducted verification in multiple robot control and navigation scenarios. 
## Should the "Musar" be referred to as "MARS"?
We will correct all of them in the new version.
