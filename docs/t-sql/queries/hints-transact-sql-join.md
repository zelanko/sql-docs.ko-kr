---
title: "조인 힌트 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Join Hint
- Join_Hint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- HASH join hint
- REMOTE join hint
- LOOP join hint
- join hints
- MERGE join hint
- hints [SQL Server], join
ms.assetid: 09069f4a-f2e3-4717-80e1-c0110058efc4
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 230241b9626c8d2790fb55fa82c40bab24613dbc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="hints-transact-sql---join"></a>조인 힌트 (Transact SQL)-
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  조인 힌트는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 쿼리 최적화 프로그램이 두 테이블 간의 조인 전략을 강제 적용하도록 지정합니다. 조인 및 조인 구문에 대 한 일반 정보를 참조 하십시오. [from&#40; Transact SQL &#41; ](../../t-sql/queries/from-transact-sql.md).  
  
> [!IMPORTANT]  
>  때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 일반적으로 쿼리에 대해 최적의 실행 계획을 선택 하는 힌트를 포함 하는 것이 좋습니다, \<알아서 >, 숙련 된 개발자가 최후의 수단 으로만 사용할 수 및 데이터베이스 관리자입니다.
  
 **적용 대상:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
<join_hint> ::=   
     { LOOP | HASH | MERGE | REMOTE }  
```  
  
## <a name="arguments"></a>인수  
 LOOP | HASH | MERGE  
 쿼리의 조인이 루프, 해시 또는 병합을 사용하도록 지정합니다. LOOP | HASH | MERGE JOIN을 사용하면 두 테이블 간에 특정 조인이 적용됩니다. LOOP에는 조인 형식으로 RIGHT 또는 FULL을 지정할 수 없습니다.  
  
 REMOTE  
 오른쪽 테이블에서 조인 작업을 수행하도록 지정합니다. 왼쪽 테이블이 로컬 테이블이고 오른쪽 테이블이 원격 테이블인 경우에 유용합니다. 왼쪽 테이블의 행 수가 오른쪽 테이블보다 적을 때만 REMOTE를 사용해야 합니다.  
  
 오른쪽 테이블이 로컬이면 조인이 로컬로 수행됩니다. 두 테이블 모두 원격 테이블이지만 데이터 원본이 다른 경우 REMOTE를 사용하면 오른쪽 테이블에서 조인이 수행됩니다. 두 테이블 모두 원격 테이블이며 데이터 원본이 동일한 경우에는 REMOTE를 사용할 필요가 없습니다.  
  
 조인 조건자에서 비교되는 값 중의 하나가 COLLATE 절을 사용하여 다른 데이터 정렬로 캐스팅되는 경우에는 REMOTE를 사용할 수 없습니다.  
  
 REMOTE는 INNER JOIN 작업에 대해서만 사용할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 조인 힌트는 쿼리의 FROM 절에서 지정됩니다. 조인 힌트는 두 테이블 간에 조인 전략을 강제 적용합니다. 두 테이블에 대해 조인 힌트가 지정된 경우 쿼리 최적화 프로그램이 ON 키워드의 위치를 기반으로 하여 쿼리에서 조인된 모든 테이블에 대해 조인 순서를 강제 적용합니다. CROSS JOIN이 ON 절 없이 사용된 경우 괄호를 사용하여 조인 순서를 나타낼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-hash"></a>1. HASH 사용  
 다음 예에서는 쿼리의 `JOIN` 연산이 `HASH` 조인에 의해 수행되도록 지정합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT p.Name, pr.ProductReviewID  
FROM Production.Product AS p  
LEFT OUTER HASH JOIN Production.ProductReview AS pr  
ON p.ProductID = pr.ProductID  
ORDER BY ProductReviewID DESC;  
```  
  
### <a name="b-using-loop"></a>2. LOOP 사용  
 다음 예에서는 쿼리의 `JOIN` 연산이 `LOOP` 조인에 의해 수행되도록 지정합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
    INNER LOOP JOIN Sales.SalesPerson AS sp  
    ON spqh.SalesPersonID = sp.SalesPersonID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
### <a name="c-using-merge"></a>3. MERGE 사용  
 다음 예에서는 쿼리의 `JOIN` 연산이 `MERGE` 조인에 의해 수행되도록 지정합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT poh.PurchaseOrderID, poh.OrderDate, pod.ProductID, pod.DueDate, poh.VendorID   
FROM Purchasing.PurchaseOrderHeader AS poh  
INNER MERGE JOIN Purchasing.PurchaseOrderDetail AS pod   
    ON poh.PurchaseOrderID = pod.PurchaseOrderID;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [힌트 &#40; Transact SQL &#41;](../../t-sql/queries/hints-transact-sql.md)  
  
  

