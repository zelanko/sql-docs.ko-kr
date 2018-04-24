---
title: FOR XML에서 AUTO 모드 사용 | Microsoft 문서
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
- FOR XML clause, AUTO mode
- ELEMENTS option
- FOR XML AUTO mode
- AUTO FOR XML mode
ms.assetid: 7140d656-1d42-4f01-a533-5251429f4450
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b665fc99fd92ecb2ff11a06a4d0a4f11186d96a1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="use-auto-mode-with-for-xml"></a>FOR XML에서 AUTO 모드 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)에 설명된 대로 AUTO 모드는 쿼리 결과를 중첩 XML 요소로 반환합니다. 이 모드에서는 쿼리 결과로 생성되는 XML의 모양을 상세하게 조정할 수 없습니다. AUTO 모드 쿼리는 간단한 계층을 생성하려는 경우에 유용합니다. 그러나 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md) 및 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md) 에서는 쿼리 결과로 생성되는 XML의 모양을 좀 더 상세하게 조정할 수 있습니다.  
  
 최소한 한 개의 해당 열이 SELECT 절에 나열되는 FROM 절의 각 테이블은 XML 요소로 표시됩니다. 선택 항목인 ELEMENTS 옵션이 FOR XML 절에 지정된 경우 SELECT 절에 나열되는 열은 특성이나 하위 요소로 매핑됩니다.  
  
 결과 XML에서 요소가 중첩된 XML 계층은 SELECT 절에 지정된 열에 의해 식별되는 테이블의 순서를 기반으로 합니다. 따라서 SELECT 절에 열 이름이 지정되는 순서가 중요합니다. 맨 앞에서 가장 왼쪽에 있는 것으로 식별되는 테이블은 결과 XML 문서의 최상위 요소를 만듭니다. 그 다음으로 SELECT 문의 열로 식별되는 왼쪽에서 두 번째에 있는 테이블은 최상위 요소 안에서 하위 요소를 만듭니다.  
  
 SELECT 절에 나열되는 열 이름이 SELECT 절에서 이전에 지정한 열에 의해 이미 식별된 테이블로부터 비롯된 경우 새로운 계층 수준을 여는 대신 이미 생성된 요소의 특성으로 열이 추가됩니다. ELEMENTS 옵션이 지정된 경우 열이 특성으로 추가됩니다.  
  
 예를 들어 다음 쿼리를 실행하십시오.  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<Cust CustomerID="1" CustomerType="S">  
  <OrderHeader CustomerID="1" SalesOrderID="43860" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="44501" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="45283" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="46042" Status="5" />  
</Cust>  
...  
```  
  
 SELECT 절에서 다음에 유의하십시오.  
  
-   CustomerID는 Cust 테이블을 참조합니다. 따라서 <`Cust`> 요소가 생성되고 CustomerID가 그 특성으로 추가됩니다.  
  
-   그런 다음 OrderHeader.CustomerID, OrderHeader.SaleOrderID 및 OrderHeader.Status의 3개 열은 OrderHeader 테이블을 참조합니다. 따라서 <`OrderHeader`> 요소는 <`Cust`> 요소의 하위 요소로 추가되고 이 3개의 열이 <`OrderHeader`>의 특성으로 추가됩니다.  
  
-   그런 다음 Cust.CustomerType 열은 Cust.CustomerID 열로 이미 식별된 Cust 테이블을 다시 참조합니다. 따라서 새 요소는 생성되지 않습니다. 대신 이전에 생성된 <`Cust`> 요소에 CustomerType 특성이 추가됩니다.  
  
-   이 쿼리는 테이블 이름에 대한 별칭을 지정합니다. 이러한 별칭은 해당 요소 이름으로 나타납니다.  
  
-   ORDER BY는 하나의 부모 아래에 있는 모든 자식을 그룹화하는 데 필요합니다.  
  
 이 쿼리는 이전 쿼리와 비슷하지만 SELECT 절에서 Cust 테이블의 열 앞에 OrderHeader 테이블의 열을 지정합니다. 따라서 첫 번째 <`OrderHeader`> 요소가 생성된 다음 <`Cust`> 자식 요소가 여기에 추가됩니다.  
  
```  
select OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerID,   
       Cust.CustomerType  
from Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
where Cust.CustomerID = OrderHeader.CustomerID  
for xml auto  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<OrderHeader CustomerID="1" SalesOrderID="43860" Status="5">  
  <Cust CustomerID="1" CustomerType="S" />  
</OrderHeader>  
...  
```  
  
 ELEMENTS 옵션이 FOR XML 절에 추가된 경우 요소 중심 XML이 반환됩니다.  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO, ELEMENTS  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<Cust>  
  <CustomerID>1</CustomerID>  
  <CustomerType>S</CustomerType>  
  <OrderHeader>  
    <CustomerID>1</CustomerID>  
    <SalesOrderID>43860</SalesOrderID>  
    <Status>5</Status>  
  </OrderHeader>  
   ...  
</Cust>  
...  
```  
  
 이 쿼리에서 CustomerID 값은 CustomerID가 테이블의 기본 키이기 때문에 \<Cust> 요소를 만들 때 한 행씩 순서대로 비교됩니다. CustomerID가 테이블의 기본 키로 식별되지 않는 경우 모든 열 값(이 쿼리의 CustomerType인 CustomerID)이 한 행씩 순서대로 비교됩니다. 값이 다르면 새로운 \<Cust> 요소가 XML에 추가됩니다.  
  
 이러한 열 값을 비교할 때 비교되는 임의의 열 유형이 **text**, **ntext**, **image**또는 **xml**인 경우 값이 같더라도 FOR XML은 값이 다르고 비교되지 않는 것으로 가정합니다. 이러한 이유는 큰 개체에 대한 비교가 지원되지 않기 때문입니다. 선택한 각 행에 대한 결과에 요소가 추가됩니다. **(n)varchar(max)** 및 **varbinary(max)** 의 열이 비교되는지 확인합니다.  
  
 집계 열 또는 계산 열의 경우와 같이 SELECT 절의 열이 FROM 절에서 식별된 어떤 테이블과도 연결될 수 없는 경우 그 열은 목록에서 나타날 때 XML 문서의 가장 깊은 중첩 수준에 추가됩니다. 그러한 열이 SELECT 절에서 첫 번째 열로 나타나는 경우에는 최상위 요소에 추가됩니다.  
  
 별표(*) 와일드카드 문자를 SELECT 절에 지정하는 경우 위에 설명한 방법과 동일한 방식으로 행이 쿼리 엔진에 의해 반환되는 순서에 따라 중첩이 결정됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 AUTO 모드에 대한 자세한 내용을 제공합니다:  
  
-   [BINARY BASE64 옵션 사용](../../relational-databases/xml/use-the-binary-base64-option.md)  
  
-   [반환된 XML 모양 지정에서 AUTO 모드 추론](../../relational-databases/xml/auto-mode-heuristics-in-shaping-returned-xml.md)  
  
-   [예제: AUTO 모드 사용](../../relational-databases/xml/examples-using-auto-mode.md)  
  
## <a name="see-also"></a>참고 항목  
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
