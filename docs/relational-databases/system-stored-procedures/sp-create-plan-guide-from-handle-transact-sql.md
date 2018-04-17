---
title: sp_create_plan_guide_from_handle (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide_from_handle_TSQL
- sp_create_plan_guide_from_handle
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide_from_handle
ms.assetid: 02cfb76f-a0f9-4b42-a880-1c3e7d64fe41
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d82828ccf7e1628140a6a20f51685334dd01982
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spcreateplanguidefromhandle-transact-sql"></a>sp_create_plan_guide_from_handle(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  계획 캐시의 쿼리 계획에서 한 개 이상의 계획 지침을 만듭니다. 이 저장 프로시저를 사용하여 쿼리 최적화 프로그램이 항상 지정한 쿼리에 특정 쿼리 계획을 사용하도록 할 수 있습니다. 계획 지침에 대한 자세한 내용은 [Plan Guides](../../relational-databases/performance/plan-guides.md)를 참조하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_create_plan_guide_from_handle [ @name = ] N'plan_guide_name'  
    , [ @plan_handle = ] plan_handle  
    , [ [ @statement_start_offset = ] { statement_start_offset | NULL } ]  
```  
  
## <a name="arguments"></a>인수  
 [ @name =] N'*plan_guide_name*'  
 계획 지침의 이름입니다. 계획 지침 이름은 현재 데이터베이스 범위에 적용됩니다. *plan_guide_name* 에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md) 숫자 기호 시작할 수 없습니다 (#). 최대 길이 *plan_guide_name* 는 124 자입니다.  
  
 [ @plan_handle =] *plan_handle*  
 계획 캐시의 일괄 처리를 식별합니다. *plan_handle* 은 **varbinary(64)**합니다. *plan_handle* 에서 가져올 수는 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 동적 관리 뷰.  
  
 [ @statement_start_offset =] { *statement_start_offset* | NULL}]  
 지정 된 일괄 처리 안에 있는 문의 시작 위치를 식별 *plan_handle*합니다. *statement_start_offset* 은 **int**, 기본값은 NULL입니다.  
  
 문 오프셋의 statement_start_offset 열에 해당는 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 동적 관리 뷰.  
  
 NULL이 지정되거나 문 오프셋이 지정되지 않으면 지정한 계획 핸들에 대한 쿼리 계획을 사용하여 일괄 처리에서 각 문에 대해 계획 지침이 만들어집니다. 결과 계획 지침은 특정 계획을 강제로 사용하게 하는 USE PLAN 쿼리를 사용하는 계획 지침과 동일합니다.  
  
## <a name="remarks"></a>주의  
 계획 지침은 일부 문 유형에 대해 만들 수 없습니다. 일괄 처리의 문에 대해 계획 지침을 만들 수 없으면 저장 프로시저가 문을 무시하고 일괄 처리의 다음 문을 계속 수행합니다. 문이 같은 일괄 처리로 여러 번 수행되면 마지막 수행을 위한 계획이 활성화되고 문에 대한 이전 계획이 비활성화됩니다. 일괄 처리의 문은 계획 지침에 사용할 수 없습니다. 오류 10532이 발생하고 문이 실패합니다. 이 오류의 발생을 방지하려면 항상 sys.dm_exec_query_stats 동적 관리 뷰에서 계획 핸들을 가져오는 것이 좋습니다.  
  
> [!IMPORTANT]  
>  sp_create_plan_guide_from_handle은 계획 캐시에 표시된 계획에 따라 계획 지침을 만듭니다. 이것은 일괄 처리 텍스트, [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 XML 실행 계획을 문자 단위로 계획 캐시에서 결과 계획 지침으로 가져옵니다. 이러한 텍스트 문자열에는 중요한 정보가 포함될 수 있습니다. 이 경우 이러한 정보는 데이터베이스의 메타데이터에 저장됩니다. 적절 한 권한이 있는 사용자는 sys.plan_guides 카탈로그 뷰를 사용 하 여이 정보를 볼 수 있습니다 및 **계획 지침 속성** 대화 상자에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 중요한 정보가 계획 지침에서 공개되지 않게 하려면 계획 캐시에서 만든 계호기 지침을 검토하는 것이 좋습니다.  
  
## <a name="creating-plan-guides-for-multiple-statements-within-a-query-plan"></a>쿼리 힌트 내에 여러 명령문에 대한 계획 지침 만들기  
 sp_create_plan_guide와 같이 sp_create_plan_guide_from_handle은 계획 캐시에서 대상 일괄 처리 또는 모듈에 대한 쿼리 계획을 제거합니다. 이 작업을 통해 모든 사용자가 새 계획 지침을 사용하여 시작할 수 있습니다. 단일 쿼리 계획 내에 여러 명령문에 대한 계획 지침을 만들 경우 명시적 트랜잭션에 모든 계획 지침을 만들어 캐시에서 계획 제거를 연기할 수 있습니다. 이 방법을 사용하여 트랜잭션이 완료되고 지정한 각 문에 대한 계획 지침을 만들 때까지 캐시에 계획이 남아 있게 할 수 있습니다. 예 B를 참조하십시오.  
  
## <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다. 그리고 sp_create_plan_guide_from_handle을 사용하여 만든 각 계획 지침에 대해 개별 권한이 필요합니다. OBJECT 유형의 계획 지침을 만들려면 참조된 개체에 ALTER 권한이 있어야 합니다. SQL 또는 TEMPLATE 유형의 계획 지침을 만들려면 현재 데이터베이스에 대한 ALTER 권한이 있어야 합니다. 만들어질 계획 지침 유형을 확인하려면 다음 쿼리를 실행하십시오.  
  
```  
SELECT cp.plan_handle, sql_handle, st.text, objtype   
FROM sys.dm_exec_cached_plans AS cp  
JOIN sys.dm_exec_query_stats AS qs ON cp.plan_handle = qs.plan_handle  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st;  
```  
  
 계획 지침을 만들 문이 포함된 행에서 결과 집합의 `objtype` 열을 검사하십시오. `Proc` 값은 계획 지침이 OBJECT 유형임을 나타냅니다. `AdHoc` 또는 `Prepared`와 같은 다른 값은 결과 지침이 SQL 유형임을 나타냅니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-plan-guide-from-a-query-plan-in-the-plan-cache"></a>1. 계획 캐시의 쿼리 계획에서 계획 지침 만들기  
 다음 예에서는 계획 캐시에서 쿼리 계획을 지정하여 단일 SELECT 문에 대한 계획 지침을 만듭니다. 이 예에서는 계획 지침이 만들어지는 간단한 `SELECT` 문을 실행하여 시작합니다. 이 쿼리의 계획은 `sys.dm_exec_sql_text` 및 `sys.dm_exec_text_query_plan` 동적 관리 뷰를 사용하여 검사됩니다. 그런 다음 쿼리와 관련된 계획 캐시에서 쿼리 계획을 지정하여 쿼리에 대한 계획 지침을 만듭니다. 이 예에서 마지막 문은 계획 지침의 존재를 확인합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT WorkOrderID, p.Name, OrderQty, DueDate  
FROM Production.WorkOrder AS w   
JOIN Production.Product AS p ON w.ProductID = p.ProductID  
WHERE p.ProductSubcategoryID > 4  
ORDER BY p.Name, DueDate;  
GO  
-- Inspect the query plan by using dynamic management views.  
SELECT * FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle)  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
-- Create a plan guide for the query by specifying the query plan in the plan cache.  
DECLARE @plan_handle varbinary(64);  
DECLARE @offset int;  
SELECT @plan_handle = plan_handle, @offset = qs.statement_start_offset  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
  
EXECUTE sp_create_plan_guide_from_handle   
    @name =  N'Guide1',  
    @plan_handle = @plan_handle,  
    @statement_start_offset = @offset;  
GO  
-- Verify that the plan guide is created.  
SELECT * FROM sys.plan_guides  
WHERE scope_batch LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
```  
  
### <a name="b-creating-multiple-plan-guides-for-a-multistatement-batch"></a>2. 다중 문 일괄 처리에 대한 여러 계획 지침 만들기  
 다음 예에서는 다중 문 일괄 처리 내에 있는 두 개의 문에 대한 계획 지침을 만듭니다. 계획 지침은 명시적 트랜잭션 내에서 만들어지므로 일괄 처리에 대한 쿼리 계획은 첫 번째 계획 지침을 만든 후에 계획 캐시에서 제거되지 않습니다. 이 예에서는 다중 문 일괄 처리를 실행하여 시작합니다. 일괄 처리에 대한 계획은 동적 관리 뷰를 사용하여 검사됩니다. 일괄 처리의 각 문에 대한 행이 반환됩니다. 그런 다음 `@statement_start_offset` 매개 변수를 지정하여 일괄 처리의 첫 번째 문과 세 번째 문에 대한 계획 지침을 만듭니다. 이 예에서 마지막 문은 계획 지침의 존재를 확인합니다.  
  
 [!code-sql[PlanGuides#Create_From_Handle2](../../relational-databases/system-stored-procedures/codesnippet/tsql/sp-create-plan-guide-fro_1.sql)]  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [계획 지침](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_text_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
  
  
