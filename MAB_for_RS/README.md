## Multi-Armed Bandits in Python: Epsilon Greedy, UCB1, Bayesian UCB, and EXP3
* [code reference](https://jamesrledoux.com/algorithms/bandit-algorithms-epsilon-ucb-exp-python/)

### Datasets and Experiment Setup
- [Movielens 25m](https://grouplens.org/datasets/movielens/25m/): ratings for 27,000 movies provided by 138,000 users
- binary 문제로 정의: 4.5점 이상은 1(liked), 미만은 0(disliked)
- `Replay` method 사용: 과거 데이터셋의 편향을 제거하고 실제 production 환경에서 bandit이 수행하는 방식을 시뮬레이션하기 위해
- `Replay` method를 사용하여 알고리즘의 성능 평가를 위해 "liked"를 받은 bandit의 추천 비율을 평가
- 실행 시간 단축을 위해 한 번에 한 편의 영화 대신, 여러 편의 영화를 추천
- 각 데이터에 대해 bandit의 정책을 한 번씩 업데이트 하는 대신, 여러 사용자에게 영화 추천
- 데이터의 최종 형태: `[timestamp, userId, movieId, liked]`

### Bandit Setting
- k개의 arm: 추천할 content
- 정보 관찰: 각각의 arms들이 과거에 얼마나 많이 pull 당했는지, 그때의 보상 가치는 얼마였는지
- 알고리즘의 정책에 의해 가장 적합하다고 생각되는 arm pulling
- 그 arm의 reward (결과가 얼마나 좋은지) 또는 regret (얼마나 더 나쁜지)
- reward/regret으로 미래에 arm을 선택할 정책을 업데이트
- 이 과정을 계속해서 반복 -> regret를 최소화하기 위해 exploration-exploitation
