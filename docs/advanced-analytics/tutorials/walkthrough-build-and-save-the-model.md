---
title: R 모델을 작성 하 고 SQL Server (연습)-SQL Server Machine Learning에 저장
description: SQL Server 데이터베이스 내 분석에 사용 되는 R 언어 모델을 빌드하는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b02b1e0298af6fbb96ba5ddd8d5a18dc8e154598
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645482"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>R 모델을 작성 하 고 SQL Server (연습)에 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단계에서는 기계 학습 모델을 빌드하고 모델을 저장 하는 방법을 알아봅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 모델을 저장 하면에서 직접 호출할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저를 사용 하 여 코드 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 또는 [(T-SQL) PREDICT 함수](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 단계에서는이 연습의 이전 단계에 따라 진행 중인 R 세션을 가정 합니다. 이러한 단계에서 만든 연결 문자열 및 데이터 원본 개체를 사용 합니다. 스크립트를 실행 하려면 다음 도구 및 패키지 사용 됩니다.

+ Rgui.exe R 명령을 실행 하려면
+ T-SQL을 실행 하기 위해 management Studio
+ ROCR 패키지
+ RODBC 패키지

### <a name="create-a-stored-procedure-to-save-models"></a>모델을 저장 하려면 저장된 프로시저 만들기

이 단계는 SQL Server에 학습 된 모델을 저장 하려면 저장된 프로시저를 사용 합니다. 태스크를 쉽게이 작업을 수행 하려면 저장된 프로시저를 만들고 있습니다.

저장된 프로시저를 만들려면 Management Studio를 쿼리 창에서 다음 T-SQL 코드를 실행 합니다.

```sql
USE [NYCTaxi_Sample]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PersistModel')
  DROP PROCEDURE PersistModel
GO

CREATE PROCEDURE [dbo].[PersistModel] @m nvarchar(max)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;
    insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
END
GO
```

> [!NOTE]
> 오류가 발생 하는 경우에 로그인 개체를 만들 수 있는 권한이 있는지 확인 합니다. 다음과 같은 T-SQL 문을 실행 하 여 개체를 만들 수 있는 명시적 권한을 부여할 수 있습니다: `exec sp_addrolemember 'db_owner', '<user_name>'`합니다.

## <a name="create-a-classification-model-using-rxlogit"></a>rxLogit을 사용해서 분류모델(classification model) 만들기

모델은 택시 기사가 특정 여정에서 팁을 받을 가능성이 있는지 여부를 예측 하는 이진 분류자 됩니다. 지난 과정(lesson)에서 만들었던 데이터 소스(data source)를  사용하여 이 팁 예측 모델을 학습하고, 이때 로지스틱 회귀(logistic regression)를 사용합니다.

