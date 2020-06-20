---
title: '예제: AUTO 모드 사용 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, examples
ms.assetid: 11e8d0e4-df8a-46f8-aa21-9602d4f26cad
author: rothja
ms.author: jroth
ms.openlocfilehash: bb6567924747d9325610c23d1f11de8ced1bc017
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059487"
---
# <a name="examples-using-auto-mode"></a>예제: AUTO 모드 사용
  다음 예에서는 AUTO 모드를 사용하는 방법을 보여 줍니다. 이러한 쿼리는 대부분 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스의 ProductModel 테이블에 있는 Instructions 열에 저장된 자전거 제조 지침 XML 문서에 대해 지정됩니다.  
  
## <a name="example-retrieving-customer-order-and-order-detail-information"></a>예제: 고객, 주문 및 주문 세부 정보 검색  
 이 쿼리는 특정 고객에 대한 고객, 주문 및 주문 세부 정보를 검색합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       Detail.SalesOrderID, Detail.LineTotal, Detail.ProductID,   
       Product.Name,  
       Detail.OrderQty  
FROM Sales.Customer AS Cust  
INNER JOIN Sales.SalesOrderHeader AS OrderHeader   
    ON Cust.CustomerID = OrderHeader.CustomerID  
INNER JOIN Sales.SalesOrderDetail AS Detail  
    ON OrderHeader.SalesOrderID = Detail.SalesOrderID  
INNER JOIN Production.Product AS Product  
    ON Product.ProductID = Detail.ProductID  
WHERE Cust.CustomerID IN (29672, 29734)  
ORDER BY OrderHeader.CustomerID,  
         OrderHeader.SalesOrderID  
FOR XML AUTO;  
```  
  
 이 쿼리는 `Cust`, `OrderHeader`, `Detail`및 `Product` 테이블 별칭을 식별하기 때문에 해당 요소가 `AUTO` 모드에 의해 생성됩니다. 다시 말해서 `SELECT` 절에 지정된 열에 의해 식별되는 테이블 순서에 따라 이러한 요소들의 계층이 결정됩니다.  
  
 다음은 결과의 일부입니다.  
  
 `<Cust CustomerID="29672">`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="43660">`  
  
 `<Detail SalesOrderID="43660" LineTotal="874.794000" ProductID="758" OrderQty="1">`  
  
 `<Product Name="Road-450 Red, 52" />`  
  
 `</Detail>`  
  
 `<Detail SalesOrderID="43660" LineTotal="419.458900" ProductID="762" OrderQty="1">`  
  
 `<Product Name="Road-650 Red, 44" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="47660">`  
  
 `<Detail SalesOrderID="47660" LineTotal="469.794000" ProductID="765" OrderQty="1">`  
  
 `<Product Name="Road-650 Black, 58" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="49857">`  
  
 `<Detail SalesOrderID="49857" LineTotal="44.994000" ProductID="852" OrderQty="1">`  
  
 `<Product Name="Women's Tights, S" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `...`  
  
 `</Cust>`  
  
## <a name="example-specifying-group-by-and-aggregate-functions"></a>예제: GROUP BY 및 집계 함수 지정  
 다음 쿼리는 개별 고객 ID와 고객이 요청한 주문 번호를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT C.CustomerID, COUNT(*) AS NoOfOrders  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
On C.CustomerID = SOH.CustomerID  
GROUP BY C.CustomerID  
FOR XML AUTO;This is the partial result:  
```  
  
 `<I CustomerID="11000" NoOfOrders="3" />`  
  
 `<I CustomerID="11001" NoOfOrders="3" />`  
  
 `...`  
  
## <a name="example-specifying-computed-columns-in-auto-mode"></a>예제: AUTO 모드에서 계산 열 지정  
 이 쿼리는 연결된 개별 고객 이름 및 주문 정보를 반환합니다. 계산 열은 해당 시점에 발생하는 가장 안쪽 수준으로 할당됩니다(이 예에서는 <`SOH`> 요소). 연결된 고객 이름은 결과에서 <`SOH`> 요소의 특성으로 추가됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT P.FirstName + ' ' + P.LastName AS Name,  
       SOH.SalesOrderID  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
