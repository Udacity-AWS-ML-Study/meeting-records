# 210807) Lesson 3 - meeting record

### 👾 **소진님 발표**
> AWS DeepRacer를 이용한 자율주행 모델 구축

- 주제 선정 이유
  -  RL에 대한 관심
      - 인간 학습에 대한 기본적인 이론 => 행동주의 조건형성 학습과 유사
      - 행동 심리 이론을 코딩으로 구현했다는 것에 대한 흥미로움

    <br>
    
  -  기업협업 프로젝트에서 시도했다가 실패한 기억
      -  연비를 최소화 하도록 하는 버스 자율주행 모델 구현을 시도했지만 실패
      -  => Unity에서 트랙을 만들고, C#으로 직접 하나부터 열까지 다 구현해야 했음
      -  but, AWS DeepRacer로는 더 쉽게 자율주행 모델 구현 가능

- Reinforce Learning
  - RL 구성요소
    - agent : 우리가 training 시키는 대상 ex) 자동차 => environment 속에서 목표를 달성하기 위해 action을 취한다.
    - environments :  agent가 상호작용하는 주변영역 ex) 트랙
    - rewards : 주어진 상태에서 agent가 수행하는 각 action에 대해 제공되는 feedback
  > 어떠 상태일 때 어떤 보상을 주는지에 따라 모델의 성능에 큰 영향을 준다 <br>
  > => 이를 잘 코딩하는 것이 우리의 역할
  
- modeling 결과
  - training environments <br>

    <img width="727" alt="Screen Shot 2021-08-09 at 3 32 24 PM" src="https://user-images.githubusercontent.com/69139242/128667762-5bf65750-ba35-4c16-9551-ff9c826a1a0a.png">

  - RL algoritms 
    - PPO(Proximal Policy Optimization) <br>
      - TRPO(Actor Critic 알고리즘 기반으로 반복되는 학습 정책을 정규화. 
      - 규제(Penalty) 사용으로 불필요한 학습을 억제하여 빠르게 수렴)와 유사한 알고리즘으로 대리 손실함수를 생성하여 더 빠른 수렴을 지원
      - TRPO보다 구현이 간단
    - SAC (Soft Actor Critic) <br>
      - DDPG(DQN의 Replay Memory를 사용하여 연속적인 Batch 업데이트가 가능. 
      - 빠른 수렴을 위해 정책제어를 사용함)와 유사한 방식으로 Q-function의 근사값으로 탐색을 제어.
      - 로봇 시뮬레이션 모델링을 위해 많이 사용됨
   
   - Hyperparameter <br>

   <img width="285" alt="Screen Shot 2021-08-09 at 3 35 10 PM" src="https://user-images.githubusercontent.com/69139242/128667987-97a71625-be17-40f0-af9f-12c6abb5aada.png">
   
   - Reward Function <br>
   : DeepRacer에서 제공하는 기본적인 reward function에 핸들의 steering 각도를 추가적인 parameter로 받아와 일정 범위가 넘을 시 보상에 0.8배르 주어 지그재그로 주행하는 불필요한 움직임을 막는 rf를 사용하였다. 


### 👾 **보윤님 발표**
