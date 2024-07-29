# 경사하강법 탐구하기

> 경사하강법은 함수의 최솟값을 찾는 optimizer 이다.

~~인공신경망을 만만하게 본 학우들이 처음으로 갈려나가는 관문이다.~~

optimizer는 최적화 이론 기법이라고 할 수 있다.

---

## 개념

1. 정의

   경사하강법이란 함수의 값이 낮아지는 방향으로 각 독립변수들의 값을 변형시키면서 함수가 최솟값을 갖도록 하는 독립변수의 값을 탐색하는 방법이다. 함수의 gradient(경사)를 구하고, 해당 gradient의 반대 방향으로 이동시킨다. 이 과정을 극값, 즉 최소 지점에 이를 때 까지 반복한다. 반대로 이를 최고 지점에 이를 때 까지 반복하면 경사상승법이라고 한다.

2. gradient

   여기서 gradient란 $R^n$ -> $R$ 형태의 실수 함수의 미분을 뜻한다.

   함수값이 실수인 $n$차원 다변수함수 $f(x)=f(x_1, x_2, ..., x_n)$가 있을 때, **$f(x)$를 각 변수에 대해 일차 편미분한 벡터**를 gradient라고 하며 매개변수가 $x$일 때 목적함수 $f$의 gradient 값을 $∇f(x)$와 같이 표현한다. 따라서 gradient는 $x$에 대해 $f(x)$가 가장 가파르게 증가하는 방향과 증가율을 나타낸다고 할 수 있다.

---

## 알고리즘

기본적인~~아주 이상적인 데이터의~~ 경사하강법의 알고리즘은 다음 순서를 거친다.

