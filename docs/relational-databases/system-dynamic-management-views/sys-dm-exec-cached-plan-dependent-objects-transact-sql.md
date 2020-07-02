---
title: sys. dm_exec_cached_plan_dependent_objects (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plan_dependent_objects
- dm_exec_cached_plan_dependent_objects_TSQL
- sys.dm_exec_cached_plan_dependent_objects_TSQL
- dm_exec_cached_plan_dependent_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plan_dependent_objects dynamic management function
ms.assetid: 9b6cf5f7-b267-44fb-aac8-f49c9aa10cc1
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ba7ea5697888a421c5cf9902d795b837aff352fb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85677205"
---
# <a name="sysdm_exec_cached_plan_dependent_objects-transact-sql"></a>sys.dm_exec_cached_plan_dependent_objects(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  각 [!INCLUDE[tsql](../../includes/tsql-md.md)] 실행 계획, CLR(공용 언어 런타임) 실행 계획 및 계획에 연결된 커서에 대해 행을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_exec_cached_plan_dependent_objects(plan_handle)  
```  
  
## <a name="arguments"></a>인수  
*plan_handle*  
는 실행 된 일괄 처리에 대 한 쿼리 실행 계획을 고유 하 게 식별 하는 토큰이 고 해당 계획은 계획 캐시에 상주 합니다. *plan_handle* 은 **varbinary (64)** 입니다.   

*Plan_handle* 는 다음과 같은 동적 관리 개체에서 가져올 수 있습니다.  
  
-   [sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**usecounts**|**int**|실행 컨텍스트 또는 커서가 사용된 횟수입니다.<br /><br /> 열은 Null을 허용하지 않습니다.|  
|**memory_object_address**|**varbinary(8)**|실행 컨텍스트 또는 커서의 메모리 주소입니다.<br /><br /> 열은 Null을 허용하지 않습니다.|  
|**cacheobjtype**|**nvarchar(50)**|계획 캐시 개체 유형입니다. 열은 Null을 허용하지 않습니다. 가능한 값은 아래와 같습니다.<br /><br /> 실행 계획<br /><br /> CLR 컴파일 함수<br /><br /> CLR 컴파일 프로시저<br /><br /> 커서|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW SERVER STATE` 권한이 필요합니다.  
  
## <a name="physical-joins"></a>물리적 조인  
 ![관계 다이어그램](../../relational-databases/system-dynamic-management-views/media/dm-dependent-objects.gif "관계 다이어그램")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|시작|대상|켜기|관계|  
|----------|--------|--------|------------------|  
|**dm_exec_cached_plan_dependent_objects**|**dm_os_memory_objects**|**memory_object_address**|일 대 일|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.syscacheobjects &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)  
  
  
