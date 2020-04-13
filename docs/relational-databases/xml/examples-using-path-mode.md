---
title: '예제: PATH 모드 사용 | Microsoft 문서'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, examples
ms.assetid: 3564e13b-9b97-49ef-8cf9-6a78677b09a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 51bdad5bc62e9dc47a3f9cd4c3bf90d0c41c59bb
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665167"
---
# <a name="examples-using-path-mode"></a>예제: PATH 모드 사용
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  다음 예에서는 SELECT 쿼리에서 XML을 생성할 때 PATH 모드를 사용하는 방법을 보여 줍니다. 이러한 쿼리는 대부분 ProductModel 테이블의 Instructions 열에 저장된 자전거 제조 지침 XML 문서에 대해 지정됩니다.  
  
## <a name="specifying-a-simple-path-mode-query"></a>간단한 PATH 모드 쿼리 지정  
 이 쿼리는 FOR XML PATH 모드를 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   
       ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH;  
GO  
```  
  
 다음 결과는 결과 행 집합의 각 열 값이 요소에 래핑되는 요소 중심 XML입니다. `SELECT` 절은 열 이름에 별칭을 지정하지 않으므로 생성된 자식 요소 이름은 `SELECT` 절에 있는 해당 열 이름과 같습니다. 행 집합의 각 행마다 <`row`> 태그가 추가됩니다.  
  
 ```
<row>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</row>  
<row>  
  <ProductModelID>119</ProductModelID>
  <Name>Bike Wash</Name>
</row>
```
  
 다음 결과는 `RAW` 옵션이 지정된 `ELEMENTS` 모드 쿼리와 같습니다. 여기서는 결과 집합의 각 행에 대해 기본 <`row`> 요소가 있는 요소 중심 XML을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML RAW, ELEMENTS;  
```  
  
 필요에 따라 행 요소 이름을 지정하여 기본 <`row`>를 덮어쓸 수 있습니다. 예를 들어 다음 쿼리는 행 집합의 각 행에 대해 <`ProductModel`> 요소를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModel');  
GO  
```  
  
 결과 XML은 지정된 행 요소 이름을 갖습니다.  
  
```
<ProductModel>
  <ProductModelID>122</ProductModelID>
  <Name>All-Purpose Bike Stand</Name>
</ProductModel>
<ProductModel>
  <ProductModelID>119</ProductModelID>
  <Name>Bike Wash</Name>
</ProductModel>
```
  
 길이가 0인 문자열을 지정하면 래핑 요소가 생성되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('');  
GO  
```  
  
 다음은 결과입니다.  
  
```
<ProductModelID>122</ProductModelID>
<Name>All-Purpose Bike Stand</Name>
<ProductModelID>119</ProductModelID>
<Name>Bike Wash</Name>
```
  
## <a name="specifying-xpath-like-column-names"></a>XPath 형식의 열 이름 지정  
 다음 쿼리에서 지정된 열 이름 `ProductModelID`는 ‘\@’으로 시작하며 슬래시 기호('/')를 포함하지 않으므로 해당 열 값을 포함하는 <`row`> 요소의 특성이 결과 XML에 만들어집니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('ProductModelData');  
GO  
```  
  
 다음은 결과입니다.  
  
```
<ProductModelData id="122">
  <Name>All-Purpose Bike Stand</Name>
</ProductModelData>
<ProductModelData id="119">
  <Name>Bike Wash</Name>
</ProductModelData>
```
  
 `root` 에 `FOR XML`옵션을 지정하여 최상위 요소 하나를 추가할 수 있습니다.  
  
```  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 계층을 생성하려면 PATH 형식 구문을 포함합니다. 예를 들어 `Name` 열의 열 이름을 "SomeChild/ModelName"으로 변경하면 다음 결과와 같이 계층이 있는 XML이 생성됩니다.  
  
