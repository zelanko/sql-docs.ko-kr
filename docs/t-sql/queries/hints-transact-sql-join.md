---
title: 조인 힌트(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f6f89e973d5f021dbd48a1bc7fc8234f9c9b6a89
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67902012"
---
# <a name="hints-transact-sql---join"></a>힌트 (Transact-SQL) - 조인
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  조인 힌트는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 쿼리 최적화 프로그램이 두 테이블 간의 조인 전략을 강제 적용하도록 지정합니다. 조인 및 조인 구문에 대한 자세한 내용은 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
> [!CAUTION]  
>  일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리에 대해 최상의 실행 계획을 선택하므로 숙련된 개발자 및 데이터베이스 관리자가 마지막 방법으로만 힌트를 사용하는 것이 좋습니다.
  
 **적용 대상:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
## <a name="remarks"></a>설명  
 조인 힌트는 쿼리의 FROM 절에서 지정됩니다. 조인 힌트는 두 테이블 간에 조인 전략을 강제 적용합니다. 두 테이블에 대해 조인 힌트가 지정된 경우 쿼리 최적화 프로그램이 ON 키워드의 위치를 기반으로 하여 쿼리에서 조인된 모든 테이블에 대해 조인 순서를 강제 적용합니다. CROSS JOIN이 ON 절 없이 사용된 경우 괄호를 사용하여 조인 순서를 나타낼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-hash"></a>A. HASH 사용  
 다음 예에서는 쿼리의 `JOIN` 연산이 `HASH` 조인에 의해 수행되도록 지정합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT p.Name, pr.ProductReviewID  
FROM Production.Product AS p  
LEFT OUTER HASH JOIN Production.ProductReview AS pr  
ON p.ProductID = pr.ProductID  
ORDER BY ProductReviewID DESC;  
```  
  
### <a name="b-using-loop"></a>B. LOOP 사용  
 다음 예에서는 쿼리의 `JOIN` 연산이 `LOOP` 조인에 의해 수행되도록 지정합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
    INNER LOOP JOIN Sales.SalesPerson AS sp  
    ON spqh.SalesPersonID = sp.SalesPersonID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
### <a name="c-using-merge"></a>C. MERGE 사용  
 다음 예에서는 쿼리의 `JOIN` 연산이 `MERGE` 조인에 의해 수행되도록 지정합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT poh.PurchaseOrderID, poh.OrderDate, pod.ProductID, pod.DueDate, poh.VendorID   
FROM Purchasing.PurchaseOrderHeader AS poh  
INNER MERGE JOIN Purchasing.PurchaseOrderDetail AS pod   
    ON poh.PurchaseOrderID = pod.PurchaseOrderID;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [힌트 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)  
  
  
