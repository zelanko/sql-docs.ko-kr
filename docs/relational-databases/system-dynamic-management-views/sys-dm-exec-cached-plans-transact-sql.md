---
title: sys.dm_exec_cached_plans (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plans
- dm_exec_cached_plans
- dm_exec_cached_plans_TSQL
- sys.dm_exec_cached_plans_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plans dynamic management view
ms.assetid: 95b707d3-3a93-407f-8e88-4515d4f2039d
caps.latest.revision: 44
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 44740badeb2d763727aeba2ce81adc524e3de0d4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43100772"
---
# <a name="sysdmexeccachedplans-transact-sql"></a>sys.dm_exec_cached_plans(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 빠른 쿼리 실행을 위해 캐시하는 각 쿼리 계획에 대한 행을 반환합니다. 이 동적 관리 뷰를 사용하여 캐시된 쿼리 계획, 캐시된 쿼리 텍스트, 캐시된 계획이 사용한 메모리 양, 캐시된 계획의 재사용 횟수를 찾을 수 있습니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이러한 정보 노출을 방지하기 위해 연결된 테넌트에 속하지 않는 데이터가 포함된 행은 모두 필터링됩니다. 또한 열에 값 **memory_object_address** 및 **pool_id** 필터링 되는 열 값이 NULL로 설정 됩니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_exec_cached_plans**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|bucketid|**int**|항목이 캐시된 해시 버킷의 ID입니다. 값은 0에서 캐시 유형별 해시 테이블 크기까지의 범위를 나타냅니다.<br /><br /> SQL Plans 및 Object Plans 캐시의 경우 해시 테이블 크기는 32비트 시스템에서 최대 10007까지, 64비트 시스템에서 최대 40009까지 가능합니다. Bound Trees 캐시의 경우 해시 테이블 크기는 32비트 시스템에서 최대 1009까지, 64비트 시스템에서 최대 4001까지 가능합니다. Extended Stored Procedures 캐시의 경우 해시 테이블 크기는 32비트 및 64비트 시스템에서 최대 127까지 가능합니다.|  
|refcounts|**int**|이 캐시 개체를 참조하는 캐시 개체의 수입니다. **Refcounts** 항목을 캐시에 적어도 1 이어야 합니다.|  
|usecounts|**int**|캐시 개체를 조회한 횟수입니다. 매개 변수가 있는 쿼리가 캐시에서 계획을 찾는 경우에는 증가하지 않습니다. 실행 계획을 사용하는 경우에는 여러 번 증가할 수 있습니다.|  
|size_in_bytes|**int**|캐시 개체가 사용한 바이트 수입니다.|  
|memory_object_address|**varbinary(8)**|캐시된 항목의 메모리 주소입니다. 이 값을 사용 하 여 사용할 수 있습니다 [sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) 캐시 된 계획의 메모리 분석을 가져오려면 [sys.dm_os_memory_cache_entries](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)항목 캐시 비용을 가져오려고와 함께 사용 합니다.|  
|cacheobjtype|**nvarchar(34)**|캐시에 있는 개체의 유형입니다. 이 값은<br /><br /> Compiled Plan<br /><br /> Compiled Plan Stub<br /><br /> Parse Tree<br /><br /> Extended Proc<br /><br /> CLR Compiled Func<br /><br /> CLR Compiled Proc|  
|objtype|**nvarchar(16)**|개체의 유형입니다. 사용 가능한 값과 해당 설명을 다음과 같습니다.<br /><br /> 저장된 프로시저가 프로시저:<br />준비: 준비 된 문<br />임시: 임시 쿼리입니다. 가리키는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 사용 하 여 언어 이벤트로 전송 된 **osql** 또는 **sqlcmd** 대신 원격 프로시저 호출으로.<br />ReplProc: 복제 필터 프로시저<br />트리거: 트리거<br />보기: 보기<br />기본값: 기본값<br />UsrTab: 사용자 테이블<br />SysTab: 시스템 테이블<br />CHECK 제약 조건 확인:<br />규칙: 규칙|  
|plan_handle|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값은 다음 동적 관리 함수와 함께 사용할 수 있습니다.<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|  
|pool_id|**int**|이 계획 메모리 사용량이 계산된 리소스 풀의 ID입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
 <sup>1.</sup>  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   

## <a name="examples"></a>예  
  
### <a name="a-returning-the-batch-text-of-cached-entries-that-are-reused"></a>1. 다시 사용된 캐시된 항목의 일괄 처리 텍스트 반환  
 다음 예에서는 두 번 이상 사용되었던 모든 캐시된 항목의 SQL 텍스트를 반환합니다.  
  
```  
SELECT usecounts, cacheobjtype, objtype, text   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
WHERE usecounts > 1   
ORDER BY usecounts DESC;  
GO  
```  
  
### <a name="b-returning-query-plans-for-all-cached-triggers"></a>2. 모든 캐시된 트리거에 대한 쿼리 계획 반환  
 다음 예에서는 모든 캐시된 트리거의 쿼리 계획을 반환합니다.  
  
```  
SELECT plan_handle, query_plan, objtype   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_query_plan(plan_handle)   
WHERE objtype ='Trigger';  
GO  
```  
  
### <a name="c-returning-the-set-options-with-which-the-plan-was-compiled"></a>3. 계획 컴파일 시 사용된 SET 옵션의 반환  
 다음 예에서는 계획 컴파일 시 사용된 SET 옵션을 반환합니다. `sql_handle` 계획도 반환 됩니다. PIVOT 연산자는 출력 하는 `set_options` 및 `sql_handle` 특성 행 대신 열으로. 반환 된 값에 대 한 자세한 내용은 `set_options`를 참조 하세요 [sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)합니다.  
  
```  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
      SELECT plan_handle, epa.attribute, epa.value   
      FROM sys.dm_exec_cached_plans   
      OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
      WHERE cacheobjtype = 'Compiled Plan'  
      ) AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
### <a name="d-returning-the-memory-breakdown-of-all-cached-compiled-plans"></a>4. 모든 캐시된 컴파일 계획의 메모리 분석 반환  
 다음 예에서는 캐시에서 모든 컴파일된 계획에 사용되는 메모리 분석을 반환합니다.  
  
```  
SELECT plan_handle, ecp.memory_object_address AS CompiledPlan_MemoryObject,   
    omo.memory_object_address, type, page_size_in_bytes   
FROM sys.dm_exec_cached_plans AS ecp   
JOIN sys.dm_os_memory_objects AS omo   
    ON ecp.memory_object_address = omo.memory_object_address   
    OR ecp.memory_object_address = omo.parent_address  
WHERE cacheobjtype = 'Compiled Plan';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_os_memory_objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)   
 [sys.dm_os_memory_cache_entries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  


