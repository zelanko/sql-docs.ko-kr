---
title: EXCEPT 및 INTERSECT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INTERSECT_TSQL
- EXCEPT_TSQL
- INTERSECT
- EXCEPT
dev_langs:
- TSQL
helpviewer_keywords:
- EXCEPT operator [Transact-SQL]
- queries [SQL Server], comparing
- comparing queries
- INTERSECT operator
ms.assetid: b1019300-171a-4a1a-854f-e1e751de3565
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c6ff3bafd6d01fb9f4ac591d88104e19e71b2713
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064974"
---
# <a name="set-operators---except-and-intersect-transact-sql"></a>집합 연산자 - EXCEPT 및 INTERSECT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 쿼리의 결과를 비교하여 고유한 행을 반환합니다.  
  
 EXCEPT는 오른쪽 입력 쿼리의 출력이 아닌 고유한 행을 왼쪽 입력 쿼리에서 반환합니다.  
  
 INTERSECT는 왼쪽 및 오른쪽 입력 쿼리 연산자 모두에서 출력되는 고유 행을 반환합니다.  
  
 EXCEPT 또는 INTERSECT를 사용하는 두 쿼리의 결과 집합을 결합할 때는 다음 기본 규칙을 따라야 합니다.  
  
-   열의 개수와 순서가 모든 쿼리에서 동일해야 합니다.  
  
-   데이터 형식이 호환되어야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
{ <query_specification> | ( <query_expression> ) }   
{ EXCEPT | INTERSECT }  
{ <query_specification> | ( <query_expression> ) }  
```  
  
## <a name="arguments"></a>인수  
 \<*query_specification*> | ( \<*query_expression*> )  
 다른 쿼리 사양이나 쿼리 식의 데이터와 비교할 데이터를 반환하는 쿼리 사양 또는 쿼리 식입니다. EXCEPT 또는 INTERSECT 연산의 일부인 열의 정의는 같을 필요는 없지만 암시적 변환을 통해 비교할 수 있어야 합니다. 데이터 형식이 다른 경우 비교를 수행하고 결과를 반환하는 데 사용되는 형식은 [데이터 형식 우선 순위](../../t-sql/data-types/data-type-precedence-transact-sql.md)에 따라 결정됩니다.  
  
 형식은 동일하지만 전체 자릿수, 소수 자릿수 또는 길이가 다르면 식 결합에 대한 동일한 규칙에 따라 결과가 결정됩니다. 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
 쿼리 사양 또는 식은 비교할 수 없는 데이터 형식이므로 **xml**, **text**, **ntext**, **image** 또는 이진이 아닌 CLR 사용자 정의 형식 열을 반환할 수 없습니다.  
  
 EXCEPT  
 오른쪽 쿼리에서 반환되지 않는 EXCEPT 연산자의 왼쪽에 있는 쿼리에서 고유한 값을 반환합니다.  
  
 INTERSECT  
 INTERSECT 연산자의 왼쪽과 오른쪽에 있는 두 쿼리에 의해 반환된 고유한 값을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 EXCEPT 또는 INTERSECT 연산자의 왼쪽과 오른쪽에 있는 쿼리에서 반환되는 비교 가능한 열의 데이터 형식이 서로 다른 데이터 정렬이 있는 문자 데이터 형식이면, [선행 정렬](../../t-sql/statements/collation-precedence-transact-sql.md) 규칙에 따라 필요한 비교가 수행됩니다. 이러한 변환을 수행할 수 없는 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 오류를 반환합니다.  
  
 DISTINCT 행을 확인하기 위해 열 값을 비교할 때 두 NULL 값은 동일한 것으로 간주됩니다.  
  
 EXCEPT 또는 INTERSECT에 의해 반환된 결과 집합의 열 이름은 연산자의 왼쪽에 있는 쿼리에 의해 반환된 결과 집합의 열 이름과 같습니다.  
  
 ORDER BY 절의 열 이름이나 별칭은 왼쪽 쿼리에 의해 반환된 열 이름을 참조해야 합니다.  
  
 EXCEPT 또는 INTERSECT에 의해 반환된 결과 집합의 열에 대한 Null 허용 여부는 연산자의 왼쪽에 있는 쿼리에 의해 반환된 해당 열의 Null 허용 여부와 같습니다.  
  
 EXCEPT 또는 INTERSECT가 식에서 다른 연산자와 함께 사용되는 경우 컨텍스트에서 다음 우선 순위에 따라 계산됩니다.  
  
1.  괄호가 있는 식  
  
2.  INTERSECT 연산자  
  
3.  식에서 EXCEPT와 UNION의 위치를 기준으로 왼쪽에서 오른쪽으로 계산되는 EXCEPT 및 UNION  
  
 EXCEPT 또는 INTERSECT가 두 개 이상의 쿼리 집합을 비교하는 데 사용되는 경우 한 번에 두 개의 쿼리를 비교하여 앞서 언급한 식 계산 규칙에 따라 데이터 형식 변환이 결정됩니다.  
  
 EXCEPT 및 INTERSECT는 분산형 분할 뷰 정의, 쿼리 알림에서 사용될 수 없습니다.  
  
 EXCEPT 및 INTERSECT는 분산 쿼리에서 사용될 수 있지만 로컬 서버에서만 실행되며 연결된 서버에 밀어넣지 못합니다. 따라서 EXCEPT 및 INTERSECT를 분산 쿼리에서 사용하면 성능에 영향을 미칠 수 있습니다.  
  
 빠른 정방향 전용 및 정적 커서는 EXCEPT 또는 INTERSECT 연산에 사용될 때 결과 집합에서 전적으로 지원됩니다. EXCEPT 또는 INTERSECT 연산에 키 집합 또는 동적 커서가 함께 사용되는 경우 연산의 결과 집합 커서는 정적 커서로 변환됩니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 그래픽 실행 계획 기능을 사용하여 EXCEPT 연산이 표시되면, 이 연산은 [Left Anti Semi Join](../../relational-databases/showplan-logical-and-physical-operators-reference.md)으로 나타나고, INTERSECT 연산은 [Left Semi Join](../../relational-databases/showplan-logical-and-physical-operators-reference.md)으로 나타납니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `INTERSECT` 및 `EXCEPT` 연산자를 사용하는 방법을 보여 줍니다. 첫 번째 쿼리는 해당 결과를 `Production.Product` 및 `INTERSECT`와 비교하기 위해 `EXCEPT` 테이블의 모든 값을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product ;  
--Result: 504 Rows  
```  
  
 다음 쿼리는 `INTERSECT` 연산자의 왼쪽과 오른쪽에 있는 두 쿼리에 의해 반환된 고유한 값을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