INNER JOIN Person.Person AS P  
    ON P.BusinessEntityID = C.PersonID  
FOR XML AUTO;  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<SOH Name="Jon Yang" SalesOrderID="43793" />  
<SOH Name="Eugene Huang" SalesOrderID="43767" />  
```  
  
 각 판매 주문 헤더 정보가 하위 요소로 들어 있는 `IndividualCustomer` 특성이 포함된 <`Name`> 요소를 검색하기 위해 하위 SELECT를 사용하여 쿼리가 다시 작성되었습니다. 내부 SELECT는 개별 고객의 이름이 포함된 계산 열이 있는 임시 `IndividualCustomer` 테이블을 만듭니다. 그런 다음 이 테이블이 `SalesOrderHeader` 테이블에 조인되어 결과를 가져옵니다.  
  
 `Sales.Customer` 테이블은 해당 고객에 대한 `PersonID` 값을 포함하여 개별 고객 정보를 저장합니다. 그런 다음 이 `PersonID` 는 `Person.Person` 테이블에서 연락처 이름을 찾는 데 사용됩니다.  
  
```  
SELECT IndividualCustomer.Name, SOH.SalesOrderID  
FROM (SELECT FirstName+ ' '+LastName AS Name, C.PersonID, C.CustomerID  
      FROM Sales.Customer AS C, Person.Person AS P  
      WHERE C.PersonID = P.BusinessEntityID) AS IndividualCustomer  
LEFT OUTER JOIN  Sales.SalesOrderHeader AS SOH  
   ON IndividualCustomer.CustomerID = SOH.CustomerID  
ORDER BY IndividualCustomer.CustomerID, SOH.CustomerIDFOR XML AUTO;  
```  
  
 다음은 결과의 일부입니다.  
  
 `<IndividualCustomer Name="Jon Yang">`  
  
 `<SOH SalesOrderID="43793" />`  
  
 `<SOH SalesOrderID="51522" />`  
  
 `<SOH SalesOrderID="57418" />`  
  
 `</IndividualCustomer>`  
  
 `...`  
  
 `...`  
  
## <a name="example-returning-binary-data"></a>예제: 이진 데이터 반환  
 이 쿼리는 `ProductPhoto` 테이블에서 제품 사진을 반환합니다. `ThumbNailPhoto`는 `ProductPhoto` 테이블의 `varbinary(max)` 열입니다. 기본적으로 `AUTO` 모드는 이진 데이터에 대해 쿼리가 실행되는 데이터베이스의 가상 루트에 대한 상대 URL인 참조를 반환합니다. 이미지를 식별하기 위해서는 `ProductPhotoID` 키 특성을 지정해야 합니다. 이 예에서 설명된 것과 같이 이미지 참조를 검색할 때 테이블의 기본 키도 행을 고유하게 식별할 수 있도록 `SELECT` 절에서 지정되어야 합니다.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 다음은 결과입니다.  
  
 `-- result`  
  
 `<Production.ProductPhoto`  
  
 `ProductPhotoID="70"`  
  
 `ThumbNailPhoto= "dbobject/Production.ProductPhoto[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 `BINARY BASE64` 옵션으로도 동일한 쿼리가 실행됩니다. 다음 쿼리는 이진 데이터를 base64 인코딩 형식으로 반환합니다.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO, BINARY BASE64;  
