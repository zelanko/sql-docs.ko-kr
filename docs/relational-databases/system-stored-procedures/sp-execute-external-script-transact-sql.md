---
description: sp_execute_external_script(Transact-SQL)
title: sp_execute_external_script (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning-services
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
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: cceb8ad1df56eabaf0aa9507187e71b8db15bcaa
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482372"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script(Transact-SQL)
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
**Sp_execute_external_script** 저장 프로시저는 프로시저에 대 한 입력 인수로 제공 된 스크립트를 실행 하 고 [Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md) 및 [언어 확장과](../../language-extensions/language-extensions-overview.md)함께 사용 됩니다. 

Machine Learning Services의 경우 [Python](../../machine-learning/concepts/extension-python.md) 및 [R](../../machine-learning/concepts/extension-r.md) 은 지원 되는 언어입니다. 언어 확장의 경우 Java는 지원 되지만 [CREATE EXTERNAL Language](../../t-sql/statements/create-external-language-transact-sql.md)를 사용 하 여 정의 해야 합니다.

**Sp_execute_external_script** 를 실행 하려면 먼저 Machine Learning Services 또는 언어 확장을 설치 해야 합니다. 자세한 내용은 Windows 및 Linux [에서 SQL Server Machine Learning Services (Python 및 R) 설치](../../machine-learning/install/sql-machine-learning-services-windows-install.md) 또는 Windows [](../../linux/sql-server-linux-setup-machine-learning.md)및 [Linux](../../linux/sql-server-linux-setup-language-extensions-java.md) [에서 SQL Server 언어 확장 설치](../../language-extensions/install/windows-java.md) 를 참조 하세요.
::: moniker-end

::: moniker range="=sql-server-2017"
**Sp_execute_external_script** 저장 프로시저는 프로시저에 대 한 입력 인수로 제공 된 스크립트를 실행 하 고 SQL Server 2017에서 [Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md) 와 함께 사용 됩니다.

Machine Learning Services의 경우 [Python](../../machine-learning/concepts/extension-python.md) 및 [R](../../machine-learning/concepts/extension-r.md) 은 지원 되는 언어입니다.

**Sp_execute_external_script** 를 실행 하려면 먼저 Machine Learning Services를 설치 해야 합니다. 자세한 내용은 [Windows에서 SQL Server Machine Learning Services (Python 및 R) 설치](../../machine-learning/install/sql-machine-learning-services-windows-install.md)를 참조 하세요.
::: moniker-end

::: moniker range="=sql-server-2016"
**Sp_execute_external_script** 저장 프로시저는 프로시저에 대 한 입력 인수로 제공 된 스크립트를 실행 하 고 SQL Server 2016에서 [R Services](../../machine-learning/r/sql-server-r-services.md) 와 함께 사용 됩니다.

R 서비스의 경우  [r](../../machine-learning/concepts/extension-r.md) 은 지원 되는 언어입니다.

**Sp_execute_external_script** 를 실행 하려면 먼저 R Services를 설치 해야 합니다. 자세한 내용은 [Windows에서 SQL Server Machine Learning Services (Python 및 R) 설치](../../machine-learning/install/sql-r-services-windows-install.md)를 참조 하세요.
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
**Sp_execute_external_script** 저장 프로시저는 프로시저에 대 한 입력 인수로 제공 되는 스크립트를 실행 하며, [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)와 함께 사용 됩니다.

Machine Learning Services의 경우 [Python](../../machine-learning/concepts/extension-python.md) 및 [R](../../machine-learning/concepts/extension-r.md) 은 지원 되는 언어입니다.

**Sp_execute_external_script** 를 실행 하려면 먼저 Machine Learning Services를 사용 하도록 설정 해야 합니다. 자세한 내용은 [AZURE SQL Managed Instance 설명서의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)을 참조 하세요.
::: moniker-end

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current"
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
::: moniker range="=sql-server-2016"
## <a name="syntax-for-sql-server-2017-and-earlier"></a>SQL Server 2017 이전 구문

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
 **\@ language** = N '*language*'  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
 스크립트 언어를 나타냅니다. *language* 는 **sysname** 입니다. 유효한 값은 **R**, **PYTHON** 및 [CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) (예: Java)로 정의 된 모든 언어입니다.
::: moniker-end
::: moniker range="=sql-server-2017"
 스크립트 언어를 나타냅니다. *language* 는 **sysname** 입니다. SQL Server 2017에서 유효한 값은 **R** 및 **Python** 입니다.
::: moniker-end
::: moniker range="=sql-server-2016"
 스크립트 언어를 나타냅니다. *language* 는 **sysname** 입니다. SQL Server 2016에서 유일 하 게 유효한 값은 **R** 입니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
 스크립트 언어를 나타냅니다. *language* 는 **sysname** 입니다. Azure SQL Managed Instance에서 유효한 값은 **R** 및 **Python** 입니다.
::: moniker-end

 **\@ script** = N '*script*' 외부 언어 스크립트를 리터럴 또는 변수 입력으로 지정 했습니다. *스크립트* 는 **nvarchar (max)** 입니다.  

`[ @input_data_1 =  N'input_data_1' ]` 외부 스크립트에서 사용 하는 입력 데이터를 쿼리 형식으로 지정 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . *Input_data_1* 데이터 형식은 **nvarchar (max)** 입니다.

`[ @input_data_1_name = N'input_data_1_name' ]` 에서 정의 된 쿼리를 나타내는 데 사용 되는 변수의 이름을 지정 합니다 @input_data_1 . 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 입력 변수는 데이터 프레임입니다. Python의 경우 입력은 테이블 형식 이어야 합니다. *input_data_1_name* 는 **sysname** 입니다.  기본값은 *Inputdataset* 입니다.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` 파티션당 모델을 작성 하는 데 사용 됩니다. 결과 집합의 순서를 지정 하는 데 사용 되는 열의 이름을 지정 합니다. 예를 들어 제품 이름입니다. 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 입력 변수는 데이터 프레임입니다. Python의 경우 입력은 테이블 형식 이어야 합니다.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` 파티션당 모델을 작성 하는 데 사용 됩니다. 지리적 지역 또는 날짜와 같은 데이터를 분할 하는 데 사용 되는 열의 이름을 지정 합니다. 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 입력 변수는 데이터 프레임입니다. Python의 경우 입력은 테이블 형식 이어야 합니다. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]저장 프로시저 호출이 완료 될 때 반환 될 데이터를 포함 하는 외부 스크립트의 변수 이름을 지정 합니다. 외부 스크립트에 있는 변수의 데이터 형식은 언어에 따라 달라 집니다. R의 경우 출력은 데이터 프레임 이어야 합니다. Python의 경우 출력은 pandas 데이터 프레임 이어야 합니다. *output_data_1_name* 는 **sysname** 입니다.  기본값은 *Outputdataset* 입니다.  