```
<Root>
  <ProductModelData id="122">
    <SomeChild>
      <ModelName>All-Purpose Bike Stand</ModelName>
    </SomeChild>
  </ProductModelData>
  <ProductModelData id="119">
    <SomeChild>
      <ModelName>Bike Wash</ModelName>
    </SomeChild>
  </ProductModelData>
</Root>
```
  
 다음 쿼리에서는 제품 모델 ID와 이름 외에 제품 모델의 제조 지침 위치를 검색합니다. Instructions 열은 **xml** 유형이므로 **xml** 데이터 형식의 **query()** 메서드를 지정하여 위치를 검색합니다.  
  
```  
SELECT ProductModelID AS "@id",  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') AS ManuInstr  
FROM Production.ProductModel  
WHERE ProductModelID = 7  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 다음은 결과의 일부입니다. 쿼리에서 ManuInstr을 열 이름으로 지정하므로 **query()** 메서드가 반환한 XML이 다음과 같이 <`ManuInstr`> 태그에 래핑됩니다.  

```
<Root>
  <ProductModelData id="7">
    <Name>HL Touring Frame</Name>
    <ManuInstr>
      <MI:Location xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"
        <MI:step>...</MI:step>...
      </MI:Location>
      ...
    </ManuInstr>
  </ProductModelData>
</Root> 
```

위의 FOR XML 쿼리에 <`Root`> 및 <`ProductModelData`> 요소에 대한 네임스페이스를 포함하려고 할 수 있습니다. 먼저 WITH XMLNAMESPACES를 사용하여 네임스페이스 바인딩에 접두사를 정의하고 FOR XML 쿼리에 접두사를 사용하여 네임스페이스에 포함할 수 있습니다. 자세한 내용은 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)를 참조하세요.  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES (  
   'uri1' AS ns1,    
   'uri2' AS ns2,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' as MI)  
SELECT ProductModelID AS "ns1:ProductModelID",  
       Name           AS "ns1:Name",  
       Instructions.query('  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ('ns2:ProductInfo'), root('ns1:root');  
GO  
```  
  
 `MI` 에는 `WITH XMLNAMESPACES`접두사도 정의됩니다. 그 결과로 지정된 **xml** 유형의 **query()** 메서드는 쿼리 프롤로그에 접두사를 정의하지 않습니다. 다음은 결과입니다.  
  
```
<ns1:root xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">
  <ns2:ProductInfo>
    <ns1:ProductModelID>7</ns1:ProductModelID>
    <ns1:Name>HL Touring Frame</ns1:Name>
    <MI:Location xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" LaborHours="2.5" LotSize="100" MachineHours="3" SetupHours="0.5" LocationID="10" xmlns="">
    <MI:step>
      Insert <MI:material>aluminum sheet MS-2341</MI:material> into the <MI:tool>T-85A framing tool</MI:tool>.
    </MI:step>
    ...
    </MI:Location>
    ...
  </ns2:ProductInfo>
</ns1:root>
```
  
## <a name="generating-a-value-list-using-path-mode"></a>PATH 모드를 사용하여 값 목록 생성  
 이 쿼리에서는 각 제품 모델에 대해 제품 ID의 값 목록을 생성하고 이 XML 조각에서와 같이 각 제품 ID에 대해 <`ProductName`> 중첩 요소를 생성합니다.  

```
<ProductModelData ProductModelID="7" ProductModelName="..." ProductIDs="product id list in the product model">
  <ProductName>...</ProductName>
  <ProductName>...</ProductName>
  ...
</ProductModelData>
```
  
 다음은 필요한 XML을 생성하는 쿼리입니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID     AS "@ProductModelID",  
       Name               AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')) AS "@ProductIDs",  
       (SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
        FOR XML PATH ('')) AS "ProductNames"  
FROM   Production.ProductModel  
WHERE  ProductModelID= 7 or ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   첫 번째 중첩 `SELECT` 는 `data()` 를 열 이름으로 사용하여 ProductID 목록을 반환합니다. 쿼리에서 빈 문자열을 `FOR XML PATH`의 행 요소 이름으로 지정하므로 요소가 생성되지 않습니다. 대신 값 목록이 `ProductID` 특성에 할당됩니다.  
  