1. [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 패키지에 들어있는 **rxLogit** 함수를 호출하여 로지스틱 회귀 모델을 만들어 봅시다.  

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    모델을 빌드하는 호출은 system.time 함수 내에 포함되어 있습니다. 이것으로 모델을 빌드하는 데 필요한 시간을 구할 수 있습니다.

2. 모델을 빌드한 후에 `summary` 함수를 사용해서 모델을 점검하고 계수를 확인할 수 있습니다.

    ```R
    summary(logitObj);
    ```

    **결과**
    
    ```R
     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*
     direct_distance* 
     *Data: featureDataSource (RxSqlServerData Data Source)*
     *Dependent variable(s): tipped*
     *Total independent variables: 5*
     *Number of valid observations: 17068*
     *Number of missing observations: 0*
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*
     *Coefficients:*
     *Estimate Std. Error z value Pr(>|z|)*
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     *---*
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     *Condition number of final variance-covariance matrix: 48.3933*
     *Number of iterations: 4*
   ```

## <a name="use-the-logistic-regression-model-for-scoring"></a>로지스틱 회귀 모델을 사용하여 채점하기

이제 모델이 작성되었으므로 모델을 사용하여 기사가 특정 여정에서 팁을 받을 가능성이 있는지 여부를 예측할 수 있습니다.

1. 먼저 사용 합니다 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 점수 매기기 결과 저장 하는 것에 대 한 데이터 원본 개체를 정의 하는 함수입니다.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 예제를 간단하게 하기 위해, 로지스틱 회귀 모델의 입력값은 모델을 학습시키는 데에 사용되었던 특성값 데이터(`sql_feature_ds`)를 그대로 사용할 것입니다.  하지만 테스트 때에 사용하는 데이터는 학습 때와는 다른 새로운 데이터인 경우가 대부분이며, 테스트용 데이터와 학습용 테이터를 따로 준비해서 사용하는 것이 보다 일반적입니다.
  
    + 예측 결과는 _taxiscoreOutput_ 테이블에 저장됩니다. 이 테이블의 스키마는 이 테이블이 RxSqlServerData 함수를 통해 생성될 때 만들어지는 것이 아니라 rxPredict의 출력값으로부터 오는 것입니다.이 부분을 눈여겨 보세요.
  
    + 예측된 값을 저장하기 위한 테이블을 만들려면, RxSqlServerData 함수를 실행하는 SQL 데이터베이스의 계정에 DDL 권한이 있어야 합니다. 만약 지금 로그인 되어있는 계정이 테이블을 만들 수 없는 경우 실행문은 실패하게 됩니다.

2. [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 함수를 호출하여 결과를 생성합니다.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    문이 성공 하면 경우에 다소 시간이 걸립니다. 완료 되 면 SQL Server Management Studio를 열고 테이블을 만든를 예상 된 출력 점수 열 및 기타 포함 되어 있는지 확인 하십시오.

## <a name="plot-model-accuracy"></a>모델 정확도 그리기

모델의 정확도 파악 하려면 사용 합니다 [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) 수신기 운영 곡선을 그릴 함수입니다. RxRoc RevoScaleR 패키지에서 제공 하는 새 함수 중 하나 이므로 원격 계산 컨텍스트를 지 원하는, 두 가지 옵션이 있습니다.

+ rxRoc 함수를 사용하여 원격 계산 컨텍스트에서 플롯을 실행한 다음 로컬 클라이언트에 플롯을 반환합니다.

+ 데이터를 R환경의 로컬 클라이언트 컴퓨터로 불러온 후 다른 종류의 R 그래프 함수를 사용해서 성능 그래프를 만들 수도 있습니다.

이 절에서는 두 가지 방법을 모두 시도해 봅니다.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>원격(SQL Server) 계산 컨텍스트에서 플롯 실행

1. 함수 rxRoc를 호출 하 고 앞에서 정의한 입력으로 데이터를 제공 합니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    이 호출은 ROC 차트를 계산할 때 사용되는 값을 반환합니다. 라벨(Label) 열은 _tipped_ 이고 예측하려는 실제 결과를 가지고 있으며 _Score_ 열에는 예측이 들어 있습니다. 

2. 그릴 실제로 차트 ROC 개체를 저장할 수 있으며 다음 그리기 함수를 사용 하 여 그릴 수 있습니다. 그래프는 원격 계산 컨텍스트에 생성되고 R 환경에 반환됩니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    R 그래픽 장치를 열거나 RStudio의 **Plot** 창을 클릭해서 그래프를 봅니다.

    ![모델에 대한 ROC 그림](media/rsql-e2e-rocplot.png "모델에 대한 ROC 그림")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>SQL Server의 데이터를 사용하여 로컬 계산 컨텍스트에서 플롯 만들기

실행 하 여 계산 컨텍스트는 로컬을 확인할 수 있습니다 `rxGetComputeContext()` 명령 프롬프트에서. 반환 값은 "RxLocalSeq 계산 컨텍스트" 이어야 합니다.

1. 로컬 계산 컨텍스트에 대해서도 절차는 거의 동일합니다. [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 함수를 사용해서 로컬 R 환경에 지정된 데이터를 가져옵니다.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 로컬 메모리 내 데이터를 사용해서 **ROCR** 패키지를 로드하고 예측 함수를 사용해서 몇가지 새로운 예측을 만듭니다.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 출력 변수 `pred`에 저장된 값을 기반으로 로컬 플롯을 생성합니다.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![R을 사용하여 모델 성능 그리기](media/rsql-e2e-performanceplot.png "R을 사용하여 모델 성능 그리기")

> [!NOTE]
> 차트는 사용한 데이터 포인트의 수에 따라 다르게 보일 수 있습니다.

## <a name="deploy-the-model"></a>모델 배포

모델을 작성하고 잘 수행되는 것을 확인한 후 그 모델을 사용하거나 혹은 정기적으로 재교육과 재조정하는 조직의 사용자나 사람들이 있는 사이트로 배포하길 원할 것입니다. 이러한 절차를 때때로 *operationalizing a model* 이라고 합니다. SQL Server 운영 화 저장된 프로시저에서 R 코드를 포함 하 여 수행 됩니다. 코드를 프로시저에 있으므로 SQL Server에 연결할 수 있는 모든 응용 프로그램에서 호출할 수 있습니다.

외부 응용 프로그램에서 모델을 호출할 수 있습니다, 전에 모델을 프로덕션에 사용 되는 데이터베이스에 저장 해야 합니다. 학습 된 모델 유형의 단일 열에 이진 형식으로 저장 됩니다 **varbinary (max)** 합니다.

일반적인 배포 워크플로 다음 단계로 구성 됩니다.

1. 16 진수 문자열로 모델 직렬화
2. 데이터베이스에 serialize 된 개체를 전송 합니다.
3. Varbinary (max) 열에 모델을 저장 합니다.

이 섹션에서는 모델을 유지 하 고 예측에 사용할 수 있도록 하려면 저장된 프로시저를 사용 하는 방법에 알아봅니다. 이 섹션에 사용 되는 저장된 프로시저를 PersistModel입니다. PersistModel의 정의가 [필수 구성 요소](#prerequisites)합니다.

1. 로컬 R 환경으로 다시 전환하고(사용하지 않고 있다면) 모델을 직렬화하고 변수에 저장합니다.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. **RODBC**를 사용하여 ODBC 연결을 엽니다. 패키지를 이미 로드한 경우 RODBC 호출을 생략할 수 있습니다.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. 호출 PersistModel 저장 프로시저를 SQL Server에서 transmite에 직렬화 된 개체는 데이터베이스를 하 고 모델의 이진 열에 저장 합니다. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. 모델을 확인 하려면 Management Studio를 사용 하 여 존재 합니다. 개체 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **nyc_taxi_models** 클릭 **상위 1000 개의 행 선택**합니다. 결과에서 이진 표현을 표시 되어야 합니다 **모델** 열입니다.

테이블에 모델을 저장하는 경우 INSERT 문만 있으면 됩니다. 그러나 쉽습니다 때와 같은 저장된 프로시저에서 래핑된 *PersistModel*합니다.

## <a name="next-steps"></a>다음 단계

다음 및 최종 단원에서는 사용 하 여 저장 된 모델에 대 한 점수 매기기를 수행 하는 방법에 알아봅니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.

> [!div class="nextstepaction"]
> [R 모델을 배포하고 SQL에서 사용하기](walkthrough-deploy-and-use-the-model.md)
