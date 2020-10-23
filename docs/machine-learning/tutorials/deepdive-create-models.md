---
title: RevoScaleR을 사용하여 R 모델 만들기
description: 선형 회귀 모델을 만들어 이전 자습서에서 보강한 데이터를 분석하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c17b74aff83412dd7f74d3c9a9cb1fb7ec711b19
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196307"
---
# <a name="create-r-models-sql-server-and-revoscaler-tutorial"></a>R 모델 만들기(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이것은 SQL Server에서 [RevoScaleR 함수](/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 7에 해당됩니다.

학습 데이터를 보강했습니다. 이 자습서에서는 회귀 모델링을 사용하여 데이터를 분석합니다. 선형 모델은 예측 분석 분야에서 중요한 도구입니다. **RevoScaleR** 패키지에는 워크로드를 세분화하고 병렬로 실행할 수 있는 회귀 알고리즘이 포함되어 있습니다.

> [!div class="checklist"]
> * 선형 회귀 모델 만들기
> * 로지스틱 회귀 모델 만들기

## <a name="create-a-linear-regression-model"></a>선형 회귀 모델 만들기

이 단계에서는 *gender* 및 *creditLine* 열의 값을 독립 변수로 사용하여 고객의 신용 카드 잔액을 추정하는 간단한 선형 모델을 만듭니다.
  
이렇게 하려면 원격 컴퓨팅 컨텍스트를 지원하는 [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod) 함수를 사용합니다.
  
1. R 변수를 만들어 완료된 모델을 저장하고 **rxLinMod**를 호출하여 적절한 수식을 전달합니다.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. 결과 요약을 보려면 모델 개체에서 표준 R **summary** 함수를 호출합니다.
  
     ```R
     summary(linModObj)
     ```

이전 단계에서 컴퓨팅 컨텍스트를 서버로 설정했으므로 **summary** 와 같은 일반 R 함수가 여기서 작동하는 것이 이상하다고 생각할 수 있습니다. 그러나 **rxLinMod** 함수는 원격 컴퓨팅 컨텍스트를 사용하여 모델을 만들더라도 로컬 워크스테이션에 대한 모델을 포함하고 이를 공유 디렉터리에 저장하는 개체도 반환합니다.

따라서 "로컬" 컨텍스트를 사용하여 만들어진 것처럼 모델에 대해 표준 R 명령을 실행할 수 있습니다.

**결과**

```R
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>로지스틱 회귀 모델 만들기

다음으로, 특정 고객이 사기 위험인지 여부를 나타내는 로지스틱 회귀 모델을 만듭니다. 원격 컴퓨팅 컨텍스트에서 로지스틱 회귀 분석 모델의 맞춤을 지원하는 **RevoScaleR** [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) 함수를 사용합니다.

컴퓨팅 컨텍스트를 그대로 유지합니다. 또한 계속해서 같은 데이터 원본을 사용합니다.

1. **rxLogit** 함수를 호출하고 모델을 정의하는 데 필요한 수식을 전달합니다.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    삭제된 더미 변수 3개를 비롯하여 60개의 독립 변수를 포함하는 큰 모델이기 때문에 컴퓨팅 컨텍스트에서 개체가 반환될 때까지 잠시 기다려야 할 수도 있습니다.
    
    모델이 이렇게 큰 이유는 R 및 **RevoScaleR** 패키지에서 모든 수준의 범주 요소 변수가 자동으로 별도의 더미 변수로 처리되기 때문입니다.
  
2. 반환된 모델의 요약을 확인하려면 R **summary** 함수를 호출합니다.
  
    ```R
    summary(logitObj)
    ```
  
**일부 결과**

```R
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 '\*\*\*' 0.001 '\*\*' 0.01 '\*' 0.05 '.' 0.1 ' ' 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [새 데이터 점수 매기기](../../machine-learning/tutorials/deepdive-score-new-data.md)