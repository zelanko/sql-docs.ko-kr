---
title: 'Python 자습서: 모델 학습 (선형 회귀)'
description: 이 자습서에서는 SQL Server Machine Learning Services에서 Python 및 선형 회귀를 사용 하 여 ski 대 여의 수를 예측 합니다. Python에서 선형 회귀 모델을 학습 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 30f390681dc63d6de9a95e805b6cc8f273b2b8d7
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242551"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 자습서: SQL Server Machine Learning Services에서 선형 회귀 모델 학습
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

네 부분으로 구성 된 자습서 시리즈의 3 부에서는 Python에서 선형 회귀 모델을 학습 합니다. 이 시리즈의 다음 부분에서는 Machine Learning Services를 사용 하 여 SQL Server 데이터베이스에이 모델을 배포 합니다.

이 문서에서는 다음 방법을 설명합니다.

> [!div class="checklist"]
> * 선형 회귀 모델 학습
> * 선형 회귀 모델을 사용 하 여 예측 만들기

[1 부](python-ski-rental-linear-regression.md)에서는 샘플 데이터베이스를 복원 하는 방법을 배웠습니다.

[2 부](python-ski-rental-linear-regression-prepare-data.md)에서는 SQL Server에서 python 데이터 프레임으로 데이터를 로드 하 고 python에서 데이터를 준비 하는 방법을 배웠습니다.

[4 부](python-ski-rental-linear-regression-deploy-model.md)에서는 SQL Server에 모델을 저장 한 다음 2 단계와 3 부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법에 대해 알아봅니다. 저장 프로시저는 새 데이터를 기반으로 예측을 수행 하기 위해 SQL Server에서 실행 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 3 부에서는 [1 부](python-ski-rental-linear-regression.md) 및 해당 필수 구성 요소를 완료 했다고 가정 합니다.

## <a name="train-the-model"></a>모델 학습

예측 하려면 데이터 집합의 변수 간 종속성을 가장 잘 설명 하는 함수 (모델)를 찾아야 합니다. 이를 모델 학습 이라고 합니다. 학습 데이터 집합은이 시리즈의 2 부에서 만든 pandas data 프레임 **df** 에서 전체 데이터 집합의 하위 집합입니다.

선형 회귀 알고리즘을 사용 하 여 모델 **lin_model** 를 학습 합니다.

```python
# Store the variable we'll be predicting on.
target = "RentalCount"

# Generate the training set.  Set random_state to be able to replicate results.
train = df.sample(frac=0.8, random_state=1)

# Select anything not in the training set and put it in the testing set.
test = df.loc[~df.index.isin(train.index)]

# Print the shapes of both sets.
print("Training set shape:", train.shape)
print("Testing set shape:", test.shape)

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(train[columns], train[target])
```

다음과 유사한 결과가 표시 됩니다.

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>예측 만들기

Predict 함수를 사용 하 여 **lin_model**모델을 사용 하 여 임대 수를 예측 합니다.

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

```results
Predictions: [  40.   38.  240.   39.  514.   48.  297.   25.  507.   24.   30.   54.
   40.   26.   30.   34.   42.  390.  336.   37.   22.   35.   55.  350.
  252.  370.  499.   48.   37.  494.   46.   25.  312.  390.   35.   35.
  421.   39.  176.   21.   33.  452.   34.   28.   37.  260.   49.  577.
  312.   24.   24.  390.   34.   64.   26.   32.   33.  358.  348.   25.
   35.   48.   39.   44.   58.   24.  350.  651.   38.  468.   26.   42.
  310.  709.  155.   26.  648.  617.   26.  846.  729.   44.  432.   25.
   39.   28.  325.   46.   36.   50.   63.]
Computed error: 3.59831533436e-26
```

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 3 부에서는 다음 단계를 완료 했습니다.

* 선형 회귀 모델 학습
* 선형 회귀 모델을 사용 하 여 예측 만들기

만든 machine learning 모델을 배포 하려면이 자습서 시리즈의 4 부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: Machine learning 모델 배포](python-ski-rental-linear-regression-deploy-model.md)