# 하이퍼볼릭탄젠트

1. 개념

   Tanh는 sigmoid의 한계를 보완하고 크기와 위치를 조정한 함수이다. 데이터의 -1과 1 사이의 비선형 형태 변환을 위해 사용한다.

2. 특징

   Sigmoid보다 범위가 무려 2배 크기 때문에 출력값의 진폭이 크고 gradient vanishing(기울기 소실) 현상이 적...지만 완벽하게 일어나지 않는다는 보장은 없다. 따라서 hidden layer에서의 사용은 여전히 조심해야 한다.

3. 사용

   Sigmoid와 유사하게 사용된다. ~~여러모로 애매한 녀석.~~