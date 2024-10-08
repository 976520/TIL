## 예측이라고 쓰고 회귀라고 읽는다.

1. 개념

   예측 모델은 학습 데이터에서 확립한 모델로 계산한 임의의 값이 결과값이 된다. 가령 ‘A’, ‘B’, ‘C’라는 label을 부여한 데이터로 학습하였더라도 결과가 ‘D’가 될 수 있다. 이러한 예측 모델은 연속적인 범위 내의 값에서 그 결과값을 예측할 때 사용한다. ~~사실상 회귀 분석이 전부이다.~~

2. 회귀 분석

   > 회귀 분석은 관찰된 연속형 변수들에 대해 두 변수 사이의 모형을 구한 뒤 적합도를 측정해 내는 분석 방법이다.

   회귀 분석은 데이터들이 특정한 경향성을 띠고 있다는 아이디어로부터 비롯된다. 즉, 변수들 사이의 함수적인 관련성을 규명하기 위해 현실을 본뜬 모형을 수학적으로 가정하고, 이 모형을 측정된 변수들의 자료로부터 추정해내는 것이다. 이는 시간에 따라 변화하는 데이터나 가설, 인과관계등의 통계적 예측에 사용된다. 데이터가 시간에 따르기 때문에 출력에 연속성이 있는 경우가 보통이다.

   데이터들을 평면 위에 쭉 흩뿌려놓고 이를 잘 설명하는 linear(선형) 모델, 즉 직선 혹은 곡선을 찾기 위해 회귀를 사용하는 것이다. 회귀 분석 역시 지도학습의 일종이기에, 분석에 사용되는 데이터는 결국 입력 $x$와 label $y$의 쌍$(x, y)$으로 이루어져 있고, 새로운 임의의 입력 $x$에 대해 label $y$를 추정하는 $h(x)$를 도출한다.

   이를 요약하면, 회귀는 **주어진 입력값과 출력값의 관계**를 모델링하는 방법이다.