`[ @parallel = 0 | 1 ]` 매개 변수를 1로 설정 하 여 R 스크립트의 병렬 실행을 사용 하도록 설정 `@parallel` 합니다. 이 매개 변수의 기본값은 0 (병렬 처리 없음)입니다. `@parallel = 1`및 출력을 클라이언트 컴퓨터로 직접 스트리밍하는 경우 `WITH RESULT SETS` 절이 필요 하며 출력 스키마를 지정 해야 합니다.  

 + RevoScaleR 함수를 사용 하지 않는 R 스크립트의 경우 매개 변수를 사용 하면  `@parallel` 큰 데이터 집합을 처리 하는 데 도움이 될 수 있습니다 .이 경우 스크립트가 일반적으로 병렬 처리 될 수 있다고 가정 합니다. 예를 들어 모델에서 R 함수를 사용 하 여 `predict` 새 예측을 생성 하는 경우 `@parallel = 1` 쿼리 엔진에 대 한 힌트로를 설정 합니다. 쿼리를 병렬화 할 수 있는 경우 행은 **MAXDOP** 설정에 따라 분산 됩니다.  
  
 + RevoScaleR 함수를 사용 하는 R 스크립트의 경우 병렬 처리는 자동으로 처리 되며 `@parallel = 1` **sp_execute_external_script** 호출을 지정 하면 안 됩니다.  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` 외부 스크립트에서 사용 되는 입력 매개 변수 선언의 목록입니다.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` 외부 스크립트에서 사용 하는 입력 매개 변수에 대 한 값의 목록입니다.  

## <a name="remarks"></a>설명

> [!IMPORTANT]
> 쿼리 트리는 SQL machine learning에 의해 제어 되며 사용자는 쿼리에 대해 임의의 작업을 수행할 수 없습니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
**Sp_execute_external_script** 를 사용 하 여 지원 되는 언어로 작성 된 스크립트를 실행 합니다. 지원 되는 언어는 Machine Learning Services에 사용 되는 **Python** 및 **R** 이며, 언어 확장과 함께 사용 되는 [CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) (예: Java)로 정의 된 모든 언어입니다.
::: moniker-end
::: moniker range="=sql-server-2017"
**Sp_execute_external_script** 를 사용 하 여 지원 되는 언어로 작성 된 스크립트를 실행 합니다. 지원 되는 언어는 SQL Server 2017 Machine Learning Services의 **Python** 및 **R** 입니다.
::: moniker-end
::: moniker range="=sql-server-2016"
**Sp_execute_external_script** 를 사용 하 여 지원 되는 언어로 작성 된 스크립트를 실행 합니다. SQL Server 2016 R Services에서는 유일 하 게 지원 되는 언어는 **r** 입니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
**Sp_execute_external_script** 를 사용 하 여 지원 되는 언어로 작성 된 스크립트를 실행 합니다. 지원 되는 언어는 Azure SQL Managed Instance Machine Learning Services의 **Python** 및 **R** 입니다.
::: moniker-end

