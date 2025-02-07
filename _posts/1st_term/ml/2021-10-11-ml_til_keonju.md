---
layout: post
title: 5주차 ML WIL
data: 2021-10-10 23:00:00 +0900
author: keonju2
categories: ["1st_term"]
tags: ["ml"]
---

# 비지도 학습의 종류

책에서는 두 가지 비지도 학습을 공부합니다.  
비지도 변환과 군집입니다.  
비지도 변환은 데이터를 새롭게 표현하여 사람이나 다른 머신러닝 알고리즘이 원래 데이터보다 쉽게 해석할 수 있도록 만드는 알고리즘입니다.  
특히 고차원 데이터를 특성의 수를 줄이면서 꼭 필요한 특징을 포함한 데이터로 표현하는 방법인 차원축소가 대표적인 예입니다.  

비지도 변환으로 데이터를 구성하는 단위나 성분을 찾기도 합니다.  
텍스트 문서에서 주제를 추출하는 것이 예입니다.  
소셜 미디어에서 선거, 총기 규제, 팝스타 같은 주제로 일어나는 토론을 추적할 때 사용한다고 합니다.  

군집 알고리즘은 데이터를 서로 비슷하게 그룹으로 묶는 것 입니다.  
같은 사람이 찍힌 사진을 같은 그룹으로 묶게 추천해주는 것을 생각하면 이해하기 쉽습니다.  


# 비지도 학습의 도전과제  

비지도 학습에서 가장 어려운 일은 알고리즘이 유용한 가를 평가하는 것 입니다.  
비지도 학습은 보통 레이블이 없어서 어떤 것이 올바른 것인지 모릅니다.  
그래서 비지도 학습의 결과를 평가하기 위해서는 직접 확인하는 것이 유일한 방법일 때도 있다고 합니다.  

비지도 학습 알고리즘은 데이터를 잘 이해하고 싶을 때 탐색적 분석 단계에서도 많이 사용합니다.  
전처리 단계에서도 사용되는데 비지도 학습 결과를 사용하여 학습하면 지도 학습의 정확도가 좋아지기도 하고 메모리나 시간 절약도 할 수 있습니다.  


# 데이터 전처리와 스케일 조정

신경망이나 SVM과 같은 스케일에 민감한 알고리즘은 데이터 특성 값을 조정해야합니다.  


## 여러 가지 전처리 방법

#### StandardSclaer

각 특성의 평균을 0, 분산을 1로 변경하여 모든 특성이 같은 크기를 가지게 합니다.  
특성의 최솟값과 최댓값의 크기를 제한하지는 않습니다.  

$$ z= \frac {x−μ} σ ( z점수= \frac{자료값-평균} {표준편차}) $$


#### RobustScaler

특성이 같은 스케일을 갖게되지만 평균과 분산 대신 중간 값과 사분위 값을 사용합니다.  
따라서 이상치에 영향을 받지 않습니다.  


#### MinMaxScaler

모든 특성이 정확하게 0과 1 사이에 위치하도록 변경합니다.  
2차원 데이터셋일 경우에는 모든 데이터가 x 축의 0과 1, y축의 0과 1 사이의 사각 영역에 담기게 됩니다.  
(q는 각 사분위값을 뜻합니다.)

$$ \frac {x-q~2} {q~3-q~1} $$


#### Nomarlizer

특성 벡터의 유클리디안 길이가 1이 되도록 데이터 포인트를 조정합니다.  
다른 말로 하면 지름이 1인 원(3차원에서는 구)에 들어옵니다.  
각 데이터 포인트가 다른 비율로 조정됩니다.  특성 벡터의 길이는 상관 없고 데이터의 방향이 중요할 때 많이 사용합니다.  


## 데이터 변환 적용하기

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

scaler.fit(X_train)

X_train_scaled = scaler.transform(X_train)

