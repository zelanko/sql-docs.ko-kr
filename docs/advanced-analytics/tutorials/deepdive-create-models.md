---
title: R 모델 (SQL과 R 심층 분석)을 만들고 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a2f6e9b23e1592073c1b21bc41e4975ffaf17075
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-r-models-sql-and-r-deep-dive"></a>R 모델 (SQL과 R 심층 분석)을 만들으십시오
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이제 교육 데이터를 보강했으므로 선형 회귀를 사용하여 데이터를 분석해야 합니다. 선형 모델은 예측 분석 분야의 중요한 도구이며, **의** RevoScaleR [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 패키지에는 확장성 있는 고성능 알고리즘이 포함되어 있습니다.

## <a name="create-a-linear-regression-model"></a>선형 회귀 모델 만들기

이 단계에 있는 값의 독립 변수로 사용 하 여 고객에 대 한 신용 카드 잔액을 예측 하는 간단한 선형 모델을 만듭니다는 *성별* 및 *creditLine* 열입니다.
  
이 위해 사용 하 여는 [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) 원격 계산 컨텍스트를 지 원하는 함수입니다.
  
1. 완료 된 저장 하는 R 변수를 만들 모델 및 호출 **rxLinMod**, 적절 한 수식 전달 합니다.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. 표준 R을 호출 하는 결과의 요약을 보려면 `summary` 모델 개체에 대해 함수입니다.
  
     ```R
     summary(linModObj)
     ```

일반 R 함수 등의 특이 한 생각할 수 있습니다 `summary` 이전 단계에서 서버에 계산 컨텍스트를 설정 하므로 여기에서 작동할 것입니다. 그러나 **rxLinMod** 함수는 원격 계산 컨텍스트를 사용하여 모델을 만들더라도 로컬 워크스테이션에 대한 모델을 포함하고 이를 공유 디렉터리에 저장하는 개체도 반환합니다.

따라서 "로컬" 컨텍스트를 사용하여 만들어진 것처럼 모델에 대해 표준 R 명령을 실행할 수 있습니다.

**결과**

```
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
Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>로지스틱 회귀 모델 만들기

다음으로, 특정 고객 사기 위험 인지 여부를 나타내는 로지스틱 회귀 모델을 만듭니다. 사용 하 여는 **RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) 계산 컨텍스트는 원하는 맞춤 원격에 로지스틱 회귀 모델의 함수입니다.

1.  계산 컨텍스트를 그대로 유지합니다. 또한 계속해서 같은 데이터 원본을 사용합니다.

2.  **rxLogit** 함수를 호출하고 모델을 정의하는 데 필요한 수식을 전달합니다.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    삭제된 더미 변수 3개를 비롯하여 60개의 독립 변수를 포함하는 큰 모델이기 때문에 계산 컨텍스트에서 개체가 반환될 때까지 잠시 기다려야 할 수도 있습니다.
    
    모델이 이렇게 큰 이유는 R 및 **RevoScaleR** 패키지에서 모든 수준의 범주 요소 변수가 자동으로 별도의 더미 변수로 처리되기 때문입니다.
  
3.  반환 된 모델의 요약을 확인 하려면 R을 호출 `summary` 함수입니다.
  
    ```R
    summary(logitObj)
    ```
  
**일부 결과**

```
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

Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-step"></a>다음 단계

[새 데이터 채점하기](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>이전 단계

[R을 사용하여 SQL Server 데이터 시각화](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
