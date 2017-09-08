---
title: SET FORCEPLAN (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_FORCEPLAN_TSQL
- SET FORCEPLAN
- FORCEPLAN
- FORCEPLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- joins [SQL Server], overriding query optimizer process
- FORCEPLAN option
- SET FORCEPLAN statement
- query optimizer [SQL Server], optimizing process
- overriding query optimizer process
ms.assetid: b6c0b08f-2060-4696-9e12-50cb7e674321
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df0bb88faa940a54f3b3eb14c34998b1982879c6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-forceplan-transact-sql"></a>SET FORCEPLAN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  FORCEPLAN이 ON으로 설정되어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리의 FROM 절에 테이블이 나타나는 순서대로 조인을 처리합니다. 또한 FORCEPLAN을 ON으로 설정하면 쿼리 계획을 구성하는 데 다른 유형의 조인이 필요하거나 조인 힌트 또는 쿼리 힌트로 요청되지 않은 경우 중첩 루프 조인이 강제로 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET FORCEPLAN { ON | OFF }  
```  
  
## <a name="remarks"></a>주의  
 SET FORCEPLAN 옵션은 기본적으로 쿼리 최적화 프로그램이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 처리하는 데 사용하는 논리보다 우선 적용됩니다. 이 옵션 설정에 상관 없이 반환되는 데이터는 같습니다. 쿼리를 충족시키기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 테이블을 처리하는 방법에만 차이가 있습니다.  
  
 쿼리 최적화 프로그램 참고를 사용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 SELECT 문을 처리하는 방법을 지정할 수도 있습니다.  
  
 SET FORCEPLAN 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 SET FORCEPLAN 권한은 기본적으로 모든 사용자로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 테이블 4개의 조인을 수행합니다. `SHOWPLAN_TEXT` 옵션을 설정해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 쿼리를 다른 방식으로 처리하는 방법에 대한 정보를 반환할 수 있도록 `SET FORCE_PLAN` 옵션이 설정되어 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Make sure FORCEPLAN is set to OFF.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Example where the query plan is not forced.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET FORCEPLAN to ON.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN ON;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Reexecute inner join to see the effect of SET FORCEPLAN ON.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e   
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET showplan_all 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET showplan_text 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  