기본적으로이 저장 프로시저에서 반환 되는 결과 집합은 명명 되지 않은 열을 사용 하 여 출력 됩니다. 스크립트 내에서 사용 되는 열 이름은 스크립팅 환경에서 로컬로 사용 되며 출력 결과 집합에 반영 되지 않습니다. 결과 집합 열의 이름을로 설정 하려면 `WITH RESULT SET` 의 절을 사용 [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md) 합니다.

결과 집합을 반환 하는 것 외에도 스칼라 값을 반환 하 여 출력 매개 변수를 사용할 수 있습니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15"
외부 리소스 풀을 구성 하 여 외부 스크립트에서 사용 하는 리소스를 제어할 수 있습니다. 자세한 내용은 [CREATE EXTERNAL RESOURCE POOL &#40;transact-sql&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)를 참조 하세요. 작업에 대 한 정보는 리소스 관리자 카탈로그 뷰, DMV의 및 카운터에서 가져올 수 있습니다. 자세한 내용은 transact-sql [&#41;&#40;Resource Governor 카탈로그 뷰 ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md) [Resource Governor, transact-sql &#40;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)및 [&#41;, External Scripts 개체](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)SQL Server을 참조 하세요.  
::: moniker-end

### <a name="monitor-script-execution"></a>스크립트 실행 모니터링

[Sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 및 [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)를 사용 하 여 스크립트 실행을 모니터링 합니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
### <a name="parameters-for-partition-modeling"></a>파티션 모델링에 대 한 매개 변수

분할 된 데이터에 대 한 모델링을 가능 하 게 하는 두 개의 추가 매개 변수를 설정할 수 있습니다. 여기서 파티션은 데이터 집합을 스크립트 실행 중에만 생성 및 사용 되는 논리적 파티션으로 자연스럽 게 분할 하는 하나 이상의 열을 기반으로 합니다. 보존 기간, 성별, 지역, 날짜 또는 시간에 대 한 반복 값을 포함 하는 열은 분할 된 데이터 집합에 적합 한 몇 가지 예입니다.

두 매개 변수는 **input_data_1_partition_by_columns** 및 **input_data_1_order_by_columns** 이며 두 번째 매개 변수는 결과 집합의 순서를 정렬 하는 데 사용 됩니다. 매개 변수는 `sp_execute_external_script` 모든 파티션에 대해 한 번씩 실행 되는 외부 스크립트를 사용 하 여에 대 한 입력으로 전달 됩니다. 자세한 내용 및 예제는 [자습서: 파티션 기반 모델 만들기](../../machine-learning/tutorials/r-tutorial-create-models-per-partition.md)를 참조 하세요.

를 지정 하 여 스크립트를 병렬로 실행할 수 있습니다 `@parallel=1` . 입력 쿼리를 병렬화 할 수 있는 경우 `@parallel=1` 인수의 일부로를로 설정 해야 합니다 `sp_execute_external_script` . 기본적으로 쿼리 최적화 프로그램은 `@parallel=1` 행이 256 개를 초과 하는 테이블에서 작동 하지만이를 명시적으로 처리 하려는 경우이 스크립트에는 매개 변수가 데모용으로 포함 됩니다.

> [!Tip]
> 학습 워크로드의 경우 비-Microsoft-rx 알고리즘을 사용 중이어도 임의의 학습 스크립트에 `@parallel`을 사용할 수 있습니다. 일반적으로 RevoScaleR 알고리즘(rx 접두사 포함)만이 SQL Server의 학습 시나리오에서 병렬 처리를 제공합니다. 그러나 SQL Server 2019 이상에서 새 매개 변수를 사용 하는 경우 해당 기능으로 특별히 엔지니어링 되지 않은 함수를 호출 하는 스크립트를 병렬화 할 수 있습니다.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Python 및 R 스크립트에 대 한 스트리밍 실행  

스트리밍을 사용 하면 Python 또는 R 스크립트를 메모리에 포함할 수 있는 것 보다 더 많은 데이터와 함께 사용할 수 있습니다. 스트리밍 중에 전달 되는 행 수를 제어 하려면 컬렉션에서 매개 변수에 대 한 정수 값을 지정 합니다 `@r_rowsPerRead` `@params` .  예를 들어 매우 넓은 데이터를 사용 하는 모델을 학습 하는 경우에는 값을 조정 하 여 모든 행이 하나의 데이터 청크로 전송 될 수 있도록 해야 합니다. 이 매개 변수를 사용 하 여 서버 성능 문제를 완화 하기 위해 한 번에 읽고 처리 되는 행 수를 관리할 수도 있습니다. 
  
`@r_rowsPerRead`스트리밍 및 인수에 대 한 매개 변수는 모두 `@parallel` 힌트로 간주 됩니다. 힌트를 적용 하려면 병렬 처리를 포함 하는 SQL 쿼리 계획을 생성할 수 있어야 합니다. 이렇게 할 수 없는 경우 병렬 처리를 사용 하도록 설정할 수 없습니다.  
  
> [!NOTE]  
> 스트리밍 및 병렬 처리는 Enterprise Edition 에서만 지원 됩니다. 오류를 발생 시 키 지 않고 표준 버전의 쿼리에 매개 변수를 포함할 수 있지만 매개 변수는 영향을 주지 않으며 R 스크립트는 단일 프로세스로 실행 됩니다.  
  
## <a name="restrictions"></a>제한  

### <a name="data-types"></a>데이터 형식

다음 데이터 형식은 **sp_execute_external_script** 프로시저의 입력 쿼리 또는 매개 변수에 사용 될 때 지원 되지 않으며 지원 되지 않는 형식 오류를 반환 합니다.  

해결 방법으로, 외부 스크립트로 보내기 전에 열 또는 값을에서 지원 되는 형식으로 **캐스팅** [!INCLUDE[tsql](../../includes/tsql-md.md)] 합니다.  
  
+ **cursor**  
  
+ **timestamp**  
  
+ **datetime2**, **datetimeoffset**, **time**  
  
+ **sql_variant**  
  
+ **텍스트**, **이미지**  
  
+ **xml**  
  
+ **hierarchyid**, **geometry**, **geography**  
  
+ CLR 사용자 정의 형식

일반적으로 데이터 형식에 매핑할 수 없는 결과 집합 [!INCLUDE[tsql](../../includes/tsql-md.md)] 은 NULL로 출력 됩니다.  

### <a name="restrictions-specific-to-r"></a>R에 한정 되는 제한 사항

입력에 R에서 허용 되는 값 범위에 맞지 않는 **datetime** 값이 포함 된 경우 값은 **NA** 로 변환 됩니다. 이는 SQL machine learning에서 R 언어에서 지원 되는 것 보다 더 큰 범위의 값을 허용 하기 때문에 필요 합니다.

Float 값 (예: `+Inf` , `-Inf` , `NaN` )은 두 언어 모두 IEEE 754를 사용 하지만 SQL machine learning에서는 지원 되지 않습니다. 현재 동작은 값을 SQL로 직접 보냅니다. 따라서 SQL 클라이언트에서 오류를 throw 합니다. 따라서 이러한 값은 **NULL** 로 변환 됩니다.

## <a name="permissions"></a>사용 권한

**EXECUTE ANY EXTERNAL SCRIPT** database 권한이 필요 합니다.  

## <a name="examples"></a>예

이 섹션에서는를 사용 하 여이 저장 프로시저를 사용 하 여 R 또는 Python 스크립트를 실행 하는 방법의 예를 보여 줍니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. SQL Server으로 R 데이터 집합 반환  

다음 예에서는 **sp_execute_external_script** 를 사용 하 여 R에 포함 된 iri 데이터 집합을 반환 하는 저장 프로시저를 만듭니다.  

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

### <a name="b-create-a-python-model-and-generate-scores-from-it"></a>B. Python 모델을 만들고 거기서 점수 생성

이 예에서는를 사용 하 여 `sp_execute_external_script` 간단한 Python 모델에서 점수를 생성 하는 방법을 보여 줍니다.

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

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15"
### <a name="c-generate-an-r-model-based-on-data-from-sql-server"></a>C. SQL Server의 데이터를 기반으로 R 모델 생성  

다음 예에서는 **sp_execute_external_script** 를 사용 하 여 iri 모델을 생성 하 고 모델을 반환 하는 저장 프로시저를 만듭니다.  

> [!NOTE]
> 이 예에서는 e1071 패키지를 미리 설치 해야 합니다. 자세한 내용은 [SQL Server에 추가 R 패키지 설치](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)를 참조 하세요.

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
::: moniker-end

점수 매기기의 경우 네이티브 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 함수를 사용할 수도 있으며, 이 함수는 Python 또는 R 런타임 호출을 방지하기 때문에 일반적으로 더 빠릅니다.

## <a name="see-also"></a>참조

+ [SQL Machine Learning](../../machine-learning/index.yml)
+ [언어 확장을 SQL Server](../../language-extensions/language-extensions-overview.md)합니다. 
+ [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Transact-sql&#41;&#40;외부 라이브러리 만들기 ](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [외부 스크립트 설정 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server, 외부 스크립트 개체](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)