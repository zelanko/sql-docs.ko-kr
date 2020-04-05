---
title: sp_execute_external_script (거래 -SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 8800df26e505f1fffe25e6f65218481e7a8158f0
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80663007"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**sp_execute_external_script** 저장 프로시저는 프로시저에 입력 인수로 제공된 스크립트를 실행하고 [기계 학습 서비스](../../machine-learning/index.yml) 및 언어 확장과 함께 [사용됩니다.](../../language-extensions/language-extensions-overview.md) 

기계 학습 서비스의 경우 [파이썬](../../machine-learning/concepts/extension-python.md) 및 [R이](../../machine-learning/concepts/extension-r.md) 지원되는 언어입니다. 언어 확장의 경우 Java가 지원되지만 [외부 언어 만들기로](../../t-sql/statements/create-external-language-transact-sql.md)정의되어야 합니다.

**sp_execute_external_script**실행하려면 먼저 기계 학습 서비스 또는 언어 확장을 설치해야 합니다. 자세한 내용은 Windows 및 [Linux에 SQL Server 기계 학습 서비스 설치(파이썬 및 R)](../../machine-learning/install/sql-machine-learning-services-windows-install.md) 또는 Windows 및 [Linux에](../../linux/sql-server-linux-setup-machine-learning.md)SQL Server 언어 확장 프로그램을 [설치를](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md) 참조하십시오. [Linux](../../linux/sql-server-linux-setup-language-extensions.md)
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**sp_execute_external_script** 저장 프로시저는 프로시저에 입력 인수로 제공된 스크립트를 실행하고 SQL Server 2017의 [기계 학습 서비스와](../../machine-learning/index.yml) 함께 사용됩니다. 

기계 학습 서비스의 경우 [파이썬](../../machine-learning/concepts/extension-python.md) 및 [R이](../../machine-learning/concepts/extension-r.md) 지원되는 언어입니다. 

**sp_execute_external_script**실행하려면 먼저 기계 학습 서비스를 설치해야 합니다. 자세한 내용은 [Windows에서 SQL Server 기계 학습 서비스(파이썬 및 R) 설치를](../../machine-learning/install/sql-machine-learning-services-windows-install.md)참조하십시오.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**sp_execute_external_script** 저장 프로시저는 프로시저에 입력 인수로 제공된 스크립트를 실행하고 SQL Server 2016의 [R 서비스와](../../machine-learning/r/sql-server-r-services.md) 함께 사용됩니다.

R 서비스의 경우 [R은](../../machine-learning/concepts/extension-r.md) 지원되는 언어입니다.

**sp_execute_external_script**실행하려면 먼저 R 서비스를 설치해야 합니다. 자세한 내용은 [Windows에서 SQL Server 기계 학습 서비스(파이썬 및 R) 설치를](../../machine-learning/install/sql-r-services-windows-install.md)참조하십시오.
::: moniker-end

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

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
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>2017년 이전 구문

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
 언어 = N'*언어*' ** \@**  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 스크립트 언어를 나타냅니다. *언어는* **sysname입니다.** 유효한 값은 **R**, **파이썬**및 [외부 언어 만들기](../../t-sql/statements/create-external-language-transact-sql.md) (예 : Java)로 정의 된 모든 언어입니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 스크립트 언어를 나타냅니다. *언어는* **sysname입니다.** SQL Server 2017에서 유효한 값은 **R** 및 **파이썬**입니다.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 스크립트 언어를 나타냅니다. *언어는* **sysname입니다.** SQL Server 2016에서 유효한 값은 **R**입니다.
::: moniker-end

 스크립트 = N'*스크립트*' 리터럴 또는 변수 입력으로 지정 된 외부 언어 스크립트입니다. ** \@** *스크립트는* **nvarchar (최대)입니다.**  

`[ @input_data_1 =  N'input_data_1' ]`외부 스크립트에서 사용하는 입력 데이터를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 형식으로 지정합니다. *input_data_1* 데이터 형식은 **nvarchar(최대)입니다.**

`[ @input_data_1_name = N'input_data_1_name' ]`에서 정의된 쿼리를 나타내는 데 사용되는 변수의 @input_data_1이름을 지정합니다. 외부 스크립트에서 변수의 데이터 형식은 언어에 따라 다릅니다. R의 경우 입력 변수는 데이터 프레임입니다. 파이썬의 경우 입력은 테이블 형식이어야 합니다. *input_data_1_name* **sysname입니다.**  기본값은 *InputDataSet*입니다.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`파티션당 모델을 빌드하는 데 사용됩니다. 결과 집합(예: 제품 이름)을 정렬하는 데 사용되는 열의 이름을 지정합니다. 외부 스크립트에서 변수의 데이터 형식은 언어에 따라 다릅니다. R의 경우 입력 변수는 데이터 프레임입니다. 파이썬의 경우 입력은 테이블 형식이어야 합니다.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`파티션당 모델을 빌드하는 데 사용됩니다. 지리적 지역 또는 날짜와 같은 데이터를 분할하는 데 사용되는 열의 이름을 지정합니다. 외부 스크립트에서 변수의 데이터 형식은 언어에 따라 다릅니다. R의 경우 입력 변수는 데이터 프레임입니다. 파이썬의 경우 입력은 테이블 형식이어야 합니다. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`저장 프로시저 호출이 완료되면 반환할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터가 포함된 외부 스크립트의 변수 이름을 지정합니다. 외부 스크립트에서 변수의 데이터 형식은 언어에 따라 다릅니다. R의 경우 출력은 데이터 프레임이어야 합니다. 파이썬의 경우 출력은 팬더 데이터 프레임이어야 합니다. *output_data_1_name* **sysname입니다.**  기본값은 *OutputDataSet*입니다.  

`[ @parallel = 0 | 1 ]`매개 변수를 1로 설정하여 `@parallel` R 스크립트의 병렬 실행을 활성화합니다. 이 매개 변수의 기본값은 0입니다(평행식 없음). 출력이 클라이언트 컴퓨터로 직접 스트리밍되는 경우 `@parallel = 1` 절이 `WITH RESULT SETS` 필요하며 출력 스키마를 지정해야 합니다.  

 + RevoScaleR 함수를 사용하지 않는 R 스크립트의 `@parallel` 경우 스크립트가 병렬화될 수 있다고 가정할 때 매개 변수를 사용하면 큰 데이터 집합을 처리하는 데 도움이 될 수 있습니다. 예를 들어 모델과 `predict` 함께 R 함수를 사용하여 새 `@parallel = 1` 예측을 생성하는 경우 쿼리 엔진에 대한 힌트로 설정합니다. 쿼리를 병렬화할 수 있는 경우 **MAXDOP** 설정에 따라 행이 분산됩니다.  
  
 + RevoScaleR 함수를 사용하는 R 스크립트의 경우 병렬 처리가 자동으로 `@parallel = 1` 처리되며 **sp_execute_external_script** 호출에 지정해서는 안 됩니다.  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`외부 스크립트에 사용되는 입력 매개 변수 선언 목록입니다.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`외부 스크립트에서 사용하는 입력 매개 변수의 값 목록입니다.  

## <a name="remarks"></a>설명

> [!IMPORTANT]
> 쿼리 트리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제어되며 사용자는 쿼리에서 임의의 작업을 수행할 수 없습니다. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**sp_execute_external_script** 사용하여 지원되는 언어로 작성된 스크립트를 실행합니다. 지원되는 언어는 기계 학습 서비스와 함께 사용되는 **파이썬** 및 **R이며** 언어 확장과 함께 사용되는 [외부 언어 만들기(예:](../../t-sql/statements/create-external-language-transact-sql.md) Java)로 정의된 모든 언어입니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**sp_execute_external_script** 사용하여 지원되는 언어로 작성된 스크립트를 실행합니다. 지원되는 언어는 SQL Server 2017 기계 학습 서비스에서 **파이썬** 및 **R입니다.**
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**sp_execute_external_script** 사용하여 지원되는 언어로 작성된 스크립트를 실행합니다. 지원되는 언어는 SQL Server 2016 R 서비스에서 **R입니다.**
::: moniker-end

기본적으로 이 저장 프로시저에서 반환되는 결과 집합은 명명되지 않은 열로 출력됩니다. 스크립트 내에서 사용되는 열 이름은 스크립팅 환경에 로컬이며 출력된 결과 집합에 반영되지 않습니다. 결과 집합 열의 이름을 `WITH RESULT SET` 지정하려면 [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)의 절을 사용합니다.

결과 집합을 반환하는 것 외에도 OUTPUT 매개 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변수를 사용하여 스칼라 값을 반환할 수 있습니다. 
  
외부 리소스 풀을 구성하여 외부 스크립트에서 사용하는 리소스를 제어할 수 있습니다. 자세한 내용은 [외부 리소스 풀 만들기 &#40;거래-SQL&#41;. ](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 워크로드에 대한 정보는 리소스 관리자 카탈로그 보기, DMV 및 카운터에서 얻을 수 있습니다. 자세한 내용은 [Transact-SQL&#41;&#40;리소스 관리자 카탈로그 보기, ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md) [리소스 관리자 관련 동적 관리 보기 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)및 SQL [Server, 외부 스크립트 개체를](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)참조하십시오.  

### <a name="monitor-script-execution"></a>스크립트 실행 모니터

[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 및 [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)를 사용하여 스크립트 실행을 모니터링합니다. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>파티션 모델링을 위한 매개 변수

분할된 데이터에 대한 모델링을 활성화하는 두 개의 추가 매개 변수를 설정할 수 있으며, 여기서 파티션은 스크립트 실행 중에만 생성되고 사용되는 논리 파티션으로 데이터 집합을 자연스럽게 분할하는 하나 이상의 열을 기반으로 합니다. 연령, 성별, 지역, 날짜 또는 시간에 대한 반복 값을 포함하는 열은 분할된 데이터 집합에 적합한 몇 가지 예입니다.
 
두 매개 변수는 **input_data_1_partition_by_columns** 및 **input_data_1_order_by_columns,** 여기서 두 번째 매개 변수는 결과 집합을 정렬 하는 데 사용 됩니다. 매개 변수는 모든 파티션에 `sp_execute_external_script` 대해 한 번 실행되는 외부 스크립트와 함께 입력으로 전달됩니다. 자세한 정보 및 예제는 [자습서: 파티션 기반 모델 만들기를](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition)참조하십시오.

을 지정하여 스크립트를 병렬로 `@parallel=1`실행할 수 있습니다. 입력 쿼리를 병렬화할 수 있는 `@parallel=1` 경우 인수의 일부로 `sp_execute_external_script`설정해야 합니다. 기본적으로 쿼리 최적화 프로그램은 256개 이상의 행이 있는 테이블에서 작동하지만 `@parallel=1` 이 것을 명시적으로 처리하려는 경우 이 스크립트에는 데모로 매개 변수가 포함됩니다.

> [!Tip]
> 학습 워크로드의 경우 비-Microsoft-rx 알고리즘을 사용 중이어도 임의의 학습 스크립트에 `@parallel`을 사용할 수 있습니다. 일반적으로 RevoScaleR 알고리즘(rx 접두사 포함)만이 SQL Server의 학습 시나리오에서 병렬 처리를 제공합니다. 그러나 SQL Server vNext의 새 매개 변수를 사용하면 해당 기능으로 특별히 설계되지 않은 함수를 호출하는 스크립트를 병렬화할 수 있습니다.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>파이썬 및 R 스크립트에 대한 스트리밍 실행  

스트리밍을 사용하면 Python 또는 R 스크립트가 메모리에 들어갈 수 있는 것보다 많은 데이터로 작업할 수 있습니다. 스트리밍 중에 전달되는 행 수를 제어하려면 `@r_rowsPerRead` `@params` 컬렉션에서 매개 변수에 대한 정수 값을 지정합니다.  예를 들어 매우 넓은 데이터를 사용하는 모델을 학습하는 경우 값을 조정하여 더 적은 수의 행을 읽고 모든 행을 하나의 데이터 청크로 보낼 수 있도록 할 수 있습니다. 이 매개 변수를 사용하여 한 번에 읽고 처리하는 행 수를 관리하여 서버 성능 문제를 완화할 수도 있습니다. 
  
스트리밍에 `@r_rowsPerRead` 대한 매개 변수와 인수는 `@parallel` 모두 힌트로 간주되어야 합니다. 힌트를 적용하려면 병렬 처리를 포함하는 SQL 쿼리 계획을 생성할 수 있어야 합니다. 이 작업을 사용할 수 없는 경우 병렬 처리를 사용할 수 없습니다.  
  
> [!NOTE]  
> 스트리밍 및 병렬 처리는 엔터프라이즈 에디션에서만 지원됩니다. 오류를 발생 하지 않고 표준 에디션에서 쿼리에 매개 변수를 포함할 수 있지만 매개 변수는 영향을 주지 않으며 R 스크립트는 단일 프로세스에서 실행 됩니다.  
  
## <a name="restrictions"></a>제한  

### <a name="data-types"></a>데이터 형식

다음 데이터 형식은 입력 쿼리 또는 **sp_execute_external_script** 프로시저의 매개 변수에 사용될 때 지원되지 않으며 지원되지 않는 형식 오류를 반환합니다.  

해결 방법으로 외부 스크립트로 보내기 전에 지원되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 형식에 열이나 값을 **CAST합니다.**  
  
-   **커서**  
  
-   **타임 스탬프**  
  
-   **datetime2**, **날짜 시간 오프셋**, **시간**  
  
-   **Sql_variant**  
  
-   **텍스트**, **이미지**  
  
-   **xml**  
  
-   **계층 구조,** **지오메트리,** **지리**  
  
-   CLR 사용자 정의 형식

일반적으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식에 매핑할 수 없는 모든 결과 집합은 NULL로 출력됩니다.  

### <a name="restrictions-specific-to-r"></a>R관련 제한 사항

입력에 R의 허용되는 값 범위에 맞지 않는 **datetime** 값이 포함된 경우 값이 **NA로**변환됩니다. 이는 R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어에서 지원되는 것보다 더 많은 범위의 값을 허용하기 때문에 필요합니다.

Float 값(예: `+Inf` `-Inf`, `NaN`" , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ")은 두 언어 모두 IEEE 754를 사용하는 경우에도 지원되지 않습니다. 현재 동작은 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 직접 전송합니다. 결과적으로 SQL 클라이언트에서 오류가 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 발생합니다. 따라서 이러한 값은 **NULL로**변환됩니다.

## <a name="permissions"></a>사용 권한

외부 스크립트 데이터베이스 권한을 **실행해야** 합니다.  

## <a name="examples"></a>예

이 섹션에는 이 저장 프로시저를 사용하여 R 또는 Python [!INCLUDE[tsql](../../includes/tsql-md.md)]스크립트를 실행하는 데 사용할 수 있는 방법에 대한 예제가 포함되어 있습니다.

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. R 데이터 집합을 SQL Server로 반환  

다음 예제에서는 **sp_execute_external_script** 사용 하 여 R에 포함 된 아이리스 데이터 집합을 반환 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]저장 프로시저를 만듭니다.  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. SQL Server의 데이터를 기반으로 R 모델 생성  

다음 예제에서는 **sp_execute_external_script** 사용하여 아이리스 모델을 생성하고 모델을 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환하는 저장 프로시저를 만듭니다.  

> [!NOTE]
>  이 예제에서는 e1071 패키지를 사전 설치해야 합니다. 자세한 내용은 [SQL Server에 추가 R 패키지 설치를](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)참조하십시오.

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

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Python 모델을 만들고 거기서 점수 생성

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

파이썬 코드에 사용되는 열 제목은 SQL Server에 출력되지 않습니다. 따라서 WITH RESULT 문을 사용 하 여 SQL에서 사용할 열 이름 및 데이터 형식을 지정 합니다.

점수 매기기의 경우 네이티브 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 함수를 사용할 수도 있으며, 이 함수는 Python 또는 R 런타임 호출을 방지하기 때문에 일반적으로 더 빠릅니다.

## <a name="see-also"></a>참고 항목

+ [SQL Server Machine Learning Services](../../machine-learning/index.yml)
+ [SQL 서버 언어 확장](../../language-extensions/language-extensions-overview.md). 
+ [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [파이썬 라이브러리 및 데이터 유형](../../machine-learning/python/python-libraries-and-data-types.md)  
+ [R 라이브러리 및 R 데이터 유형](../../machine-learning/r/r-libraries-and-data-types.md)  
+ [SQL 서버 R 서비스](../../machine-learning/r/sql-server-r-services.md)   
+ [SQL 서버 기계 학습 서비스에 대한 알려진 문제](../../machine-learning/known-issues-for-sql-server-machine-learning-services.md)   
+ [외부 라이브러리 만들기 &#40;거래-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;&#41;거래](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [External Scripts Enabled 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server, External Scripts 개체](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
