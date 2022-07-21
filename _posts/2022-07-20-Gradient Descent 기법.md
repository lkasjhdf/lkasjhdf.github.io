---

layout: post
title: "[8] Gradient Descent 방법들, Regularization"
date: 2022-07-20 12:00:00
use_math: true

---

# Gradient Descent
## Gradient Descent 방법들

- Stochastic gradient descent (SGD)
  - 하나의 샘플을 통해 gradient 구한 후 업데이트
- Mini-batch gradient descent 
  - 전체 데이터 중 일부를 통해 gradient 구한 후 업데이트
- Batch gradient descent 
  - 한번에 모든 데이터를 다 써서 gradient 업데이트



batch: 하나의 그룹에 속해진 데이터의 양
<br/>
<br/>
<br/>
<br/>
<br/>
## Batch-size 문제들

- 큰 batch size를 활용하게 되면 Sharp Minimizer에 도달함
- 작은 batch size를 활용하게 되면 Flat Minimizer에 도달함

![gd-1](https://user-images.githubusercontent.com/90087083/179951231-b3d4a8a7-5c9c-4790-852b-a971f1f54bd8.jpg){: width=”50%” height=”50%”}


- Flat Minimum: generalization performance 높다
- Sharp Minimum: generalization performance 낮다
<br/>
<br/>
<br/>
<br/>
<br/>
## Gradient Descent Methods

- Stochastic Gradient Descent 
- Momentum
- Nesterov Accelerated Gradient 
- Adagrad 
- Adadelta 
- RMSprop 
- Adam
<br/>
<br/>
<br/>
<br/>
<br/>
## (Stochastic) Gradient Descent

$$
W_{t+1}\leftarrow W_t-\eta g_t
$$

$\eta$: Learning rate(너무 크거나 작으면 안된다)

$g_t$: Gradient
<br/>
<br/>
<br/>
<br/>
<br/>
## Momentum

$$
a_{t+1}\leftarrow \beta a_t+g_t\\
W_{t+1}\leftarrow W_t-\eta a_{t+1}
$$

$\beta$: Momentum

$a_{t+1}$: accumulation

한번 gradient가 흐른 방향대로 정보를 좀 더 이어감
<br/>
<br/>
<br/>
<br/>
<br/>
## Nesterov Accelerated Gradient 

$$
a_{t+1}\leftarrow \beta a_t+\nabla\mathcal{L}\left( W_t-\eta\beta a_t \right)\\
W_{t+1}\leftarrow W_t-\eta a_{t+1}
$$

$\nabla\mathcal{L}\left( W_t-\eta\beta a_t \right)$: Lookahead gradient

a라는 현재 정보가 있으면 그 방향으로 한번 가본 후 거기서 gradient를 계산한 후 accumulation 함
<br/>
<br/>
<br/>
<br/>
<br/>
## Adagrad 

$$
W_{t+1}\leftarrow W_t-\frac{\eta}{\sqrt{G_t+\epsilon}}g_t
$$

$G_t$: gradient들을 제곱 후 더한 것. $G_t$가 커질수록 학습이 멈춰짐

$\epsilon$: 0으로 안나눠지기 위한 것

많이 변한 파라메터들에 대해서는 적게 변화시키고 적게 변한 파라메터들에 대해서는 많이 변화시키기 위한 것
<br/>
<br/>
<br/>
<br/>
<br/>
## Adadelta 

$$
G_t=\gamma G_{t-1}+\left(1-\gamma\right)g_t^2\\
W_{t+1}=W_t-\frac{\sqrt{H_{t-1}+\epsilon}}{\sqrt{G_t+\epsilon}}g_t\\
H_t=\gamma H_{t-1}+\left(1-\gamma\right)\left(\Delta W_t\right)^2
$$

$G_t$: Exponential Moving Average of gradient squares

$H_t$: EMA of difference squares

Adagrad에서 $G_t$가 무한히 커졌을 때 생기는 문제를 해결하기 위한 것 
<br/>
<br/>
<br/>
<br/>
<br/>
## RMSprop 

$$
G_t=\gamma G_{t-1}+\left(1-\gamma\right)g_t^2\\
W_{t+1}=W_t-\frac{\eta}{\sqrt{G_t+\epsilon}}g_t
$$

$G_t$: EMA of gradient squares

$\eta$: stepsize

Geoffrey Hinton교수가 그냥 해봤더니 잘되더라 라고 해서 나온 방법
<br/>
<br/>
<br/>
<br/>
<br/>
## Adam

$$
m_t=\beta_1m_{t=1}+\left(1-\beta_1\right)g_t\\
v_t=\beta_2v_{t-1}+\left(1-\beta_2\right)g_t^2\\
W_{t+1}=W_{t}-\frac{\eta}{\sqrt{v_t+\epsilon}}\frac{\sqrt{1-\beta_2^t}}{1-\beta_1^t}m_t
$$

$m_t$: momentum

$v_t$: EMA of gradient squares

$\eta$: stepsize

Adam: Adaptive Moment Estimation.

 gradient의 제곱을 EMA로 가져감과 동시에 momentum을 동시에 활용
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# Regularization

## Regularization

학습 데이터 뿐만 아니라 테스트 데이터에서도 잘 동작할 수 있도록 만들어 주는 것
<br/>
<br/>
<br/>
<br/>
<br/>
## Regularization 방법들

- Early stopping 
- Parameter norm penalty 
- Data augmentation 
- Noise robustness 
- Label smoothing 
- Dropout 
- Batch normalization
<br/>
<br/>
<br/>
<br/>
<br/>
## Early stopping 

![1](https://user-images.githubusercontent.com/90087083/180112111-bc1951b9-a188-47f8-9436-df6bc817952f.JPG){: width=”50%” height=”50%”}

Loss가 커지기 시작하는 순간부터 멈추기
<br/>
<br/>
<br/>
<br/>
<br/>
## Parameter norm penalty 

$$
total cost=loss\left(\mathcal{D};W\right)+\frac{\alpha}{2}\begin{Vmatrix} W\end{Vmatrix}_2^2
$$

Nural network의 파라메터가 너무 커지지 않게 하기

$\frac{\alpha}{2}\begin{Vmatrix} W\end{Vmatrix}_2^2$: Parameter Norm Penalty
<br/>
<br/>
<br/>
<br/>
<br/>
## Data augmentation 

![2](https://user-images.githubusercontent.com/90087083/180112165-4e9ed32a-ec75-4a87-8d1e-6a036757e76d.jpg){: width=”50%” height=”50%”}

데이터의 양이 많을수록 좋다. 

하지만 주어진 데이터가 한정되어 있으므로 

주어진 데이터를 지지고 볶아서 새로운 데이터를 만들어 내자
<br/>
<br/>
<br/>
<br/>
<br/>
## Noise robustness 

![3](https://user-images.githubusercontent.com/90087083/180112209-3d4e0371-633f-4e37-b397-8ef3cb0f0250.png){: width=”50%” height=”50%”}

입력데이터 및 neural network에도 noise 집어넣기
<br/>
<br/>
<br/>
<br/>
<br/>
## Label smoothing 

![4](https://user-images.githubusercontent.com/90087083/180112256-1890a232-3625-4845-9bde-d4e42ee98edd.png){: width=”50%” height=”50%”}

학습 데이터 두개를 뽑아서 섞어주기

이미지들의 decision 바운더리를 부드럽게 만들어주는 역할



- Mixup: 두개의 이미지를 고른다음 섞음
- Cutout: 이미지에서 일정 영역을 빼버림
- CutMix: 이미지의 일정 영역을 섞음
<br/>
<br/>
<br/>
<br/>
<br/>
## Dropout 

일부 뉴런들을 랜덤하게 0으로 설정하기
<br/>
<br/>
<br/>
<br/>
<br/>
## Batch normalization

Batch normalization을 적용하려는 층의  활성화함수의 입력값 또는 출력값을 정규화 시키기
$$
\mu_B=\frac{1}{m}\sum_{i=1}^m x_i\\
\sigma^2_B=\frac{1}{m}\sum_{i=1}^m \left(x_i-\mu_B\right)^2\\
\widehat{x}_i=\frac{x_i-\mu_B}{\sqrt{\sigma^2_B+\epsilon}}
$$
