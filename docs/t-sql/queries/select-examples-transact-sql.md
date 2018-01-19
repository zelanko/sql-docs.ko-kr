---
title: "예제 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- GROUP BY clause, SELECT statement
- query hints [SQL Server]
- ALL keyword
- ROLLUP operator
- SELECT statement [SQL Server], examples
- correlated subqueries, SELECT statement
- SELECT INTO statement
- ORDER BY clause [Transact-SQL]
- GROUPING function
- index hints [SQL Server]
- HAVING clause, SELECT statement
- DISTINCT keyword
- CUBE operator
- UNION operator [SQL Server]
- computed sums
- WHERE clause, SELECT statement
ms.assetid: 9b9caa3d-e7d0-42e1-b60b-a5572142186c
caps.latest.revision: "45"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 47f9b996d749fab983056150ee374c5fd181cb52
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="select-examples-transact-sql"></a>SELECT 예(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이 항목에서는 사용 하는 예제는 [선택](../../t-sql/queries/select-transact-sql.md) 문.  
  
## <a name="a-using-select-to-retrieve-rows-and-columns"></a>1. SELECT를 사용하여 행 및 열 검색  
 다음 예에서는 세 개의 코드 예를 보여 줍니다. 첫 번째 코드 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `*` 테이블에서 모든 행(WHERE 절이 지정되지 않음) 및 모든 열(`Product` 사용)을 반환합니다.  
  
 [!code-sql[Select#SelectExamples1](../../t-sql/queries/codesnippet/tsql/select-examples-transact_1.sql)]  
  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `Name` 테이블에서 모든 행(WHERE 절이 지정되지 않음) 및 열의 하위 집합(`ProductNumber`, `ListPrice`, `Product`)을 반환합니다. 또한 열 머리글이 추가됩니다.  
  
 [!code-sql[Select#SelectExamples2](../../t-sql/queries/codesnippet/tsql/select-examples-transact_2.sql)]  
  
 다음 예에서는 제품 라인이 `Product`이고 제조에 필요한 기간이 `R`일보다 작은 `4`에 대한 행만 반환합니다.  
  
 [!code-sql[Select#SelectExamples3](../../t-sql/queries/codesnippet/tsql/select-examples-transact_3.sql)]  
  
## <a name="b-using-select-with-column-headings-and-calculations"></a>2. SELECT에 열 머리글 및 계산 사용  
 다음 예에서는 `Product` 테이블의 모든 행을 반환합니다. 첫 번째 예에서는 각 제품에 대한 총 판매액과 할인 판매액을 반환합니다. 두 번째 예에서는 각 제품에 대한 총 수익이 계산됩니다.  
  
 [!code-sql[Select#SelectExamples4](../../t-sql/queries/codesnippet/tsql/select-examples-transact_4.sql)]  
  
 다음 쿼리에서는 각 판매 주문의 각 제품에 대한 총 수익을 계산합니다.  
  
 [!code-sql[Select#SelectExamples5](../../t-sql/queries/codesnippet/tsql/select-examples-transact_5.sql)]  
  
## <a name="c-using-distinct-with-select"></a>3. SELECT에 DISTINCT 사용  
 다음 예에서는 `DISTINCT`를 사용하여 중복된 제목을 검색하지 않도록 합니다.  
  
 [!code-sql[Select#SelectExamples6](../../t-sql/queries/codesnippet/tsql/select-examples-transact_6.sql)]  
  
## <a name="d-creating-tables-with-select-into"></a>4. SELECT INTO로 테이블 만들기  
 다음 첫 번째 예에서는 `#Bicycles`에 `tempdb`라는 임시 테이블을 만듭니다.  
  
 [!code-sql[Select#SelectExamples7](../../t-sql/queries/codesnippet/tsql/select-examples-transact_7.sql)]  
  
 다음 두 번째 예에서는 영구 테이블 `NewProducts`를 만듭니다.  
  
 [!code-sql[Select#SelectExamples8](../../t-sql/queries/codesnippet/tsql/select-examples-transact_8.sql)]  
  
## <a name="e-using-correlated-subqueries"></a>5. 상관 하위 쿼리 사용  
 다음 예에서는 기능상 동일한 쿼리를 보여 주고 `EXISTS` 키워드와 `IN` 키워드를 사용할 때의 차이점에 대해 설명합니다. 두 예는 모두 제품 모델이 긴 팔 로고 셔츠이고 `ProductModelID`와 `Product` 테이블 간에 `ProductModel`가 일치하는 각 제품 이름의 인스턴스 하나를 검색하는 유효한 하위 쿼리입니다.  
  
 [!code-sql[Select#SelectExamples9](../../t-sql/queries/codesnippet/tsql/select-examples-transact_9.sql)]  
  
 다음 예에서는 상관 또는 반복 하위 쿼리에 `IN`을 사용합니다. 이것은 외부 쿼리에 따라 해당 값이 달라지는 쿼리입니다. 이 쿼리는 외부 쿼리에서 선택한 각 행마다 한 번씩 반복적으로 실행됩니다. 이 쿼리는 `SalesPerson` 테이블에서 보너스가 `5000.00`이고 `Employee` 및 `SalesPerson` 테이블에서 직원 ID가 일치하는 각 직원의 이름 및 성의 인스턴스 하나를 검색합니다.  
  
 [!code-sql[Select#SelectExamples10](../../t-sql/queries/codesnippet/tsql/select-examples-transact_10.sql)]  
  
 이 문의 이전 하위 쿼리는 외부 쿼리와 독립적으로 평가할 수 없습니다. `Employee.EmployeeID`의 값이 필요하지만 이 값은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 `Employee`의 다른 행을 검사하는 경우 변경됩니다.  
  
 상관 하위 쿼리는 외부 쿼리의 `HAVING` 절에서도 사용할 수 있습니다. 다음 예에서는 최고 가격이 모델 평균 가격의 두 배 이상인 제품 모델을 찾습니다.  
  
 [!code-sql[Select#SelectExamples11](../../t-sql/queries/codesnippet/tsql/select-examples-transact_11.sql)]  
  
 다음 예에서는 두 개의 상관 하위 쿼리를 사용하여 특정 제품을 판매한 직원의 이름을 찾습니다.  
  
 [!code-sql[Select#SelectExamples12](../../t-sql/queries/codesnippet/tsql/select-examples-transact_12.sql)]  
  
## <a name="f-using-group-by"></a>6. GROUP BY 사용  
 다음 예에서는 데이터베이스에서 각 판매 주문의 합계를 구합니다.  
  
 [!code-sql[Select#SelectExamples13](../../t-sql/queries/codesnippet/tsql/select-examples-transact_13.sql)]  
  
 `GROUP BY` 절을 사용했으므로 각 판매 주문에 대해 모든 판매의 합계를 포함하는 한 행만 반환됩니다.  
  
## <a name="g-using-group-by-with-multiple-groups"></a>7. GROUP BY에 여러 그룹 사용  
 다음 예에서는 제품 ID 및 특별 행사 ID별로 그룹화된 평균 가격과 연간 판매액의 합계를 구합니다.  
  
 [!code-sql[Select#SelectExamples14](../../t-sql/queries/codesnippet/tsql/select-examples-transact_14.sql)]  
  
## <a name="h-using-group-by-and-where"></a>8. GROUP BY 및 WHERE 사용  
 다음 예에서는 가격이 `$1000`보다 큰 행만 검색한 후 그 결과를 그룹화합니다.  
  
 [!code-sql[Select#SelectExamples15](../../t-sql/queries/codesnippet/tsql/select-examples-transact_15.sql)]  
  
## <a name="i-using-group-by-with-an-expression"></a>9. GROUP BY에 식 사용  
 다음 예에서는 식으로 그룹화를 수행합니다. 식에 집계 함수가 없는 경우 식으로 그룹화를 수행할 수 있습니다.  
  
 [!code-sql[Select#SelectExamples16](../../t-sql/queries/codesnippet/tsql/select-examples-transact_16.sql)]  
  
## <a name="j-using-group-by-with-order-by"></a>10. GROUP BY 및 ORDER BY 사용  
 다음 예에서는 각 제품 유형의 평균 가격을 찾아 그 결과를 평균 가격에 따라 정렬합니다.  
  
 [!code-sql[Select#SelectExamples18](../../t-sql/queries/codesnippet/tsql/select-examples-transact_17.sql)]  
  
## <a name="k-using-the-having-clause"></a>11. HAVING 절 사용  
 다음 첫 번째 예에서는 `HAVING` 절에 집계 함수를 사용합니다. `SalesOrderDetail` 테이블의 행을 제품 ID별로 그룹화하고 평균 주문 수량이 5개 이하인 제품을 제외시킵니다. 두 번째 예에서는 집계 함수 없이 `HAVING` 절을 사용합니다.  
  
 [!code-sql[Select#SelectExamples19](../../t-sql/queries/codesnippet/tsql/select-examples-transact_18.sql)]  
  
 다음 쿼리는 `LIKE` 절에서 `HAVING` 절을 사용합니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, CarrierTrackingNumber   
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID, CarrierTrackingNumber  
HAVING CarrierTrackingNumber LIKE '4BD%'  
ORDER BY SalesOrderID ;  
GO  
```  
  
## <a name="l-using-having-and-group-by"></a>12. HAVING 및 GROUP BY 사용  
 다음 예에서는 하나의 `GROUP BY` 문에 `HAVING`, `WHERE`, `ORDER BY` 및 `SELECT` 절을 사용합니다. 가격이 $25를 초과하는 제품과 평균 주문 수량이 5 미만인 제품을 제거한 후에 그룹과 요약 값을 생성합니다. 또한 결과를 `ProductID`별로 정렬합니다.  
  
 [!code-sql[Select#SelectExamples21](../../t-sql/queries/codesnippet/tsql/select-examples-transact_19.sql)]  
  
## <a name="m-using-having-with-sum-and-avg"></a>13. SUM 및 AVG와 함께 HAVING 사용  
 다음 예에서는 `SalesOrderDetail` 테이블을 제품 ID별로 그룹화하며 총 주문액이 `$1000000.00` 이상이며 평균 주문 수량이 `3` 미만인 제품의 그룹만 포함합니다.  
  
 [!code-sql[Select#SelectExamples22](../../t-sql/queries/codesnippet/tsql/select-examples-transact_20.sql)]  
  
 총 판매액이 `$2000000.00` 이상인 제품을 보려면 다음 쿼리를 사용합니다.  
  
 [!code-sql[Select#SelectExamples23](../../t-sql/queries/codesnippet/tsql/select-examples-transact_21.sql)]  
  
 각 제품에 대한 계산에 최소 1500개 이상의 항목을 포함시키려는 경우 `HAVING COUNT(*) > 1500`을 사용하여 `1500`개 미만으로 판매된 항목에 대한 합계를 반환하는 제품은 제외시킬 수 있습니다. 다음 쿼리를 사용합니다.  
  
 [!code-sql[Select#SelectExamples24](../../t-sql/queries/codesnippet/tsql/select-examples-transact_22.sql)]  
  
## <a name="n-using-the-index-optimizer-hint"></a>14. INDEX 최적화 프로그램 힌트 사용  
 다음 예에서는 `INDEX` 최적화 프로그램 힌트를 사용하는 두 가지 방법을 보여 줍니다. 첫 번째 예에서는 최적화 프로그램이 테이블에서 비클러스터형 인덱스를 사용하여 행을 검색하도록 하며 두 번째 예에서는 인덱스 0을 사용하여 테이블 검색을 수행하도록 합니다.  
  
 [!code-sql[Select#SelectExamples45](../../t-sql/queries/codesnippet/tsql/select-examples-transact_23.sql)]  
  
## <a name="m-using-option-and-the-group-hints"></a>13. OPTION 및 GROUP 힌트 사용  
 다음 예에서는 `OPTION (GROUP)` 절과 함께 `GROUP BY` 절을 사용하는 방법을 보여 줍니다.  
  
 [!code-sql[Select#SelectExamples46](../../t-sql/queries/codesnippet/tsql/select-examples-transact_24.sql)]  
  
## <a name="o-using-the-union-query-hint"></a>15. UNION 쿼리 힌트 사용  
 다음 예에서는 `MERGE UNION` 쿼리 힌트를 사용합니다.  
  
 [!code-sql[Select#SelectExamples47](../../t-sql/queries/codesnippet/tsql/select-examples-transact_25.sql)]  
  
## <a name="p-using-a-simple-union"></a>16. 단순 UNION 사용  
 다음 예에서는 결과 집합에 `ProductModelID` 및 `Name` 테이블의 `ProductModel` 및 `Gloves` 열의 내용이 포함됩니다.  
  
 [!code-sql[Select#SelectExamples48](../../t-sql/queries/codesnippet/tsql/select-examples-transact_26.sql)]  
  
## <a name="q-using-select-into-with-union"></a>17. UNION과 함께 SELECT INTO 사용  
 다음 예에서 두 번째 `INTO` 문의 `SELECT` 절은 `ProductResults` 및 `ProductModel` 테이블의 지정된 열에 대해 UNION 연산을 수행한 마지막 결과 집합을 `Gloves` 테이블에 포함시키도록 지정합니다. `Gloves` 테이블은 첫 번째 `SELECT` 문에서 생성됩니다.  
  
 [!code-sql[Select#SelectExamples49](../../t-sql/queries/codesnippet/tsql/select-examples-transact_27.sql)]  
  
## <a name="r-using-union-of-two-select-statements-with-order-by"></a>18. 두 SELECT 문에서 ORDER BY와 함께 UNION 사용  
 UNION 절과 함께 사용되는 특정 매개 변수의 순서는 중요합니다. 다음 예에서는 출력 시 이름이 바뀌는 열이 있는 두 `UNION` 문에서 `SELECT`을 잘못 사용한 경우와 올바르게 사용한 경우를 보여 줍니다.  
  
 [!code-sql[Select#SelectExamples50](../../t-sql/queries/codesnippet/tsql/select-examples-transact_28.sql)]  
  
## <a name="s-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>S.는 세 개의 SELECT 문에서 UNION을 사용하여 ALL 및 괄호의 효과 확인  
 다음 예에서는 `UNION`을 사용하여 동일한 5개의 데이터 행이 있는 세 테이블의 결과를 결합합니다. 첫 번째 예에서는 `UNION ALL`을 사용하여 중복 레코드를 보여 주고 15개 행을 모두 반환합니다. 두 번째 예에서는 `UNION` 없이 `ALL`을 사용하여 세 `SELECT` 문의 결합된 결과에서 중복 행을 제거하고 5개 행만 반환합니다.  
  
 세 번째 예에서는 첫 번째 `ALL`에서 `UNION`을 사용하고 `UNION`을 사용하지 않는 두 번째 `ALL`은 괄호로 묶습니다. 두 번째 `UNION`은 괄호로 묶었기 때문에 먼저 처리되고 `ALL` 옵션을 사용하지 않아 중복 행이 제거되기 때문에 5개 행을 반환합니다. 이러한 5개 행은 `SELECT` 키워드를 사용하여 첫 번째 `UNION ALL` 결과와 결합됩니다. 이 때 5개 행으로 된 두 집합 간의 중복 행은 제거되지 않습니다. 따라서 마지막 결과에는 10개의 행이 포함됩니다.  
  
 [!code-sql[Select#SelectExamples51](../../t-sql/queries/codesnippet/tsql/select-examples-transact_29.sql)]  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [UNION &#40; Transact SQL &#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [제외 하 고 및 INTERSECT &#40; Transact SQL &#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [경로 이름 &#40; Transact SQL &#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [절 &#40;에 Transact SQL &#41;](../../t-sql/queries/select-into-clause-transact-sql.md)  
  
  