print("변환된 후 크기:", X_train_scaled.shape)
print("스케일 조정 전 특성별 최소값:\n", X_train.min(axis=0))
print("스케일 조정 전 특성별 최대값:\n", X_train.max(axis=0))
print("스케일 조정 후 특성별 최소값:\n", X_train_scaled.min(axis=0))
print("스케일 조정 후 특성별 최대값:\n", X_train_scaled.max(axis=0))
```
    변환된 후 크기: (426, 30)
    스케일 조정 전 특성별 최소값:
    [  6.981   9.71   43.79  143.5     0.053   0.019   0.      0.      0.106
    0.05    0.115   0.36    0.757   6.802   0.002   0.002   0.      0.
    0.01    0.001   7.93   12.02   50.41  185.2     0.071   0.027   0.
    0.      0.157   0.055]
    스케일 조정 전 특성별 최대값:
    [  28.11    39.28   188.5   2501.       0.163    0.287    0.427    0.201
        0.304    0.096    2.873    4.885   21.98   542.2      0.031    0.135
        0.396    0.053    0.061    0.03    36.04    49.54   251.2   4254.
        0.223    0.938    1.17     0.291    0.577    0.149]
    스케일 조정 후 특성별 최소값:
    [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
    0. 0. 0. 0. 0. 0.]
    스케일 조정 후 특성별 최대값:
    [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
    1. 1. 1. 1. 1. 1.]

변환 된 값들이 모두 0과 1 사이가 된 것을 알 수 있습니다.  

```python

X_test_scaled = scaler.transform(X_test)

print("스케일 조정 후 특성별 최소값:\n", X_test_scaled.min(axis=0))
print("스케일 조정 후 특성별 최대값:\n", X_test_scaled.max(axis=0))
```

    스케일 조정 후 특성별 최소값:
    [ 0.034  0.023  0.031  0.011  0.141  0.044  0.     0.     0.154 -0.006
    -0.001  0.006  0.004  0.001  0.039  0.011  0.     0.    -0.032  0.007
    0.027  0.058  0.02   0.009  0.109  0.026  0.     0.    -0.    -0.002]
    스케일 조정 후 특성별 최대값:
    [0.958 0.815 0.956 0.894 0.811 1.22  0.88  0.933 0.932 1.037 0.427 0.498
    0.441 0.284 0.487 0.739 0.767 0.629 1.337 0.391 0.896 0.793 0.849 0.745
    0.915 1.132 1.07  0.924 1.205 1.631]


테스트 세트의 최솟값과 최댓값은 0과 1이 아닐 수 있다.  
테스트 세트의 최솟값과 범위를 사용하지 않고 훈련 세트의 최솟값을 빼고 훈련 세트의 범위로 나누기 때문이다.  
MinMaxScaler을 사용하려면 항상 테스트와 훈련 세트 모두 같은 변환을 해야한다.  


## Quantile Transformer 와 Power Transformer

#### Quantile Transformer
Quantile Transformer은 1000개의 분위를 사용하여 데이터를 균등하게 분포시킵니다.  
RobustScaler과 비슷하게 이상치에 민감하지 않으며 전체 데이터를 0과 1 사이로 압축합니다.  

분위 수는 n_quantiles 매개 변수로 설정할 수 있으며 속성의 크기는 (n_quantiles,n_features) 입니다.  

output_distribution 매개변수를 통해 균등 분포에서 정규 분포로 출력을 바꿀 수도 있습니다.  

#### Power Transformer

Power Transformer는 method 매개변수에 'yeo-johnson'과 'box-cox' 알고리즘을 지정할 수 있습니다.  
어떤 변환이 정규 분포에 가깝게 변환할지 사전에 알기 힘들기 때문에 히스토그램으로 확인해보는 것이 좋습니다.  


## 훈련 데이터와 테스트 데이터의 스케일을 같은 방법으로 조정하기

지도 학습에서는 훈련 세트와 테스트 세트에 같은 변환을 적용하는 것이 중요합니다.  
잘 조정된 데이터는 같은 비율로 데이터를 바꿔 원본 데이터와 비율만 다른 그래프를 보여주지만 잘못 조정된 데이터는 배열이 엉망이 되어서 결과에 영향을 미칩니다.  


## 지도 학습에서 데이터 전처리 효과

```python
from sklearn.svm import SVC

X_train, X_test, y_train, y_test = train_test_split(cancer.data, cancer.target, random_state=0)

svm = SVC(gamma='auto')

svm.fit(X_train, y_train)
print("테스트 세트 정확도: {:.2f}".format(svm.score(X_test, y_test)))
```

    테스트 세트 정확도: 0.63

```python
# 0~1 사이로 스케일 조정
scaler = MinMaxScaler()
scaler.fit(X_train)
X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)

svm.fit(X_train_scaled, y_train)

print("스케일 조정된 테스트 세트의 정확도: {:.2f}".format(svm.score(X_test_scaled, y_test)))
```

    스케일 조정된 테스트 세트의 정확도: 0.95

```python
# 평균 0, 분산 1을 갖도록 스케일 조정
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
scaler.fit(X_train)
X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)

svm.fit(X_train_scaled, y_train)

