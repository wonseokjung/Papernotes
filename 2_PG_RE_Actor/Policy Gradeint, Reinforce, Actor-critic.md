## Policy Gradeint, Reinforce, Actor-critic 

휴가 잉여력이 남아 간단하게 policy gradient 논문을 타고 올라가보았습니다. 



2000년 sutton의 policy gradient 방법을 기반으로 한 REINFORCE와 ACTOR-CRITIC 의 설명입니다. 

1. #### Sutton 2000, NIPS 



<img src="https://www.dropbox.com/s/zxbzo75v6mwp33i/Screenshot%202018-08-05%2017.26.41.png?raw=1">





##### Policy Gradient Methods for Reinforcement Learning with Function Approximation

Paper 링크 : 

https://papers.nips.cc/paper/1713-policy-gradient-methods-for-reinforcement-learning-with-function-approximation.pdf

###### - Abstract : 

Reinforcement Learning(강화학습)에서 Function Approximation(함수근사) 을 적용할때 기존 접근방법은 valuefunction (가치함수)을 Approximation(근사)한 뒤 Policy(정책)를 determining(결정)하는 방법을 사용하였다. 

이 Paper에서는 그와 다른  접근 방법으로 policy가 function approximator에 의해 표현되며, 독립된 value function을 가지고 있으며 expected reward(보상)의 gradient에 따라 policy parameter가 update되는 방법이다. 

##### REINFORCE method와 actor-critic method가 이 접근 방법의 예이다. 

이 paper에서는Experience( 경험 )으부터 받은  Action-value (행동의 가치) 혹은 advantage function (어드벤테이지 함수)을 이용하여 gradient를 적용할수 있는 form(형태)로 written(쓰여질수) 있다는 것이다. 

##### 우리는 처음으로  이 방법을 사용하여 arbitrary differentiable function approxmation을 사용한 policy iteration이 locally optimal policy에 convergent(수렴)한다는 것을 증명한다.

---



### 1.1 Value-function approach 



action-selection policy란 estimated values들 중 "greedy"한 action을 선택하는 policy 였다. ( 각 state에서의 action들중 갖아 높은 estimated value인 action을 선택하는 것)

##### Value function approach는 많은 application에서 좋은 성능을 보였지만 몇가지 한계가 있다. 



##### 첫번째 한계 : 

policy가 stochastic하지 않고 deterministic하다는 것. (Jaakkola and Jordan 1994)



##### 두번째 한계 : 

Estimaed 된 action value의 아주 작은 변화에도 예민하다는것 ( greedy하게 선택되기 때문에 예를 들어 두개의 action value가 굉장히 비슷해도 아주 작은 차이도 선택될수도 선택되지 않을수도 있다. )

##### 예를 들어 Q-learning, Sarsa, Dynnamic programming방법이 간단한 MDP와 simple function approximator에서 되지 않는다는것을 보였다. 

( Gordon, 1995, 1996; Baird, 1995 : Tsitsilils and van Roy 1996, Bersekas and Tsitsiklis 1996) 

(나의 의견 : 의 관점은 Policy gradient 논문이 쓰였던 2000년 때의 관점으로 보인다. 
Deep learning이 function approximation으로 잘 쓰이기 이전에 쓰여진 논문이다.
또한 Action value를 사용하여 Atari에서 좋은 성능을 보인 DQN과 DQN으로부터 파생되어 좋은 성능을 보인 연구결과등이 고려되지 않은 논문이기에 현재의 시점에서는 다른 관점으로 이 논문을 봐야할것 같다.) 

---

###  1.2 Approximate a stochastic policy



 이 paper에서는 

##### Value function을 Approximating하기위해 사용하지 않고 deterministic policy를 계산하기 위해 사용할 것이며, 

##### 독립적인 function approximator을 사용하여 Stochastic policy를 직접 approximate하는 방법을 사용할 것이다.

<img src="https://www.dropbox.com/s/oize488nllhdvee/Screenshot%202018-08-05%2017.59.03.png?raw=1">

예를들어, 

function approxmator가 neural network이며 input은 state이고 output은 각 action을 선택할 "확률"이다. 그리고 weight는 policy parameter이다. 



#### $\theta$ 는 policy parameter의 vector, $\rho$ policy에 의한 performance ( eg : 각 step마다의 average reward)로 정의하며, 

