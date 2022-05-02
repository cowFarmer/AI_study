# 강화학습 키워드 정리

---
### Reference
- [바닥부터 배우는 강화 학습](https://book.naver.com/bookdb/book_detail.nhn?bid=16657505)
- [혁펜하임의 "트이는" 강화 학습](https://www.youtube.com/playlist?list=PL_iJu012NOxehE8fdF9me4TLfbdv3ZW8g)
- [퀀티랩 블로그: 강화학습이란?](http://blog.quantylab.com/rl.html)

### markov process
마르코프 가정은 어떠한 시점의 상태는 바로 이전의 상태에만 영향을 받는다는 가정이다. 이를 응용하면 이전의 상태 t-1은 그 전인 t-2에 영향을 더 받는다.      

$P(S_t|S_1,S_2,...,S_{t-1})$ = $P(S_t|S_{t-1})$   
수식을 보면 $S_t$는 $S_{t-1}$에 큰 영향을 바독 $S_{t-1}$은 $S_{t-2}$에 영향을 받는 연쇄적인 상태들이 반영됐음을 알려준다.

다시 돌아와 마르코프 프로세스는 위의 가정을 만족하는 연속적인 상태이다.   

상태 전이 확률을 $P$라고 표현한다.   
$P_{s,s'} = P(S_{t+1} = s'|S_t=s)$   
수식으로 표현하면 다음과 같다. 현재 상태 $S_t=s$에서 $S_{t+1}=s'$이 될 확률을 말한다.

### markov decision process
강화학습의 목표는 return을 최대화 하는 것이다.   
$MDP = (S,A,P,R,\gamma)$   
MDP는 state의 집합 $S$, action의 집합 A, 상태 전이 확률 행렬 $P$, reward $R$, discount $\gamma$로 구성되어 있다.

$s$에서 특정 행동을 취했을 때 $s'$으로 갈 확률을 수식으로 표현해보자. 이는 MDP에서 상태 전이 확률 수식을 의미한다.   
$P^a_{s,s'} = P(S_{t+1}=s'|S_t=s,A_t=a$

특정 행동을 했을 때 받는 reward의 기대값을 수치로 변환하는 수식은 다음과 같다.   
$R_s^a=E[R_{t+1}|S_t=s,A_t=a]$   

### policy
policy는 특정 상태 $s$에서 수행할 행동 $a$를 정할 수 있는 정책을 말한다.   
$policy(a|s) = P(A_t=a|S_t=s)$

### 상태 가치 함수, state value function   
지금 $s_t$에서 기대되는 return의 expected 값이다.   
즉 현재 state에 대한 가치를 매겨주는 값이다.

### 행동 가치 함수, action value function   
지금 $s_t$에서 $a_t$할 때 기대되는 return의 expected 값이다.   
즉 행동에 대한 가치를 매겨주는 값이다.

### Optimal policy
state value function을 maximize 하는게 목표이다.

### 벨만 방정식

### Q-learning, Q-policy

### greedy action
### E greedy action
### model free 

### $G_t$
$G_t$는 goal(혹은 에피소드 끝)까지의 $R_t+\gamma R_{t2}+\gamma^2R_{t3}...$ reward를 말한다.   
$R_t$는 $S_t, a_t$의 reward를 말한다.

### Q*
Q*를 알기 위해 에피소드를 진행하면서 알고리즘으로 수렴을 해야함
-> 로봇이 자빠지는거
그 다음 test할때 입실론 그리디 그만하고 Q*를 기반으로 액션함

그래서 Q*를 구하기 위한 MC, TD 두 가지를 알아보자.

### Monte Carlo(MC)
Q*를 구하기 위해 monte carlo는 G_t를 n개만큼 다 해보는 것이다.   
맨 처음은 완전 random으로 진행한다.   
$\epsilon-greedy$으로 $G_t$를 반복하며 reward를 받아 이를 토대로 Q*를 알아낼 수 있음 -> optimal policy를 알아낼 수 있음

### Temporal difference(TD)
environment가 slippery인 상황에서 $P(s_{t+1}|s_t,a_t$는 예측이 벗어난 $s_{t+1}$로 움직일 수 있다.
MC와 큰 차이점으로 MC는 끝까지 가봐야 해봐야 결과를 알 수 있다.   
하지만 TD는 한 스텝만 움직이고 그 스텝에서 $R_t+\gamma Q(s_{t+1}, a_{t+1}$을 N개 만큼 합한 후 평균을 구해 $s_{t+1}$에 있는 action value를 알 수 있다.   
이를 통해 $s_{t+1}$의 Q*를 알 수 있다. 그리고 이를 1-step TD라고 말한다. 응용하면 여러 step TD도 가능하다.

- SARSA   
SARSA는 현재 state, 현재 action, reward, 다음 state, 다음 action을 뜻한다.   
즉 현재 state에서 action을 취한 뒤에 다음 state에서 action을 취한 후 policy가 update 된다.   
TD의 수식을 차례대로 보면 SARSA가 차례대로 들어있다.   
$Q(s_t, a_t) <- (1-\alpha)\hat{Q}_{N-1}+\alpha(R_t^N+\gamma Q(s_{t+1}^N, a_{t+1}^n)-\hat{Q}_{N-1})$   
TD에서 Q-learning과 다른점으로 Q-learning은 argmax로 다음 state의 action 값을 가져온다.
TD도 Q*의 최적화를 위해 exploration하는 $\epsilon-greedy$ 방식을 사용한다.

### MC와 TD의 차이점   
- MC는 직접 경험한 내용을 바탕으로 policy를 예측하고 개선하는 과정을 거친다. 그리고 이를 on policy라고 한다.
- TD는 예측한 샘플을 토대로 expectation을 구하고, 다시 예측하기 때문에 샘플들에 bias가 생긴다.   
최종적으로 정리해보자.   
MC는 unbiased한다. 하지만 여러 경로로 돌아다니면서 같은 state여도 $\gamma^t$ 만큼 곱하여 값이 구해지기 때문에 값들이 various가 크다.   
TD는 bias한다. 하지만 바로 다음 state의 값들만 expectation 하기 떄문에 various가 적다.

### $\theta$
neural network의 parameter vector를 말한다.

---

지금까지 MDP를 알때, 모를때 두 가지로 나뉜다
Markov는 현재만 갖고 미래를 예측한다.
이를 기반으로 예측을 시작한다.

환경, agent, action, reward가 주어지는데
환경을 구성하는 전이 확률과 보상을 아느냐 모르느냐로 나뉘진다.


MDP를 안다 -> 전이확률과 보상을 안다
상태 value 평가 -> s_1, s_2, s_3 들이 갖는 값
value 평가를 위해 반복적 정책 평가를 한다.
$V_{\pie}(s)$ <- 벨만 기대 방정식


정책 찾기
정책 이터레이션
파이_0 -> V_0 -> 파이_1 -> V_1
여기서 V에 벨만 기대 방정식이 들어옴

벨류 이터레이션
V_*(s)
벨만 최적 방정식을 씀


MDP를 모른다 -> 
value 평가를 위해 MC, TD를 사용한다.
MC는 V_0 -> V_1 ... V_무한대 반복해서 나온 value를 쓴다.
TD는 V_0 -> V_1만 쓴다.

정책을 찾기 위해
파이_0 -> V_0 -> 파이_1 -> V_1
여기서 V에 MC혹은 TD를 사용한다. 그리고 TD를 SARSA라고 말한다.

그리고 파이_1 대신 q(s,a)인 액션 가치 함수

그래서 q를 사용하면서 grid에 이제 q값이 나온다.
그리고 이를 Q(s,a) 러닝을 배움

1~6 챕터의 내용
위의 경우 그리드가 작아서 괜찮았는데 경우의 수가 엄청 많아서 딥러닝을 사용함

딥러닝의 기본 형태인 f = wx+b -> v = $\theta$s+b
로 표현함.

최적의 w를 찾기 위한 loss 찾기   
Loss(\theta) = [v_{true}(s)-v_{\theta}(s)]^2

그리고 이를 뉴럴 네트워크로 배워서 딥큐네트워크; DQN 이라고함