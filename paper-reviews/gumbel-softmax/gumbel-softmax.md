# Abstract
* 확률적 NN들은 Categorical 잠재 변수들을 역전파가 불가능하기 때문에 잘 사용하지 않음
* 본 논문에서는 새로운 Gumbel softmax 분포로 부터의 sample을 사용해 효율적인 gradient estimator을 선보임

# Introduction
* Stochastic NN + 이산 random variables = powerful BUT, 역전파 알고리즘 때문에 train이 불편 ->미분 불가 layers 때문
1. Gumbel softmax는 연속분포로서 범주형 변수를 근사해줌 (reparameterization trick 사용해서 파라미터 쉽게 찾음)
  * Categorical variables는 Nominal(명목형) ex. 성별 Ordinal(순서형) ex. 교육수준(초졸=1,...대졸 이상=4)를 모두 포함.
2. 베르누이 변수 & 범주형 변수 모두 사용해서 실험
3. Semi-supervised models train 하는데도 효과적이라는 것을 보임

# The Gumbel-Softmax Distribution   
* 참고자 [AI 공부 3. 쉽게 배우는 Gumbel-Softmax](https://www.youtube.com/watch?v=SRcPE0-SGOM)
* 하고 싶은 것 : discrete distribution에서 뽑고 싶다. 샘플링을 differentiable(미분가능) 하게 하고 싶다. (네트워크에서 loss로 쓰이던지 하려고)   
    -> 출력 + Gumbel 가장 높은 애를 One-hot으로 지정해서 나오도록 하게 하고 싶다.
* Let z be a categorical variable with class probabilities π1, π2, ...πk. For the remainder of this paper we assume categorical samples are encoded as k-dimensional one-hot vectors lying on the corners of the (k − 1)-dimensional simplex, ∆k−1. This allows us to define quantities such as the element-wise mean Ep[z] = [π1, ..., πk] of these vectors.
* The Gumbel Max trick   
  * ![gumbel-distribution](https://upload.wikimedia.org/wikipedia/commons/thumb/3/32/Gumbel-Density.svg/1200px-Gumbel-Density.svg.png)
* softmax temperature = annealing
