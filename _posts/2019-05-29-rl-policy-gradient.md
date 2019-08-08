---
layout:     post
title:      "强化学习:Policy Gradient"
subtitle:   ""
date:       2019-05-29 12:00:00
author:     "btyzkelili"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 强化学习
---
## 算法
![](/img/rl/1-9.jpg)  
* ▽log(P(a&#124;s))就是增大P(a|s)的方向，也就是减小cross entropy的方向，相当于看成分类问题，让输出向着此时选的action方向更新，此时选的Action的概率不一定最大，向着增大这个概率的方向更新，乘以vt是指导方向和增大幅度，如果vt是负值就像反方向增大

* Vt是r序列处理后的值，怎么处理可以自己定，例如令∑r = R ,Vt=R  Vt=R-d(在R只有正值时，d可以自己定，为了让vt有正有负)  vt=∑r(后面动作的r，认为前面动作的r和现在动作无关)-d vt=∑λr(后面动作的r乘以λ，λ随着动作越靠后越小，表示越靠后的动作对此刻的影响越小)-d

* Vt也可以全为正值：P(a1|s)、P(s2|s) 、P(s3|s)都是增大，但是增大幅度不同，由于P之和为1，所以增大小的相当于减少，但是这样sample不完全的情况会出现问题，因为可能P(a1|s)、P(s2|s)都不同幅度增大了，但是没有走到a选s3的情况，它没有增大，导致最终P(s3|a)减小只因为没有sample到而减小，而不是因为选这个动作r小而减少，会出现问题

* 之所以是基于策略： 输出的不是value，而是直接输出动作的概率，根据概率直接选择动作，不需要再根据value去选择动作

* 损失函数loss = -log(prob) * v<sub>t</sub>: -log(prob)表示在状态s所选动作a的吃惊度，如果选该动作的可能性越小，-log(prob)就越大，v<sub>t</sub>是选该动作的奖励，由于policy gradient是回合更新，所以v<sub>t</sub>由该回合所有选择动作a得到的reward共同决定的，意味着回合过程中，需要存储该回合经验，包括所有状态、动作、奖励，如果奖励是正值且较大，则-log(prob)越大，表示选了一个小可能的动作但是奖励很大，即惊喜度较大，需要对参数进行较大的修改，若奖励是负值，-log(prob)变得更小（先增大，后取负），示意图如下：![](/img/rl/1-10.jpg)

* Policy Gradient的核心思想是更新参数时有两个考虑：如果这个回合选择某一动作，下一回合选择该动作的概率大一些，然后再看奖惩值，如果奖惩是正的，那么会放大这个动作的概率，如果奖惩是负的，就会减小该动作的概率。算法中，是先以上一次得到的action作为正确的label，用entropy cross对比误差，计算梯度，然后向着这个方向更新，但是这个方向不一定是正确的，所以用vt指导方向，如果vt是负数，就向着这个方向的反方向更新，如果是正的，就加大这个方向的更新步伐。

* Policy Gradient可以选择**连续动作**，而基于值的q-learning和DQN等则不行，DQN为什么不行？因为即使DQN可以表示很多状态，但是它输出的是value，并且需要找到value的最大值，连续情况下无法穷举每一个动作，也就无法计算最大Q值对应的动作。

## 实例

#### RL_brain.py
```python3
	
This part of code is the reinforcement learning brain, which is a brain of the agent.
All decisions are made in here.
Policy Gradient, Reinforcement Learning.
View more on my tutorial page: https://morvanzhou.github.io/tutorials/
Using:
Tensorflow: 1.0
gym: 0.8.0

import numpy as np
import tensorflow as tf

#reproducible
np.random.seed(1)
tf.set_random_seed(1)


class PolicyGradient:
    def __init__(
	    self,
	    n_actions,
	    n_features,
	    learning_rate=0.01,
	    reward_decay=0.95,
	    output_graph=False,
    ):
	self.n_actions = n_actions
	self.n_features = n_features
	self.lr = learning_rate
	self.gamma = reward_decay

	self.ep_obs, self.ep_as, self.ep_rs = [], [], []

	self._build_net()

	self.sess = tf.Session()

	if output_graph:
	    # $ tensorboard --logdir=logs
	    # http://0.0.0.0:6006/
	    # tf.train.SummaryWriter soon be deprecated, use following
	    tf.summary.FileWriter("logs/", self.sess.graph)

	self.sess.run(tf.global_variables_initializer())

    def _build_net(self):
	with tf.name_scope('inputs'):
	    self.tf_obs = tf.placeholder(tf.float32, [None, self.n_features], name="observations")
	    self.tf_acts = tf.placeholder(tf.int32, [None, ], name="actions_num")
	    self.tf_vt = tf.placeholder(tf.float32, [None, ], name="actions_value")
	# fc1
	layer = tf.layers.dense(
	    inputs=self.tf_obs,
	    units=10,
	    activation=tf.nn.tanh,  # tanh activation
	    kernel_initializer=tf.random_normal_initializer(mean=0, stddev=0.3),
	    bias_initializer=tf.constant_initializer(0.1),
	    name='fc1'
	)
	# fc2
	all_act = tf.layers.dense(
	    inputs=layer,
	    units=self.n_actions,
	    activation=None,
	    kernel_initializer=tf.random_normal_initializer(mean=0, stddev=0.3),
	    bias_initializer=tf.constant_initializer(0.1),
	    name='fc2'
	)

	self.all_act_prob = tf.nn.softmax(all_act, name='act_prob')  # use softmax to convert to probability

	# 计算loss:
	with tf.name_scope('loss'):
	    # to maximize total reward (log_p * R) is to minimize -(log_p * R), and the tf only have minimize(loss)
	    neg_log_prob = tf.nn.sparse_softmax_cross_entropy_with_logits(logits=all_act, labels=self.tf_acts)   # this is negative log of chosen action
	    # or in this way:
	    # neg_log_prob = tf.reduce_sum(-tf.log(self.all_act_prob)*tf.one_hot(self.tf_acts, self.n_actions), axis=1)
	    loss = tf.reduce_mean(neg_log_prob * self.tf_vt)  # reward guided loss

	with tf.name_scope('train'):
	    self.train_op = tf.train.AdamOptimizer(self.lr).minimize(loss)

    def choose_action(self, observation):
	prob_weights = self.sess.run(self.all_act_prob, feed_dict={self.tf_obs: observation[np.newaxis, :]})
	action = np.random.choice(range(prob_weights.shape[1]), p=prob_weights.ravel())  # select action w.r.t the actions prob
	return action

    # 存储回合经验
    def store_transition(self, s, a, r):
	self.ep_obs.append(s)
	self.ep_as.append(a)
	self.ep_rs.append(r)

    def learn(self):
	# discount and normalize episode reward
	discounted_ep_rs_norm = self._discount_and_norm_rewards()

	# train on episode
	self.sess.run(self.train_op, feed_dict={
	     self.tf_obs: np.vstack(self.ep_obs),  # shape=[None, n_obs]
	     self.tf_acts: np.array(self.ep_as),  # shape=[None, ]
	     self.tf_vt: discounted_ep_rs_norm,  # shape=[None, ]
	})

	self.ep_obs, self.ep_as, self.ep_rs = [], [], []    # empty episode data
	return discounted_ep_rs_norm

    # 计算vt
    def _discount_and_norm_rewards(self):
	# discount episode rewards
	discounted_ep_rs = np.zeros_like(self.ep_rs)
	running_add = 0
	for t in reversed(range(0, len(self.ep_rs))):
	    running_add = running_add * self.gamma + self.ep_rs[t]
	    discounted_ep_rs[t] = running_add

	# normalize episode rewards
	discounted_ep_rs -= np.mean(discounted_ep_rs)
	discounted_ep_rs /= np.std(discounted_ep_rs)
	return discounted_ep_rs
```

#### run_CartPole.py  
```python3

Policy Gradient, Reinforcement Learning.
The cart pole example
View more on my tutorial page: https://morvanzhou.github.io/tutorials/
Using:
Tensorflow: 1.0
gym: 0.8.0

import gym
from RL_brain import PolicyGradient
import matplotlib.pyplot as plt

DISPLAY_REWARD_THRESHOLD = 400  # renders environment if total episode reward is greater then this threshold
RENDER = False  # rendering wastes time

env = gym.make('CartPole-v0')
env.seed(1)     # reproducible, general Policy gradient has high variance
env = env.unwrapped

print(env.action_space)
print(env.observation_space)
print(env.observation_space.high)
print(env.observation_space.low)

RL = PolicyGradient(
    n_actions=env.action_space.n,
    n_features=env.observation_space.shape[0],
    learning_rate=0.02,
    reward_decay=0.99,
    # output_graph=True,
)

for i_episode in range(3000):

    observation = env.reset()

    while True:
	if RENDER: env.render()

	action = RL.choose_action(observation)

	observation_, reward, done, info = env.step(action)

	RL.store_transition(observation, action, reward)

	# 回合结束，更新
	if done:
	    ep_rs_sum = sum(RL.ep_rs)

	    if 'running_reward' not in globals():
		running_reward = ep_rs_sum
	    else:
		running_reward = running_reward * 0.99 + ep_rs_sum * 0.01
	    if running_reward > DISPLAY_REWARD_THRESHOLD: RENDER = True     # rendering
	    print("episode:", i_episode, "  reward:", int(running_reward))

	    vt = RL.learn()

	    if i_episode == 0:
		plt.plot(vt)    # plot the episode vt
		plt.xlabel('episode steps')
		plt.ylabel('normalized state-action value')
		plt.show()
	    break

	observation = observation_
```
#### run_MountainCar.py  
	
```python3
Policy Gradient, Reinforcement Learning.
The cart pole example
View more on my tutorial page: https://morvanzhou.github.io/tutorials/
Using:
Tensorflow: 1.0
gym: 0.8.0

import gym
from RL_brain import PolicyGradient
import matplotlib.pyplot as plt

DISPLAY_REWARD_THRESHOLD = -2000  # renders environment if total episode reward is greater then this threshold
#episode: 154   reward: -10667
#episode: 387   reward: -2009
#episode: 489   reward: -1006
#episode: 628   reward: -502

RENDER = False  # rendering wastes time

env = gym.make('MountainCar-v0')
env.seed(1)     # reproducible, general Policy gradient has high variance
env = env.unwrapped

print(env.action_space)
print(env.observation_space)
print(env.observation_space.high)
print(env.observation_space.low)

RL = PolicyGradient(
    n_actions=env.action_space.n,
    n_features=env.observation_space.shape[0],
    learning_rate=0.02,
    reward_decay=0.995,
    # output_graph=True,
)

for i_episode in range(1000):

    observation = env.reset()

    while True:
	if RENDER: env.render()

	action = RL.choose_action(observation)

	observation_, reward, done, info = env.step(action)     # reward = -1 in all cases

	RL.store_transition(observation, action, reward)

	if done:
	    # calculate running reward
	    ep_rs_sum = sum(RL.ep_rs)
	    if 'running_reward' not in globals():
		running_reward = ep_rs_sum
	    else:
		running_reward = running_reward * 0.99 + ep_rs_sum * 0.01
	    if running_reward > DISPLAY_REWARD_THRESHOLD: RENDER = True     # rendering

	    print("episode:", i_episode, "  reward:", int(running_reward))

	    vt = RL.learn()  # train

	    if i_episode == 30:
		plt.plot(vt)  # plot the episode vt
		plt.xlabel('episode steps')
		plt.ylabel('normalized state-action value')
		plt.show()

	    break

	observation = observation_
```

