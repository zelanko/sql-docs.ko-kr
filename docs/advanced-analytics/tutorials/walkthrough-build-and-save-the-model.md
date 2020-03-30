---
title: 'R 자습서: 모델 빌드 및 저장'
description: SQL Server 데이터베이스 내 분석에 사용되는 R 언어 모델을 작성하는 방법을 보여주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cb806c0a6286ec8a6608b346d12e666a8e9a09f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73724523"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>R 모델을 빌드하여 SQL Server에 저장(연습)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단계에서는 기계 학습 모델을 작성하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장하는 방법을 알아봅니다. 모델을 저장하면 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 또는 [PREDICT (T-SQL) function](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에서 직접 호출할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

이 단계는 이 연습의 이전 단계에서 진행 중인 R 세션을 전제로 합니다. 이전 단계에서 만든 연결 문자열과 데이터 원본 개체를 사용합니다. 다음 도구 및 패키지는 스크립트를 실행하는 데 사용됩니다.

+ R 명령을 실행하는 Rgui.exe
+ T-SQL을 실행하는 Management Studio
+ ROCR 패키지
+ RODBC 패키지

### <a name="create-a-stored-procedure-to-save-models"></a>모델에 저장하는 저장 프로시저 만들기

이 단계에서는 저장 프로시저를 사용하여 학습된 모델을 SQL Server에 저장합니다. 이 작업을 수행하기 위해 저장 프로시저를 만들면 작업이 손쉬워집니다.

Management Studio의 쿼리 창에서 다음 T-SQL 코드를 실행하여 저장 프로시저를 만듭니다.

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
> 오류가 발생하는 경우 로그인에 개체를 만들 수 있는 권한이 있는지 확인합니다. `exec sp_addrolemember 'db_owner', '<user_name>'`과 같이 T-SQL 문을 실행하여 개체를 만들기 위한 명시적 권한이 있어야 합니다.

## <a name="create-a-classification-model-using-rxlogit"></a>rxLogit을 사용하여 분류 모델 만들기

모델은 택시 기사가 특정 여정에서 팁을 받을 가능성이 있는지 여부를 예측하는 이진 분류자입니다. 이전 단원에서 만든 데이터 원본을 사용하여 로지스틱 회귀를 통해 팁 분류자를 학습합니다.