1. 시작점

   임의의 매개변수를 시작점으로 설정한다.

   이 시작점을 어디로 잡느냐에 따라 나중에 수렴 지점이 달라질 수 있다. $y$값이 가장 낮은 부분인 global minima(전역 최소점)을 목적으로 했지만, 미분계수가 가장 낮은 부분인 local minima(지역 최소점)으로 수렴할 가능성이 있다. 이러한 문제를 local minimum 문제라고 한다. 따라서 수렴 지점이 무조건 최소값이 아닐 수 있다.

   ![Untitled](https://github.com/user-attachments/assets/bb8e8ebd-7dce-408b-8075-05cc73504846)

2. 업데이트

   최적화하고자 하는 함수 $f(x)$에 대해 다음과 같은 식을 이용해 다음 가중치의 위치로 이동하며, 이를 업데이트라고 한다. 이때 $x_t$는 $t$번째 반복의 매개변수 $x$값이다.

   > $\$x_{t+1}$ $=$ $x_t - η \frac{∂f}{∂x}(x_t)$

   이를 다변수함수에 대해 확장하면 다음과 같다.

   > $x_{t+1}$ $=$ $x_t - η∇f(x_t)$

   미분의 인수가 함수 $f$의 그것과 ~~편미분이니까 당연히~~같으므로, 함수 의존성을 명시적으로 표기하여 정의하자면 다음과 같다.

   > $∇f(x_1, x_2, ..., x_n) = (\frac{∂f}{∂x_1},\frac{∂f}{∂x_2},...,\frac{∂f}{∂x_n}) = \frac{∂f}{∂x}(x_1, x_2,...,x_n)$

   이때 계수 **$η$는 step size(이동할 거리)를 조정하는 하이퍼파라미터이며, 이를 learning rate(학습률)라고 한다.** learning rate가 너무 크면 수렴할 값을 놓치고 발산할 수 있고(overshooting), learning rate가 너무 작으면 그만큼 수렴이 늦어질(learn too slow) 수 있다. 다음은 이를 표현한 그림이다.

   ![Untitled2](https://github.com/user-attachments/assets/4d799835-d665-4575-af65-75ff74b592e9)

3. 반복

   Objective function(목적함수)이 특정 값으로 알맞게 수렴할 때 까지 이 과정을 반복한다. 인공신경망에서는 loss function(손실함수)이 최소가 되는 지점을 찾기 위해 경사하강법을 사용한다.

---

## 사용

Javascript로 다음과 같이 간단한 선형 [회귀](https://github.com/976520/TIL/blob/main/AI/Machine%20Learning/supervised%20learning/prediction.md) 문제를 경사하강법으로 해결할 수 있다.

```javascript
// 데이터셋
const data = [
  { x: 1, y: 2 },
  { x: 2, y: 3 },
  { x: 3, y: 4 },
  { x: 4, y: 5 },
];

// weight와 bias 초기화
let weight = 0;
let bias = 0;

// 하이퍼파라미터 설정
const learningRate = 0.01;
const epochs = 1000;

// 회귀식 예측 (y = wx + b)
function predict(x) {
  return weight * x + bias;
}

// loss function
function loss() {
  let totalError = 0;
  for (let i = 0; i < data.length; i++) {
    const { x, y } = data[i];
    const error = predict(x) - y;
    totalError += error * error;
  }
  return totalError / data.length;
}

// gradient 계산
function gradientDescent() {
  let weightGradient = 0;
  let biasGradient = 0;

  for (let i = 0; i < data.length; i++) {
    const { x, y } = data[i];
    const error = predict(x) - y;
    weightGradient += 2 * error * x;
    biasGradient += 2 * error;
  }

  weightGradient /= data.length;
  biasGradient /= data.length;

  weight -= learningRate * weightGradient;
  bias -= learningRate * biasGradient;
}

// 반복
for (let epoch = 0; epoch < epochs; epoch++) {
  gradientDescent();
  if (epoch % 100 === 0) {
    console.log(`Epoch ${epoch}: Loss = ${loss()}`);
  }
}

// 결과 출력
console.log(`weight: ${weight}`);
console.log(`bias: ${bias}`);
```

---

## 종류

Optimizer에도 여러 종류가 있다. 보통 한 방법론의 단점을 개선하여 발전시키는 방향으로 다른 방법론이 제시되지만, 모든 상황에 특정 optimizer가 가장 성능이 좋다고 단언하기는 어려운 부분이 많다. 데이터셋과 신경망의 특성에 따라 각 optimizer의 성능은 크게 차이가 날 수 있다. 현재로써는 대부분의 상황에 후술할 ADAM 알고리즘을 채택하고는 있지만, 어떤 알고리즘이 가장 적절할 지 실험해 볼 필요성은 아직 다분하다고 할 수 있다.

여기서 기술할 알고리즘은 모두 first-order optimization의 변형들이다. 이는 한 번 미분한 값을 활용하여 optimization하는 것이다. First가 있으니 물론 second-order optimization을 기반으로 한 알고리즘들도 있으나, hessian matrix라는 2차 편미분 행렬과 그 역행렬을 계산하는 과정에서 막대한 비용이 발생하므로 잘 사용하지 않는다.

~~필자의 능지 이슈로 인해 단일 변수 함수에 대한 편미분 수식만 기술했다.~~

1. SGD

   1. 개념

      SGD는 Stochastic Gradient Descent의 약자로, 확률적 경사하강법이라고 하여 mini batch라고 하는 전체 데이터셋에서 확률적으로 선택된 소규모 데이터 샘플 그룹을 사용하여 각 단계에서 gradient를 계산하고 가중치를 업데이트 하는 방식으로 작동한다.

      기존의 경사하강법은 full batch를 바탕으로 진행하기에 학습 수렴속도가 느리다는 단점이 있었지만, 이 방법은 대량의 데이터에 대한 훈련을 빠르게 수행할 수 있게 한다. 하지만 mini batch의 크기(batch size)와 learning rate에 따라 모델 성능에 큰 영향을 받는다는 단점이 있다.

   2. 알고리즘

      앞서 설명했듯, mini batch 내의 각 데이터 포인트에 대한 손실을 계산하고 그에 대한 가중치의 편미분을 수행한다. 이를 통해 loss function의 gradient를 산출하고, 이 gradient를 이용하여 가중치를 업데이트한다. 이때 하이퍼파라미터로 정해진 learning rate가 사용되어 가중치를 얼마나 크게 조정할 지 결정한다. ~~가중치의 가중치~~ mini batch 단위로 이 과정을 반복하여 모델을 최적화할 수 있다.

      업데이트 식은 다음과 같으며 이는 경사하강법과 동일하다. SGD와 경사하강법의 차이는 오직 입력된 데이터에서만 존재한다.

      > $x_{t+1}$ $=$ $x_t - η \frac{∂f}{∂x}(x_t)$

   3. 사용

      Javascript로 다음과 같이 간단한 선형 회귀 문제를 SGD로 해결할 수 있다.

      ```javascript
      const data = [
        { x: 1, y: 2 },
        { x: 2, y: 3 },
        { x: 3, y: 4 },
        { x: 4, y: 5 },
      ];

      let weight = 0;
      let bias = 0;

      const learningRate = 0.01;
      const epochs = 100;

      function predict(x) {
        return weight * x + bias;
      }

      function loss() {
        let totalError = 0;
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          const error = predict(x) - y;
          totalError += error * error;
        }
        return totalError / data.length;
      }

      function stochasticGradientDescent(x, y) {
        const error = predict(x) - y;
        const weightGradient = 2 * error * x;
        const biasGradient = 2 * error;

        weight -= learningRate * weightGradient;
        bias -= learningRate * biasGradient;
      }

      for (let epoch = 0; epoch < epochs; epoch++) {
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          stochasticGradientDescent(x, y);
        }
        if (epoch % 10 === 0) {
          console.log(`Epoch ${epoch}: Loss = ${loss()}`);
        }
      }

      console.log(`weight: ${weight}`);
      console.log(`bias: ${bias}`);
      ```

2. Momentum

   1. 개념

      Momentum은 기존 경사하강법에 가속도항을 추가하여 local minimum 문제를 해결한 경사하강 방법론이다.

   2. 알고리즘

      가속도 $v$에 대한 식은 다음과 같다.

      > $v_{t+1}=mv_t-η\frac{∂L}{∂x}$

      $v$의 영향으로 인해 기존 가중치가 이전 업데이트 방향으로 더 크게 변화하게끔 하였다. 당연히 $v$는 처음에 0으로 초기화된다.

      또한 $m$은 momentum 운동량 또는 momentum 계수라고 하며, 이를 통해 업데이트가 양의 방향와 음의 방향을 순차적으로 오가며 일어나는 지그재그 현상이 줄어들고, 이전 이동을 고려하여 일정 비율만큼 다음 값을 결정하기에 관성의 효과를 낼 수 있다.

      업데이트 식은 다음과 같다.

      > $x_{t+1} = x_t + v_t$

      $v$에 따른 관성 효과 덕분에 미분계수가 0인 지점에 도달하여도 계속 업데이트가 될 수 있다.

   3. 사용

      Javascript로 다음과 같이 간단한 선형 회귀 문제를 momentum으로 해결할 수 있다.

      ```javascript
      const data = [
        { x: 1, y: 2 },
        { x: 2, y: 3 },
        { x: 3, y: 4 },
        { x: 4, y: 5 },
      ];

      let weight = 0;
      let bias = 0;

      const learningRate = 0.01;
      const momentum = 0.9;

      const epochs = 100;

      let velocityWeight = 0;
      let velocityBias = 0;

      function predict(x) {
        return weight * x + bias;
      }

      function loss() {
        let totalError = 0;
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          const error = predict(x) - y;
          totalError += error * error;
        }
        return totalError / data.length;
      }

      function stochasticGradientDescentWithMomentum(x, y) {
        const error = predict(x) - y;
        const weightGradient = 2 * error * x;
        const biasGradient = 2 * error;

        velocityWeight = momentum * velocityWeight - learningRate * weightGradient;
        velocityBias = momentum * velocityBias - learningRate * biasGradient;

        weight += velocityWeight;
        bias += velocityBias;
      }

      for (let epoch = 0; epoch < epochs; epoch++) {
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          stochasticGradientDescentWithMomentum(x, y);
        }
        if (epoch % 10 === 0) {
          console.log(`Epoch ${epoch}: Loss = ${loss()}`);
        }
      }

      console.log(`weight: ${weight}`);
      console.log(`bias: ${bias}`);
      ```

3. Adagrad

   1. 개념

      Adagrad는 ADAptive GRADient descent의 약자로, 적응형 하강법이라는 뜻이다. 각각의 매개변수에 대해 learning rate를 동적으로 조절해주는 원리이다. Adagrad는 뉴럴 네트워크 내부에서 많이 변화한 변수에 대해서는 learning rate를 적게 하고, 그렇지 않은 변수에 대해서는 learning rate를 크게 한다. 많이 변화한 변수는 최소점에 가까워졌을 것이라고 생각하고 세밀하게 조정하며, 반대로 적게 변화한 변수는 learning rate를 크게 하여 loss를 줄인다. 따라서 adagrad의 장점은 learning rate를 신경쓰지 않아도 된다는 것에 있다.

   2. 알고리즘

      업데이트 식은 다음과 같다. 이때 $ϵ$는 0으로 나눠지는 것을 방지하기 위한 상수이며, 보통 $10^{-4}$ 에서 $10^{-8}$ 사이의 값을 취한다.

      > $x_{t+1} = x_t - \frac{η}{\sqrt{G_t+ϵ}}\frac{∂f}{∂x}(x_t)$

      다음은 gradient를 누적하는 식이며, 처음에 0으로 초기화된다. 간단히 얼마나 많이 변화했는지에 대한 정보를 저장한다고 이해하면 된다.

      > $G_t=G_{t−1}+(\frac{∂f}{∂x}(x_t))^2$

      gradient를 누적하는 식을 합쳐서 업데이트 식을 다음과 같이 표현하기도 한다.

      > $x_{t+1} = x_t - \frac{η}{\sqrt{\displaystyle\sum^t_{i=1}{(\frac{∂f}{∂x}(x_i))^2}+ϵ}}\frac{∂f}{∂x}(x_t)$

      학습을 계속 진행함에 따라 step size가 지나치게 줄어들어 거의 움직이지 않는 상태가 된다는 단점이 있다. 앞선 식에서 알 수 있듯, $G$에서 계속 제곱된 값을 할당해주기 때문에 $G$의 값들은 계속 빠르게 증가(property of monotonic increasing)하기 때문이다.

   3. 사용

      Javascript로 다음과 같이 간단한 선형 회귀 문제를 adagrad로 해결할 수 있다.

      ```javascript
      const data = [
        { x: 1, y: 2 },
        { x: 2, y: 3 },
        { x: 3, y: 4 },
        { x: 4, y: 5 },
      ];

      let weight = 0;
      let bias = 0;

      const learningRate = 0.01;
      const epochs = 100;

      let gradSquaredWeight = 0;
      let gradSquaredBias = 0;

      const epsilon = 1e-8;

      function predict(x) {
        return weight * x + bias;
      }

      function loss() {
        let totalError = 0;
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          const error = predict(x) - y;
          totalError += error * error;
        }
        return totalError / data.length;
      }

      function adagrad(x, y) {
        const error = predict(x) - y;
        const weightGradient = 2 * error * x;
        const biasGradient = 2 * error;

        gradSquaredWeight += weightGradient * weightGradient;
        gradSquaredBias += biasGradient * biasGradient;

        weight -= (learningRate / Math.sqrt(gradSquaredWeight + epsilon)) * weightGradient;
        bias -= (learningRate / Math.sqrt(gradSquaredBias + epsilon)) * biasGradient;
      }

      for (let epoch = 0; epoch < epochs; epoch++) {
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          adagrad(x, y);
        }
        if (epoch % 10 === 0) {
          console.log(`Epoch ${epoch}: Loss = ${loss()}`);
        }
      }

      console.log(`weight: ${weight}`);
      console.log(`bias: ${bias}`);
      ```

4. RMSProp

   1. 개념

      RMSProp은 adagrad의 $G_t$ 값이 무한히 커지는 문제를 지수 가중 이동 평균을 이용해 방지한 방법론이다. $G_t$를 합이 아니라 지수 가중 이동 평균으로 대체함으로써, $G_t$가 최근 변화량의 변수간 상대적인 크기 차이를 유지한다.

      지수 가중 이동 평균이란, 최근 값을 예전 값보다 더 영향력있게 반영하기 위해 최근 값과 예전 값에 각각 적절한 가중치를 주어 계산하는 방법이라고 할 수 있다.

      이해하기 쉽게 식으로 표현하자면 다음과 같다.

      > $x_t = αp_t + (1-α)x_{t-1}$

      $t$번째 step에서의 지수 이동평균값 $x_t$에서 현재 값을 $p$, 가중치를 $α$로 표현하였다. 예를 들어 가중치 $α$의 값을 다음과 같이 표현할 수 있다.

      > $α = \frac{2}{t+1}$

      $t$는 값의 개수라고도 할 수 있으며, $t$가 0일 경우를 대비하여 1을 더해준 모습이다. 가중치 $α$는 $t$가 작을 수록 커질 것이다. 필터이론에서는 이러한 가중치를 forgetting factor 또는 decaying factor라고 한다.

   2. 알고리즘

      지수 가중 이동 평균을 적용한 RMSProp의 업데이트 식은 다음과 같다.

      > $x_{t+1} = x_t - \frac{η}{\sqrt{E[g^2]_t+ϵ}}\frac{∂f}{∂x}(x_t)$

      다음은 분모에 있는 gradient 제곱의 지수 가중 이동 평균 $E[g^2]_t$를 수식으로 정의한 것이다.

      > $E[g^2]_t=γE[g^2]_{t-1}+(1-γ)(\frac{∂f}{∂x}(x_t))^2$

      여기서 $ϵ$는 adagrad의 그것과 같은 용도이고, $γ$는 gradient 제곱의 가중치를 조절하는 감쇠 계수로, 보통 0.9정도로 설정된다.

   3. 사용

      Javascript로 다음과 같이 간단한 선형 회귀 문제를 RMSProp으로 해결할 수 있다.

      ```javascript
      const data = [
        { x: 1, y: 2 },
        { x: 2, y: 3 },
        { x: 3, y: 4 },
        { x: 4, y: 5 },
      ];

      let weight = 0;
      let bias = 0;

      const learningRate = 0.01;
      const epochs = 100;
      const beta = 0.9;
      const epsilon = 1e-8;

      let gradSquaredWeight = 0;
      let gradSquaredBias = 0;

      function predict(x) {
        return weight * x + bias;
      }

      function loss() {
        let totalError = 0;
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          const error = predict(x) - y;
          totalError += error * error;
        }
        return totalError / data.length;
      }

      function rmsprop(x, y) {
        const error = predict(x) - y;
        const weightGradient = 2 * error * x;
        const biasGradient = 2 * error;

        gradSquaredWeight = beta * gradSquaredWeight + (1 - beta) * weightGradient * weightGradient;
        gradSquaredBias = beta * gradSquaredBias + (1 - beta) * biasGradient * biasGradient;

        weight -= (learningRate / Math.sqrt(gradSquaredWeight + epsilon)) * weightGradient;
        bias -= (learningRate / Math.sqrt(gradSquaredBias + epsilon)) * biasGradient;
      }

      for (let epoch = 0; epoch < epochs; epoch++) {
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          rmsprop(x, y);
        }
        if (epoch % 10 === 0) {
          console.log(`Epoch ${epoch}: Loss = ${loss()}`);
        }
      }

      console.log(`weight: ${weight}`);
      console.log(`bias: ${bias}`);
      ```

5. Adam

   1. 개념

      Adam(ADAptive Moment estimation)은 RMSProp과 momentum 방식을 결합한 알고리즘이다.

   2. 알고리즘

      우선 momentum처럼 지금까지 계산한 gradient와

      > $g_t=∇_xJ(x_{t-1})$

      그의 지수 평균을 저장하고,

      > $m_t=β_1m_{t-1}+(1-β_1)g_t$

      RMSProp의 제곱된 gradient의 지수 가중 이동 평균을 저장한다.

      > $m_t=β_1m_{t-1}+(1-β_1)g_t^2$

      다만 adam에서는 다음과 같이 초기화가 이루어지기 때문에

      > $m = 0$

      > $v = 0$

      학습 초반에 $m_t$와 $v_t$가 0에 가깝게 bias되어 있을 것이라고 추정하고 다음과 같이 이를 보정하는 과정을 거친다.

      > $\hat{m}_t=\frac{m_t}{1-β_1^t}$

      > $\hat{v}_t=\frac{v_t}{1-β_2^t}$

      보정 이후 gradient의 자리에 $\hat{m}_t$를, $G_t$의 자리에 $\hat{v}_t$를 넣으면 다음과 같은 최종적인 업데이트 식이 나온다.

      > $x_t=x_{t-1}-\frac{η}{\sqrt{\hat{v}_t}+ϵ}\frac{\sqrt{1-β_2^t}}{1-β_1^t}\hat{m}_t$

      여기서 $β_1$과 $β_2$는 1차, 2차 모먼트 추정치의 지수적 감쇠율이며, 보통 각각 0.9, 0.999를 취한다. 또한 $\hat{m}_t$ 앞의 항은 unbiased estimator(비편향 추정량)가 되기 위해 붙인 항이며 크게 중요하지 않다.

   3. 사용

      Javascript로 다음과 같이 간단한 선형 회귀 문제를 adam으로 해결할 수 있다.

      ```javascript
      const data = [
        { x: 1, y: 2 },
        { x: 2, y: 3 },
        { x: 3, y: 4 },
        { x: 4, y: 5 },
      ];

      let weight = 0;
      let bias = 0;

      const learningRate = 0.01;
      const epochs = 100;

      const beta1 = 0.9;
      const beta2 = 0.999;
      const epsilon = 1e-8;

      let mWeight = 0;
      let vWeight = 0;
      let mBias = 0;
      let vBias = 0;

      let t = 0;

      function predict(x) {
        return weight * x + bias;
      }

      function loss() {
        let totalError = 0;
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          const error = predict(x) - y;
          totalError += error * error;
        }
        return totalError / data.length;
      }

      function adam(x, y) {
        const error = predict(x) - y;
        const weightGradient = 2 * error * x;
        const biasGradient = 2 * error;

        t += 1;

        mWeight = beta1 * mWeight + (1 - beta1) * weightGradient;
        mBias = beta1 * mBias + (1 - beta1) * biasGradient;

        vWeight = beta2 * vWeight + (1 - beta2) * weightGradient * weightGradient;
        vBias = beta2 * vBias + (1 - beta2) * biasGradient * biasGradient;

        const mWeightHat = mWeight / (1 - Math.pow(beta1, t));
        const mBiasHat = mBias / (1 - Math.pow(beta1, t));
        const vWeightHat = vWeight / (1 - Math.pow(beta2, t));
        const vBiasHat = vBias / (1 - Math.pow(beta2, t));

        weight -= (learningRate * mWeightHat) / (Math.sqrt(vWeightHat) + epsilon);
        bias -= (learningRate * mBiasHat) / (Math.sqrt(vBiasHat) + epsilon);
      }

      for (let epoch = 0; epoch < epochs; epoch++) {
        for (let i = 0; i < data.length; i++) {
          const { x, y } = data[i];
          adam(x, y);
        }
        if (epoch % 10 === 0) {
          console.log(`Epoch ${epoch}: Loss = ${loss()}`);
        }
      }

      console.log(`weight: ${weight}`);
      console.log(`bias: ${bias}`);
      ```

---
