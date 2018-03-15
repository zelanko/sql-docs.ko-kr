---
title: PERCENT_RANK(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PERCENT_RANK_TSQL
- PERCENT_RANK
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENT_RANK function
- analytic functions, PERCENT_RANK
ms.assetid: e361c2d4-c01f-4da4-8e89-1ddc724a2629
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f506b8f3007157f9e1757da76442af848d023494
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="percentrank-transact-sql"></a>PERCENT_RANK(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 행 그룹 내에서 행의 상대 순위를 계산합니다. PERCENT_RANK를 사용하여 쿼리 결과 집합 또는 파티션 내에서 값의 상대 순위를 평가할 수 있습니다. PERCENT_RANK는 CUME_DIST 함수와 유사합니다.  
  
## <a name="syntax"></a>구문  
  
```  
PERCENT_RANK( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>인수  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*는 FROM 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause*는 작업이 수행되는 논리적 순서를 결정합니다. *order_by_clause*가 필요합니다. PERCENT_RANK 함수에는 OVER 구문의 \<rows 또는 range 절>을 지정할 수 없습니다.  자세한 내용은 [OVER 절 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 **float(53)**  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 PERCENT_RANK가 반환하는 값 범위는 0보다 크고 1보다 작거나 같습니다. 모든 집합의 첫 번째 행은 PERCENT_RANK가 0입니다. NULL 값은 기본적으로 포함되며 가능한 가장 낮은 값으로 취급됩니다.  
  
 PERCENT_RANK는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 CUME_DIST 함수를 사용하여 지정한 부서 내 각 직원의 연봉을 백분율로 계산합니다. CUME_DIST 함수가 반환하는 값은 같은 동일 부서 내에서 현재 직원보다 연봉이 적거나 같은 직원의 백분율을 나타냅니다. PERCENT_RANK 함수는 부서 내 직원의 연봉 순위를 백분율로 계산합니다. 결과 집합의 행을 부서별로 분할하기 위해 PARTITION BY 절이 지정되었습니다. OVER 절에서 ORDER BY 절은 각 파티션의 행을 정렬합니다. SELECT 문의 ORDER BY 절은 전체 결과 집합의 행을 정렬합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [CUME_DIST &#40;Transact-SQL&#41;](../../t-sql/functions/cume-dist-transact-sql.md)  
  
  