3. 종류

   1. 선형 회귀 (linear regression)

      선형 회귀는 제공된 $(x, y)$와 함께 여러 통계적 요소를 고려하여 직선 혹은 곡선을 만들고 그를 이용해서 종속변수를 예측해낸다. 다음은 학습 데이터에 가중치 $W$와 편향 $b$를 이용하여 간단한 직선 형태로 모델을 도출한 것이다.

      > $h(x) = Wy + b$

      이처럼 특성 $x$가 1개여서 하나의 종속변수와 하나의 독립변수 사이의 관계를 분석하는 경우를 단순(simple) 선형회귀라고 하고, 2개 이상인 경우 다중(multiple) 선형회귀라고 한다.

      ![회귀](https://github.com/user-attachments/assets/0ab06dbc-f460-4d6f-ac0f-1e2b1a2d2a01)

      이때 실제 label인 $y$와 직선 $h(x)$의 거리 $|h(x)-y|^2$가 짧을수록 잘 만들어진 모델로 간주한다. 데이터들을 잘 표현하는 직선을 찾았다는 뜻이기 때문이다. 하지만 이를 판단하기 위해서는 하나의 입력값에 대해서만 판단하는 것이 아니라 모든 경우를 고려해야 한다. 따라서 입력값의 개수가 $m$일 때, cost function(비용함수) 식은 다음과 같다.

      > $c(W,b)=\frac{\displaystyle\sum^m_{i=1}|h(x^i)-y^i|^2}{m}$

      여기서 $h(x)$는 예측 함수로, 이를 아래와 같이 표현하여

      > $h(x) = Wy + b$

      비용함수를 아래와 같이 쓸 수 있다.

      > $c(W,b)=\frac{\displaystyle\sum^m_{i=1}|Wx^i+b-y^i|^2}{m}$

      당연히 이러한 cost function은 작을수록 좋으며, $h(x)$를 $W$와 $b$에 대한 식으로 구현했기 때문에, 이 경우 cost function은 $W$, $b$에 대한 함수일 것이다. cost function을 최소화하는 $W$와 $b$를 찾는 것이 목적이다.

      경사하강법을 이용하여 최적값을 찾기 위해 이 cost function을 $W$와 $b$에 대해 미분하여 현재 $W$와 $b$에서의 접선의 gradient를 구한다. 다음 갱신식을 반복하여 cost function을 최소화하는 $W$를 찾는다.

      > $W := W-\alpha\frac{\displaystyle\sum^m_{i=1}(Wx^i+b-y^i)x^i}{m}$

      > $b := b-\alpha\frac{\displaystyle\sum^m_{i=1}(Wx^i+b-y^i)x^i}{m}$

      이로써 비용함수 $c(W, b)$가 최소가 되는 $W$ 와 $b$의 값을 산출하게 되면, 이때 얻어진 $W$ 와 $b$가 데이터에 가장 적합한 회귀 직선을 의미하게 된다.

      gradient descent를 이용하여 간단한 단일 변수 선형 회귀 분석을 C++로 구현하면 다음과 같다.

      ```cpp

         #include <iostream>
         #include <vector>
         #include <cmath>

         double predict(double x, double w, double b);
         void train(std::vector<double>& X, std::vector<double>& y, double& w, double& b, double learning_rate, int iterations);

         int main() {
            std::vector<double> X = {1.0, 2.0, 3.0, 4.0, 5.0};
            std::vector<double> y = {2.0, 3.0, 4.0, 5.0, 6.0};

            // 하이퍼파라미터 설정
            double learning_rate = 0.01;
            int iterations = 1000;

            // 초기화
            double w = 0.0;
            double b = 0.0;

            // 학습
            train(X, y, w, b, learning_rate, iterations);

            // 예측
            double test_x = 6.0;
            double predicted_y = predict(test_x, w, b);
            std::cout << "value for x = " << test_x << " is " << predicted_y << std::endl;

            return 0;
         }

         double predict(double x, double w, double b) {
            return w * x + b;
         }

         void train(std::vector<double>& X, std::vector<double>& y, double& w,double& b, double learning_rate, int iterations) {
            int n = X.size();

            for (int i = 0; i < iterations; ++i) {
               double w_grad = 0.0;
               double b_grad = 0.0;

               for (int j = 0; j < n; ++j) {
                     double prediction = predict(X[j], w, b);
                     double error = prediction - y[j];

                     w_grad += error * X[j];
                     b_grad += error;
               }

               w_grad = w_grad / n;
               b_grad = b_grad / n;

               w -= learning_rate * w_grad;
               b -= learning_rate * b_grad;
            }
         }


      ```

   2. 로지스틱 회귀 (logistic regression)

      종속변수가 범주형 데이터일 때 로지스틱 회귀를 사용한다. 알고리즘 자체는 회귀를 따르지만 분류에 사용된다.

      로지스틱 회귀는 독립변수의 선형 조합을 sigmoid 함수를 이용하여 종속변수에 대한 확률 점수로 변환한다. Sigmoid 함수는 입력값을 0과 1 사이의 값으로 매핑하며, 이는 종속변수가 1의 값을 취할 확률로 해석할 수 있다. 또한 로지스틱 회귀 모델은 독립변수의 계수, 즉 기울기를 추정한다. 이 계수는 해당 독립변수의 한 단위 변화에 대한 종속 변수의 log odds 변화를 나타내며, 다른 모든 변수를 일정하게 유지하는 동안 적용된다.

      로지스틱 회귀는 이진 분류 문제에서 주로 사용되며, 주어진 독립변수 집합을 기반으로 특정 클래스에 속할 확률을 예측하는 데 유용하다. 모델의 계수는 최대 우도 추정법(MLE)을 통해 추정되며, 이는 관측된 데이터를 기반으로 가장 높은 확률을 가지는 계수를 찾아내는 방법이다. 로지스틱 회귀의 손실 함수로는 로그 손실(log loss)이 사용되며, 이는 예측 확률과 실제 결과 간의 차이를 측정하여 모델의 성능을 평가하는 데 도움을 준다.

      또한, 로지스틱 회귀는 다중 클래스 문제에 대한 확장이 가능하다. 종속변수가 3개 이상의 범주형 데이터일 때 다항(multinomial) 로지스틱 회귀를 통해 여러 클래스에 대한 확률을 동시에 예측할 수 있다. 각 계수는 독립변수가 1 단위 증가할 때 종속변수가 1일 확률의 log odds 변화량을 나타내며, 이러한 계수의 지수값은 해당 독립변수의 변화가 odds에 미치는 영향을 나타낸다.

      ```cpp
         #include <iostream>
         #include <vector>
         #include <cmath>

         double sigmoid(double z);
         double predict(double x, double w, double b);
         void train(std::vector<double>& X, std::vector<double>& y, double& w, double& b, double learning_rate, int iterations);

         int main() {
            // 학습 데이터
            std::vector<double> X = {1.0, 2.0, 3.0, 4.0, 5.0};
            std::vector<double> y = {0.0, 0.0, 0.0, 1.0, 1.0}; // 이진 분류 문제

            // 하이퍼파라미터
            double learning_rate = 0.01;
            int iterations = 1000;

            // 초기화
            double w = 0.0;
            double b = 0.0;

            // 학습
            train(X, y, w, b, learning_rate, iterations);

            // 예측
            double test_x = 3.5;
            double predicted_y = predict(test_x, w, b);
            std::cout << "probability for x = " << test_x << " is " << predicted_y << std::endl;
            std::cout << "class for x = " << test_x << " is " << (predicted_y >= 0.5 ? 1 : 0) << std::endl;

            return 0;
         }

         double sigmoid(double z) {
            return 1.0 / (1.0 + std::exp(-z));
         }

         double predict(double x, double w, double b) {
            return sigmoid(w * x + b);
         }

         void train(std::vector<double>& X, std::vector<double>& y, double& w, double& b, double learning_rate, int iterations) {
            int n = X.size();

            for (int i = 0; i < iterations; ++i) {
               double w_grad = 0.0;
               double b_grad = 0.0;

               for (int j = 0; j < n; ++j) {
                     double prediction = predict(X[j], w, b);
                     double error = prediction - y[j];

                     w_grad += error * X[j];
                     b_grad += error;
               }

               w_grad = w_grad / n;
               b_grad = b_grad / n;

               w -= learning_rate * w_grad;
               b -= learning_rate * b_grad;
            }
         }

      ```

---
