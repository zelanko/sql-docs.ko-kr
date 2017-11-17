---
title: COUNT_BIG (Transact SQL) | Microsoft Docs
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
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ce3046c36b7d224f6294948029cef6cf5afd43c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="countbig-transact-sql"></a>COUNT_BIG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

그룹의 항목 개수를 반환합니다. COUNT_BIG은 COUNT 함수와 비슷하며 두 함수 간의 유일한 차이점은 반환 값뿐입니다. COUNT_BIG은 항상 반환 된 **bigint** 데이터 값을 입력 합니다. COUNT는 항상 반환는 **int** 데이터 값을 입력 합니다.
  
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
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 종류의 합니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.
  
*\**  
테이블 행의 전체 개수를 반환할 때 모든 행이 포함되도록 지정합니다. COUNT_BIG (*\**) 매개 변수가 없으며 DISTINCT와 함께 사용할 수 없습니다. COUNT_BIG (*\**) 필요 하지 않습니다는 *식* 매개 변수 이므로 기본적으로 사용 하지 않는 특정 열에 대 한 정보입니다. COUNT_BIG (*\**) 중복 지정된 된 테이블에서 행의 수를 반환 합니다. 각 행은 개별적으로 계산되며 Null 값을 가진 행도 포함됩니다.
  
ALL  
모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.
  
DISTINCT  
값이 중복될 경우 횟수에 관계 없이 무시하고 고유한 값에 대해서만 AVG를 수행하도록 지정합니다.
  
*expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 정확한 수치 또는 근사치 숫자 데이터 형식 범주에서를 제외 하 고는 **비트** 데이터 형식입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.
  
통해 **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause* 함수가 적용 되는 파티션으로 FROM 절에서 생성 한 결과 집합을 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause* 작업이 수행 되는 논리적 순서를 결정 합니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>반환 형식
**bigint**
  
## <a name="remarks"></a>주의  
COUNT_BIG(*)은 그룹의 항목 개수를 반환합니다. 여기에는 NULL 값과 중복 항목이 포함됩니다.
  
COUNT_BIG (모든 *식*) 평가 *식* 그룹의 각 행에 대해 null이 아닌 값의 수를 반환 합니다.
  
COUNT_BIG (DISTINCT *식*) 평가 *식* 그룹의 각 행에 대해 null이 아닌 값의 수를 반환 합니다.
  
COUNT_BIG은 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.
  
## <a name="examples"></a>예  
예제를 보려면 [수 &#40; Transact SQL &#41; ](../../t-sql/functions/count-transact-sql.md).
  
## <a name="see-also"></a>참고 항목
[집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40; Transact SQL &#41;](../../t-sql/functions/count-transact-sql.md)  
[int, bigint, smallint 및 tinyint &#40; Transact SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[절 &#40; 조치 Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