1. [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 패키지에 포함된 **rxLogit** 함수를 호출하여 로지스틱 회귀 모델을 만듭니다. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    모델을 빌드하는 호출은 system.time 함수 내에 있어야 합니다. 이렇게 하면 모델을 빌드하는 데 필요한 시간을 얻을 수 있습니다.

2. 모델을 빌드한 후 `summary` 함수를 사용하여 검사하고 계수를 확인하는 것이 좋습니다.

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

## <a name="use-the-logistic-regression-model-for-scoring"></a>점수 매기기에 로지스틱 회귀 모델 사용

이제 모델이 작성되었으므로 모델을 사용하여 기사가 특정 여정에서 팁을 받을 가능성이 있는지 여부를 예측할 수 있습니다.

1. 먼저 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 함수를 사용하여 채점 결과를 저장하기 위한 데이터 원본 개체를 정의합니다.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 이 예제를 더 간소화하기 위해 로지스틱 회귀 모델에 대한 입력은 모델 학습에 사용한 것과 동일한 기능 데이터 원본(`sql_feature_ds`)입니다.  대체로 점수를 매길 새 데이터가 있거나, 테스트 및 학습을 위해 일부 데이터를 따로 보관했을 수 있습니다.
  
    + 예측 결과는 _taxiscoreOutput_테이블에 저장됩니다. rxSqlServerData를 사용하여 만들 때 이 테이블에 대한 스키마는 정의되지 않습니다. 스키마는 rxPredict 출력에서 가져옵니다.
  
    + 예측된 값을 저장하는 테이블을 만들려면 rxSqlServer 데이터 함수를 실행하는 SQL 로그인에 데이터베이스에 대한 DDL 권한이 있어야 합니다. 로그인이 테이블을 만들 수 없는 경우에는 문이 실패합니다.

2. [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 함수를 호출하여 결과를 생성합니다.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    문이 성공하면 실행하는 데까지 시간이 걸립니다. 완료되면 SQL Server Management Studio를 열어 테이블이 생성되었고 점수 열 및 다른 예상 출력이 포함되어 있는지 확인할 수 있습니다.

## <a name="plot-model-accuracy"></a>모델 정확도 그리기

모델의 정확도를 파악하기 위해 [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) 함수를 사용하여 수신기 운영 곡선을 그릴 수 있습니다. rxRoc는 RevoScaleR 패키지에서 제공하는 새 함수 중 하나로, 원격 컴퓨팅 컨텍스트를 지원하며 다음 두 가지 옵션을 사용할 수 있습니다.

+ rxRoc 함수를 사용하여 원격 컴퓨팅 컨텍스트에서 플롯을 실행한 다음, 로컬 클라이언트에 플롯을 반환할 수 있습니다.

+ 데이터를 R 클라이언트 컴퓨터로 가져온 후 다른 R 그리기 함수를 사용하여 성능 그래프를 만들 수도 있습니다.

이 섹션에서는 두 가지 방법을 모두 사용합니다.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>원격(SQL Server) 컴퓨팅 컨텍스트에서 그림 실행

1. rxRoc 함수를 호출하고 이전에 정의된 데이터를 입력으로 제공합니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    이 호출은 ROC 차트 계산에 사용되는 값을 반환합니다. 레이블 열은 _tipped_로, _점수_ 열에는 예측이 있는 반면, 예측하려는 실제 결과를 포함합니다.

2. 실제로 차트를 그리려면 ROC 개체를 저장한 다음, 플롯 함수를 사용하여 그릴 수 있습니다. 이 그래프는 원격 컴퓨팅 컨텍스트에서 생성된 다음, R 환경으로 반환됩니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    R 그래픽 디바이스를 열거나 RStudio에서 **플롯** 창을 클릭하면 그래프를 볼 수 있습니다.

    ![모델에 대한 ROC 플롯](media/rsql-e2e-rocplot.png "모델에 대한 ROC 플롯")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>SQL Server에서 데이터를 사용하여 로컬 컴퓨팅 컨텍스트에서 그림 만들기

명령 프롬프트에서 `rxGetComputeContext()`를 실행하여 컴퓨팅 컨텍스트가 로컬인지 확인할 수 있습니다. 반환 값은 “RxLocalSeq 컴퓨팅 컨텍스트”여야 합니다.

1. 로컬 컴퓨팅 컨텍스트의 경우 프로세스는 거의 동일합니다. [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 함수를 사용하여 지정된 데이터를 로컬 R 환경으로 가져옵니다.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 로컬 메모리의 데이터를 사용하여 **ROCR** 패키지를 로드하고 해당 패키지의 예측 함수를 사용하여 몇 가지 새로운 예측을 만들 수 있습니다.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. `pred` 출력 변수에 저장된 값에 따라 로컬 플롯을 생성합니다.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![R을 사용하여 모델 성능 그리기](media/rsql-e2e-performanceplot.png "R을 사용하여 모델 성능 그리기")

> [!NOTE]
> 차트는 사용하는 데이터 요소 수에 따라 다르게 표시될 수 있습니다.

## <a name="deploy-the-model"></a>모델 배포

모델을 빌드하고 잘 작동됨을 확인한 후 조직의 사용자나 사람들이 모델을 사용할 수 있는 사이트에 배치하거나, 정기적으로 모델을 다시 학습하고 다시 보정할 수 있습니다. 이 프로세스를 모델 *운영화*라고도 합니다. SQL Server에서 운영화는 저장 프로시저에 R 코드를 포함하여 달성할 수 있습니다. 코드는 프로시저에 있으므로 SQL Server에 연결할 수 있는 모든 애플리케이션에서 호출될 수 있습니다.

그러나 외부 애플리케이션에서 모델을 호출하려면 먼저 프로덕션에서 사용되는 데이터베이스에 모델을 저장해야 합니다. 학습된 모델은 **varbinary(max)** 형식의 단일 열에 이진 형식으로 저장됩니다.

일반적인 배포 워크플로는 다음 단계로 구성됩니다.

1. 16진수 문자열로 모델 직렬화
2. 직렬화된 개체를 데이터베이스로 전송
3. varbinary(max) 열에 모델 저장

이 섹션에서는 저장 프로시저를 사용하여 모델을 유지하고 예측에 사용할 수 있도록 설정하는 방법에 대해 알아봅니다. 이 섹션에 사용된 저장 프로시저는 PersistModel입니다. PersistModel의 정의는 [필수 구성 요소](#prerequisites)입니다.

1. 아직 사용하지 않는 경우 로컬 R 환경으로 다시 전환하고 모델을 직렬화한 후, 변수에 저장합니다.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. **RODBC**를 사용하여 ODBC 연결을 엽니다. 패키지를 이미 로드한 경우 RODBC에 대한 호출을 생략할 수 있습니다.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. SQL Server에서 PersistModel 저장 프로시저를 호출하여 직렬화된 개체를 데이터베이스로 전송하고 모델의 이진 표현을 열에 저장합니다. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Management Studio를 사용하여 모델이 있는지 확인합니다. 개체 탐색기에서 **nyc_taxi_models** 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 1000개 행 선택**을 클릭합니다. 결과에서 **models** 열에 이진 표현이 표시됩니다.

테이블에 모델을 저장하는 경우 INSERT 문만 있으면 됩니다. 그러나 *PersistModel*과 같이 저장 프로시저에 래핑되는 경우가 많습니다.

## <a name="next-steps"></a>다음 단계

다음 단원 및 마지막 단원에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장된 모델에 대한 채점을 수행하는 방법을 알아봅니다.

> [!div class="nextstepaction"]
> [SQL에서 R 모델 배포 및 사용](walkthrough-deploy-and-use-the-model.md)
