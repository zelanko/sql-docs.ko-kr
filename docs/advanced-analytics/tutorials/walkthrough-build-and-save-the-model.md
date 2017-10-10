---
title: "R 모델을 작성 하 고 SQL Server에 저장 | Microsoft Docs"
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
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 281f5026bc3aa7dc67cff418eb0868eeb81bc80a
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="build-an-r-model-and-save-to-sql-server"></a>R 모델을 작성 하 고 SQL Server에 저장

이 단계에서는 기계 학습 모델을 빌드하고에서 모델을 저장 하는 방법을 알아봅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

## <a name="create-a-classification-model-using-rxlogit"></a>RxLogit를 사용 하 여 분류 모델 만들기

작성 한 모델은 택시 드라이버는 특정 안에서에 팁 얻거나 가능성이 있는지 여부를 예측 하는 이진 분류자입니다. 로지스틱 회귀를 사용 하 여 팁 분류자를 학습 하 고 이전 단원에서 만든 데이터 원본을 사용 합니다.

1. [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 패키지에 포함된 **rxLogit** 함수를 호출하여 로지스틱 회귀 모델을 만듭니다. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = sql_feature_ds));
    ```

    모델을 빌드하는 호출은 system.time 함수 내에 있어야 합니다. 이렇게 하면 모델을 빌드하는 데 필요한 시간을 얻을 수 있습니다.

2. 모델을 구성한 후에 사용 하 여 검사할 수 있습니다는 `summary` 함수 및 계수 보기.

    ```R
    summary(logitObj);
    ```

     *결과*

     *에 대 한 로지스틱 회귀 결과: 크리스마스 ~ passenger_count trip_distance + trip_time_in_secs + +*
     <br/>*direct_distance*
     <br/>*데이터: featureDataSource (RxSqlServerData 데이터 원본)*
     <br/>*Dependent variable(s): 크리스마스*
     <br/>*독립 변수 총: 5*
     <br/>*유효한 관찰의 수가: 17068*
     <br/>*누락 된 관측 치 수가: 0*
     <br/>*-2\*LogLikelihood: 23540.0602 (17063 자유도에 남아 있는 편차)*
     <br/>*계수:*
     <br/>*Estimate Std. 오류 z 값 Pr (> | z |)*
     <br/>*(가로채)-2.509e-03 3.223e-02-0.078 0.93793*
     <br/>*passenger_count-5.753e-02 1.088e-02-5.289 1.23 e-07\*\*\**
     <br/>*trip_distance-3.896e-02 1.466e-02-2.658 0.00786\*\**
     <br/>*trip_time_in_secs 2.115e-4.336e 04-05 4.878 1.07e-06\*\*\**
     <br/>*direct_distance 6.156e-02 2.076e-02 2.966 0.00302\*\**
     <br/>*---*
     <br/>*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     <br/>*최종 분산 공 분산 행렬 수가 조건: 48.3933*
     <br/>*Number of iterations: 4*

## <a name="use-the-logistic-regression-model-for-scoring"></a>점수 매기기에 로지스틱 회귀 모델 사용

이제 모델이 작성되었으므로 모델을 사용하여 기사가 특정 여정에서 팁을 받을 가능성이 있는지 여부를 예측할 수 있습니다.

1. 먼저, 사용 하 여는 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 점수 매기기 resul 저장 하기 위한 데이터 원본 개체를 정의 하는 함수

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 이 예에서는 더 간단 하 게 하려면 로지스틱 회귀 모델에 대 한 입력은 동일한 기능 데이터 원본 (`sql_feature_ds`) 모델의 학습에 사용 합니다.  대체로 점수를 매길 새 데이터가 있거나, 테스트 및 학습을 위해 일부 데이터를 따로 보관했을 수 있습니다.
  
    + 예측 결과 테이블에 저장 됩니다 _taxiscoreOutput_합니다. 이 테이블에 대 한 스키마 rxSqlServerData를 사용 하 여 만들 때 정의 되어 있지 확인 합니다. RxPredict 출력에서 스키마를 가져옵니다.
  
    + 예측된 값을 저장 하는 테이블을 만들려면 rxSqlServer 데이터 함수를 실행 하는 SQL 로그인 데이터베이스에서 DDL 권한이 있어야 합니다. 로그인 테이블을 만들 수 없는 경우 문이 실패 합니다.

2. [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 함수를 호출하여 결과를 생성합니다.

    ```R
    rxPredict(modelObject = logitObj,
        data = sql_feature_ds,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    문은 성공 하는 경우 실행 하는 데 약간의 시간이 취해야 합니다. 완료 되 면 SQL Server Management Studio를 열고 테이블을 만든 및 예상 출력은 점수 열 오류 코드 및 기타 포함 되어 있는지 확인 하십시오.

## <a name="plot-model-accuracy"></a>모델 정확도 출력 합니다.

모델의 정확도 파악 하려면 사용할 수 있습니다는 [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) 함수 수신기 운영 곡선을 그립니다. RxRoc RevoScaleR 패키지에서 제공 하는 새 기능 중 하나 이므로 원격 계산 컨텍스트를 지 원하는, 두 가지 옵션이 있습니다.

+ 원격 계산 컨텍스트 내에서 플롯을 실행 하 고 다음을 로컬 클라이언트에서 플롯을 반환 하려면 rxRoc 함수를 사용할 수 있습니다.

+ 데이터를 R 클라이언트 컴퓨터로 가져온 후 다른 R 그리기 함수를 사용하여 성능 그래프를 만들 수도 있습니다.

이 섹션에서는 두 가지 방법을 모두을 시험해 보겠습니다.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>원격(SQL Server) 계산 컨텍스트에서 그림 실행

1. 함수 rxRoc를 호출 하 고 앞에서 정의한 입력으로 데이터를 제공 합니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    이 호출은 ROC 차트 계산에 사용 되는 값을 반환 합니다. 레이블 열이 _크리스마스_, 실제 결과 예측 하려는 있는 동안는 _점수_ 열에 예측 합니다.

2. 실제로 그릴 차트를 ROC 개체를 저장 및 사용 하 여를 그릴 수는 `plot` 함수입니다. 그래프에는 원격 계산 컨텍스트를 만들고 R 환경에 반환 합니다.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    R 그래픽 장치를 열어 하거나 클릭 하 여 그래프를 봅니다는 **그릴** RStudio의 창.

    ![모델에 대한 ROC 그림](media/rsql-e2e-rocplot.png "모델에 대한 ROC 그림")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>SQL Server에서 데이터를 사용하여 로컬 계산 컨텍스트에서 그림 만들기

1. 에 대 한 로컬 계산 컨텍스트는 프로세스는 동일 합니다. 사용 하면는 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 함수 로컬 R 환경에 지정 된 데이터를 가져올 수 있습니다.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 로드할 데이터를 사용 하 여 로컬 메모리에,는 **ROCR** 패키지 및 해당 패키지에서 예측 함수를 사용 하 여 몇 가지 새로운 예측을 만듭니다.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 출력 변수에 저장 된 값에 따라 로컬 플롯을 생성할 `pred`합니다.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![R을 사용하여 모델 성능 그리기](media/rsql-e2e-performanceplot.png "R을 사용하여 모델 성능 그리기")

> [!NOTE]
> 차트는 사용한 데이터 요소에 따라 이러한 다르게 보일 수 있습니다.

## <a name="deploy-the-model"></a>모델 배포

모델을 작성 하 고 정상적으로 수행 하는 것을 확인 후에 아마도 모델을 사용 하 여 또는 아마도 다시 학습 하 고 정기적으로 모델을 조정 사용자 또는 조직의 사용자에에서 만들 수 있는 사이트에 배포 합니다. 이 프로세스는 라고도 *작업 활용* 모델입니다.

때문에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 사용 하 여 R 모델을 호출할 수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 클라이언트 응용 프로그램에서 R 사용 하기가 쉽습니다 저장된 프로시저입니다.

그러나 외부 응용 프로그램에서 모델을 호출하려면 먼저 프로덕션에서 사용되는 데이터베이스에 모델을 저장해야 합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서는 학습된 모델이 **varbinary(max)**형식의 단일 열에 이진 형식으로 저장됩니다.

따라서 학습된 모델을 R에서 SQL Server로 이동하는 단계는 다음과 같습니다.

+ 16진수 문자열로 모델 직렬화

+ 직렬화된 개체를 데이터베이스로 전송

+ varbinary(max) 열에 모델 저장

이 섹션에서는 예측을 만드는 메서드를 호출 하는 방법과 모델을 유지 하는 방법을 설명 합니다.

1. 이미 사용 하지 않는 경우 로컬 R 환경으로 다시 전환 하 고 모델을 직렬화 한 다음 변수에 저장 합니다.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. 사용 하 여 ODBC 연결을 열고 **RODBC**합니다.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

    로드 된 패키지에 이미 있는 경우 RODBC에 대 한 호출을 생략할 수 있습니다.

3. 모델의 이진 표현을 데이터베이스의 열에 저장 하는 PowerShell 스크립트로 만든 저장된 프로시저를 호출 합니다.

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

    테이블에 모델을 저장하는 경우 INSERT 문만 있으면 됩니다. 그러나 저장된 프로시저에서와 같은 줄이 바뀔 때 보다 쉽게는 _PersistModel_합니다.

    > [!NOTE]
    > 와 같은 오류가 발생 하는 경우 "EXECUTE 권한이 거부 되었습니다 PersistModel 개체에" 로그인 권한이 있는지 확인 합니다. 다음과 같은 T-SQL 문을 실행 하 여 방금 저장된 프로시저에 대 한 명시적 권한을 부여할 수 있습니다.`GRANT EXECUTE ON [dbo].[PersistModel] TO <user_name>`

4. 모델을 만든 후 데이터베이스에 저장을 호출할 수 있습니다에서 직접 [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저를 사용 하 여 코드 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

    그러나 자주 사용 하는 모든 모델을 사용자 지정 저장된 프로시저에서 입력된 쿼리 및 기타 매개 변수를 모델에 대 한 호출을 래핑하는 것이 쉽습니다.

    다음은 이러한 한 저장된 프로시저의 전체 코드입니다. 관리 및 업데이트에서 R 모델을 쉽게 수행할 수 있도록이 이와 같은 저장된 프로시저를 만드는 것이 좋습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

    ```tsql
    CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)
    AS
    BEGIN
      SET NOCOUNT ON;
      INSERT INTO nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
    END
    ```

  > [!NOTE]
  > 사용 하 여는 **SET NOCOUNT ON** 추가적인 결과 방지 하기 위해 절은 SELECT 문에서 방해 하지 않도록 설정 합니다.


다음 및 최종 단원에서 사용 하 여 저장 된 모델에 대 한 점수 매기기를 수행 하는 방법을 배웁니다 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.

## <a name="next-lesson"></a>다음 단원

[R 모델을 배포 하 고 SQL에서 사용](walkthrough-deploy-and-use-the-model.md)

## <a name="previous-lesson"></a>이전 단원

[R과 SQL을 사용 하 여 데이터 기능 만들기](walkthrough-create-data-features.md)


