---
title: "PIVOT 및 UNPIVOT 사용 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PIVOT_TSQL
helpviewer_keywords:
- FROM clause, UNPIVOT operator
- unpivoting tables
- table pivoting [SQL Server]
- UNPIVOT operator
- crosstab query
- PIVOT operator
- rotating table-valued expressions
- pivoting tables
- FROM clause, PIVOT operator
- rotating columns
ms.assetid: 24ba54fc-98f7-4d35-8881-b5158aac1d66
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1feee91c251b5c1f326e8e69569186c049007d9e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="from---using-pivot-and-unpivot"></a>-PIVOT 및 UNPIVOT 사용
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  사용할 수는 `PIVOT` 및 `UNPIVOT` 테이블 반환 식을 다른 테이블로 변경 하려면 관계 연산자입니다. `PIVOT`출력에서 여러 열에 식에서 한 열에서 고유 값을 설정 하 여 테이블 반환 식을 회전 하 고 최종 출력에서 원하는 모든 남은 열 값에 필요한 위치에 집계를 수행 합니다. `UNPIVOT`열의 열 값에는 테이블 반환 식 회전 하 여 피벗 작업을 수행 합니다.  
  
 에 대 한 구문 `PIVOT` 제공 더 간단 하 고 보다 복잡 한 일련의 지정 될 수 있는 구문 보다 읽기 쉬운 `SELECT...CASE` 문. 에 대 한 구문에 대 한 전체 설명은 `PIVOT`, 참조 [(TRANSACT-SQL)에서](../../t-sql/queries/from-transact-sql.md)합니다.  
  
## <a name="syntax"></a>구문  
 다음 구문을 사용 하는 방법을 요약 한 것은 `PIVOT` 연산자입니다.  
  
```  
SELECT <non-pivoted column>,  
    [first pivoted column] AS <column name>,  
    [second pivoted column] AS <column name>,  
    ...  
    [last pivoted column] AS <column name>  
FROM  
    (<SELECT query that produces the data>)   
    AS <alias for the source query>  
PIVOT  
(  
    <aggregation function>(<column being aggregated>)  
FOR   
[<column that contains the values that will become column headers>]   
    IN ( [first pivoted column], [second pivoted column],  
    ... [last pivoted column])  
) AS <alias for the pivot table>  
<optional ORDER BY clause>;  
```  

## <a name="remarks"></a>주의  
열 식별자는 `UNPIVOT` 카탈로그 데이터 정렬에 따라 절. 에 대 한 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 데이터 정렬은 항상 `SQL_Latin1_General_CP1_CI_AS`합니다. 에 대 한 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 부분적으로 포함 된 데이터베이스를 데이터 정렬은 항상 `Latin1_General_100_CI_AS_KS_WS_SC`합니다. 열은 다른 열을 다음 collate 절과 결합 되어 있으면 (`COLLATE DATABASE_DEFAULT`) 충돌을 방지 하려면 필요 합니다.  

  
## <a name="basic-pivot-example"></a>기본 PIVOT 예  
 다음 코드 예제에서는 4개의 행이 있는 2열 테이블을 생성합니다.  
  
```  
USE AdventureWorks2014 ;  
GO  
SELECT DaysToManufacture, AVG(StandardCost) AS AverageCost   
FROM Production.Product  
GROUP BY DaysToManufacture;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 DaysToManufacture AverageCost
 ----------------- -----------
 0                 5.0885
 1                 223.88
 2                 359.1082
 4                 949.4105
 ```
  
 3일 `DaysToManufacture`에 대해 정의된 제품은 없습니다.  
  
 다음 코드는 같은 결과를 표시하지만 `DaysToManufacture` 값이 열 제목이 되도록 피벗됩니다. 또한 결과가 `[3]`이라도 `NULL`일에 대한 열을 제공합니다.  
  
```  
-- Pivot table with one row and five columns  
SELECT 'AverageCost' AS Cost_Sorted_By_Production_Days,   
[0], [1], [2], [3], [4]  
FROM  
(SELECT DaysToManufacture, StandardCost   
    FROM Production.Product) AS SourceTable  
PIVOT  
(  
AVG(StandardCost)  
FOR DaysToManufacture IN ([0], [1], [2], [3], [4])  
) AS PivotTable;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Cost_Sorted_By_Production_Days 0           1           2           3           4         
------------------------------ ----------- ----------- ----------- ----------- -----------
AverageCost                    5.0885      223.88      359.1082    NULL        949.4105
```
  
## <a name="complex-pivot-example"></a>복잡한 PIVOT 예  
 일반적으로 교차 집계 보고서를 생성하여 데이터를 요약하려는 경우 `PIVOT`을 사용하면 유용합니다. 예를 들어 `PurchaseOrderHeader` 예제 데이터베이스의 `AdventureWorks2014` 테이블을 쿼리하여 특정 직원의 구매 주문 수를 파악하려고 합니다. 다음 쿼리에서는 이 보고서를 공급업체별로 제공합니다.  
  
