---
description: COUNT_BIG(Transact-SQL)
title: COUNT_BIG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 83a90f19316b80951cb7f4584ac34e4c2f69dbb6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474184"
---
# <a name="count_big-transact-sql"></a>COUNT_BIG(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 그룹에 있는 항목의 수를 반환합니다. `COUNT_BIG`은 [COUNT](../../t-sql/functions/count-transact-sql.md) 함수처럼 작동합니다. 이러한 함수는 해당 반환 값의 데이터 형식만이 다릅니다. `COUNT_BIG`은 항상 **bigint** 데이터 형식 값을 반환합니다. `COUNT`은 항상 **int** 데이터 형식 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( [ ALL ] { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
ALL  
모든 값에 집계 함수를 적용합니다. ALL은 기본값으로 사용됩니다.
  
DISTINCT  
`COUNT_BIG`이 Null이 아닌 고유한 값의 수를 반환하도록 지정합니다.
  
*expression*  
모든 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. `COUNT_BIG`은 집계 함수 또는 하위 쿼리를 지원하지 않습니다.
  
*\**  
`COUNT_BIG`이 반환할 총 테이블 행 개수를 결정하는 모든 행을 계산해야 한다고 지정합니다. `COUNT_BIG(*)`에는 매개 변수가 없으며 DISTINCT의 사용을 지원하지 않습니다. `COUNT_BIG(*)`은 특정 열에 대한 정보를 사용하지 않도록 정의되어 있으므로 *expression* 매개 변수가 필요하지 않습니다. `COUNT_BIG(*)`은 지정한 테이블에서 행의 수를 반환하고 중복 행을 유지합니다. Null 값을 포함하는 행을 포함하여 각 행을 개별적으로 계산합니다.
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause* 는 `FROM` 절이 생성한 결과 집합을 `COUNT_BIG` 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause* 는 작업의 논리적 순서를 결정합니다. 자세한 내용은 [OVER 절 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.
  
## <a name="return-types"></a>반환 형식
**bigint**
  
## <a name="remarks"></a>설명  
COUNT_BIG(\*)은 그룹의 항목 개수를 반환합니다. 여기에는 NULL 값과 중복 항목이 포함됩니다.
  
COUNT_BIG(ALL *식*)은 그룹에 포함된 각 행의 *식* 을 계산하여 Null이 아닌 값의 수를 반환합니다.
  
COUNT_BIG(DISTINCT *식*)은 그룹에 포함된 각 행의 *식* 을 계산하여 Null이 아닌 고유 값의 수를 반환합니다.
  
COUNT_BIG은 OVER 및 ORDER BY 절 **_없이_** 사용되는 경우 결정적 함수입니다. COUNT_BIG은 OVER 및 ORDER BY 절과 **_함께_** 사용되는 경우 비결정적 함수입니다. 자세한 내용은 [결정적 및 비결정 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.
  
## <a name="examples"></a>예제  
예제는 [COUNT&#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)을 참조하세요.
  
## <a name="see-also"></a>참고 항목
[집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT&#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)  
[int, bigint, smallint 및 tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
