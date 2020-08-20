---
description: sys.dm_exec_plan_attributes(Transact-SQL)
title: sys. dm_exec_plan_attributes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes
- sys.dm_exec_plan_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_plan_attributes dynamic management function
ms.assetid: dacf3ab3-f214-482e-aab5-0dab9f0a3648
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 46c41c4bf06082e36df1ea48165520afbc4a3210
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481986"
---
# <a name="sysdm_exec_plan_attributes-transact-sql"></a>sys.dm_exec_plan_attributes(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  계획 핸들로 지정한 계획의 각 계획 특성에 대해 행을 하나씩 반환합니다. 이 테이블 반환 함수를 사용하여 계획의 현재 동시 실행 수 또는 캐시 키 값과 같은 특정 계획에 대한 정보를 가져올 수 있습니다.  
  
> [!NOTE]  
>  이 함수를 통해 반환 되는 정보 중 일부는 [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) 의 이전 버전과의 호환성 보기에 매핑됩니다.

## <a name="syntax"></a>구문  
```  
sys.dm_exec_plan_attributes ( plan_handle )  
```  
  
## <a name="arguments"></a>인수  
 *plan_handle*  
 실행된 일괄 처리에 대한 쿼리 계획을 고유하게 식별하며 해당 계획은 계획 캐시에 있습니다. *plan_handle* 은 **varbinary (64)** 입니다. 계획 핸들은 [sys. dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) 동적 관리 뷰에서 가져올 수 있습니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|특성|**varchar(128)**|이 계획과 연결된 특성의 이름입니다. 이 항목의 바로 아래 표에는 가능한 특성, 해당 데이터 형식 및 해당 설명이 나열 되어 있습니다.|  
|값|**sql_variant**|이 계획과 연결된 특성의 값입니다.|  
|is_cache_key|**bit**|특성이 계획에 대한 캐시 조회 키의 일부로 사용되는지 여부를 나타냅니다.|  

위의 표에서 **특성** 에는 다음 값을 사용할 수 있습니다.

