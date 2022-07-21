---
layout: post
title: "[9] Regularization"
date: 2022-07-21 10:40:00
use_math: true
---

# Regularization

## Regularization

학습 데이터 뿐만 아니라 테스트 데이터에서도 잘 동작할 수 있도록 만들어 주는 것





## Regularization 방법들

- Early stopping 
- Parameter norm penalty 
- Data augmentation 
- Noise robustness 
- Label smoothing 
- Dropout 
- Batch normalization





## Early stopping 

![1](C:\Users\서장원\Desktop\1.JPG)

Loss가 커지기 시작하는 순간부터 멈추기





## Parameter norm penalty 

$$
total cost=loss\left(\mathcal{D};W\right)+\frac{\alpha}{2}\begin{Vmatrix} W\end{Vmatrix}_2^2
$$

Nural network의 파라메터가 너무 커지지 않게 하기

$\frac{\alpha}{2}\begin{Vmatrix} W\end{Vmatrix}_2^2$: Parameter Norm Penalty





## Data augmentation 

![2](C:\Users\서장원\Desktop\2.jpg)

데이터의 양이 많을수록 좋다. 

하지만 주어진 데이터가 한정되어 있으므로 

주어진 데이터를 지지고 볶아서 새로운 데이터를 만들어 내자





## Noise robustness 

![3](C:\Users\서장원\Desktop\3.png)

입력데이터 및 neural network에도 noise 집어넣기





## Label smoothing 

![4](C:\Users\서장원\Desktop\4.png)

학습 데이터 두개를 뽑아서 섞어주기

이미지들의 decision 바운더리를 부드럽게 만들어주는 역할



- Mixup: 두개의 이미지를 고른다음 섞음
- Cutout: 이미지에서 일정 영역을 빼버림
- CutMix: 이미지의 일정 영역을 섞음





## Dropout 

일부 뉴런들을 랜덤하게 0으로 설정하기





## Batch normalization

Batch normalization을 적용하려는 층의  활성화함수의 입력값 또는 출력값을 정규화 시키기
$$
\mu_B=\frac{1}{m}\sum_{i=1}^m x_i\\
\sigma^2_B=\frac{1}{m}\sum_{i=1}^m \left(x_i-\mu_B\right)^2\\
\widehat{x}_i=\frac{x_i-\mu_B}{\sqrt{\sigma^2_B+\epsilon}}
$$
