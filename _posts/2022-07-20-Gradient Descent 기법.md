---

layout: post
title: "[8] Gradient Descent 방법들"
use_math: true

---

## Gradient Descent 방법들

- Stochastic gradient descent (SGD)
  - 하나의 샘플을 통해 gradient 구한 후 업데이트
- Mini-batch gradient descent 
  - 전체 데이터 중 일부를 통해 gradient 구한 후 업데이트
- Batch gradient descent 
  - 한번에 모든 데이터를 다 써서 gradient 업데이트



	batch: 하나의 그룹에 속해진 데이터의 양



## Batch-size 문제들

- 큰 batch size를 활용하게 되면 Sharp Minimizer에 도달함
- 작은 batch size를 활용하게 되면 Flat Minimizer에 도달함

![gd-1](https://user-images.githubusercontent.com/90087083/179951231-b3d4a8a7-5c9c-4790-852b-a971f1f54bd8.jpg){: width=”50%” height=”50%”}


- Flat Minimum: generalization performance 높다
- Sharp Minimum: generalization performance 낮다





## Gradient Descent Methods

- Stochastic Gradient Descent 
- Momentum
- Nesterov Accelerated Gradient 
- Adagrad 
- Adadelta 
- RMSprop 
- Adam



## (Stochastic) Gradient Descent

$$
W_{t+1}\leftarrow W_t-\eta g_t
$$

$\eta$: Learning rate(너무 크거나 작으면 안된다)

$g_t$: Gradient



## Momentum

$$
a_{t+1}\leftarrow \beta a_t+g_t\\
W_{t+1}\leftarrow W_t-\eta a_{t+1}
$$

$\beta$: Momentum

$a_{t+1}$: accumulation

한번 gradient가 흐른 방향대로 정보를 좀 더 이어감



## Nesterov Accelerated Gradient 

$$
a_{t+1}\leftarrow \beta a_t+\nabla\mathcal{L}\left( W_t-\eta\beta a_t \right)\\
W_{t+1}\leftarrow W_t-\eta a_{t+1}
$$

$\nabla\mathcal{L}\left( W_t-\eta\beta a_t \right)$: Lookahead gradient

a라는 현재 정보가 있으면 그 방향으로 한번 가본 후 거기서 gradient를 계산한 후 accumulation 함



## Adagrad 

$$
W_{t+1}\leftarrow W_t-\frac{\eta}{\sqrt{G_t+\epsilon}}g_t
$$

$G_t$: gradient들을 제곱 후 더한 것. $G_t$가 커질수록 학습이 멈춰짐

$\epsilon$: 0으로 안나눠지기 위한 것

많이 변한 파라메터들에 대해서는 적게 변화시키고 적게 변한 파라메터들에 대해서는 많이 변화시키기 위한 것



## Adadelta 

$$
G_t=\gamma G_{t-1}+\left(1-\gamma\right)g_t^2\\
W_{t+1}=W_t-\frac{\sqrt{H_{t-1}+\epsilon}}{\sqrt{G_t+\epsilon}}g_t\\
H_t=\gamma H_{t-1}+\left(1-\gamma\right)\left(\Delta W_t\right)^2
$$

$G_t$: Exponential Moving Average of gradient squares

$H_t$: EMA of difference squares

Adagrad에서 $G_t$가 무한히 커졌을 때 생기는 문제를 해결하기 위한 것 



## RMSprop 

$$
G_t=\gamma G_{t-1}+\left(1-\gamma\right)g_t^2\\
W_{t+1}=W_t-\frac{\eta}{\sqrt{G_t+\epsilon}}g_t
$$

$G_t$: EMA of gradient squares

$\eta$: stepsize

Geoffrey Hinton교수가 그냥 해봤더니 잘되더라 라고 해서 나온 방법



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

