---
title: 중첩 AUTO 모드 쿼리를 사용하여 형제 생성 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- queries [XML in SQL Server], nested AUTO mode
- nested AUTO mode query
ms.assetid: 748d9899-589d-4420-8048-1258e9e67c20
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b03f2b00ab34c9afa56738611dad4e760fc3c92
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="generate-siblings-with-a-nested-auto-mode-query"></a>중첩 AUTO 모드 쿼리를 사용하여 형제 생성
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  다음 예에서는 중첩된 AUTO 모드 쿼리를 사용하여 형제를 생성하는 방법을 보여 줍니다. 이러한 XML을 생성하는 다른 방법은 EXPLICIT 모드를 사용하는 것 뿐입니다. 하지만 이 방법은 복잡할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 쿼리는 판매 주문 정보를 제공하는 XML을 생성합니다. 여기에는 다음이 포함됩니다.  
  
-   판매 주문 헤더 정보, `SalesOrderID`, `SalesPersonID`및 `OrderDate`가 포함됩니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 에서는 이 정보를 `SalesOrderHeader` 테이블에 저장합니다.  
  
-   판매 주문 세부 정보. 여기에는 주문된 하나 이상의 제품, 단가 및 주문 수량이 포함됩니다. 이 정보는 `SalesOrderDetail` 테이블에 저장됩니다.  
  
-   판매 직원 정보. 주문을 접수한 판매 직원입니다. `SalesPerson` 테이블은 `SalesPersonID`를 제공합니다. 이 쿼리에서는 판매 직원 이름을 찾기 위해 이 테이블을 `Employee` 테이블에 조인해야 합니다.  
  
 다음과 같은 두 개의 고유 `SELECT`는 모양이 약간 다른 XML을 생성합니다.  
  
 첫 번째 쿼리는 <`SalesPerson`> 및 <`SalesOrderHeader`>가 <`SalesOrder`>의 자식(형제)으로 나타나는 XML을 생성합니다.  
  
```  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID =   
                   SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
        FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
        for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As   
                     SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
```  
  
 위의 쿼리에서 가장 외부에 있는 `SELECT` 문은 다음을 수행합니다.  
  
-   `SalesOrder` 절에 지정된 행 집합인 `FROM`를 쿼리합니다. 결과는 하나 이상의 <`SalesOrder`> 요소가 있는 XML입니다.  
  
-   `AUTO` 모드 및 `TYPE` 지시어를 지정합니다. `AUTO` 모드는 쿼리 결과를 XML로 변환하고 `TYPE` 지시어는 결과를 **xml** 유형으로 반환합니다.  
  
-   쉼표로 구분된 두 개의 중첩된 `SELECT` 문을 포함합니다. 첫 번째 중첩된 `SELECT` 는 판매 주문 정보, 헤더 및 세부 정보를 검색하고 두 번째 중첩된 `SELECT` 문은 판매 직원 정보를 검색합니다.  
  
    -   `SELECT` , `SalesOrderID`및 `SalesPersonID`를 검색하는 `CustomerID` 문 자체에 판매 주문 세부 정보를 반환하는 다른 중첩된 `SELECT ... FOR XML` 문( `AUTO` 모드와 `TYPE` 지시어 사용)이 포함됩니다.  
  
 판매 직원 정보를 검색하는 `SELECT` 문은 `SalesPerson`절에서 생성된 `FROM` 행 집합을 쿼리합니다. `FOR XML` 쿼리가 작동하려면 `FROM` 절에서 생성된 익명 행 집합에 이름을 제공해야 합니다. 이 경우에 제공된 이름은 `SalesPerson`입니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<SalesOrder>  
  <Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  </Sales.SalesOrderHeader>  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</SalesOrder>  
...  
```  
  
 다음 쿼리는 같은 판매 주문 정보를 생성하지만 결과 XML에서 <`SalesPerson`>이 <`SalesOrderDetail`>의 형제로 표시되는 점이 다릅니다.  
  
```  
<SalesOrder>  
    <SalesOrderHeader ...>  
          <SalesOrderDetail .../>  
          <SalesOrderDetail .../>  
          ...  
          <SalesPerson .../>  
    </SalesOrderHeader>  
  
</SalesOrder>  
<SalesOrder>  
  ...  
</SalesOrder>  
```  
  
 다음은 쿼리입니다.  
  
```  
SELECT SalesOrderID, SalesPersonID, CustomerID,  
             (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
              from Sales.SalesOrderDetail  
              WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
              FOR XML AUTO, TYPE),  
              (SELECT *   
               FROM  (SELECT SalesPersonID, EmployeeID  
                    FROM Sales.SalesPerson, HumanResources.Employee  
                    WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
               WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
         FOR XML AUTO, TYPE)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID=43659 or SalesOrderID=43660  
FOR XML AUTO, TYPE  
```  
  
 다음은 결과입니다.  
  
```  
<Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
<Sales.SalesOrderHeader SalesOrderID="43660" SalesPersonID="279" CustomerID="117">  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="762" OrderQty="1" UnitPrice="419.4589" />  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="758" OrderQty="1" UnitPrice="874.7940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
```  
  
 `TYPE` 지시어는 쿼리 결과를 **xml** 유형으로 반환하기 때문에 여러 **xml** 데이터 형식 메서드를 사용하여 결과 XML을 쿼리할 수 있습니다. 자세한 내용은 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)를 참조하십시오. 다음 쿼리에서는 아래 사항을 유의하십시오.  
  
-   이전 쿼리가 `FROM` 절에 추가되었습니다. 쿼리 결과는 테이블로 반환됩니다. 추가된 `XmlCol` 별칭에 유의하십시오.  
  
-   `SELECT` 절은 `XmlCol` 절에 반환된 `FROM` 에 대해 XQuery를 지정합니다. **xml** 데이터 형식의 **query()** 메서드는 XQuery를 지정하는 데 사용됩니다. 자세한 내용은 [query&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](../../t-sql/xml/query-method-xml-data-type.md)를 참조하세요.  
  
    ```  
    SELECT XmlCol.query('<Root> { /* } </Root>')  
    FROM (  
    SELECT SalesOrderID, SalesPersonID, CustomerID,  
                 (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
                  from Sales.SalesOrderDetail  
                  WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
                  FOR XML AUTO, TYPE),  
                  (SELECT *   
                   FROM  (SELECT SalesPersonID, EmployeeID  
                        FROM Sales.SalesPerson, HumanResources.Employee  
                        WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
                   WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
             FOR XML AUTO, TYPE)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesOrderID='43659' or SalesOrderID='43660'  
    FOR XML AUTO, TYPE ) as T(XmlCol)  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [중첩 FOR XML 쿼리 사용](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