#### policy gradient approach는 gradient에 의해 policy parameter가 update되는 접근방법이다.



# $\bigtriangleup \theta \approx \alpha \frac{\partial \rho}{\partial \theta}$

<img src="https://www.dropbox.com/s/bh3c5vj0dkhmncy/Screenshot%202018-08-05%2018.07.10.png?raw=1">



$\alpha$는 step size이며, $\theta$는 performance measure $\rho$에 의해 locally optimal policy로 converge 한다. 



<img src="https://www.dropbox.com/s/nkvuc1b2kc38nh2/Screenshot%202018-08-05%2018.18.05.png?raw=1">



##### Value-function approach와는 다르게 Polciy gradient 방법은 $\theta$ 가 조금 변한다면 policy와 state distribution에도 작은 영향을 미친다. 



---

### 1.3 Policy Gradient with REINFORCE and actor-critic 





##### 1.3.1  Unbiased estimate of the gradient

##### 이 페이퍼에서는 unbiased estimate of the gradient를 특정 properties를 축종시키는 approximate value function을 사용하여 얻은 경험으로부터 얻을수 있다는 것을 증명하였다. 



<img src="https://www.dropbox.com/s/m7ztydonjyff4jl/Screenshot%202018-08-05%2018.45.26.png?raw=1">



Willams's (1988, 1992) REINFORCE 알고리즘에서도 unbiased estimate of the gradient를 찾았지만  학습된 value function을 이용하지 않았다. 



REINFORCE는 value function을 사용한 RL 방법보다 훨씬 느리게 학습하며, 
Learning value functin을 사용하므로서 variance를 줄이고 더 빠르게 학습할수 있도록 한다.  



### ---

Actor-Critic의 기초가 된 논문 :NeuronLike Adaptive Elements That Can Solve Difficult Learning Control Problems

### 

### Neuronlike Adaptive Elements That Can Solve Difficult Learning Control Problems 

<img src="https://user-images.githubusercontent.com/11300712/43935038-087bf022-9c8d-11e8-90ea-7201470c472e.JPG">

"Two neuronlike adaptive elements"는 어려운 control problem을 풀 수 있다. 

여기서 어려운 taks는 Pole의 균형을 맞추는 것이다. 



여기서 Learning system은 두가지로 구성되어 있다.

1. Single Associative search element(ASE)
2. Single adaptive critice element (ASE)



Pole의 균형을 맞추기 위해,

ASE는 reinforcement의 feeback에 영향을 받아서 찾은 input과 output의 assoication 이다. 

ACE는 좀 더 informative evaluation function으로 구성되어 있으며 reinforcement feedback과는 단독으로 제공한다. 



## ASE

ASE의 input은  cart-pole state의 vector이며 이것은 decorder에 의해 계산되어진 것이다. 

또한 ASE의 output은 Cartpole에 가해질 force를 측정한다. 



<img src="https://user-images.githubusercontent.com/11300712/43935037-085990ae-9c8d-11e8-957a-52b3622b0756.JPG">



## ACE



ACE는 ASE와 마찬가지로 nonreinforcing input을 받으며 이것을 ASE를 개선하기 위해 사용한다. 

<img src="https://user-images.githubusercontent.com/11300712/43935035-08326ace-9c8d-11e8-9dee-dfd856ed76cf.JPG">

Note 1 

**Association** in psychology refers to a mental connection between concepts, events, or mental states that usually stems from specific experiences. 
https://en.wikipedia.org/wiki/Association_(psychology)





현재 Reinforcement Learning에서 Actor-Critic으로 불리는 학습 알고리즘의 아이디어가 제시된 1983년의 논문을 보았다. 


현재는 네트워크 두개를 사용해 하나는 action을 다른 하나는 state를  측정하는 방법을 actor - critic이라고 범용적으로 부르는 것 같지만, 
이 논문에서는 ASE와 ACE를 사용하여 Pole의 balance를 맞추는 환경에서 더 좋은 performace를 보였다 라고 제시하는 것 같다. 

재밌는점은 이 논문은 동물이 학습할때 short term memory와 long-term memory를 통해 학습한다는 것을  출발한것처럼 보인다. 



---



##### 1.3.2 Proving the convergence of a wide variety of algorithms 



