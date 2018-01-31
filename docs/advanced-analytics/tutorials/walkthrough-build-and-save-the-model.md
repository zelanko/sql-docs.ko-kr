---
title: "R 모델을 작성하고 SQL Server에 저장하기 | Microsoft Docs"
ms.custom: 
ms.date: 07/14/2017
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
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 281f5026bc3aa7dc67cff418eb0868eeb81bc80a
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="build-an-r-model-and-save-to-sql-server"></a>R 모델을 작성하고 SQL Server에 저장하기

이 단계에서는 기계 학습 모델을 작성하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 그 모델을 저장하는 방법을 학습합니다.

## <a name="create-a-classification-model-using-rxlogit"></a>RxLogit를 사용하여 분류 모델 만들기

작성하는 모델은 택시 운전사가 특정 승차에 대해 팁을 받을 수 있는지를 예측하는 이진 분류기입니다. 이전 단원에서 만든 데이터 원본을 사용하여 팁 분류기를 학습하며 로지스틱 회귀를 사용합니다.

1. [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 패키지에 포함된 **rxLogit** 함수를 호출하여 로지스틱 회귀 모델을 만듭니다. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = sql_feature_ds));
    ```

    모델을 작성하는 호출은 system.time 함수로 묶여 있습니다. 이것으로 모델을 작성하는 데 필요한 시간을 구할 수 있습니다.

2. 모델을 작성한 후에 `summary` 함수를 사용하여 모델을 조사하고 계수를 관찰할 수 있습니다.

    ```R
    summary(logitObj);
    ```

     *결과*

     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs + 
direct_distance*
     <br/>*Data: featureDataSource (RxSqlServerData Data Source)*
     <br/>*Dependent variable(s): tipped *
     <br/>*Total independent variables: 5*
     <br/>*Number of valid observations: 17068*
     <br/>*Number of missing observations: 0*
     <br/>*-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*
     <br/>*Coefficients:*
     <br/>*Estimate Std. Error z value Pr (> | z |)*
     <br/>*(Intercept)-2.509e-03 3.223e-02-0.078 0.93793*
     <br/>*passenger_count-5.753e-02 1.088e-02-5.289 1.23 e-07\*\*\**
     <br/>*trip_distance-3.896e-02 1.466e-02-2.658 0.00786\*\**
     <br/>*trip_time_in_secs 2.115e-4.336e 04-05 4.878 1.07e-06\*\*\**
     <br/>*direct_distance 6.156e-02 2.076e-02 2.966 0.00302\*\**
     <br/>*---*
     <br/>*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     <br/>*Condition number of final variance-covariance matrix: 48.3933*
     <br/>*Number of iterations: 4*

## <a name="use-the-logistic-regression-model-for-scoring"></a>로지스틱 회귀 모델을 사용하여 채점하기

이제 모델이 작성되었으므로 드라이버가 특정 드라이브에서 팁을 받을 가능성이 있는지 여부를 예측할 수 있습니다.

1. 우선 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 함수를 사용해서 채점 결과를 저장하기 위한 데이터 원본 개체를 정의합니다. (역주. 원본에 “scoring resul” 이라는 단어로 끝나는 문장을 가지고 있으며 이를 역자는 “scoring result” 라고 판단해 해석에 적용했습니다.)

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 예제를 더 간단하게 만들기 위해 로지스틱 회귀 모델의 입력은 모델 훈련에 사용했던 같은 특성 데이터 원본(`sql_feature_ds`)입니다. 보다 일반적으로는 채점을 위해 새로운 데이터를 가지고 있거나 혹은 검증용(test)과 훈련용(training)으로 일부 데이터를 따로 준비했을 것입니다.
  
    + 예측 결과는 _taxiscoreOutput_ 테이블에 저장 됩니다. 이 테이블에 대한 스키마는 rxSqlServerData를 사용하여 생성될 때 정의되지 않았습니다. rxPredict 출력에서 스키마를 가져옵니다.
  
    + 예측된 값을 저장하는 테이블을 만들려면 rxSqlServer 데이터 함수를 실행하는 SQL 로그인에 데이터베이스의 DDL 권한이 있어야 합니다. 로그인이 테이블을 만들 수 없는 경우 문이 실패합니다.

2. [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 함수를 호출하여 결과를 생성합니다.

    ```R
    rxPredict(modelObject = logitObj,
        data = sql_feature_ds,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    문이 성공하면 실행하는 데 약간의 시간이 걸립니다. 완료되면 SQL Server Management Studio를 열어서 해당 테이블의 생성 여부 그리고 Score 열과 기타 예상되는 결과가 포함되어 있는지 확인합니다.

## <a name="plot-model-accuracy"></a>모델 정확도 그리기

모델의 정확도에 대한 아이디어를 얻기 위해 rxRoc(https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) 함수를 사용하여 Receiver Operating Curve를 그릴 수 있습니다. rxRoc는 원격 계산 컨택스트를 지원하는 RevoScaleR에서 제공된 새 함수 중 하나이며 두 가지 옵션이 있습니다.

+ rxRoc 함수를 사용하여 원격 계산 컨텍스트에서 플롯을 실행한 다음 로컬 클라이언트에 플롯을 반환합니다.

+ 데이터를 R 클라이언트 컴퓨터로 가져온 후 다른 R 플로팅 함수를 사용해서 성능 그래프를 만들 수도 있습니다.

이 절에서는 두 가지 방법을 모두 시험합니다.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>원격(SQL Server) 계산 컨텍스트에서 플롯 실행

1. rxRoc 함수를 호출하고 앞에서 정의한 데이터를 입력으로 제공합니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    이 호출은 ROC 차트를 계산할 때 사용되는 값을 반환합니다. 라벨(Label) 열은 _tipped_ 이고 예측하려는 실제 결과를 가지고 있으며 _Score_ 열에는 예측이 들어 있습니다.

2. 실제로 차트를 그리기 위해서는 ROC 개체를 저장한 다음에 `plot` 함수로 그릴 수 있습니다. 그래프는 원격 계산 컨텍스트에 생성되고 R 환경에 반환됩니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    R 그래픽 장치를 열거나 RStudio의 **Plot** 창을 클릭해서 그래프를 봅니다.

    ![모델에 대한 ROC 그림](media/rsql-e2e-rocplot.png "모델에 대한 ROC 그림")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>SQL Server의 데이터를 사용하여 로컬 계산 컨텍스트에서 플롯 만들기

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

모델을 작성하고 잘 수행되는 것을 확인한 후 그 모델을 사용하거나 혹은 정기적으로 재교육과 재조정하는 조직의 사용자나 사람들이 있는 사이트로 배포하길 원할 것입니다. 이러한 절차를 때때로 *operationalizing a model* 이라고 합니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 사용하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용해서 R 모델을 호출할 수 있으므로 클라이언트 응용 프로그램에서 R을 쉽게 사용할 수 있습니다.

그러나 외부 응용 프로그램에서 모델을 호출하려면 프로덕션에서 사용되는 데이터베이스에 모델을 저장해야 합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서는 학습된 모델이 **varbinary(max)** 형식의 단일 열에 이진 형식으로 저장됩니다.

따라서 훈련된 모델을 R에서 SQL Server로 이동하는 단계는 다음과 같습니다.

+ 모델을 16진수 문자열로 직렬화

+ 직렬화된 개체를 데이터베이스로 전송

+ varbinary(max) 열에 모델 저장

이번 절에서는 모델을 유지하는 방법과 예측을 수행하기 위해 모델을 호출하는 방법을 배웁니다.

1. 로컬 R 환경으로 다시 전환하고(사용하지 않고 있다면) 모델을 직렬화하고 변수에 저장합니다.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. **RODBC**를 사용하여 ODBC 연결을 엽니다.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

    패키지를 이미 로드한 경우 RODBC 호출을 생략할 수 있습니다.

3. PowerShell 스크립트로 만든 저장된 프로시저를 호출하여 모델의 이진 표현을 데이터베이스의 열에 저장합니다.

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

    테이블에 모델을 저장하는데 INSERT 문만 있으면 되지만 _PersistModel_처럼 저장 프로시저로 구성하는 것이 더 용이합니다.

    > [!NOTE]
    > 만일 "PersistModel 개체에 EXECUTE 권한이 거부되었습니다" 같은 오류가 발생하는 경우 로그인에 권한이 있는지 확인하세요. `GRANT EXECUTE ON [dbo].[PersistModel] TO <user_name>` 같은 T-SQL 문을 실행하여 저장 프로시저에 명시적으로 권한을 줄 수 있습니다

4. 모델을 만들고 데이터베이스에 저장한 후에는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 시스템 저장 프로시저를 사용해서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드로부터 모델을 직접 호출할 수 있습니다.

    그런데 자주 사용하는 모델이라면 사용자 저장 프로시저 내에서 입력 쿼리와 모델 호출을 다른 매개변수와 함께 구성하는 것이 더 용이합니다.

    다음은 그러한 저장 프로시저의 전체 코드입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 모델을 보다 쉽게 관리하고 업데이트할 수 있도록 이와 같은 저장된 프로시저를 만드는 것이 좋습니다.

    ```tsql
    CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)
    AS
    BEGIN
      SET NOCOUNT ON;
      INSERT INTO nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
    END
    ```

  > [!NOTE]
  > **SET NOCOUNT ON** 절을 사용하여 SELECT 문의 추가 결과 집합을 방지합니다. (역주. SELECT 결과 외 추가로 반환되는 메시지를 제거하는 목적임).


다음 및 최종 단원에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장된 모델을 대상으로 채점을 수행하는 방법을 배웁니다.

## <a name="next-lesson"></a>다음 단원

[R 모델을 배포하고 SQL에서 사용하기](walkthrough-deploy-and-use-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[R과 SQL을 사용하여 데이터 특성 만들기](walkthrough-create-data-features.md)