```  
USE AdventureWorks2014;  
GO  
SELECT VendorID, [250] AS Emp1, [251] AS Emp2, [256] AS Emp3, [257] AS Emp4, [260] AS Emp5  
FROM   
(SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM Purchasing.PurchaseOrderHeader) p  
PIVOT  
(  
COUNT (PurchaseOrderID)  
FOR EmployeeID IN  
( [250], [251], [256], [257], [260] )  
) AS pvt  
ORDER BY pvt.VendorID;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
```
VendorID    Emp1        Emp2        Emp3        Emp4        Emp5  
----------- ----------- ----------- ----------- ----------- -----------
1492        2           5           4           4           4
1494        2           5           4           5           4
1496        2           4           4           5           5
1498        2           5           4           4           4
1500        3           4           4           5           4
```
  
 이 하위 SELECT 문에서 반환하는 결과는 `EmployeeID` 열에서 피벗됩니다.  
  
```  
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
 이는 `EmployeeID` 열에서 반환하는 각 고유 값이 최종 결과 집합의 필드가 됨을 의미합니다. 이에 따라 피벗 절에 지정된 각 `EmployeeID` 번호에 대해 열이 제공되며 여기서는 직원 `164`, `198`, `223`, `231` 및 `233`에 대해 열이 하나씩 제공됩니다. `PurchaseOrderID` 열은 최종 출력에 반환되는 열(그룹화 열)을 그룹화하는 기준 값 열로 사용됩니다. 이 경우 그룹화 열은 `COUNT` 함수로 집계됩니다. `PurchaseOrderID` 열에 표시되는 Null 값이 각 직원에 대한 `COUNT` 계산 시 사용되지 않았다는 경고 메시지가 나타납니다.  
  
> [!IMPORTANT]  
>  집계 함수가 사용 됩니다 때 `PIVOT`를 집계 하는 경우 값 열에 null 값의 존재 여부 고려 되지 않습니다.  
  
 `UNPIVOT`반대 작업을 거의 수행 `PIVOT`, 열을 행으로 회전 하 여 합니다. 위의 예에서 생성된 테이블이 데이터베이스에 `pvt`로 저장되어 있는 상태에서 `Emp1`, `Emp2`, `Emp3`, `Emp4` 및 `Emp5` 열 식별자를 특정 공급업체에 해당하는 행 값으로 회전하려고 한다고 가정합니다. 이는 추가로 두 열을 식별해야 함을 의미합니다. 회전하는 열 값(`Emp1`, `Emp2`,...)이 포함될 열을 `Employee`라고 하며 회전할 열 아래의 현재 값이 포함될 열을 `Orders`라고 합니다. 이러한 열에 해당 하는 *pivot_column* 및 *value_column*각각에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 정의 합니다. 쿼리는 다음과 같습니다.  
  
```  
-- Create the table and insert values as portrayed in the previous example.  
CREATE TABLE pvt (VendorID int, Emp1 int, Emp2 int,  
    Emp3 int, Emp4 int, Emp5 int);  
GO  
INSERT INTO pvt VALUES (1,4,3,5,4,4);  
INSERT INTO pvt VALUES (2,4,1,5,5,5);  
INSERT INTO pvt VALUES (3,4,3,5,4,4);  
INSERT INTO pvt VALUES (4,4,2,5,5,4);  
INSERT INTO pvt VALUES (5,5,1,5,5,5);  
GO  
-- Unpivot the table.  
SELECT VendorID, Employee, Orders  
FROM   
   (SELECT VendorID, Emp1, Emp2, Emp3, Emp4, Emp5  
   FROM pvt) p  
UNPIVOT  
   (Orders FOR Employee IN   
      (Emp1, Emp2, Emp3, Emp4, Emp5)  
)AS unpvt;  
GO  
```  
  
 다음은 결과 집합의 일부입니다.  
  
```
VendorID    Employee    Orders
----------- ----------- ------
1            Emp1       4
1            Emp2       3 
1            Emp3       5
1            Emp4       4
1            Emp5       4
2            Emp1       4
2            Emp2       1
2            Emp3       5
2            Emp4       5
2            Emp5       5
...
```
  
 다음에 유의 `UNPIVOT` 의 정반대 않습니다 `PIVOT`합니다. `PIVOT`집계를 수행 하 고 따라서 출력에 행으로 가능한 여러 행 병합 합니다. `UNPIVOT`행이 병합 되었기 때문에 원래 테이블 반환 식의 결과 재현 되지 않습니다. 게다가 입력의 값이 null `UNPIVOT` 반면 있었다는 원래 null 값 하기 전에 입력에서 출력에 나타나지 않지만 `PIVOT` 작업 합니다.  
  
 `Sales.vSalesPersonSalesByFiscalYears` 의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 샘플 데이터베이스에서는 `PIVOT` 을 각 회계 연도 대 한 각 영업 사원의 총 매출액을 반환 합니다. 뷰를 스크립팅하려면를 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 **개체 탐색기**에서 뷰를 찾습니다는 **뷰** 에 대 한 폴더는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스입니다. 뷰 이름을 마우스 오른쪽 단추로 클릭 한 다음 선택 **뷰 스크립팅**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [FROM (TRANSACT-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [대/소문자 (Transact SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  
