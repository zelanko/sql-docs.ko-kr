---
title: sys.fn_validate_plan_guide (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_validate_plan_guide
- sys.fn_validate_plan_guide_TSQL
- fn_validate_plan_guide
- fn_validate_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_validate_plan_guide function
- sys.fn_validate_plan_guide function
ms.assetid: 3af8b47a-936d-4411-91d1-d2d16dda5623
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6b941fabfd4ebbd3ca41375622bf682f12b0fc26
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysfnvalidateplanguide-transact-sql"></a>sys.fn_validate_plan_guide(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 계획 지침의 유효성을 확인할 수 있습니다. sys.fn_validate_plan_guide 함수는 계획 지침이 쿼리에 적용될 때 발생하는 첫 번째 오류 메시지를 반환합니다. 계획 지침이 유효하면 빈 행 집합이 반환됩니다. 데이터베이스의 물리적 디자인을 변경한 후에 계획 지침이 잘못될 수 있습니다. 예를 들어 계획 지침이 특정 인스턴스를 지정한 이후 해당 인스턴스가 삭제되면 쿼리가 더 이상 계획 지침을 사용할 수 없습니다.  
  
 계획 지침을 확인하여 최적화 프로그램이 수정하지 않고 해당 계획을 사용할 수 있는지 확인할 수 있습니다. 작동 결과에 따라 계획 지침을 삭제할지 결정하고 쿼리를 반환하거나 데이터베이스 디자인을 수정할 수 있습니다. 예를 들어 계획 지침에 지정된 인덱스를 다시 만들어서 이 작업을 수행할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sys.fn_validate_plan_guide ( plan_guide_id )  
```  
  
## <a name="arguments"></a>인수  
 *plan_guide_id*  
 보고 되는 계획 지침의 ID는 [sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) 카탈로그 뷰에 있습니다. *plan_guide_id* 은 **int** 이며 기본값은 없습니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|msgnum|**int**|오류 메시지 ID입니다.|  
|severity|**tinyint**|1에서 25 사이의 메시지 심각도입니다.|  
|state|**smallint**|오류가 발생한 코드의 지점을 나타내는 오류의 상태 번호입니다.|  
|message|**nvarchar(2048)**|오류의 메시지 텍스트입니다.|  
  
## <a name="permissions"></a>Permissions  
 OBJECT 범위 계획 지침에는 참조된 개체에 대한 VIEW DEFINITION 또는 ALTER 권한이 필요하고 계획 지침에 제공된 쿼리나 일괄 처리에 대한 권한이 필요합니다. 예를 들어 일괄 처리에 SELECT 문이 있으면 참조 개체의 SELECT 권한이 필요합니다.  
  
 SQL 범위 또는 TEMPLATE 범위의 계획 지침에는 데이터베이스에 대한 ALTER 권한과 계획 지침에 제공된 쿼리나 일괄 배치를 컴파일할 수 있는 권한이 필요합니다. 예를 들어 일괄 처리에 SELECT 문이 있으면 참조 개체의 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-validating-all-plan-guides-in-a-database"></a>1. 데이터베이스에 있는 모든 계획 지침 확인  
 다음 예에서는 현재 데이터베이스에 있는 모든 계획 지침의 유효성을 확인합니다. 빈 결과 집합이 반환되면 모든 계획 지침을 사용할 수 있습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT plan_guide_id, msgnum, severity, state, message  
FROM sys.plan_guides  
CROSS APPLY fn_validate_plan_guide(plan_guide_id);  
GO  
```  
  
### <a name="b-testing-plan-guide-validation-before-implementing-a-change-to-the-database"></a>2. 데이터베이스를 변경하기 전에 계획 지침 유효성 테스트  
 다음 예에서는 명시적 트랜잭션을 사용하여 인덱스를 삭제합니다. `sys.fn_validate_plan_guide` 함수는이 작업은 데이터베이스에 있는 모든 계획 지침 무효화 됩니다 있는지 여부를 확인 하려면 실행 합니다. 함수의 결과에 따라 `DROP INDEX` 문이 커밋되거나 트랜잭션이 롤백되고 인덱스가 삭제되지 않습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DROP INDEX IX_SalesOrderHeader_CustomerID ON Sales.SalesOrderHeader;  
-- Check for invalid plan guides.  
IF EXISTS (SELECT plan_guide_id, msgnum, severity, state, message  
           FROM sys.plan_guides  
           CROSS APPLY sys.fn_validate_plan_guide(plan_guide_id))  
    ROLLBACK TRANSACTION;  
ELSE  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [계획 지침](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