##### 이 연구가 제안한 또 다른 결과는 "actor-critic"또는 policy-iteration architectures (Barto, Sutton and Anderson 1983, sutton 1984, Kimura and Kobayashi 1998)를 기반으로 하여 여러가지 알고리즘에서 convergence가 됨을 증명하였다. 

이 논문에서는 policy iteration에서의 general differentiable function approximation 은 locally optimal policy에 converge된다는 것의 아이디어를 가져왔다. 

Baird and Moore(1999)가 VAPS 방법에서 policy-gradient가 비슷한 방법을 사용하였지만 locally optimal policy에 수렴하지 않았다.  



###### * Neuronlike Adaptive Elements That Can Solve Difficult Learning Control Problems

https://github.com/wonseokjung/Papernotes/blob/master/1_Reinforcemen/1_NAETDLC/1_Neuronlike_Adaptive_Elements_that_can_solve_difficult_learning_control_problems_1983_sutton.md



---

## 2. Policy Gradient Theorem





Function Approximation에서 Agent의 objective를 두 가지 방법으로 Formulation한다. 



1. #####  Reward 를 Average하는 방법 

Policy에 따라 per step 마다 받는 reward를 average한다. (Long-term 관점)



### $\rho(\pi) = lim_{n \rightarrow \infin } \frac{1}{n} E \{ r_1 +r_2 + r_3 ... r_ \mid \pi \} = \sum_s d^{\pi}(s) \sum_{a} \pi(s,a)R^a_s$



여기서 $d^{\pi}$ 은 state $s_0$ 에서 policy $\pi$ 를 따른 state의 distribution 이며 다음과 같이 정의한다. 



$d^\pi (s) = lim_{n \rightarrow \infin} Pr \{ s_t = s \mid s_0 , \pi\}$



1.1. Average 방법에서의 State-action 



#### $Q_\pi (s,a) = \sum^\infin_{t=1} E\{r_t - \rho (\pi) \mid s_0 =s, a_0 =a, \pi\}$



2. 지정된 State state $s_0$에서 시작하는 방법 

두번째 방법은 지정된 State state $s_0$에서 시작하는 방법 으로 지정된 state에서 시작하여 얻은 long-term reward만을 고려한다. 



<img src="https://www.dropbox.com/s/9vvi05uvbdmytts/Screenshot%202018-08-20%2017.34.31.png?raw=1">





<img src="https://www.dropbox.com/s/0iwtmt3gx9h5r66/Screenshot%202018-08-20%2017.40.29.png?raw=1">

- policy를 따라 state $s_0$에서부터 받은 discounted reward를 모두 계산한다. 

##### $\gamma \in [ 0,1]$  : discount rate 



---



### Theorem 1 ( Policy Gradint )

<img src="https://www.dropbox.com/s/3ezwwoklgvjx78n/Screenshot%202018-08-20%2019.53.31.png?raw=1">



$d^\pi(s)= \sum_{t=0}^{\infin} \gamma^t Pr\{s_t = s \mid s_0, \pi\}$



$$d^\pi(s)$$ : state $$s_0$$ 부터 시작, policy $$\pi$$를 따른 encountered된 state의 discounted weighting



** History



##### Marbach and Tsitsikis (1998) : expressing the gradient was first discussed for the average-reward formulation



##### Singh, and Jordan (1995) :related expression state-value function 



위의 연구들의 결과를 사용하여 start-state formulation과 더 간단한 증명으로 발전시켰다.



##### Willams's(1988,1992) ,REINFORCE algorithm 가 위의 event와 다른 점은 위의 두 연구들은  state의 distribution에 따라 policy가 변하는 term인 $\frac{\partial d^\pi(s)}{\partial \theta}$ 가 고려되지 않았다는 것이다. 





### 3. 	Policy Gradient with Approximation 



이번에는 function approximator을 사용하여 Estimate 된 $Q^\pi$를 고려하는 것을 알아보도록 하겠다. 



<img src="https://www.dropbox.com/s/j1kelgxd3spbwz5/Screenshot%202018-08-20%2022.23.33.png?raw=1">



이 부분은 예전에 내가 정리해놓은 글과 크게 다르지 않아 블로그 글 링크로 대체함 



https://wonseokjung.github.io//reinforcementlearning/update/RL-PG_RE/























