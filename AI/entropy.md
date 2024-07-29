# 엔트로피 얘는 물리 아닌가요

> Entropy는 주어진 데이터 집합의 혼잡도를 의미한다.

1. 개념

   확률분포의 불확실성을 나타내는 척도 혹은 정보량의 기댓값이라고 할 수 있다. ~~뭐야 물리에 걔 맞잖아~~ 정보량을 측정하기 위해서 개발되었고 집단에 각 부류의 데이터들이 균등한 비율로 섞여 있을수록 entropy가 커진다. 얼마나 균질히 얼마나 섞여있느냐가 기준인 것이다.

   예를 들어 동전을 던졌을 때와 주사위를 던졌을 때 중 어떤 데이터가 나올 지 예측하기 어려운 것은 당연히 후자이다. 이때 주사위가 더 불확실성이 높은 것이며 이러한 불확실성을 숫자로 나타낸 것이 entropy이다.

   Entropy는 어떤 사건이 정보적 측면에서 얼마나 중요한가를 반영한 로그 지표에 대한 기댓값을 통해 표현한다. 따라서 분포 $p$에 대한 entropy는 다음과 같다.

   > $H(p) = -\displaystyle\sum^n_{i=1}p(x_i)log_a(p(x_i))$

   여기서 $p(x_i)$는 주어진 데이터 집합에서 부류 $x_i$에 속하는 데이터의 비율을 나타낸다. $\frac{(속해있는 데이터)}{(전체 데이터)}$ 이므로 항상 분수가 나오게 된다. 때문에 $log_a\frac{1}{p(x_i)}$ 였지만, 분수를 없애기 위해 변환하고 $-$를 붙인 것이다. 또한 $log$가 들어가는 이유는 확률값 혹은 확률밀도값에 반비례해야하기 때문이다. $log$의 밑 $a$는 보통 10, 즉 자연로그가 사용된다.

2. Cross Entropy

   Cross entropy는두 확률 분포의 차이를 구하기 위해 사용된다. Machine learning에서는 실제 데이터의 확률 분포와 모델이 계산한 확률 분포의 dissimilarity(차이)를 구할 때 사용한다.

   실제 분포 $p$를 예측하는 분포 $q$가 있을 때, cross entropy는 다음과 같이 정의된다.

   > $H_q(p)=\displaystyle\sum^n*{i=1}p(x_i)log_a(q(x_i))$

3. KL Divergence

   여기서 KL은 Kullback Leibler의 약자로, 서로 다른 두 분포의 dissimilarity를 측정하는데 쓰인다. 이를 entropy와 cross entropy 개념에 대입하면, 두 entropy의 차이로 계산된다는 사실을 알 수 있다.

   실제 분포 $p$를 예측하는 분포 $q$가 있을 때, KL Divergence는 다음과 같이 정의된다. 아래 식의 경우 $p$와 $q$가 모두 이산분포일 때 해당된다.

   > $D_{KL}(p||q) = \displaystyle\sum_ip(x_i)log_a\frac{p(x_i)}{q(x_i)}$

   $p$와 $q$가 연속적인 확률 분포인 경우, 적분을 이용하여 다음과 같이 정의한다.

   > $D_{KL}(p||q) = \displaystyle\int_{-∞}^∞p(x_i)log_a\frac{p(x_i)}{q(x_i)}dx$

   KL Divergence는 비대칭적인 특성을 지닌다. 따라서 $D_{KL}(p||q)\neq D_{KL}(q||p)$ 일 수 있다.

---
