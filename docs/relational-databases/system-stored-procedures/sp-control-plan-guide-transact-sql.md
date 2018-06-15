---
title: sp_control_plan_guide (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_control_plan_guide
- sp_control_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_plan_guide
ms.assetid: c96d43d5-6507-4d66-b3f5-f44c0617cb5c
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9f7514e07f4a363072dc527827a858becab8dc0d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238380"
---
# <a name="spcontrolplanguide-transact-sql"></a>sp_control_plan_guide(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  계획 지침을 삭제하거나 활성화하거나 비활성화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_control_plan_guide [ @operation = ] N'<control_option>'  
  [ , [ @name = ] N'plan_guide_name' ]  
  
<control_option>::=  
{   
    DROP   
  | DROP ALL  
  | DISABLE  
  | DISABLE ALL  
  | ENABLE   
  | ENABLE ALL  
}  
```  
  
## <a name="arguments"></a>인수  
 **N'** *plan_guide_name* **'**  
 삭제되거나 활성화되거나 비활성화되는 계획 지침을 지정합니다. *plan_guide_name* 현재 데이터베이스로 확인 됩니다. 지정 하지 않으면 *plan_guide_name* 은 기본적으로 NULL입니다.  
  
 DROP  
 에 지정 된 계획 지침 삭제 *plan_guide_name*합니다. 계획 지침이 삭제된 후 이전에 이 계획 지침에 맞춘 쿼리를  실행할 경우 이 계획 지침의 영향을 받지 않습니다.  
  
 DROP ALL  
 현재 데이터베이스에 있는 모든 계획 지침을 삭제합니다. **N' * * * plan_guide_name* DROP ALL이 지정 되 면 지정할 수 없습니다.  
  
 DISABLE  
 에 지정 된 계획 지침을 사용 하지 않도록 설정 *plan_guide_name*합니다. 계획 지침이 비활성화된 후 이전에 이 계획 지침에 맞춘 쿼리를 실행할 경우 이 계획 지침의 영향을 받지 않습니다.  
  
 DISABLE ALL  
 현재 데이터베이스에 있는 모든 계획 지침을 비활성화합니다. **N' * * * plan_guide_name* 모두 사용 안 함 지정 된 경우 지정할 수 없습니다.  
  
 ENABLE  
 로 지정 된 계획 지침을 활성화 *plan_guide_name*합니다. 계획 지침을 활성화하면 적합한 쿼리에 맞출 수 있습니다. 기본적으로 계획 지침은 만들어질 때 활성화됩니다.  
  
 ENABLE ALL  
 현재 데이터베이스에 있는 모든 계획 지침을 활성화합니다. **N'***plan_guide_name***'** 모두 사용 지정 된 경우 지정할 수 없습니다.  
  
## <a name="remarks"></a>주의  
 활성화 여부에 관계없이 계획 지침에서 참조하는 함수, 저장 프로시저 또는 DML 트리거를 삭제하거나 수정하려고 하면 오류가 발생합니다.  
  
 비활성화된 계획 지침을 비활성화하거나 활성화된 계획 지침을 활성화하면 아무런 영향을 미치지 않고 오류 없이 실행됩니다.  
  
 계획 지침은 모든 버전에서 사용할 수 없는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요. 실행할 수 있습니다 **sp_control_plan_guide** 의 모든 버전에서 DROP 또는 DROP ALL 옵션으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="permissions"></a>Permissions  
 실행할 **sp_control_plan_guide** OBJECT 유형의 계획 지침에서 (지정 만든  **@type ='** 개체 **'** ) 된 개체에 대 한 ALTER 권한이 필요 하는 계획 지침에서 참조 됩니다. 다른 모든 계획 지침에는 ALTER DATABASE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-enabling-disabling-and-dropping-a-plan-guide"></a>1. 계획 지침 활성화, 비활성화 및 삭제  
 다음 예에서는 계획 지침을 만들고 비활성화하고 활성화하고 삭제합니다.  
  
```  
--Create a procedure on which to define the plan guide.  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country;  
END  
GO  
--Create the plan guide.  
EXEC sp_create_plan_guide N'Guide3',  
    N'SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country',  
    N'OBJECT',  
    N'Sales.GetSalesOrderByCountry',  
    NULL,  
    N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
GO  
--Disable the plan guide.  
EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
GO  
--Enable the plan guide.  
EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
GO  
--Drop the plan guide.  
EXEC sp_control_plan_guide N'DROP', N'Guide3';  
```  
  
### <a name="b-disabling-all-plan-guides-in-the-current-database"></a>2. 현재 데이터베이스에 있는 모든 계획 지침 비활성화  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 모든 계획 지침을 비활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_control_plan_guide N'DISABLE ALL';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.plan_guides&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [계획 지침](../../relational-databases/performance/plan-guides.md)  
  
  
