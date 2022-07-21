---
layout: post
title: "[9] Regularization"
date: 2022-07-21 09:00:00
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

![1](https://user-images.githubusercontent.com/90087083/180112111-bc1951b9-a188-47f8-9436-df6bc817952f.JPG){: width=”50%” height=”50%”}

Loss가 커지기 시작하는 순간부터 멈추기





## Parameter norm penalty 

$$
total cost=loss\left(\mathcal{D};W\right)+\frac{\alpha}{2}\begin{Vmatrix} W\end{Vmatrix}_2^2
$$

Nural network의 파라메터가 너무 커지지 않게 하기

$\frac{\alpha}{2}\begin{Vmatrix} W\end{Vmatrix}_2^2$: Parameter Norm Penalty





## Data augmentation 

![2](https://user-images.githubusercontent.com/90087083/180112165-4e9ed32a-ec75-4a87-8d1e-6a036757e76d.jpg){: width=”50%” height=”50%”}

데이터의 양이 많을수록 좋다. 

하지만 주어진 데이터가 한정되어 있으므로 

주어진 데이터를 지지고 볶아서 새로운 데이터를 만들어 내자





## Noise robustness 

![3](https://user-images.githubusercontent.com/90087083/180112209-3d4e0371-633f-4e37-b397-8ef3cb0f0250.png){: width=”50%” height=”50%”}

입력데이터 및 neural network에도 noise 집어넣기





## Label smoothing 

![4](https://user-images.githubusercontent.com/90087083/180112256-1890a232-3625-4845-9bde-d4e42ee98edd.png){: width=”50%” height=”50%”}

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
