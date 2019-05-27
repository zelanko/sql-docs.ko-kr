---
title: CUME_DIST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CUME_DIST
- CUME_DIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CUME_DIST function
- analytic functions, CUME_DIST
ms.assetid: 491b07f3-9ffd-4cdd-93e5-5abb636fc5ef
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d134e97d5e22d86d6ab3d072b5e2be29c589cde9
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944545"
---
# <a name="cumedist-transact-sql"></a>CUME_DIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 이 함수에서는 값 그룹 내에서 값의 누적 분포를 계산합니다. 즉, `CUME_DIST`는 값 그룹에서 지정한 값의 상대적 위치를 계산합니다. 오름차순으로 정렬되었다고 가정하면, 행 _r_에서 값의 `CUME_DIST`는 행 _r_에서 해당 값 이하인 값을 가진 행의 수로 정의되며 파티션 또는 쿼리 결과 집합에서 계산된 행의 수로 나뉩니다. `CUME_DIST`는 `PERCENT_RANK` 함수와 유사합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CUME_DIST( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>인수  
OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_)  

_partition\_by\_clause_는 FROM 절 결과 집합을 함수가 적용되는 파티션으로 나눕니다. _partition\_by\_clause_ 인수를 지정하지 않는 경우 `CUME_DIST`는 모든 쿼리 결과 집합 행을 단일 그룹으로 처리합니다. _order\_by\_clause_는 작업이 발생하는 논리적 순서를 결정합니다. `CUME_DIST`에는 _order\_by\_clause_가 필요합니다. `CUME_DIST`는 OVER 구문의 \<행 또는 범위 절>을 허용하지 않습니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.
  
## <a name="return-types"></a>반환 형식
**float(53)**
  
## <a name="remarks"></a>Remarks  
`CUME_DIST`는 0을 초과하거나 1 이하인 값의 범위를 반환합니다. 동일한 값은 항상 동일한 누적 분포 값으로 계산되어야 합니다. `CUME_DIST`는 기본적으로 NULL 값을 포함하고 가능한 가장 낮은 값으로 취급합니다.
  
`CUME_DIST`는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.
  
## <a name="examples"></a>예  
이 예제에서는 `CUME_DIST` 함수를 사용하여 지정한 부서 내 각 직원의 연봉을 백분율로 계산합니다. `CUME_DIST`는 동일한 부서에서 현재 직원보다 연봉이 적거나 같은 직원의 백분율을 나타내는 값을 반환합니다. `PERCENT_RANK` 함수는 부서 내 직원의 연봉을 백분율 순위로 계산합니다. 부서별로 결과 집합 행을 분할하기 위해 예제에서는 _partition\_by\_clause_ 값을 지정합니다. OVER 절의 ORDER BY 절은 각 파티션의 행을 논리적으로 정렬합니다. SELECT 문의 ORDER BY 절은 결과 집합의 표시 순서를 결정합니다.
  
```sql
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
  
```sql
  
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
  
## <a name="see-also"></a>관련 항목:
[PERCENT_RANK&#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)
  
  
