---
title: "4단원: 모델 작성 및 저장(데이터 과학 종단 간 연습) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# 4단원: 모델 작성 및 저장(데이터 과학 종단 간 연습)
이 단원에서는 Machine Learning 모델을 작성하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장하는 방법을 알아봅니다.  
  
## <a name="creating-a-classification-model"></a>분류 모델 만들기  
작성할 모델은 택시 기사가 특정 여정에서 팁을 받을 가능성이 있는지 여부를 예측하는 이진 분류자입니다. 이전 단원에서 만든 데이터 원본 `featureDataSource,` 를 사용하여 로지스틱 회귀를 통해 팁 분류자를 학습합니다.  
  
모델에서 사용할 기능은 다음과 같습니다.  
  
-   passenger_count  
  
-   trip_distance  
  
-   trip_time_in_secs  
  
-   direct_distance  

### <a name="create-the-model-using-rxlogit"></a>rxLogit를 사용하여 모델 만들기  
1.  **RevoScaleR** 패키지에 포함된 *rxLogit* 함수를 호출하여 로지스틱 회귀 모델을 만듭니다.  
  
    ```R  
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource))    
    ```  
  
2.  모델을 작성한 후 `summary` 함수를 사용하여 검사하고 계수를 확인하는 것이 좋습니다.  
  
    ```  
    summary(logitObj)  
    ```  

     *Results*

     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*  
     *direct_distance*  
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
  
### <a name="use-the-logistic-regression-model-for-scoring"></a>점수 매기기에 로지스틱 회귀 모델 사용  
이제 모델이 작성되었으므로 모델을 사용하여 기사가 특정 여정에서 팁을 받을 가능성이 있는지 여부를 예측할 수 있습니다.  
  
1.  먼저 점수 매기기 결과를 저장하는 데 사용할 데이터 개체를 정의합니다.  
  
    ```R  
    scoredOutput <- RxSqlServerData(  
      connectionString = connStr,  
      table = "taxiScoreOutput"  )  
    ```  
    + 이 예제를 보다 간소화하기 위해 로지스틱 회귀 모델에 대한 입력은 모델 학습에 사용한 것과 동일한 `featureDataSource` 입니다.  대체로 점수를 매길 새 데이터가 있거나, 테스트 및 학습을 위해 일부 데이터를 따로 보관했을 수 있습니다.  
  
    + 예측 결과는 _taxiscoreOutput_테이블에 저장됩니다. 이 테이블에 대한 스키마는 `rxSqlServerData`를 사용하여 테이블을 만들 때 정의되지 않고 *의* scoredOutput `rxPredict`개체 출력에서 가져옵니다.  
  
    + 예측된 값을 저장하는 테이블을 만들려면 `rxSqlServer` 데이터 함수를 실행하는 SQL 로그인에 데이터베이스에 대한 DDL 권한이 있어야 합니다. 로그인이 테이블을 만들 수 없는 경우에는 문이 실패합니다.  
  
2.  *rxPredict* 함수를 호출하여 결과를 생성합니다.  
  
    ```R  
    rxPredict(modelObject = logitObj, data = featureDataSource, outData = scoredOutput,   
                       predVarNames = "Score", type = "response",   
                       writeModelVars = TRUE, overwrite = TRUE)  
    ```  

  
## <a name="plotting-model-accuracy"></a>모델 정확도 그리기  
모델의 정확도를 파악하기 위해 *rxRocCurve* 함수를 사용하여 수신기 운영 곡선을 그릴 수 있습니다. *rxRocCurve*는 RevoScaleR 패키지에서 제공하는 새 함수 중 하나로, 원격 계산 컨텍스트를 지원하기 때문에 다음 두 가지 옵션이 있습니다.  
  
+ `rxRocCurve` 함수를 사용하여 원격 컴퓨터 컨텍스트에서 그림을 실행한 다음 로컬 클라이언트에 그림을 반환할 수 있습니다.
+ 데이터를 R 클라이언트 컴퓨터로 가져온 후 다른 R 그리기 함수를 사용하여 성능 그래프를 만들 수도 있습니다.  
  
이 섹션에서는 두 가지 방법을 모두 사용합니다.  
  
### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>원격(SQL Server) 계산 컨텍스트에서 그림 실행  
  
1.  *rxRocCurve* 함수를 호출하고 이전에 정의된 데이터를 입력으로 제공합니다.  
  
    ```R  
    rxRocCurve( "tipped", "Score", scoredOutput)  
    ```  
  
    또한 레이블 열 tipped(예측할 변수) 및 예측을 저장할 열 이름(_Score_)을 지정해야 합니다.  
  
2.  R 그래픽 장치를 열거나 RStudio에서 **그리기** 창을 클릭하여 생성된 그래프를 볼 수 있습니다.  
  
    ![ROC plot for the model](../../advanced-analytics/r-services/media/rsql-e2e-rocplot.png "ROC plot for the model")  

    이 그래프는 원격 계산 컨텍스트에서 생성된 다음 R 환경으로 반환됩니다.   
    
### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>SQL Server에서 데이터를 사용하여 로컬 계산 컨텍스트에서 그림 만들기  
  
1.  *rxImport* 함수를 사용하여 지정된 데이터를 로컬 R 환경으로 가져옵니다.  
  
    ```R  
    scoredOutput = rxImport(scoredOutput)  
    ```  
  
2.  로컬 메모리에 데이터를 로드한 후 **ROCR** 라이브러리를 호출하여 일부 예측을 만들고 그림을 생성할 수 있습니다.  
  
    ```R  
    library('ROCR')  
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped)  
  
    acc.perf = performance(pred, measure = 'acc')  
    plot(acc.perf)  
    ind = which.max( slot(acc.perf, 'y.values')[[1]] )  
    acc = slot(acc.perf, 'y.values')[[1]][ind]  
    cutoff = slot(acc.perf, 'x.values')[[1]][ind]  
    ```  
  
3.  두 경우 모두 다음 그림이 생성됩니다.  
  
    ![plotting model performance using R](../../advanced-analytics/r-services/media/rsql-e2e-performanceplot.png "plotting model performance using R")  
  
## <a name="deploying-a-model"></a>모델 배포  

모델을 빌드하고 성능이 양호하다고 결정한 경우 모델을 *운영화*할 수 있습니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 R 모델을 호출할 수 있으므로 클라이언트 응용 프로그램에서 R을 쉽게 사용할 수 있습니다.  
  
그러나 외부 응용 프로그램에서 모델을 호출하려면 먼저 프로덕션에서 사용되는 데이터베이스에 모델을 저장해야 합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서는 학습된 모델이 **varbinary(max)**형식의 단일 열에 이진 형식으로 저장됩니다.

따라서 학습된 모델을 R에서 SQL Server로 이동하는 단계는 다음과 같습니다.  
  
+ 16진수 문자열로 모델 직렬화
+ 직렬화된 개체를 데이터베이스로 전송
+ varbinary(max) 열에 모델 저장  
  
이 섹션에서는 모델을 저장하는 방법 및 모델을 호출하여 예측하는 방법을 알아봅니다.  
  
### <a name="serialize-the-model"></a>모델 serialize  
  
+  로컬 R 환경에서 모델을 serialize하고 변수에 저장합니다.  
  
    ```R  
    modelbin <- serialize(logitObj, NULL)  
    modelbinstr=paste(modelbin, collapse="")  
    ```  
  
    *serialize* 함수는 R **base** 패키지에 포함되어 있으며, 연결로 직렬화하기 위한 간단한 하위 수준 인터페이스를 제공합니다. 자세한 내용은 [http://www.inside-r.org/r-doc/base/serialize](http://www.inside-r.org/r-doc/base/serialize)를 참조하세요.  
  
### <a name="move-the-model-to-sql-server"></a>SQL Server로 모델 이동

+ ODBC 연결을 열고, 저장 프로시저를 호출하여 모델의 이진 표현을 데이터베이스 열에 저장합니다. 
  
    ```R  
    library(RODBC)  
    conn <- odbcDriverConnect(connStr )  
  
    # persist model by calling a stored procedure from SQL  
    q<-paste("EXEC PersistModel @m='", modelbinstr,"'", sep="")  
    sqlQuery (conn, q)    
    ```  

테이블에 모델을 저장하는 경우 INSERT 문만 있으면 됩니다. 그러나 해당 작업이 더 쉽지만 여기서는 _PersistModel_ 저장 프로시저를 사용합니다. 
 
참조를 위해 저장 프로시저의 전체 코드는 다음과 같습니다.  
  
```tsql  
CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)  
AS  
BEGIN  
        -- SET NOCOUNT ON added to prevent extra result sets from  
        -- interfering with SELECT statements.  
        SET NOCOUNT ON;  
        insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))  
END   
```  
> [!TIP] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 모델을 더 쉽게 관리 및 업데이트할 수 있으므로 이 저장 프로시저와 같은 도우미 함수를 만드는 것이 좋습니다.  
  
  
### <a name="invoke-the-saved-model"></a>저장된 모델 호출  
데이터베이스에 모델을 저장한 후 시스템 저장 프로시저 [sp_execute_external_script&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에서 직접 호출할 수 있습니다.  
  
예를 들어 예측을 생성하려면 데이터베이스에 연결한 다음 일부 입력 데이터와 함께 저장된 모델을 입력으로 사용하는 저장 프로시저를 실행하면 됩니다.  
  
그러나 자주 사용하는 모델이 있는 경우 입력 쿼리 및 모델 호출과 다른 모든 매개 변수를 사용자 지정 저장 프로시저에 래핑하는 것이 더 편리합니다.  
  
다음 단원에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 저장된 모델에 대해 점수 매기기를 수행하는 방법을 알아봅니다.  
  
## <a name="next-lesson"></a>다음 단원  
[5단원: 모델 배포 및 사용&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>이전 단원  
[3단원: 데이터 기능 만들기&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