INTERSECT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 238 Rows (products that have work orders)  
```  
  
 다음 쿼리는 오른쪽 쿼리에 없는 고유한 값을 `EXCEPT` 연산자의 왼쪽에 있는 쿼리에서 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
EXCEPT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 266 Rows (products without work orders)  
```  
  
 다음 쿼리는 오른쪽 쿼리에 없는 고유한 값을 `EXCEPT` 연산자의 왼쪽에 있는 쿼리에서 반환합니다. 테이블은 위의 예제와 반대로 바뀝니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.WorkOrder  
EXCEPT  
SELECT ProductID   
FROM Production.Product ;  
--Result: 0 Rows (work orders without products)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 `INTERSECT` 및 `EXCEPT` 연산자의 사용 방법을 보여 줍니다. 첫 번째 쿼리는 해당 결과를 `FactInternetSales` 및 `INTERSECT`와 비교하기 위해 `EXCEPT` 테이블의 모든 값을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales;  
--Result: 60398 Rows  
```  
  
 다음 쿼리는 `INTERSECT` 연산자의 왼쪽과 오른쪽에 있는 두 쿼리에 의해 반환된 고유한 값을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
INTERSECT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9133 Rows (Sales to customers that are female.)  
```  
  
 다음 쿼리는 오른쪽 쿼리에 없는 고유한 값을 `EXCEPT` 연산자의 왼쪽에 있는 쿼리에서 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
EXCEPT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9351 Rows (Sales to customers that are not female.)  
```  
  
  