print("SVM 테스트 정확도: {:.2f}".format(svm.score(X_test_scaled, y_test)))
```
    SVM 테스트 정확도: 0.97


# 차원 축소, 특성 추출, 매니폴드 학습

주성분 분석은 가장 많이 사용되는 데이터 변환 방법입니다.  
특성 추출에서는 비음수 행렬 분해가 많이 사용됩니다.  
2차원 산점도를 이용한 시각화 용도로 사용되는 t-SNE 알고리즘도 있습니다.  

## 주성분 분석(PCA)

주성분 분석은 특성들이 통계적으로 상관관계가 없도록 데이터셋을 회전시키는 기술입니다.  
회전한 뒤에 데이터를 설명하는 데 중요한 새로운 특성 중 일부만 선택합니다.  

![pca](https://user-images.githubusercontent.com/54880474/136796988-27ef69fd-7e90-4787-8fda-40e0cda1779b.png)

주성분 찾기
1. 분산이 가장 큰 가장 많은 정보를 가지고 있는 방향을 찾는다.
2. 첫 번째 방향과 직각인 방향 중에서 가장 많은 정보를 가지고 있는 방향을 찾는다.  

두 번째 그래프는 주성분 1과 2를 x 축과 y 축에 나란히 회전한 것으로 변환된 데이터의 상관관계 행렬이 대각선 방향을 제외하고 0이 됩니다.  

세 번째 그래프는 차원 축소 용도로 사용될 수 있습니다.  첫 번째 주성분만 유지하므로 2차원 데이터 셋이 1차원 데이터 셋으로 차원 감소 합니다.  
단순히 원본 특성 중 하나만 남기는 것이 아닌 가장 유용한 방향을 찾아 그 성분을 유지하는 것입니다.  

마지막 그래프는 데이터에 다시 평균을 더하고 반대로 회전시킨 그래프 입니다.  
원래 특성 공간에 있지만 첫 번째 주성분의 정보만 가지고 있습니다.  
보통 노이즈 제거나 주성분에서 유지되는 정보의 시각화를 위해 사용됩니다.  

##### 유방암 데이터 셋 시각화

유방암 데이터는 특성이 30개를 가지고 있기 때문에 너무 많은 산점도를 요구합니다.  
따라서 히스토그램을 그리는 방법이 있지만 히스토그램은 특성 간의 상호작용이나 클래스와의 곤계를 알려주지 못합니다.  
따라서 PCA를 통해 데이터를 회전시키고 차원을 축소합니다.  

![pca2](https://user-images.githubusercontent.com/54880474/136798175-2b4dfcfe-1462-4712-9df0-513074f7ad3a.png)

그러면 다음과 같이 2차원 공간에서도 잘 구분됩니다.  
분류를 할 때 좋은 결과를 얻을 수 있을 것 같은 그래프입니다.  
하지만 두 축을 해석하기 어렵다는 단점을 가지고 있습니다.  
따라서 pca.components_를 통해서 중요도를 확인할 수 있습니다.  

##### 고유얼굴 특성 추출

PCA는 특성 추출에도 이용됩니다.  
RGB 강도로 기록된 픽셀들을 분류하는데 유용합니다.  
픽셀을 사용해서 두 이미지를 비교할 때, 각 픽셀의 회색톤 값을 다른 이미지에서 동일한 위치에 있는 픽셀 값과 비교합니다.  

하지만 이는 사람이 얼굴을 인식하는 것과 많이 다르고 특징을 잡기 어렵습니다.  
따라서 주성분으로 변환하여 거리를 계산하면 정확도가 높아집니다.  
PCA의 화이트닝 옵션을 사용하면 주성분의 스케일이 같습니다.  
화이트닝 옵션은 StandardScaler과 동일한 방식입니다.  

PCA 모델은 픽셀을 기반으로 하므로 얼굴의 배치와 조명이 비슷한 이미지를 판단하는 데 큰 영향을 줍니다.  
따라서 테스트 포인트를 주성분의 가중치 합으로 나타내는 것에 PCA 변환을 사용하는 방법도 해석 중 한 가지 방법입니다.  

원본 데이터를 재구성하는 방법도 PCA 모델의 해석 방법 중 한가지입니다.  

# 느낀점과 어려운점

지도 학습과 달리 비지도 학습은 데이터 전처리 방법도 많고 데이터 전처리에 사용될 수도 있다고 합니다.  
그래서 좀 더 많은 경험이 쌓여야 익숙해질 것 같고 결과물을 낼 때도 많은 시도가 필요할 것 같습니다.  