|attribute|데이터 형식|Description|  
|---------------|---------------|-----------------|  
|set_options|**int**|계획을 컴파일할 때 사용하는 옵션 값을 나타냅니다.|  
|objectid|**int**|캐시에서 개체를 찾는 데 사용되는 기본 키 중 하나입니다. 이는 데이터베이스 개체 (프로시저, 뷰, 트리거 등)에 대해 [sys. 개체](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 에 저장 된 개체 ID입니다. 계획 유형이 "임시" 또는 "준비됨"일 경우 일괄 처리 텍스트의 내부 해시입니다.|  
|dbid|**int**|계획이 참조하는 엔터티를 포함하는 데이터베이스의 ID입니다.<br /><br /> 임시 또는 준비된 계획의 경우 일괄 처리가 실행된 데이터베이스 ID입니다.|  
|dbid_execute|**int**|**리소스** 데이터베이스에 저장 된 시스템 개체의 경우 캐시 된 계획이 실행 되는 데이터베이스 ID입니다. 다른 모든 경우에는 0입니다.|  
|user_id|**int**|값 -2는 전송된 일괄 처리가 암시적 이름 확인에 의존하지 않으며 여러 사용자들 간에 공유될 수 있음을 의미합니다. 이는 선호되는 방법입니다. 기타 값은 모두 데이터베이스에 쿼리를 전송하는 사용자의 사용자 ID를 나타냅니다.| 
|language_id|**smallint**|캐시 개체를 만든 연결의 언어 ID입니다. 자세한 내용은 [sys.sys언어 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)를 참조 하세요.|  
|date_format|**smallint**|캐시 개체를 만든 연결의 날짜 형식입니다. 자세한 내용은 [SET DATEFORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)을 참조하세요.|  
|date_first|**tinyint**|날짜의 첫 번째 값입니다. 자세한 내용은 [SET DATEFIRST&#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)를 참조하세요.|  
|상태|**int**|캐시 조회 키의 일부인 내부 상태 비트입니다.|  
|required_cursor_options|**int**|커서 유형과 같이 사용자가 지정한 커서 옵션입니다.|  
|acceptable_cursor_options|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 문의 실행을 지원하도록 암시적으로 변환될 수 있는 커서 옵션입니다. 예를 들어 사용자는 동적 커서를 지정할 수 있지만 쿼리 최적화 프로그램을 통해 이 커서 유형을 정적 커서로 변환할 수 있습니다.|  
|inuse_exec_context|**int**|쿼리 계획을 사용하고 있는 현재 실행 중인 일괄 처리의 수입니다.|  
|free_exec_context|**int**|현재 사용되고 있지 않은 쿼리 계획에 대한 캐시된 실행 컨텍스트 수입니다.|  
|hits_exec_context|**int**|계획 캐시에서 실행 컨텍스트를 얻어 다시 사용한 횟수로서 SQL 문을 다시 컴파일할 때 발생하는 오버헤드를 줄여 줍니다. 지금까지의 모든 일괄 처리 실행에 대한 집계 값입니다.|  
|misses_exec_context|**int**|계획 캐시에서 실행 컨텍스트를 찾지 못하고 일괄 처리 실행에 대한 새 실행 컨텍스트를 생성한 횟수입니다.|  
|removed_exec_context|**int**|캐시된 계획에 대한 메모리 가중으로 인해 제거된 실행 컨텍스트의 수입니다.|  
|inuse_cursors|**int**|캐시된 계획을 사용하고 있는 하나 이상의 커서를 포함하는 현재 실행 중인 일괄 처리의 수입니다.|  
|free_cursors|**int**|캐시된 계획에 대한 유휴 커서 또는 사용하지 않는 커서의 수입니다.|  
|hits_cursors|**int**|캐시된 계획에서 비활성 커서를 얻어 다시 사용한 횟수입니다. 지금까지의 모든 일괄 처리 실행에 대한 집계 값입니다.|  
|misses_cursors|**int**|캐시에서 비활성 커서를 찾지 못한 횟수입니다.|  
|removed_cursors|**int**|캐시된 계획에 대한 메모리 가중으로 인해 제거된 커서의 수입니다.|  
|sql_handle|**varbinary**(64)|일괄 처리의 SQL 핸들입니다.|  
|merge_action_type|**smallint**|MERGE 문의 결과로 사용되는 트리거 실행 계획의 유형입니다.<br /><br /> 0은 비 트리거 계획, MERGE 문의 결과로 실행되지 않는 트리거 계획 또는 DELETE 동작만 지정하는 MERGE 문의 결과로 실행되는 트리거 계획을 나타냅니다.<br /><br /> 1은 MERGE 문의 결과로 실행되는 INSERT 트리거 계획을 나타냅니다.<br /><br /> 2는 MERGE 문의 결과로 실행되는 UPDATE 트리거 계획을 나타냅니다.<br /><br /> 3은 해당 INSERT 또는 UPDATE 동작을 포함하는 MERGE 문의 결과로 실행되는 DELETE 트리거 계획을 나타냅니다.<br /><br /> 동작을 연계하여 실행되는 중첩 트리거의 경우 이 값은 연계를 유발하는 MERGE 문의 동작입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="remarks"></a>설명  
  
## <a name="set-options"></a>SET 옵션  
 동일한 컴파일된 계획의 복사본은 **set_options** 열의 값에 의해서만 다를 수 있습니다. 이는 동일한 쿼리에 대해 서로 다른 연결이 서로 다른 SET 옵션 집합을 사용하고 있음을 나타냅니다. 캐시에 있는 계획의 여러 복사본으로 인해 추가 컴파일 작업이 발생하고 계획 재사용 횟수가 줄어들며 계획 캐시 인플레이션이 발생할 수 있으므로 일반적으로 서로 다른 옵션 집합은 사용하지 않는 것이 좋습니다.  
  
### <a name="evaluating-set-options"></a>SET 옵션 평가  
 **Set_options** 에서 반환 된 값을 계획이 컴파일되는 옵션으로 변환 하려면 0에 도달할 때까지 가능한 가장 큰 값부터 시작 하 여 **set_options** 값에서 값을 뺍니다. 뺀 각 값은 쿼리 계획에 사용된 옵션에 해당합니다. 예를 들어 **set_options** 의 값이 251 인 경우 계획이 컴파일되는 옵션은 ANSI_NULL_DFLT_ON (128), QUOTED_IDENTIFIER (64), ANSI_NULLS (32), ANSI_WARNINGS (16), CONCAT_NULL_YIELDS_NULL (8), 병렬 계획 (2) 및 ANSI_PADDING (1)입니다.  
  
|옵션|값|  
|------------|-----------|  
|ANSI_PADDING|1|  
|Parallel Plan|2|  
|FORCEPLAN|4|  
|CONCAT_NULL_YIELDS_NULL|8|  
|ANSI_WARNINGS|16|  
|ANSI_NULLS|32|  
|QUOTED_IDENTIFIER|64|  
|ANSI_NULL_DFLT_ON|128|  
|ANSI_NULL_DFLT_OFF|256|  
|NoBrowseTable<br /><br /> 계획이 FOR BROWSE 작업을 구현하는 데 작업 테이블을 사용하지 않음을 나타냅니다.|512|  
|TriggerOneRow<br /><br /> 계획에 AFTER 트리거 델타 테이블에 대한 단일 행 최적화가 포함됨을 나타냅니다.|1024|  
|ResyncQuery<br /><br /> 쿼리가 내부 시스템 저장 프로시저에서 제출됨을 나타냅니다.|2048|  
|ARITH_ABORT|4096|  
|NUMERIC_ROUNDABORT|8192|  
|DATEFIRST|16384|  
|DATEFORMAT|32768|  
|LanguageID|65536|  
|UPON<br /><br /> 계획을 컴파일할 때 데이터베이스 옵션 PARAMETERIZATION이 FORCED로 설정됨을 나타냅니다.|131072|  
|ROWCOUNT|**적용 대상:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 받는 사람 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> 262144|  
  
## <a name="cursors"></a>커서  
 비활성 커서가 컴파일된 계획에서 캐시되어 커서의 동시 사용자가 커서 저장에 사용된 메모리를 다시 사용할 수 있습니다. 예를 들어 일괄 처리가 커서를 할당 취소하지 않고 선언 및 사용한다고 가정합니다. 두 사용자가 동일한 일괄 처리를 실행하는 경우에는 두 활성 커서가 있습니다. 커서가 다른 일괄 처리에서 잠재적으로 할당 취소되면 커서 저장에 사용된 메모리가 캐시되고 해제되지 않습니다. 이 비활성 커서 목록은 컴파일된 계획에서 유지됩니다. 이후에 사용자가 일괄 처리를 실행하면 캐시된 커서 메모리가 다시 사용되고 활성 커서로 적절히 초기화됩니다.  
  
### <a name="evaluating-cursor-options"></a>커서 옵션 평가  
 **Required_cursor_options** 에서 반환 된 값을 변환 하 고 계획이 컴파일되는 옵션에 **acceptable_cursor_options** 하려면 0에 도달할 때까지 가능한 가장 큰 값부터 시작 하 여 열 값에서 값을 뺍니다. 뺀 각 값은 쿼리 계획에 사용된 커서 옵션에 해당합니다.  
  
|옵션|값|  
|------------|-----------|  
|None|0|  
|INSENSITIVE|1|  
|SCROLL|2|  
|READ ONLY|4|  
|FOR UPDATE|8|  
|LOCAL|16|  
|GLOBAL|32|  
|FORWARD_ONLY|64|  
|KEYSET|128|  
|DYNAMIC|256|  
|SCROLL_LOCKS|512|  
|OPTIMISTIC|1024|  
|STATIC|2048|  
|FAST_FORWARD|4096|  
|IN PLACE|8192|  
|FOR *select_statement*|16384|  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-the-attributes-for-a-specific-plan"></a>A. 특정 계획에 대한 특성 반환  
 다음 예에서는 지정된 계획에 대한 모든 계획 특성을 반환합니다. 지정된 계획에 대한 계획 핸들을 얻기 위해 먼저 `sys.dm_exec_cached_plans` 동적 관리 뷰가 쿼리됩니다. 두 번째 쿼리에서는 `<plan_handle>`을 첫 번째 쿼리의 계획 핸들 값으로 대체합니다.  
  
```sql  
SELECT plan_handle, refcounts, usecounts, size_in_bytes, cacheobjtype, objtype   
FROM sys.dm_exec_cached_plans;  
GO  
SELECT attribute, value, is_cache_key  
FROM sys.dm_exec_plan_attributes(<plan_handle>);  
GO  
```  
  
### <a name="b-returning-the-set-options-for-compiled-plans-and-the-sql-handle-for-cached-plans"></a>B. 컴파일된 계획의 SET 옵션 및 캐시된 계획의 SQL 핸들 반환  
 다음 예에서는 각 계획이 컴파일될 때 사용한 옵션을 나타내는 값을 반환합니다. 또한 모든 캐시된 계획의 SQL 핸들도 반환됩니다.  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
    SELECT plan_handle, epa.attribute, epa.value   
    FROM sys.dm_exec_cached_plans   
        OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
    WHERE cacheobjtype = 'Compiled Plan') AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행 ](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  

