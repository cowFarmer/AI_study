# 강화학습 키워드 정리

---
### Reference
- [바닥부터 배우는 강화 학습](https://book.naver.com/bookdb/book_detail.nhn?bid=16657505)
- [혁펜하임의 "트이는" 강화 학습](https://www.youtube.com/playlist?list=PL_iJu012NOxehE8fdF9me4TLfbdv3ZW8g)
- [퀀티랩 블로그: 강화학습이란?](http://blog.quantylab.com/rl.html)

### markov decision process
MDP

### 상태 가치 함수
state value function


### 행동 가치 함수
action value function
s_t에서 a_t할 때 기대되는 return

### Q-learning

### greedy action
### E greedy action

### Optimal policy

### Q*
Q*를 알기 위해 에피소드를 진행하면서 알고리즘으로 수렴을 해야함
-> 로봇이 자빠지는거
그 다음 test할때 입실론 그리디 그만하고 Q*를 기반으로 액션함

그래서 Q*를 구하기 위한 MC, TD 두 가지를 알아보자.

### Monte Carlo(MC)
Q*를 구하기 위해 monte carlo는 G_t를 n개만큼 다 해보는 것
맨 처음은 완전 random
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


G_t는 goal(혹은 에피소드 끝)까지의 $R_t+\gamma R_{t2}+\gamma^2R_{t3}...$ reward를 말한다.
$R_t$는 $S_t, a_t$의 reward를 말한다.