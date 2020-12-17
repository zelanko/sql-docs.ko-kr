---
title: 'Python 자습서: 모델 학습'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 3부에서는 SQL 기계 학습을 사용하여 스키 대여 수요를 예측하도록 Python에서 선형 회귀 모델을 학습시킵니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: ef7dd974d77b60d3b03cf8799f7707481f32e91d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470374"
---
# <a name="python-tutorial-train-a-linear-regression-model-with-sql-machine-learning"></a>Python 자습서: SQL 기계 학습을 사용하여 선형 회귀 모델 학습
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
이 4부 자습서 시리즈의 3부에서는 Python에서 선형 회귀 모델을 학습합니다. 이 시리즈의 다음 파트에서는 Machine Learning Services를 사용하는 SQL Server 데이터베이스 또는 빅 데이터 클러스터에 이 모델을 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2017"
이 4부 자습서 시리즈의 3부에서는 Python에서 선형 회귀 모델을 학습합니다. 이 시리즈의 다음 부분에서는 Machine Learning Services가 있는 SQL Server 데이터베이스에 이 모델을 배포합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
이 4부 자습서 시리즈의 3부에서는 Python에서 선형 회귀 모델을 학습합니다. 이 시리즈의 다음 부분에서는 Machine Learning Services를 사용하여 Azure SQL Managed Instance 데이터베이스에 이 모델을 배포합니다.
::: moniker-end

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 선형 회귀 모델 학습
> * 선형 회귀 모델을 사용하여 예측 만들기

[1부](python-ski-rental-linear-regression.md)에서 샘플 데이터베이스를 복원하는 방법을 배웠습니다.

[2부](python-ski-rental-linear-regression-prepare-data.md)에서는 데이터베이스의 데이터를 Python 데이터 프레임에 로드하고, Python에서 데이터를 준비하는 방법을 배웠습니다.

[4부](python-ski-rental-linear-regression-deploy-model.md)에서는 모델을 데이터베이스에 저장한 다음, 2부와 3부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법을 알아봅니다. 저장 프로시저는 서버에서 실행되어 새 데이터를 기반으로 미래를 예측합니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 3부에서는 [1부](python-ski-rental-linear-regression.md)와 해당 필수 구성 요소를 완료했다고 가정합니다.

## <a name="train-the-model"></a>모델 학습

예측하려면 데이터 세트의 변수 간의 종속성을 가장 잘 설명하는 함수(모델)를 찾아야 합니다. 이를 모델 학습이라고 합니다. 학습 데이터 세트는 이 시리즈의 2부에서 만든 pandas 데이터 프레임 **df** 에서 전체 데이터 세트의 하위 집합입니다.

선형 회귀 알고리즘을 사용하여 모델 **lin_model** 을 학습합니다.

```python
# Store the variable we'll be predicting on.
target = "Rentalcount"

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

다음과 비슷한 결과가 표시됩니다.

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>예측 만들기

예측 함수를 사용하여 모델 **lin_model** 을 통해 임대 횟수를 예측합니다.

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

다음과 비슷한 결과가 표시됩니다.

```results
Predictions: [ 40.  38. 240.  39. 514.  48. 297.  25. 507.  24.  30.  54.  40.  26.
  30.  34.  42. 390. 336.  37.  22.  35.  55. 350. 252. 370. 499.  48.
  37. 494.  46.  25. 312. 390.  35.  35. 421.  39. 176.  21.  33. 452.
  34.  28.  37. 260.  49. 577. 312.  24.  24. 390.  34.  64.  26.  32.
  33. 358. 348.  25.  35.  48.  39.  44.  58.  24. 350. 651.  38. 468.
  26.  42. 310. 709. 155.  26. 648. 617.  26. 846. 729.  44. 432.  25.
  39.  28. 325.  46.  36.  50.  63.]
Computed error: 2.9960763804270902e-27
```

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 3부에서 다음 단계를 완료했습니다.

* 선형 회귀 모델 학습
* 선형 회귀 모델을 사용하여 예측 만들기

만든 기계 학습 모델을 배포하려면 다음 자습서 시리즈의 4부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: 기계 학습 모델 배포](python-ski-rental-linear-regression-deploy-model.md)
