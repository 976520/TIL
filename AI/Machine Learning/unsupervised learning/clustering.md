## 군집화

> 군집화는 개체의 유사도에 따라 그룹(군집)을 나누는 것을 뜻한다.

1. 개념

   데이터가 쭉 흩뿌려져 있을 때, 레이블이 없다고 해도 데이터 간 거리에 따라 데이터를 몇 개의 군집으로 나눌 수 있다. 이렇게 독립변수만 가지고 군집을 학습하는 것이 군집화이다.

   > 군집(cluster)은 데이터 집합 내에 존재하는 유용성 있는 그룹을 말한다.

   한마디로 비슷한 것끼리 묶는다는 것이다. 따라서 **같은 군집에 속한 데이터는 서로 비슷하고, 다른 군집에 속한 데이터는 서로 달라야 한다**. 이를 경영학의 마케팅 분야에서 segment라고 부르기도 한다.

   따라서 군집을 구성하기 위해서는 데이터 간의 proximity(근접성) 또는 similarity(유사성)을 파악하여 그 결과에 따라 데이터를 하나의 군집으로 모아야 한다.

   이때 거리는 보통 유클리드 거리(euclidean distance)로 정의된다. $n$차원의 데이터 $p$와 $q$가 각각 $(p_1, p_2, … , p_n)$, $(q_1, q_2, …, q_n)$ 의 좌표를 가질 때, 두 점 $p$와 $q$ 사이의 거리 $D$에 대해 다음 공식이 성립한다. ~~다음 식처럼 유클리드 노름을 통해 표현하는 경우가 많지만 필자의 지능 이슈로 인해 이 글에서는 노름을 사용하지 않는다.~~

   > $D(x,y) = ||x-y||=\sqrt{\displaystyle\sum_{i=1}^n(x_i-y_i)^2}$

   ![군집화](https://github.com/user-attachments/assets/0080383b-8b5c-422a-8192-8a7dde0c6ec7)

   이러한 군집화는 여러 종류가 있지만, 이들의 원리는 모두 같다. 그 원리라 하면, 같은 그룹끼리의 cohesion(응집도)와 다른 그룹과의 separation(분리도)를 모두 최대화하는 것이다.

   군집 $C_i에서$의 cohesion은 다음과 같이 데이터와 데이터 간의 거리의 합으로 측정할 수 있고,

   > $Cohesion(C_i) = \displaystyle\sum_{a∈C_i}\displaystyle\sum_{b∈C_i}D(a,b)$

   다음과 같이 각 데이터와 그 데이터의 중심 $R_i$간의 거리의 합을 이용해 측정할 수도 있다.

   > $Cohesion(C_i) = \displaystyle\sum_{a∈C_i}D(a, R_i)$

   군집 $C_i$, $C_j$에서의 separation은 다음과 같이 두 군집 간 데이터의 모든 쌍의 거리의 합으로 측정할 수도 있고,

   > $Separation(C_i, C_j) = \displaystyle\sum_{a∈C_i}\displaystyle\sum_{b∈C_j}D(a,b)$

   다음과 같이 두 군집의 중심 $R_i$, $R_j$간의 거리로 측정할 수도 있다.

   > $Separation(C_i, C_j) = d(R_i, R_j)$

2. 분류 모델과의 차이

   그룹을 나눈다는 점에서 지도학습의 분류 모델과 다소 비슷한 면을 보인다.

   분류 모델은 이미 종속변수가 있어서 어떤 그룹으로 묶을지 생각하고 할당하지만, 군집화의 경우 주어진 종속변수가 없는 상태로 데이터의 속성 간의 관계를 찾고자 하기 때문에 군집화의 결과로 얻어진 군집의 의미에 대해서는 군집 속의 데이터를 이용해 개발자가 차후에 분석해야 한다.

3. 종류

   1. hierarchical clustering(계층적 군집화)

      hierarchical clustering은 한 군집이 다른 하위 군집을 갖도록 군집을 만드는 방법으로, Connectivity based clustering이라고 부르기도 한다.

      군집의 시작점과 진행 순서의 차이에 따라 다음 두가지로 나뉜다.

      1. agglomerative clustering(응집형 군집화)

         agglomerative clustering은 singleton cluster(단일 원소 군집)들을 먼저 생성하고, 가까이 있는 군집을 서로 합치는 과정을 반복하는 방법이다. 하지만 이를 끝없이 반복하면 당연히 하나의 군집만 남게 되는데, 그 전에 적절한 타이밍에 병합을 종료하고 몇 개의 군집으로 정리한다.

      2. division clustering(분리형 군집화)

         division clustering은 agglomerative clustering와 반대로 모든 개체를 하나의 군집으로 보고 시작하며, 이러한 군집을 거리가 먼 순서로 분리해나간다. 이 또한 끝없이 반복하면 각각의 개체로 분리되기 때문에 적절한 타이밍을 찾아 분리를 종료하고 몇 개의 군집으로 정리한다.

   2. partitional clustering(분할적 군집화)

      Non-hierarchical clustering이라고 부르기도 한다.

      1. prototype based(중심 기반)

         Prototype based clustering은 군집의 centroid(중심점)를 먼저 설정하고, 그 centroid에 가까운 개체들을 하나의 군집으로 모아가며 확장해나가는 기법이다. 이때 centroid의 개수와 그 배치 방법에 따라 K-Means, K-Median, K-Medoid 등의 방법들이 있지만, ~~귀찮으니까~~ 가장 대표적인 K-Means을 예로 들어 설명한다.

         K-Means의 원리는 먼저 $k$개의 centroid를 random하게 선택하고 각 개체는 가장 가까운 centroid와 같은 군집으로 할당한다. 그리고 각 군집에 속한 개체의 평균을 통해 중심을 다시 계산하고 다시 각 개체의 가장 가까운 군집으로 재할당하며, 이 과정을 재할당이 더 일어나지 않아서 centroid가 이동하지 않거나 최대 반복횟수에 도달할 때 까지 반복한다.

         K-Means의 장점은 과정이 직관적이여서 이해하기 편하며, 계산량이 비교적 적어서 대용량 데이터의 처리에 유리하다는 것이다. 하지만 군집의 centroid의 개수 $k$가 hyper parameters라는 불편함이 있다. 또한 재할당 과정에서 군집에 속한 개체의 평균을 이용하기 때문에 극단적인 한 값에 굉장히 민감하다는 한계가 있다. 따라서 데이터의 분포가 circular(원형) 데이터가 아닐 경우 clustering이 잘 이루어지지 않는다. 이를 개선하기 위한 방법이 K-Median이며, 이 방법은 재할당 과정에서 평균 대신 중앙값을 활용한다는 점에서 K-Means와 차이가 있다.

      2. destiny based(밀도 기반)

         Destiny based clustering은 군집을 ‘높은 밀도를 가진 데이터의 공간’으로 정의한다. 즉, 서로 근접하거나 패턴을 보이는 데이터라고 할지라도 밀도가 낮다면 군집으로 인식하지 않고 무시한다.

         따라서 destiny based clustering은 중심 기반 군집화의 한계점을 보완했다고 볼 수 있다. destiny based clustering은 밀도가 낮은 곳, 즉 다른 개체들과 동떨어진 개체를 군집에 포함시키지 않으므로~~왕따~~, 앞서 설명한 K-Means처럼 극단적인 한 값에 대해 민감하게 반응하지 않는다.

         DBSCAN는 Density-Based Spatial Clustering of Applications with Noise의 약자로, 개체들의 밀도를 계산하여 밀도가 높게 분포된 개체들끼리 묶어주는 destiny based clustering의 표본과도 같은 기법이다. K-Means처럼 중심의 개수를 지정하지는 않지만 epsilon라고 하는 반지름의 길이를 지정해주어야 한다.

         DBSCAN에서의 데이터는 세 종류로 나뉜다. 먼저 군집 내부에 있는 core point(핵심점)이 있다. 이 core point가 중심이고 epsilon을 반지름으로 하는 원을 $p$라고 정의할 때 $p$에는 속하지만 핵심점은 아닌 border point(경계점), 원 $p$에조차 속하지 않는 noise point(잡음점)이 있다. 때문에 K-Means에서 부각된 단점 중 하나인 극단적인 한 값에 대한 효과적인 대응이 가능하다. 이에 더불어 밀도만 일정하다면 요상하게 분포된 온갖 모양의 데이터들에 대해 군집을 찾아낼 수 있다.

      3. distribution based(분포 기반)

         Distribution based clustering은 데이터가 어느 군집에 속할 확률이 더 높은지 계산하여 나눈다.

         GMM는 Gaussian mixture model의 약자로 전체 데이터를 $k$개의 정규분포로 표현할 수 있는 데이터들의 결합이라고 간주하고, 데이터로부터 maximum likelihood estimator(최대 우도 추정량)을 추정한다. 이는 해당 사건의 발생 확률을 최대로 높이는 분포를 찾는 것이다. 즉, 각 분포에 속할 수 있는 확률이 높은 개체들로 군집을 형성하는 것이다. 이에 따라 GMM은 각 정규분포의 평균과 분산, 각 데이터가 각 정규분포에 해당될 확률을 추정한다. 따라서 GMM의 총 정규분포의 개수는 hyper parameters이다.

         앞서 말한 maximum likelihood estimator을 구하는 알고리즘으로 expectation maximization(기댓값 최대화)이 있다. 이는 우선 한 분포에 대해 데이터의 maximum likelihood estimator가 최대가 될 때 까지 모든 분포에 대해 데이터를 재계산한다. maximum likelihood estimator가 최대가 된다면 이것으로 최종적인 기댓값을 산출한다. 이러한 두 단계를 각각 expectation(예측) 단계와 maximization(최대화) 단계로 명명한다.

         이러한 GMM은 데이터의 분포에 대해 굉장히 자유롭다는 장점이 있다.

---
