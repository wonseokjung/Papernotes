



# Neuronlike Adaptive Elements That Can Solve Difficult Learning Control Problems 

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

**Association** in psychology refers to a mental connection between concepts, events, or mental states that usually stems from specific experiences. 
https://en.wikipedia.org/wiki/Association_(psychology)





현재 Reinforcement Learning에서 Actor-Critic으로 불리는 학습 알고리즘의 아이디어가 제시된 1983년의 논문을 보았다. 


현재는 네트워크 두개를 사용해 하나는 action을 다른 하나는 state를  측정하는 방법을 actor - critic이라고 범용적으로 부르는 것 같지만, 
이 논문에서는 ASE와 ACE를 사용하여 Pole의 balance를 맞추는 환경에서 더 좋은 performace를 보였다 라고 제시하는 것 같다. 

재밌는점은 이 논문은 동물이 학습할때 short term memory와 long-term memory를 통해 학습한다는 것을  출발한것처럼 보인다. 
