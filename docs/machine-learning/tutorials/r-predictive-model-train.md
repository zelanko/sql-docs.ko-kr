---
title: '자습서: R에서 예측 모델 학습 및 비교'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈의 3부에서는 R에서 SQL 기계 학습을 사용하여 두 가지 예측 모델을 만든 다음, 가장 정확한 모델을 선택합니다.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 2b57a54c66259fe16c3143e0328476279a1aea01
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748503"
---
# <a name="tutorial-create-a-predictive-model-in-r-with-sql-machine-learning"></a>자습서: R에서 SQL 기계 학습을 사용하여 예측 모델 만들기
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 3부에서는 R에서 예측 모델을 학습시킵니다. 그 다음 파트에서는 Machine Learning Services 또는 빅 데이터 클러스터를 사용하여 SQL Server 데이터베이스에 이 모델을 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 3부에서는 R에서 예측 모델을 학습시킵니다. 그 다음 파트에서는 Machine Learning Services를 사용하여 SQL Server 데이터베이스에 이 모델을 배포합니다.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 3부에서는 R에서 예측 모델을 학습시킵니다. 그 다음 부분에서는 SQL Server R Services를 사용하여 데이터베이스에 이 모델을 배포합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈의 3부에서는 R에서 예측 모델을 학습시킵니다. 그 다음 부분에서는 Machine Learning Services를 사용하여 Azure SQL Managed Instance 데이터베이스에 이 모델을 배포합니다.
::: moniker-end

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 2가지 기계 학습 모델 학습
> * 두 모델에서 예측 수행
> * 결과를 비교하여 가장 정확한 모델 선택

[1부](r-predictive-model-introduction.md)에서 샘플 데이터베이스를 복원하는 방법을 배웠습니다.

[2부](r-predictive-model-prepare-data.md)에서는 데이터베이스의 데이터를 Python 데이터 프레임에 로드하고 R에서 데이터를 준비하는 방법을 배웠습니다.

[4부](r-predictive-model-deploy.md)에서는 모델을 데이터베이스에 저장한 다음, 2부와 3부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법을 알아봅니다. 저장 프로시저는 서버에서 실행되어 새 데이터를 기반으로 미래를 예측합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서 시리즈의 3부에서는 [**1부**](r-predictive-model-introduction.md)의 사전 요구 사항을 수행하고, [**2부**](r-predictive-model-prepare-data.md)의 단계를 완료했다고 가정합니다.

## <a name="train-two-models"></a>두 모델 학습

스키 대여 데이터에 가장 적합한 모델을 찾으려면 두 가지 다른 모델(선형 회귀와 의사 결정 트리)을 만들고 보다 정확하게 예약할 수 있는 모델을 확인합니다. 이 시리즈 1부에서 만든 데이터 프레임 `rentaldata`를 사용합니다.

```r
#First, split the dataset into two different sets:
# one for training the model and the other for validating it
train_data = rentaldata[rentaldata$Year < 2015,];
test_data  = rentaldata[rentaldata$Year == 2015,];


#Use the RentalCount column to check the quality of the prediction against actual values
actual_counts <- test_data$RentalCount;

#Model 1: Use lm to create a linear regression model, trained with the training data set
model_lm <- lm(RentalCount ~  Month + Day + WeekDay + Snow + Holiday, data = train_data);

#Model 2: Use rpart to create a decision tree model, trained with the training data set
library(rpart);
model_rpart  <- rpart(RentalCount ~ Month + Day + WeekDay + Snow + Holiday, data = train_data);
```

## <a name="make-predictions-from-both-models"></a>두 모델에서 예측 수행

예측 함수를 사용하여 학습된 각 모델로 대여 수를 예측합니다.

```r
#Use both models to make predictions using the test data set.
predict_lm <- predict(model_lm, test_data)
predict_lm <- data.frame(RentalCount_Pred = predict_lm, RentalCount = test_data$RentalCount, 
                         Year = test_data$Year, Month = test_data$Month,
                         Day = test_data$Day, Weekday = test_data$WeekDay,
                         Snow = test_data$Snow, Holiday = test_data$Holiday)

predict_rpart  <- predict(model_rpart,  test_data)
predict_rpart <- data.frame(RentalCount_Pred = predict_rpart, RentalCount = test_data$RentalCount, 
                         Year = test_data$Year, Month = test_data$Month,
                         Day = test_data$Day, Weekday = test_data$WeekDay,
                         Snow = test_data$Snow, Holiday = test_data$Holiday)

#To verify it worked, look at the top rows of the two prediction data sets.
head(predict_lm);
head(predict_rpart);
```

```results
    RentalCount_Pred  RentalCount  Month  Day  WeekDay  Snow  Holiday
1         27.45858          42       2     11     4      0       0
2        387.29344         360       3     29     1      0       0
3         16.37349          20       4     22     4      0       0
4         31.07058          42       3      6     6      0       0
5        463.97263         405       2     28     7      1       0
6        102.21695          38       1     12     2      1       0
    RentalCount_Pred  RentalCount  Month  Day  WeekDay  Snow  Holiday
1          40.0000          42       2     11     4      0       0
2         332.5714         360       3     29     1      0       0
3          27.7500          20       4     22     4      0       0
4          34.2500          42       3      6     6      0       0
5         645.7059         405       2     28     7      1       0
6          40.0000          38       1     12     2      1       0
```

## <a name="compare-the-results"></a>결과 비교

이제 최상의 예측을 제공할 모델을 확인하려고 합니다. 이 작업을 수행하는 쉽고 빠른 방법은 기본적인 그리기 함수를 사용하여 학습 데이터의 실제 값과 예측된 값 간의 차이를 확인하는 것입니다.

```r
#Use the plotting functionality in R to visualize the results from the predictions
par(mfrow = c(1, 1));
plot(predict_lm$RentalCount_Pred - predict_lm$RentalCount, main = "Difference between actual and predicted. lm")
plot(predict_rpart$RentalCount_Pred  - predict_rpart$RentalCount,  main = "Difference between actual and predicted. rpart")
```

![두 모델 비교](./media/compare-models.png)

의사 결정 트리 모델이 두 모델 중에서 좀 더 정확한 것 같습니다.

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행할 생각이 없으면 TutorialDB 데이터베이스를 삭제하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 3부에서는 다음 작업을 수행하는 방법을 알아보았습니다.

* 2가지 기계 학습 모델 학습
* 두 모델에서 예측 수행
* 결과를 비교하여 가장 정확한 모델 선택

만든 기계 학습 모델을 배포하려면 다음 자습서 시리즈의 4부를 따르세요.

> [!div class="nextstepaction"]
> [R에서 SQL 기계 학습을 사용하여 예측 모델 배포](r-predictive-model-deploy.md)
