---
title: COUNT_BIG(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_BIG_TSQL
- COUNT_BIG
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT_BIG function
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT_BIG function
ms.assetid: f2e3601f-487e-4917-bb01-47b1047908cd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ad2b7e5343547bb65c6d81de8c6586ef5209e52a
ms.sourcegitcommit: 0e305dce04dcd1aa83c39328397524b352c96386
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/22/2017
---
# <a name="countbig--sql"></a>COUNT_BIG(-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

그룹의 항목 개수를 반환합니다. COUNT_BIG은 COUNT 함수와 비슷하며 두 함수 간의 유일한 차이점은 반환 값뿐입니다. COUNT_BIG은 항상 **bigint** 데이터 형식 값을 반환합니다. COUNT는 항상 **int** 데이터 형식 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT_BIG ( { [ ALL | DISTINCT ] expression } | * )  
   [ OVER ( [ partition_by_clause ] [ order_by_clause ] ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>인수  
ALL  
모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.
  
DISTINCT  
COUNT_BIG이 Null이 아닌 고유한 값의 개수를 반환하도록 지정합니다.
  
*expression*  
모든 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.
  
*\**  
테이블 행의 전체 개수를 반환할 때 모든 행이 포함되도록 지정합니다. COUNT_BIG(*\**)은 매개 변수를 사용하지 않으며 DISTINCT와 함께 사용할 수 없습니다. COUNT_BIG(*\**)은 특정 열에 대한 정보를 사용하지 않도록 정의되어 있으므로 *expression* 매개 변수가 필요하지 않습니다. COUNT_BIG(*\**)은 지정한 테이블에서 중복된 행을 포함한 행의 개수를 반환합니다. 각 행은 개별적으로 계산되며 Null 값을 가진 행도 포함됩니다.
  
ALL  
모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.
  
DISTINCT  
값이 중복될 경우 횟수에 관계 없이 무시하고 고유한 값에 대해서만 AVG를 수행하도록 지정합니다.
  
*expression*  
**비트** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause*는 FROM 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause*는 작업이 수행되는 논리적 순서를 결정합니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.
  
## <a name="return-types"></a>반환 형식
**bigint**
  
## <a name="remarks"></a>Remarks  
COUNT_BIG(*)은 그룹의 항목 개수를 반환합니다. 여기에는 NULL 값과 중복 항목이 포함됩니다.
  
COUNT_BIG(ALL *expression*)은 그룹에 포함된 각 행의 *expression*을 계산하여 Null이 아닌 값의 개수를 반환합니다.
  
COUNT_BIG(DISTINCT *expression*)은 그룹에 포함된 각 행의 *expression*을 계산하여 Null이 아닌 고유 값의 개수를 반환합니다.
  
COUNT_BIG은 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.
  
## <a name="examples"></a>예  
예제는 [COUNT&#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)를 참조하세요.
  
## <a name="see-also"></a>관련 항목:
[집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT&#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)  
[int, bigint, smallint 및 tinyint&#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
