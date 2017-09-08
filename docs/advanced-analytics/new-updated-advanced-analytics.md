---
title: "업데이트-SQL Server 문서에 대 한 고급 분석 | Microsoft Docs"
description: "코드 조각에 최근에 변경 된 설명서, Microsoft SQL Server에 대 한 고급 분석에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/17/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79f979ecda1ff0851978d19ef28fa3cf909f9a43
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>새로 추가 되거나 최근에 업데이트 된: SQL Server에 대 한 고급 분석



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:* &nbsp; **2017-05-23** &nbsp; ~ &nbsp; **2017-07-17**
- *주제 영역:* &nbsp; **SQL Server에 대 한 고급 분석**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [일반적인 문제를 외부 스크립트 실행](common-issues-external-script-execution.md)
2. [기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)
3. [SQL Server Python 자습서](tutorials/sql-server-python-tutorials.md)
4. [SQL Server R 자습서입니다.](tutorials/sql-server-r-tutorials.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 업데이트된 모든 문서로 연결되는 링크가 있습니다.



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>1. &nbsp;[Revoscalepy 소개](python/what-is-revoscalepy.md)

*업데이트됨: 2017-06-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 112.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cab7330ac9944508aaa360e00cbc2e866455776d 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a  (PR=2171  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**MicrosoftML revoscalepy 사용**


MicrosoftML에 대 한 Python 함수는 계산 컨텍스트 및 revoscalepy에 제공 되는 데이터 소스와 통합 됩니다. 따라서 MicrosoftML 알고리즘을 사용 하 여 정의 하 고, Python에서 모델을 학습 하 고 revoscalepy 함수를 사용 하 여 로컬 또는 SQl Server 계산 컨텍스트에서 Python 코드를 실행 수 없습니다.

Python 코드의 모듈에서는 가져와 다음 필요한 개별 함수를 참조 합니다.

```
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**요구 사항**


SQL Server에서 Python 코드를 실행 하려면 먼저 설치 해야 SQL Server 2017를 기능과 함께 **컴퓨터 학습 서비스**, Python 언어를 사용 하도록 설정 합니다. 이전 버전의 SQL Server는 Python 통합을 지원 하지 않습니다.

> [!NOTE]
> Python의 오픈 소스 배포에서 SQL Server 계산 컨텍스트를 지원 하지 않습니다. 그러나 게시 하 고 Windows에서 Python 응용 프로그램을 사용 해야 할 경우 SQL Server를 설치 하지 않고 Microsoft 컴퓨터 학습 서버를 설치할 수 있습니다. 자세한 내용은 [만들기는 독립 실행형 R 서버-..를 참조 합니다. /r/create-a-standalone-r-server.md)

**자세한 도움말 보기**





&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-step-5-train-and-save-a-model-using-t-sqltutorialssqldev-py5-train-and-save-a-model-using-t-sqlmd"></a>2. &nbsp;[5 단계: 교육 및 T-SQL을 사용 하는 모델 저장](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)

*업데이트 됨된: 2017-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 121.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c1cbe92282b96105ffdb69efa803f58dc0ac7e2 e4077a2154a90de468c435efa5b2225125d5b0e7  (PR=1904  ,  Filename=sqldev-py5-train-and-save-a-model-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



1. [! INCLUDE [ssManStudio... /.. /includes/ssmanstudio-md.md)], 새 쿼리 창 열기 및 저장된 프로시저를 만들려면 다음 문을 실행 _TrainTipPredictionModelRxPy_합니다.  이 모델은 지금까지 준비한 학습 데이터에 따라 달라 집니다. 에 이미 저장된 프로시저는 입력된 데이터의 정의 포함 되므로 입력된 쿼리를 제공할 필요가 없습니다.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    ```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-step-6-operationalize-the-modeltutorialssqldev-py6-operationalize-the-modelmd"></a>3. &nbsp;[6 단계: 모델을 운용](tutorials/sqldev-py6-operationalize-the-model.md)

*업데이트 됨된: 2017-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_2) | [다음](#TitleNum_4))

<!-- Source markdown line 236.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1eb50ac902d4e80bafb1dd7fdf8f607dcdf0d33f 57d5abdc6119db1ecd81587d625054a5bbfb5fc8  (PR=1904  ,  Filename=sqldev-py6-operationalize-the-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



다음은 사용 하 여 점수 매기기를 수행 하는 저장된 프로시저의 정의 **revoscalepy** 모델입니다.

```
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures-- 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>4. &nbsp;[모델을 만드는 revoscalepy Python 사용](tutorials/use-python-revoscalepy-to-create-model.md)

*업데이트 됨된: 2017-06-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_3))

<!-- Source markdown line 119.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0886939f86fe12d7ff7b339689a02c7fc75e0786 23dd469349a05d535063aab3c14aec152ed2cd7b  (PR=2141  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=76839e39427e24688609353b8708d59fee772d28) -->



**코드 검토**


코드 검토 하 고 몇 가지 주요 단계를 강조 표시 해 보겠습니다.

**원본 및 계산 컨텍스트는 데이터 정의**


이 중요 한 부분을 사용 하 여 **revoscalepy** 및 해당 관련 된 R 패키지가 **RevoScaleR**합니다. 데이터 소스는 한 계산 컨텍스트와에서 다릅니다. _데이터 소스_ 코드에 사용 되는 데이터를 정의 합니다. _계산 컨텍스트_ 코드의 실행 수는 위치를 정의 합니다.

> [!NOTE]
> 시험판 버전에서 RevoScaleR에서 지원 되는 일부 데이터 원본 형식에 대 한 지원이 제한 될 수 있습니다. 최신 버전에 포함 된 함수에 대 한 자세한 내용은 참조 [이란 revoscalepy... /python/what-is-revoscalepy.md)입니다.

전체 만들기 및 데이터 원본을 사용 하 여 처리 및 계산 컨텍스트는 다음과 같습니다.

1. 과 같은 Python 변수를 만들 _sqlQuery_ 및 _connectionString_, 원본 및 사용 하려는 데이터를 정의 하는 합니다. 이러한 변수를 전달 하는 **RxSqlServerData** 생성자를 구현 하는 **데이터 원본 개체** 라는 _dataSource_합니다.
2. 계산 컨텍스트 개체를 사용 하 여 만들는 **RxInSqlServer** 생성자입니다. 이 예제에서는 계산 컨텍스트로 써 사용 하 여 동일한 SQL Server 인스턴스에서 데이터를 가정 하에서 이전에 정의 된 동일한 연결 문자열을 전달 합니다. 그러나 데이터 원본 및 계산 컨텍스트 서로 다른 서버에 있을 수 있습니다. 그 결과 **컨텍스트 개체를 계산** 라는 _computeContext_합니다.
3. 현재 계산 컨텍스트를 선택 합니다. 기본적으로 즉, 다른 계산 컨텍스트를 지정 하지 않으면 작업을 로컬로 실행 하 고 데이터 원본에서 인출 되는 데이터가 모델 맞춤 현재 Python 환경에서 실행 됩니다.

    RevoScaleR을 있습니다 사용할 수도 함수 `rxSetComputeContext` 계산 컨텍스트를 전환할 수 있습니다. 미리 보기 버전에서 함수는 아직 구현 되지 **revoscalepy**, 인수를 계산 컨텍스트를 지정할 수 있지만 **rx_lin_mod_ex**합니다.





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>유사한 문서

이 섹션에는 동일한 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(4+4) : **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(2+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(1+2): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(6+0): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(13+2): **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(8+4): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(2+2): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(1+0): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


&nbsp;


