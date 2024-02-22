### 1 高保真仿真器构建与高质量数据获取

强化学习过程离不开高质量、多样化的训练数据，而该数据的获取通常依赖仿真器。因此，高保真的仿真器构建成为了优化强化学习策略、缩小仿真与实际应用过程偏差的重要手段。然而，实际场景存在众多影响因素，且各因素之间的耦合关系复杂，这进一步加大了高保真仿真器构建的难度。离线强化学习由于不依赖于仿真器，可一定程度上缓解上述问题，但多样化、高质量的训练数据获取成为了这类方法的落地主要瓶颈。

#### 高保真的仿真器构建 sim to real

机器人领域：介绍RoboGen，自动生成任务场景和数据

论文：RoboGen: Towards Unleashing Infinite Data for Automated Robot Learning via Generative Simulation (delet)

自动驾驶领域：一些仿真环境，重点介绍CARLA和waymax/waymo

论文：Simulation-Based Reinforcement Learning for Real-World Autonomous Driving（ All real-world scenarios）、CARLA原论文、waymo原论文等



#### 离线强化学习 (TODO)

算法层面：BCQ, CQL, IQL (case)

数据增广：士熙工作，清华吕加飞double check

off to on：楷哥E2O等 （delet）

近期...，以xxx为代表的离线强化学习不依赖仿真器，直接从离线数据中学习策略，这些工作...（简要介绍），且学习到的策略可直接应用或者通过off to on进一步优化，降低对仿真器的依赖程度。但高质量，多样化的数据获取是瓶颈，一些工作聚焦于xxx数据增广，如xxx（士熙等工作）。





### 2 数据高效的强化学习优化算法设计

由于实际过程中的数据获取成本高，部分数据涉及到安全性和合法性等因素更是难以获取，因此如何利用好有限的数据，设计高效的策略学习算法是落地过程中必须解决的问题。此外，有时通过单次训练学习无法解决所有实际问题，策略部署后存在部分场景泛化性问题，针对问题场景如何做到定向提升且避免已有策略的灾难遗忘，也是落地过程中必须考虑的问题。



#### 数据高效的算法

高效的经验回放？：PPO，DQN系列等？(PPO->样本效率)


safe rl（不知道要不要说）：保证学习过程的安全性和合法性 （delet）

#### 策略泛化性 （找导航的技术案例）

迁移学习/Few shot learning：将一个领域的知识应用到另一个领域， 课程学习：逐渐提升任务难度，帮助agent更好地学习策略

元学习（）：元学习（learn to learn），训练模型以便它们能够快速适应新任务，即使这些任务的数据非常少。元学习的目标是提高模型在未见过场景中的泛化能力。通过这种方式，模型能够基于少量数据进行有效学习，从而在面对新的、不同的任务时能够迅速调整其行为或决策策略，有效解决数据稀缺的问题，增强模型的应用灵活性和广泛性。

shot: need multi-task ackowlage pretrain (costy), interaction with real-world reward costy.



### 3 非平稳动态环境下的鲁棒学习方法 (servey: rubust MDP, action random)

真实的工业场景中往往存在着大量的动态变化因素（例如人群变化、车辆移动等等），这些因素导致环境一直处于高度波动、非平稳的动态变化之中。当强化学习算法在真实环境中部署学习时，往往会受到环境中的高波动因素干扰，无法学习到有效的策略。因此需要针对这类应用场景设计更有效的鲁棒学习策略。



**领域随机化**：通过在训练过程中引入环境参数的随机变化，增强模型对未见变化的适应能力。

（domain randomization reinforcement learning）

Cyclic policy distillation: Sample-efficient sim-to-real reinforcement learning with domain randomization

DROPO: Sim-to-real transfer with offline domain randomization

**对抗训练**：通过引入对抗性扰动，训练模型抵御可能的干扰，提高其鲁棒性。

（adversarial training reinforcement learning）

Adversarial model for offline reinforcement learning（NIPS 2023）

Integrating safety constraints into adversarial training for robust deep reinforcement learning（information sciences）

**多任务学习**：同时学习多个相关任务，提升模型的泛化能力和鲁棒性。(delet)

Multi-task reinforcement Learning（找一些决策相关的工作，如DeepMind的A Generalist Agent，TMLR 2022）





### 4 多智能体复杂交互关系学习

在实际应用部署场景中，往往同时存在着大量智能体（例如无线网络中的通信基站），智能体彼此交互影响，从而决定了工业系统的整体性能。如何有效地对大量智能体之间的交互进行建模、从而更好的实现智能体间的协同决策是一大挑战。尤其是当可获得的数据有限、且智能体间交互方式存在多样性时，如何更精准地进行协同学习更是一大难点。

**相关工作**：QMIX，MADDPG？