-   두 번째 중첩 `SELECT` 는 제품 모델에 속한 제품에 대해 제품 이름을 검색합니다. 쿼리에서 `ProductName`를 열 이름으로 지정하므로 <`ProductNames`> 요소에 래핑되어 반환되는 <`ProductNames`> 요소를 생성합니다.  
  
 다음은 결과의 일부입니다.  
  
```
<ProductModelData PId="7" ProductModelName="HL Touring Frame" ProductIDs="885 887 ...">
  <ProductNames>
    <ProductName>HL Touring Frame - Yellow, 60</ProductName>
    <ProductName>HL Touring Frame - Yellow, 46</ProductName>
  </ProductNames>
  ...
</ProductModelData>
<ProductModelData PId="9" ProductModelName="LL Road Frame" ProductIDs="722 723 724 ...">
  <ProductNames>
    <ProductName>LL Road Frame - Black, 58</ProductName>
    <ProductName>LL Road Frame - Black, 60</ProductName>
    <ProductName>LL Road Frame - Black, 62</ProductName>
    ...
  </ProductNames>
</ProductModelData>
```
  
 제품 이름을 생성하는 하위 쿼리가 올바르게 수정되어 XML에 추가된 문자열로 결과를 반환합니다. type 지시어 `FOR XML PATH (''), type`을 추가하면 하위 쿼리가 **xml** 유형으로 결과를 반환하며 수정되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@ProductModelID",  
      Name AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ProductIDs",  
       (  
       SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH (''), type  
       ) AS "ProductNames"  
  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
## <a name="adding-namespaces-in-the-resulting-xml"></a>결과 XML에 네임스페이스 추가  
 [WITH XMLNAMESPACES를 사용하여 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)항목에 설명된 대로 WITH XMLNAMESPACES를 사용하여 PATH 모드 쿼리에 네임스페이스를 포함시킬 수 있습니다. 예를 들어 SELECT 절에 지정된 이름에는 네임스페이스 접두사가 포함됩니다. 다음 `PATH` 모드 쿼리는 네임스페이스가 있는 XML을 생성합니다.  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
GO  
```  
  
 <`@xml:lang`> 요소에 추가된 `English` 특성이 미리 정의된 xml 네임스페이스에 정의됩니다.  
  
 다음은 결과입니다.  

```
<Translation>
  <English xml:lang="en">food</English>
  <German xml:lang="ger">Essen</German>
</Translation>
```
  
 다음 쿼리는 `WITH XMLNAMESPACES` 를 사용하여 XML 결과에 네임스페이스를 포함한다는 점을 제외하고 예 3과 비슷합니다. 자세한 내용은 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)를 참조하세요.  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES ('uri1' AS ns1,  DEFAULT 'uri2')  
SELECT ProductModelID AS "@ns1:ProductModelID",  
      Name AS "@ns1:ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ns1:ProductIDs",  
       (  
       SELECT ProductID AS "@ns1:ProductID",   
              Name AS "@ns1:ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH , type   
       ) AS "ns1:ProductNames"  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData'), root('root');  
```  
  
 다음은 결과입니다.  
  
```
<root xmlns="uri2" 
  xmlns:ns1="uri1">
  <ProductModelData ns1:ProductModelID="7" ns1:ProductModelName="HL Touring Frame" ns1:ProductIDs="885 887 888 889 890 891 892 893">
    <ns1:ProductNames>
      <row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="885" ns1:ProductName="HL Touring Frame - Yellow, 60" />
      <row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="887" ns1:ProductName="HL Touring Frame - Yellow, 46" />
      ...
    </ns1:ProductNames>
  </ProductModelData>
  <ProductModelData ns1:ProductModelID="9" ns1:ProductModelName="LL Road Frame" ns1:ProductIDs="722 723 724 725 726 727 728 729 730 736 737 738">
    <ns1:ProductNames>
      <row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="722" ns1:ProductName="LL Road Frame - Black, 58" />
      ...
    </ns1:ProductNames>
  </ProductModelData>
</root>
```
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
