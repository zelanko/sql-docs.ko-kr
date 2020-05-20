---
title: sys. dm_exec_cached_plans (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd09fde00399dc2e96dc67334a0446ca9f618c3e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830732"
---
# <a name="sysdm_exec_cached_plans-transact-sql"></a>sys.dm_exec_cached_plans(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 빠른 쿼리 실행을 위해 캐시하는 각 쿼리 계획에 대한 행을 반환합니다. 이 동적 관리 뷰를 사용하여 캐시된 쿼리 계획, 캐시된 쿼리 텍스트, 캐시된 계획이 사용한 메모리 양, 캐시된 계획의 재사용 횟수를 찾을 수 있습니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 동적 관리 뷰는 데이터베이스 포함에 영향을 줄 수 있는 정보 또는 사용자가 액세스할 수 있는 다른 데이터베이스 정보를 노출할 수 없습니다. 이 정보를 노출 하지 않도록 하기 위해 연결 된 테 넌 트에 속하지 않는 데이터를 포함 하는 모든 행이 필터링 됩니다. 또한 **memory_object_address** 및 **pool_id** 열의 값이 필터링 됩니다. 열 값이 NULL로 설정 됩니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_exec_cached_plans**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|bucketid|**int**|항목이 캐시된 해시 버킷의 ID입니다. 값은 0에서 캐시 유형별 해시 테이블 크기까지의 범위를 나타냅니다.<br /><br /> SQL Plans 및 Object Plans 캐시의 경우 해시 테이블 크기는 32비트 시스템에서 최대 10007까지, 64비트 시스템에서 최대 40009까지 가능합니다. Bound Trees 캐시의 경우 해시 테이블 크기는 32비트 시스템에서 최대 1009까지, 64비트 시스템에서 최대 4001까지 가능합니다. Extended Stored Procedures 캐시의 경우 해시 테이블 크기는 32비트 및 64비트 시스템에서 최대 127까지 가능합니다.|  
|refcounts|**int**|이 캐시 개체를 참조하는 캐시 개체의 수입니다. 항목이 캐시에 있으려면 **Refcounts**가 1 이상이어야 합니다.|  
|usecounts|**int**|캐시 개체를 조회한 횟수입니다. 매개 변수가 있는 쿼리가 캐시에서 계획을 찾는 경우에는 증가하지 않습니다. 실행 계획을 사용하는 경우에는 여러 번 증가할 수 있습니다.|  
|size_in_bytes|**int**|캐시 개체가 사용한 바이트 수입니다.|  
|memory_object_address|**varbinary(8)**|캐시된 항목의 메모리 주소입니다. 이 값은 [sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)와 함께 사용하여 캐시된 계획의 메모리 분석을 가져올 수 있으며 [sys.dm_os_memory_cache_entries](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)와 함께 사용하여 항목 캐시 비용을 구할 수 있습니다.|  
|cacheobjtype|**nvarchar (34)**|캐시에 있는 개체의 유형입니다. 이 값은<br /><br /> Compiled Plan<br /><br /> Compiled Plan Stub<br /><br /> Parse Tree<br /><br /> Extended Proc<br /><br /> CLR Compiled Func<br /><br /> CLR Compiled Proc|  
|objtype|**nvarchar (16)**|개체의 유형입니다. 다음은 가능한 값과 해당 설명입니다.<br /><br /> Proc: 저장 프로시저<br />준비 됨: 준비 된 문<br />임시: 임시 쿼리 [!INCLUDE[tsql](../../includes/tsql-md.md)]는 원격 프로시저 호출 대신 **osql** 또는 **sqlcmd** 를 사용 하 여 언어 이벤트로 제출 된를 나타냅니다.<br />ReplProc: Replication-filter-프로시저<br />트리거: 트리거<br />보기: 보기<br />기본값: 기본값<br />UsrTab: 사용자 테이블<br />SysTab: 시스템 테이블<br />Check: CHECK 제약 조건<br />규칙: 규칙|  
|plan_handle|**varbinary(64)**|메모리 내 계획의 식별자입니다. 이 식별자는 일시적이며 계획이 캐시에 있는 동안에만 일정하게 유지됩니다. 이 값은 다음 동적 관리 함수와 함께 사용할 수 있습니다.<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|  
|pool_id|**int**|이 계획 메모리 사용량이 계산된 리소스 풀의 ID입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
 <sup>1</sup>  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="examples"></a>예  
  
### <a name="a-returning-the-batch-text-of-cached-entries-that-are-reused"></a>A. 다시 사용된 캐시된 항목의 일괄 처리 텍스트 반환  
 다음 예에서는 두 번 이상 사용되었던 모든 캐시된 항목의 SQL 텍스트를 반환합니다.  
  
```sql  
SELECT usecounts, cacheobjtype, objtype, text   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
WHERE usecounts > 1   
ORDER BY usecounts DESC;  
GO  
```  
  
### <a name="b-returning-query-plans-for-all-cached-triggers"></a>B. 모든 캐시된 트리거에 대한 쿼리 계획 반환  
 다음 예에서는 모든 캐시된 트리거의 쿼리 계획을 반환합니다.  
  
```sql  
SELECT plan_handle, query_plan, objtype   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_query_plan(plan_handle)   
WHERE objtype ='Trigger';  
GO  
```  
  
### <a name="c-returning-the-set-options-with-which-the-plan-was-compiled"></a>C. 계획 컴파일 시 사용된 SET 옵션의 반환  
 다음 예에서는 계획 컴파일 시 사용된 SET 옵션을 반환합니다. `sql_handle`계획에 대 한도 반환 됩니다. PIVOT 연산자는 `set_options` 및 특성을 행이 아닌 열로 출력 하는 데 사용 됩니다 `sql_handle` . 에서 반환 되는 값에 대 한 자세한 내용은 `set_options` [Dm_exec_plan_attributes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)을 참조 하십시오.  
  
```sql  
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
  
### <a name="d-returning-the-memory-breakdown-of-all-cached-compiled-plans"></a>D. 모든 캐시된 컴파일 계획의 메모리 분석 반환  
 다음 예에서는 캐시에서 모든 컴파일된 계획에 사용되는 메모리 분석을 반환합니다.  
  
```sql  
SELECT plan_handle, ecp.memory_object_address AS CompiledPlan_MemoryObject,   
    omo.memory_object_address, type, page_size_in_bytes   
FROM sys.dm_exec_cached_plans AS ecp   
JOIN sys.dm_os_memory_objects AS omo   
    ON ecp.memory_object_address = omo.memory_object_address   
    OR ecp.memory_object_address = omo.parent_address  
WHERE cacheobjtype = 'Compiled Plan';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [dm_exec_plan_attributes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)   
 [dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [dm_os_memory_objects &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)   
 [dm_os_memory_cache_entries &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  