```  
  
 다음은 결과입니다.  
  
 `-- result`  
  
 `<Production.ProductPhoto ProductPhotoID="70" ThumbNailPhoto="Base64 encoded photo" />`  
  
 기본적으로 이진 데이터를 검색하기 위해 AUTO 모드를 사용하는 경우 쿼리가 실행되는 데이터베이스의 가상 루트에 대한 상대 URL 참조가 이진 데이터 대신 반환됩니다. 이 경우는 BINARY BASE64 옵션이 지정되지 않은 경우에 해당합니다.  
  
 AUTO 모드가 쿼리에 지정된 테이블 또는 열 이름이 데이터베이스에 있는 테이블 또는 열 이름과 일치하지 않는 대/소문자를 구분하지 않는 데이터베이스에 있는 이진 데이터에 대한 URL 참조를 반환하는 경우 쿼리가 실행됩니다. 하지만 참조에 반환된 대/소문자가 일관적이지 않습니다. 다음은 그 예입니다.  
  
```  
SELECT ProductPhotoID, ThumbnailPhoto  
FROM   Production.ProductPhoto   
WHERE  ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 다음은 결과입니다.  
  
 `<Production.PRODUCTPHOTO`  
  
 `PRODUCTPHOTOID="70"`  
  
 `THUMBNAILPHOTO= "dbobject/Production.PRODUCTPHOTO[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 이는 특히 대/소문자를 구분하는 데이터베이스에 대해 dbobject 쿼리를 실행하는 경우에 문제가 될 수 있습니다. 이러한 문제를 방지하려면 쿼리에 지정된 테이블 또는 열 이름의 대/소문자가 데이터베이스에 있는 테이블 또는 열 이름의 대/소문자와 일치해야 합니다.  
  
## <a name="example-understanding-the-encoding"></a>예제: 인코딩 이해  
 다음 예에서는 결과에서 발생하는 여러 가지 인코딩을 보여 줍니다.  
  
 다음 테이블을 만듭니다.  
  
```  
CREATE TABLE [Special Chars] (Col1 char(1) primary key, [Col#&2] varbinary(50));  
```  
  
 테이블에 다음 데이터를 추가합니다.  
  
```  
INSERT INTO [Special Chars] VALUES ('&', 0x20), ('#', 0x20);  
```  
  
 다음 쿼리는 테이블에서 데이터를 반환합니다. FOR XML AUTO 모드가 지정됩니다. 이진 데이터가 참조로 반환됩니다.  
  
```  
SELECT * FROM [Special Chars] FOR XML AUTO;  
```  
  
 다음은 결과입니다.  
  
 `<Special_x0020_Chars`  
  
 `Col1="#"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='#']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 `<Special_x0020_Chars`  
  
 `Col1="&"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='&']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 다음은 결과에서 특수 문자를 인코딩하는 처리 과정입니다.  
  
-   쿼리 결과에서 반환된 요소와 특성 이름의 특수 XML 및 URL 문자는 그에 해당되는 유니코드 문자의 16진수 값을 사용하여 인코딩됩니다. 이전 결과에서 요소 이름 <`Special Chars`>는 <`Special_x0020_Chars`>로 반환됩니다. 특성 이름 <`Col#&2`>는 <`Col_x0023__x0026_2`>로 반환됩니다. XML 및 URL 특수 문자가 모두 인코딩됩니다.  
  
-   요소 또는 특성의 값에 5 개의 표준 XML 문자 엔터티 (', "", 및 &)가 포함 된 경우 \<, > 이러한 특수 xml 문자는 항상 xml 문자 인코딩을 사용 하 여 인코딩됩니다. 이전 결과에서 <`&`> 특성 값의 `Col1` 값은 `&`로 인코딩됩니다. 그러나 # 문자는 유효한 XML 문자이고 특수 XML 문자가 아니기 때문에 #로 그대로 유지됩니다.  
  
-   요소나 특성의 값에 URL에서 특수한 의미가 있는 특수 URL 문자가 있으면 이 문자는 DBOBJECT URL 값에서만 인코딩되고 특수 문자가 테이블이나 열 이름의 일부일 경우에만 인코딩됩니다. 결국 테이블 이름 `#` 의 일부인 문자 `Col#&2` 는 `_x0023_ in the DBOJBECT URL`으로 인코딩됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 AUTO 모드 사용](use-auto-mode-with-for-xml.md)  
  
  
