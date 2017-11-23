---
title: sp_execute_external_script (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs: TSQL
helpviewer_keywords: sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d437e6e8d86aa648d9c6ef11a8ca04297cafbaf3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  외부 위치에 대 한 인수로 제공 된 스크립트를 실행 합니다. 지원 / 등록 언어로 스크립트를 작성 되어야 합니다. 쿼리 트리에 의해 제어 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 쿼리에서 임의 작업을 수행할 수 없습니다. 실행 하려면 **sp_execute_external_script**를 사용 하 여 외부 스크립트를 먼저 활성화 해야 합니다는 `sp_configure 'external scripts enabled', 1;` 문.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_execute_external_script   
    @language = N'language,   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]   
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```  
  
## <a name="arguments"></a>인수  
 @language= N'*언어*'  
 스크립트 언어를 나타냅니다. *언어* 은 **sysname**합니다.  

 유효한 값은 `Python` 또는 `R`합니다. 
  
 @script= N'*스크립트*'  
 리터럴 또는 변수 입력으로 지정 하는 외부 언어 스크립트입니다. *스크립트* 은 **nvarchar (max)**합니다.  
  
 [ @input_data_1_name = N'*input_data_1_name*']  
 정의 된 쿼리를 나타내는 데 사용 된 변수의 이름을 지정 @input_data_1합니다. 외부 스크립트의 변수 데이터 형식이 언어에 따라 달라 집니다. R을 입력된 변수는 데이터 프레임입니다. Python의 경우 입력은 테이블 형식 이어야 합니다. *input_data_1_name* 은 **sysname**합니다.  
  
 기본값은 "InputDataSet"입니다.  
  
 [ @input_data_1 = N'*input_data_1*']  
 외부 스크립트의 형태로 사용 하는 입력된 데이터를 지정 된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 합니다. *input_data_1* 은 **nvarchar (max)**합니다.  
  
 [ @output_data_1_name = N'*output_data_1_name*']  
 반환할 데이터를 포함 하는 외부 스크립트에서 변수의 이름을 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 저장된 프로시저 호출이 완료 되 면입니다. 외부 스크립트의 변수 데이터 형식이 언어에 따라 달라 집니다. R을 출력 데이터 프레임 반드시 있어야 합니다. Python의 경우 출력 데이터 프레임 팬더 이어야 합니다. *output_data_1_name* 은 **sysname**합니다.  
  
 기본값은 "OutputDataSet"입니다.  
  
 [ @parallel = 0 | 1 ]  
 설정 하 여 R 스크립트의 병렬 실행을 사용 하도록 설정 된 `@parallel` 매개 변수를 1입니다. 이 매개 변수에 대 한 기본값은 0 (병렬 처리).  
  
 RevoScaleR 함수를 사용 하 여 사용 하지 않는 R 스크립트는 `@parallel` 매개 변수를 스크립트 다르거나 일반적으로 평행 화할 수 가정 하면 큰 데이터 집합을 처리 하기 위해 도움이 될 수 있습니다. 예를 들어, R을 사용 하는 경우 `predict` 새 예측을 생성을 설정 하는 모델로 함수 `@parallel = 1` 쿼리 엔진에 제공 합니다. 쿼리를 병렬화 할 수 있는 경우 행이에 따라 배포 되는 **MAXDOP** 설정 합니다.  
  
 경우 `@parallel = 1` 및 클라이언트 컴퓨터에 직접 스트리밍되는 출력 면 `WITH RESULTS SETS` 절이 필요 하 고 출력 스키마를 지정 해야 합니다.  
  
 RevoScaleR 함수를 사용 하는 R 스크립트에 대 한 병렬 처리는 자동으로 처리 하 고 지정 하면 안 `@parallel = 1` 에 **sp_execute_external_script** 호출 합니다.  
  
 [ @params = N' *@parameter_name data_type* [아웃 | 출력] [,...n]']  
 외부 스크립트에 사용 되는 입력된 매개 변수 선언의 목록입니다.  
  
 [ @parameter1 = '*value1*' [아웃 | 출력] [,...n]]  
 목록에 대 한 외부 스크립트에서 사용 하는 입력된 매개 변수 값입니다.  


## <a name="remarks"></a>주의  
 **sp_execute_external_script** 를 사용하여 R 등의 지원되는 언어로 작성된 스크립트를 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 설치되는 서버 구성 요소와, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 고성능 환경에 데이터 기술자를 연결해 주는 워크스테이션 도구 및 연결 라이브러리 집합으로 구성됩니다. R Services (In-database) 하는 동안 설치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R 스크립트를 실행할 수 있도록 설정 하려면. 자세한 내용은 참조 [SQL Server R Services &#40; 데이터베이스에서 &#41; 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)합니다.  
  
 외부 리소스 풀을 구성 하 여 외부 스크립트 사용 하는 리소스를 제어할 수 있습니다. 자세한 내용은 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)을 참조하세요. 리소스 관리자 카탈로그 뷰, DMV, 및 카운터에서 작업 하는 방법에 대 한 정보를 가져올 수 있습니다. 자세한 내용은 참조 [리소스 관리자 카탈로그 뷰 &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [리소스 관리자 관련 동적 관리 뷰 &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md), 및 [SQL Server, 외부 스크립트 개체](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)합니다.  

사용 하 여 모니터 스크립트 실행 [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 및 [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)합니다. 

 기본적으로이 저장된 프로시저에서 반환 된 결과 집합 명명 되지 않은 열을 사용 하 여 출력 됩니다. 스크립트 내에서 사용 되는 열 이름과 스크립팅 환경에 로컬 이며 출력된 결과 집합에 반영 되지 않습니다. 결과 집합 열 이름, 사용 된 `WITH RESULTS SET` 절 [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md)합니다.
  
 결과 집합을 반환할 뿐만 아니라를 R 스크립트에서 스칼라 값을 반환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 출력 매개 변수를 사용 합니다. 다음 예제에서는 출력 매개 변수 사용을 보여 줍니다.  
  
```  
DECLARE @model varbinary(max);  
EXEC sp_execute_external_script  
        @language = N'R'  
        , @script = N'  
    # build classification model to predict tipped or not  
    logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource, family = binomial(link=logit));  
  
    # First, serialize a model and put it into a database table  
    modelbin <- serialize(logitObj, NULL);  
    '  
        , @input_data_1 = N'  
SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance  
  FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)  
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d  
'  
        , @input_data_1_name = N'featureDataSource'  
        , @params = N'@modelbin varbinary(max) OUTPUT'  
        , @modelbin = @model OUTPUT;  
```  


## <a name="streaming-execution-for-r-script"></a>R 스크립트에 대 한 스트리밍 실행  
 지정 하 여 R 스크립트 실행의 스트리밍을 지원 `@r_rowsPerRead int parameter` 에 `@params` 컬렉션입니다.  스트리밍 R 스크립트를 메모리에 맞지 않는 데이터에 사용할 수 있습니다. 예를 들어 십억 행이 사용 하 여 점수 predict 함수는 새 `@r_rowsPerRead` 를 한 번에 한 개의 스트림에 실행 분할 매개 변수를 사용할 수 있습니다. 이 매개 변수 R 프로세스에 보내는 행 수를 제어 하므로 한 번에 읽어오는 행의 수를 제한 하 사용할 수도 있습니다. 이 경우 큰 모델을 학습 하는 예를 들어 서버 성능 문제를 완화 시킬 수 있습니다. Note이 매개 변수는 R 스크립트의 출력을 읽거나 행의 전체 집합으로 확인에 의존 하지는 없는 경우에만 사용할 수 있습니다.  
  
 두는 `@r_rowsPerRead` 스트리밍에 대 한 매개 변수 및 `@parallel` 인수 힌트 고려해 야 합니다. 적용할 힌트에 대 한 병렬 처리를 포함 하는 SQL 쿼리 계획을 생성할 수 있어야 합니다. 없는 경우에 병렬 처리를 사용할 수 없습니다.  
  
> [!NOTE]  
>  스트리밍 및 병렬 처리는 Enterprise Edition 에서만에서 지원 됩니다. 오류를 생성 하지 않고 Standard Edition에서는 쿼리에서 매개 변수를 포함할 수 있습니다 하지만 매개 변수 없는 효과 및 단일 프로세스에서 실행 되는 R 스크립트.  
  
## <a name="restrictions"></a>제한 사항  
 **데이터 형식:** 입력된 쿼리 또는의 매개 변수에서 사용 하는 경우 다음 데이터 형식은 지원 되지 않습니다 `sp_execute_external_script` 프로시저와 지원 되지 않는 유형이 오류를 반환 합니다.  
  
 이 문제를 해결 **캐스트** 열 또는 값에 지원 되는 형식으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 오른쪽에 보냅니다  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **시간**  
  
-   **sql_variant**  
  
-   **텍스트**, **이미지**  
  
-   **xml**  
  
-   **hierarchyid**, **geometry**, **geography**  
  
-   CLR 사용자 정의 형식  
  
 **날짜/시간** 입력의 값 때문에 이것이 필요 R에서 값의 허용 범위를 맞지 않는 값에 대 한 R 쪽 NA로 변환 되 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 더 큰 범위의 값 R 언어에서 지원 되는 것을 허용 합니다.  
  
 부동 소수점 값 (예를 들어 + Inf,-Inf, NaN)에서 지원 되지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어를 모두 사용 하는 IEEE 754도 합니다. 현재 동작 값을 보낸 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 직접 및 다른 이름으로 결과 sqlclient에 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 오류를 throw 합니다. 이러한 값은 **NULL**합니다.  
  
 에 매핑할 수 없는 모든 R 결과 집합이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식이 NULL로 출력 합니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 **EXECUTE ANY EXTERNAL SCRIPT** 데이터베이스 사용 권한을 합니다.  
  
## <a name="examples"></a>예  
 이 섹션에는 사용 하 여 R 스크립트를 실행 하려면이 저장된 프로시저를 사용할 수 있는 방법을의 예가 포함 되어 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.  
  
### <a name="a-return-a-data-set-from-r-to-sql-server"></a>1. R에서 SQL Server로 데이터 집합을 반환  
 다음 예제에서는 사용 하는 저장된 프로시저 **sp_execute_external_script** r 된 iris 데이터 집합을 반환할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
```  
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset  
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'  
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'  
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;  
go  
```  
  
### <a name="b-generate-a-model-based-on-data-from-sql-server"></a>2. SQL Server에서 데이터를 기반으로 모델을 생성 합니다.  
 다음 예제에서는 사용 하는 저장된 프로시저 **sp_execute_external_script** iris 모델을 생성 하 고 모델을 반환 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
> [!NOTE]  
>  이 예제에서는 e1071 패키지를 설치 합니다. 자세한 내용은 참조 [SQL Server에 추가 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)합니다.  
  
```  
DROP PROC IF EXISTS generate_iris_model;  
go  
  
CREATE PROC generate_iris_model  
AS  
BEGIN  
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;  
go  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 라이브러리 및 데이터 형식](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 라이브러리 및 R 데이터 형식](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R Services에 대 한 알려진된 문제](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [외부 라이브러리 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [external scripts enabled 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server, External Scripts 개체](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
  
