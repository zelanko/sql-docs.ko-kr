---
title: "R 모델을 만들고 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: a195d5e2-72e2-4dd6-bf43-947312e4a52a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 50176ffbdaa8631f6f928bd6ecd23ab0feb28839
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-r-models"></a>R 모델 만들기

이제 교육 데이터를 보강했으므로 선형 회귀를 사용하여 데이터를 분석해야 합니다. 선형 모델은 예측 분석 분야의 중요한 도구이며, **의** RevoScaleR [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 패키지에는 확장성 있는 고성능 알고리즘이 포함되어 있습니다.

## <a name="create-a-linear-regression-model"></a>선형 회귀 모델 만들기

*gender* 및 *creditLine* 열의 값을 독립 변수로 사용하여 고객의 신용 카드 잔액을 추정하는 간단한 선형 모델을 만듭니다.
  
이렇게 하려면 원격 계산 컨텍스트를 지원하는 **rxLinMod** 함수를 사용합니다.
  
1. R 변수를 만들어 완료된 모델을 저장하고 *rxLinMod* 함수를 호출하여 적절한 수식을 전달합니다.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. 결과 요약을 보려면 모델 개체에서 표준 R *summary* 함수를 호출하면 됩니다.
  
     ```R
     summary(linModObj)
     ```

이전 단계에서 계산 컨텍스트를 서버로 설정했으므로 **summary** 와 같은 일반 R 함수가 여기서 작동하는 것이 이상하다고 생각할 수 있습니다. 그러나 **rxLinMod** 함수는 원격 계산 컨텍스트를 사용하여 모델을 만들더라도 로컬 워크스테이션에 대한 모델을 포함하고 이를 공유 디렉터리에 저장하는 개체도 반환합니다.

따라서 "로컬" 컨텍스트를 사용하여 만들어진 것처럼 모델에 대해 표준 R 명령을 실행할 수 있습니다.

**결과**

*Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)*

*Dependent variable(s): balance*

*Total independent variables: 4 (Including number dropped: 1)*

*Number of valid observations: 10000*

*Number of missing observations: 0*

*Coefficients: (1 not defined because of singularities)*

*Estimate Std. 오류 t 값 Pr (> | t |) (절편)*

*3253.575 71.194 45.700 2.22e-16*

*gender=Male -88.813 78.360 -1.133 0.257*

*gender=Female Dropped Dropped Dropped Dropped*

*creditLine 95.379 3.862 24.694 2.22e-16*

*Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1*

*Residual standard error: 3812 on 9997 degrees of freedom*

*Multiple R-squared: 0.05765*

*Adjusted R-squared: 0.05746*

*F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16*

*Condition number: 1.0184*

## <a name="create-a-logistic-regression-model"></a>로지스틱 회귀 모델 만들기

이제 특정 고객이 사기 위험인지 여부를 나타내는 로지스틱 회귀 모델을 만듭니다. 원격 계산 컨텍스트에서 로지스틱 회귀 분석 모델의 맞춤을 지원하는 *rxLogit* 함수( **RevoScaleR** 패키지에 포함되어 있음)를 사용합니다.

1.  계산 컨텍스트를 그대로 유지합니다. 또한 계속해서 같은 데이터 원본을 사용합니다.

2.  **rxLogit** 함수를 호출하고 모델을 정의하는 데 필요한 수식을 전달합니다.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance +      numTrans + numIntlTrans + creditLine, data = sqlFraudDS,      dropFirst = TRUE)
    ```
  
    삭제된 더미 변수 3개를 비롯하여 60개의 독립 변수를 포함하는 큰 모델이기 때문에 계산 컨텍스트에서 개체가 반환될 때까지 잠시 기다려야 할 수도 있습니다.
    
    모델이 이렇게 큰 이유는 R 및 **RevoScaleR** 패키지에서 모든 수준의 범주 요소 변수가 자동으로 별도의 더미 변수로 처리되기 때문입니다.
  
3.  반환된 모델의 요약을 확인하려면 R **summary** 함수를 호출합니다.
  
    ```R
    summary(logitObj)
    ```
  
**일부 결과**

*Logistic Regression Results for: fraudRisk ~ state + gender +     cardholder + balance + numTrans + numIntlTrans + creditLine*

*Data: sqlFraudDS (RxSqlServerData Data Source)*

*Dependent variable(s): fraudRisk*

*Total independent variables: 60 (Including number dropped: 3)*

*유효한 관측값 수: 10000-2*

*LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)*

*Coefficients:*

*Estimate Std. Error z value Pr(>|z|)     (Intercept)*

*-8.627e+00  1.319e+00  -6.538 6.22e-11*

*state=AK                Dropped    Dropped Dropped  Dropped*

*state=AL             -1.043e+00  1.383e+00  -0.754   0.4511*

*(other states omitted)*

*gender=Male             Dropped    Dropped Dropped  Dropped*

*gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09*

*cardholder=Principal    Dropped    Dropped Dropped  Dropped*

*카드 소유자 보조 5.635e =-3.403e 01-01 1.656 0.0977*

*balance               3.962e-04  1.564e-05  25.335 2.22e-16*

*numTrans              4.950e-02  2.202e-03  22.477 2.22e-16*

*numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10*

*creditLine            1.042e-01  4.705e-03  22.153 2.22e-16*

*---*

*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*

*Condition number of final variance-covariance matrix: 3997.308*

*Number of iterations: 15*

## <a name="next-step"></a>다음 단계

[새 데이터 점수](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>이전 단계

[R을 사용 하 여 SQL Server 데이터를 시각화 합니다.](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)



