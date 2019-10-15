---
title: sp_execute_external_script (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 6a7eb58883a94f1eb29d2c7e26e52768f4e08d9e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304931"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

프로시저에 대 한 입력 인수로 제공 된 스크립트를 실행 합니다. [확장성 프레임 워크](../../advanced-analytics/concepts/extensibility-framework.md)에서 스크립트가 실행 됩니다. 하나 이상의 확장이 있는 데이터베이스 엔진에서 지원 되는 등록 된 언어로 스크립트를 작성 해야 합니다. [**R**](../../advanced-analytics/concepts/extension-r.md), [**Python**](../../advanced-analytics/concepts/extension-python.md)또는 [ **Java** (SQL Server 2019 미리 보기 에서만)](../../advanced-analytics/java/extension-java.md). 

**Sp_execute_external_script**를 실행 하려면 먼저 `sp_configure 'external scripts enabled', 1;` 문을 사용 하 여 외부 스크립트를 사용 하도록 설정 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> Machine learning (R 및 Python) 및 프로그래밍 확장은 데이터베이스 엔진 인스턴스에 추가 기능으로 설치 됩니다. 특정 확장에 대 한 지원은 SQL Server 버전에 따라 다릅니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>구문

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>2017 및 이전 구문

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>인수
 **\@language** = N '*language*'  
 스크립트 언어를 나타냅니다. *language* 는 **sysname**입니다.  SQL Server 버전에 따라 유효한 값은 R (SQL Server 2016 이상), Python (SQL Server 2017 이상) 및 Java (SQL Server 2019 preview)입니다. 
  
 **\@script** = N '*script*' 외부 언어 스크립트를 리터럴 또는 변수 입력으로 지정 했습니다. *스크립트* 는 **nvarchar (max)** 입니다.  

`[ @input_data_1 =  N'input_data_1' ]`은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 형식으로 외부 스크립트에서 사용 하는 입력 데이터를 지정 합니다. *Input_data_1* 데이터 형식은 **nvarchar (max)** 입니다.

`[ @input_data_1_name = N'input_data_1_name' ]` @input_data_1로 정의 된 쿼리를 나타내는 데 사용 되는 변수의 이름을 지정 합니다. 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 입력 변수는 데이터 프레임입니다. Python의 경우 입력은 테이블 형식 이어야 합니다. *input_data_1_name* 는 **sysname**입니다.  기본값은 *Inputdataset*입니다.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` SQL Server 2019에만 적용 되며 파티션당 모델을 작성 하는 데 사용 됩니다. 결과 집합의 순서를 지정 하는 데 사용 되는 열의 이름을 지정 합니다. 예를 들어 제품 이름입니다. 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 입력 변수는 데이터 프레임입니다. Python의 경우 입력은 테이블 형식 이어야 합니다.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` SQL Server 2019에만 적용 되며 파티션당 모델을 작성 하는 데 사용 됩니다. 지리적 지역 또는 날짜와 같은 데이터를 분할 하는 데 사용 되는 열의 이름을 지정 합니다. 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 입력 변수는 데이터 프레임입니다. Python의 경우 입력은 테이블 형식 이어야 합니다. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`은 저장 프로시저 호출이 완료 될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 반환 될 데이터를 포함 하는 외부 스크립트의 변수 이름을 지정 합니다. 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 출력은 데이터 프레임 이어야 합니다. Python의 경우 출력은 pandas 데이터 프레임 이어야 합니다. *output_data_1_name* 는 **sysname**입니다.  기본값은 *Outputdataset*입니다.  

`[ @parallel = 0 | 1 ]` `@parallel` 매개 변수를 1로 설정 하 여 R 스크립트의 병렬 실행을 사용 하도록 설정 합니다. 이 매개 변수의 기본값은 0 (병렬 처리 없음)입니다. @No__t-0이 고 출력을 클라이언트 컴퓨터로 직접 스트리밍하는 경우에는 `WITH RESULT SETS` 절이 필요 하며 출력 스키마를 지정 해야 합니다.  

 + RevoScaleR 함수를 사용 하지 않는 R 스크립트의 경우, `@parallel` 매개 변수를 사용 하면 큰 데이터 집합을 처리 하는 데 도움이 될 수 있습니다 .이 경우 스크립트가 일반적으로 병렬 처리 될 수 있다고 가정 합니다. 예를 들어 모델에서 R `predict` 함수를 사용 하 여 새 예측을 생성 하는 경우 `@parallel = 1`을 쿼리 엔진에 대 한 힌트로 설정 합니다. 쿼리를 병렬화 할 수 있는 경우 행은 **MAXDOP** 설정에 따라 분산 됩니다.  
  
 + RevoScaleR 함수를 사용 하는 R 스크립트의 경우 병렬 처리는 자동으로 처리 되며 **sp_execute_external_script** 호출에 `@parallel = 1`을 지정 하면 안 됩니다.  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`은 외부 스크립트에서 사용 되는 입력 매개 변수 선언의 목록입니다.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`은 외부 스크립트에서 사용 하는 입력 매개 변수에 대 한 값의 목록입니다.  

## <a name="remarks"></a>설명

> [!IMPORTANT]
> 쿼리 트리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]으로 제어 되며 사용자는 쿼리에 대해 임의의 작업을 수행할 수 없습니다. 

**Sp_execute_external_script** 를 사용 하 여 지원 되는 언어로 작성 된 스크립트를 실행 합니다. 현재 지원 되는 언어는 SQL Server 2016 R Services에 대 한 R 이며 SQL Server 2017 Machine Learning Services 용 Python 및 R입니다. 

기본적으로이 저장 프로시저에서 반환 되는 결과 집합은 명명 되지 않은 열을 사용 하 여 출력 됩니다. 스크립트 내에서 사용 되는 열 이름은 스크립팅 환경에서 로컬로 사용 되며 출력 결과 집합에 반영 되지 않습니다. 결과 집합 열의 이름을로 설정 하려면 [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)의 `WITH RESULT SET` 절을 사용 합니다.
  
 결과 집합을 반환 하는 것 외에도 출력 매개 변수를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 스칼라 값을 반환할 수 있습니다. 다음 예에서는 OUTPUT 매개 변수를 사용 하 여 스크립트의 입력으로 사용 된 직렬화 된 R 모델을 반환 하는 방법을 보여 줍니다.  
  
외부 리소스 풀을 구성 하 여 외부 스크립트에서 사용 하는 리소스를 제어할 수 있습니다. 자세한 내용은 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)을 참조하세요. 작업에 대 한 정보는 리소스 관리자 카탈로그 뷰, DMV의 및 카운터에서 가져올 수 있습니다. 자세한 내용은 [Resource Governor 카탈로그 뷰 &#40;&#41;transact-sql](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor 관련 동적 관리 뷰 &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)및 [SQL Server, 외부 스크립트 개체](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)를 참조 하세요.  

### <a name="monitor-script-execution"></a>스크립트 실행 모니터링

[Sys. dm _external_script_cs_cs__l](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 및 [sys.](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>파티션 모델링에 대 한 매개 변수

 현재 공개 미리 보기로 제공 되는 SQL Server 2019에서는 분할 된 데이터에 대 한 모델링을 가능 하 게 하는 두 개의 추가 매개 변수를 설정할 수 있습니다. 분할 된 데이터에 대 한 데이터 집합을 만들고 사용 하는 논리 파티션으로 자연스럽 게 분할 하는 하나 이상의 열을 기반으로 스크립트를 실행 하는 동안에만 보존 기간, 성별, 지역, 날짜 또는 시간에 대 한 반복 값을 포함 하는 열은 분할 된 데이터 집합에 적합 한 몇 가지 예입니다.
 
 두 매개 변수는 **input_data_1_partition_by_columns** 및 **input_data_1_order_by_columns**입니다. 여기서 두 번째 매개 변수는 결과 집합을 정렬 하는 데 사용 됩니다. 매개 변수는 모든 파티션에 대해 한 번씩 실행 되는 외부 스크립트와 `sp_execute_external_script`에 대 한 입력으로 전달 됩니다. 자세한 내용 및 예제를 보려면 [Tutorial: 파티션 기반 모델 만들기 @ no__t-0.

 @No__t-0을 지정 하 여 스크립트를 병렬로 실행할 수 있습니다. 입력 쿼리를 병렬화 할 수 있는 경우 인수를 `sp_execute_external_script`로 설정 하 `@parallel=1`을 설정 해야 합니다. 기본적으로 쿼리 최적화 프로그램은 256 개 이상의 행이 있는 테이블에서 `@parallel=1`으로 작동 하지만이를 명시적으로 처리 하려는 경우이 스크립트에는 매개 변수가 데모용으로 포함 됩니다.

 > [!Tip]
> 교육 회사의 경우 임의의 학습 스크립트와 함께 `@parallel`을 사용할 수 있습니다 .이 경우에도 비 Microsoft rx 알고리즘이 사용 됩니다. 일반적으로 RevoScaleR 알고리즘 (rx 접두사 포함)만 SQL Server의 학습 시나리오에서 병렬 처리를 제공 합니다. 하지만 SQL Server vNext의 새 매개 변수를 사용 하 여 해당 기능으로 구체적으로 엔지니어링 되지 않은 함수를 호출 하는 스크립트를 병렬화 할 수 있습니다.
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>R 및 Python 스크립트에 대 한 스트리밍 실행  

스트리밍을 사용 하면 R 또는 Python 스크립트가 메모리 크기에 적합 한 것 보다 많은 데이터를 사용할 수 있습니다. 스트리밍 중에 전달 되는 행 수를 제어 하려면 매개 변수에 대 한 정수 값을 지정 합니다 (`@params` 컬렉션에서 `@r_rowsPerRead`).  예를 들어 매우 넓은 데이터를 사용 하는 모델을 학습 하는 경우에는 값을 조정 하 여 모든 행이 하나의 데이터 청크로 전송 될 수 있도록 해야 합니다. 이 매개 변수를 사용 하 여 서버 성능 문제를 완화 하기 위해 한 번에 읽고 처리 되는 행 수를 관리할 수도 있습니다. 
  
스트리밍에 대 한 `@r_rowsPerRead` 매개 변수와 `@parallel` 인수는 모두 힌트로 간주 되어야 합니다. 힌트를 적용 하려면 병렬 처리를 포함 하는 SQL 쿼리 계획을 생성할 수 있어야 합니다. 이렇게 할 수 없는 경우 병렬 처리를 사용 하도록 설정할 수 없습니다.  
  
> [!NOTE]  
>  스트리밍 및 병렬 처리는 Enterprise Edition 에서만 지원 됩니다. 오류를 발생 시 키 지 않고 표준 버전의 쿼리에 매개 변수를 포함할 수 있지만 매개 변수는 영향을 주지 않으며 R 스크립트는 단일 프로세스로 실행 됩니다.  
  
## <a name="restrictions"></a>Restrictions  


### <a name="data-types"></a>데이터 형식

다음 데이터 형식은 **sp_execute_external_script** 프로시저의 입력 쿼리 또는 매개 변수에 사용 될 때 지원 되지 않으며 지원 되지 않는 형식 오류를 반환 합니다.  

해결 방법으로, 열 또는 값을 외부 스크립트로 보내기 전에 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 지원 되는 형식으로 **캐스팅** 합니다.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **time**  
  
-   **sql_variant**  
  
-   **text**, **image**  
  
-   **xml**  
  
-   **hierarchyid**, **geometry**, **geography**  
  
-   CLR 사용자 정의 형식

일반적으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식에 매핑할 수 없는 결과 집합은 NULL로 출력 됩니다.  

### <a name="restrictions-specific-to-r"></a>R에 한정 되는 제한 사항

입력에 R에서 허용 되는 값 범위에 맞지 않는 **datetime** 값이 포함 된 경우 값은 **NA**로 변환 됩니다. @No__t-0은 R 언어에서 지원 되는 것 보다 더 큰 범위의 값을 허용 하기 때문에 필요 합니다.

두 언어 모두 IEEE 754를 사용 하는 경우에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Float 값 (예: `+Inf`, `-Inf`, `NaN`)은 지원 되지 않습니다. 현재 동작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 직접 값을 보냅니다. 따라서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 SQL 클라이언트는 오류를 throw 합니다. 따라서 이러한 값은 **NULL**로 변환 됩니다.

## <a name="permissions"></a>사용 권한

**EXECUTE ANY EXTERNAL SCRIPT** database 권한이 필요 합니다.  

## <a name="examples"></a>예

이 섹션에는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용 하 여 R 또는 Python 스크립트를 실행 하기 위해이 저장 프로시저를 사용 하는 방법의 예제가 포함 되어 있습니다.

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. SQL Server으로 R 데이터 집합 반환  

다음 예에서는 **sp_execute_external_script** 를 사용 하 여 R에 포함 된 iri 데이터 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 반환 하는 저장 프로시저를 만듭니다.  

```sql
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
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>2\. SQL Server의 데이터를 기반으로 R 모델 생성  

다음 예에서는 **sp_execute_external_script** 를 사용 하 여 조리개 모델을 생성 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 모델을 반환 하는 저장 프로시저를 만듭니다.  

> [!NOTE]
>  이 예에서는 e1071 패키지를 미리 설치 해야 합니다. 자세한 내용은 [SQL Server에 추가 R 패키지 설치](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)를 참조 하세요.

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
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
GO
```

Python을 사용하여 비슷한 모델을 생성하려면 언어 식별자를 `@language=N'R'`에서 `@language = N'Python'`으로 변경하고 `@script` 인수를 필요한 대로 수정합니다. 그렇지 않으면 모든 매개 변수가 R과 똑같이 작동합니다.

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>3\. Python 모델을 만들고 점수를 생성 합니다.

이 예제에서는 sp\_execute\_external\_script를 사용하여 간단한 Python 모델에서 점수를 생성하는 방법을 보여줍니다. 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Python 코드에서 사용 되는 열 머리글은 SQL Server로 출력 되지 않습니다. 따라서 WITH RESULT 문을 사용 하 여 SQL에서 사용할 열 이름과 데이터 형식을 지정 합니다.

점수 매기기의 경우 네이티브 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 함수를 사용할 수도 있으며, 이 함수는 Python 또는 R 런타임 호출을 방지하기 때문에 일반적으로 더 빠릅니다.

## <a name="see-also"></a>참조

 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 라이브러리 및 데이터 형식](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 라이브러리 및 R 데이터 형식](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [SQL Server Machine Learning Services @no__t에 대 한 알려진 문제](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)-1  
 [외부 라이브러리 &#40;transact-sql 만들기&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [External Scripts Enabled 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server, External Scripts 개체](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
