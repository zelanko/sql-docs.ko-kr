---
title: FOR XML 쿼리와 중첩 FOR XML 쿼리 비교 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], comparing query types
ms.assetid: 19225b4a-ee3f-47cf-8bcc-52699eeda32c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cccb676574fe4b767d567fbe48cdb887baddf8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63205061"
---
# <a name="for-xml-query-compared-to-nested-for-xml-query"></a>FOR XML 쿼리와 중첩 FOR XML 쿼리 비교
  이 항목에서는 단일 수준 FOR XML 쿼리를 중첩 FOR XML 쿼리와 비교합니다. 중첩 FOR XML 쿼리를 사용할 때의 이점 중 하나는 쿼리 결과에 특성 중심 및 요소 중심의 XML을 조합하여 지정할 수 있다는 점입니다. 다음 예에서는 이러한 이점을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 `SELECT` 쿼리는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 제품 범주와 하위 범주 정보를 검색합니다. 쿼리에는 중첩 FOR XML이 없습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductCategory.ProductCategoryID,   
         ProductCategory.Name as CategoryName,  
         ProductSubCategory.ProductSubCategoryID,   
         ProductSubCategory.Name  
FROM     Production.ProductCategory, Production.ProductSubCategory  
WHERE    ProductCategory.ProductCategoryID = ProductSubCategory.ProductCategoryID  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
GO  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory ProductSubCategoryID="1" Name="Mountain Bike"/>  
  <ProductSubCategory ProductSubCategoryID="2" Name="Road Bike"/>  
  <ProductSubCategory ProductSubCategoryID="3" Name="Touring Bike"/>  
</ProductCategory>  
...  
```  
  
 쿼리에서 `ELEMENTS` 지시어를 지정하면 다음 결과 조각에서와 같이 요소 중심 결과를 검색합니다.  
  
```  
<ProductCategory>  
  <ProductCategoryID>1</ProductCategoryID>  
  <CategoryName>Bike</CategoryName>  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <Name>Mountain Bike</Name>  
  </ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  </ProductSubCategory>  
</ProductCategory>  
```  
  
 그런 후 다음 조각에서와 같이 특성 중심 및 요소 중심 XML이 조합된 XML 계층을 생성한다고 가정하십시오.  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 이전 조각에서 범주 ID 및 범주 이름과 같은 제품 범주 정보는 특성입니다. 하지만 하위 범주 정보는 요소 중심입니다. <`ProductCategory`> 요소를 생성하기 위해 다음과 같이 `FOR XML` 쿼리를 작성할 수 있습니다.  
  
```  
SELECT ProductCategoryID, Name as CategoryName  
FROM Production.ProductCategory ProdCat  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 다음은 결과입니다.  
  
```  
< ProdCat ProductCategoryID="1" CategoryName="Bikes" />  
< ProdCat ProductCategoryID="2" CategoryName="Components" />  
< ProdCat ProductCategoryID="3" CategoryName="Clothing" />  
< ProdCat ProductCategoryID="4" CategoryName="Accessories" />  
```  
  
 그런 다음 XML에서 원하는 중첩된 <`ProductSubCategory`> 요소를 생성하려면 다음과 같이 중첩된 `FOR XML` 쿼리를 추가합니다.  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName  
        FROM   Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 이전 쿼리에서 다음을 유의하십시오.  
  
-   내부 `FOR XML` 쿼리는 제품 하위 범주 정보를 검색합니다. `ELEMENTS` 지시어는 외부 쿼리에 의해 생성되는 XML에 추가된 요소 중심 XML을 생성하기 위해 내부 `FOR XML` 에 추가되어 있습니다. 기본적으로 외부 쿼리는 특성 중심 XML을 생성합니다.  
  
-   내부 쿼리에서 결과가 `TYPE` xml **유형이 되도록** 지시어를 지정합니다. 
  `TYPE`을 지정하지 않으면 결과가 `nvarchar(max)` 유형으로 반환되고 XML 데이터는 엔터티로 반환됩니다.  
  
-   외부 쿼리도 `TYPE` 지시어를 지정합니다. 따라서 이 쿼리의 결과는 클라이언트에 **xml** 유형으로 반환됩니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 다음 쿼리는 이전 쿼리를 확장한 것입니다. 여기에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 전체 제품 계층을 보여 줍니다. 여기에는 다음이 포함됩니다.  
  
-   제품 범주  
  
-   각 범주의 제품 하위 범주  
  
-   각 하위 범주의 제품 모델  
  
-   각 모델의 제품  
  
 다음 쿼리는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 이해하는 데 도움이 됩니다.  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName,  
               (SELECT ProductModel.ProductModelID,   
                       ProductModel.Name as ModelName,  
                       (SELECT ProductID, Name as ProductName, Color  
                        FROM   Production.Product  
                        WHERE  Product.ProductModelID =   
                               ProductModel.ProductModelID  
                        FOR XML AUTO, TYPE)  
                FROM   (SELECT distinct ProductModel.ProductModelID,   
                               ProductModel.Name  
                        FROM   Production.ProductModel,   
                               Production.Product  
                        WHERE  ProductModel.ProductModelID =   
                               Product.ProductModelID  
                        AND    Product.ProductSubCategoryID =   
                               ProductSubCategory.ProductSubCategoryID)   
                                  ProductModel  
                FOR XML AUTO, type  
               )  
        FROM Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<Production.ProductCategory ProductCategoryID="1" CategoryName="Bikes">  
  <Production.ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bikes</SubCategoryName>  
    <ProductModel ProductModelID="19" ModelName="Mountain-100">  
      <Production.Product ProductID="771"   
                ProductName="Mountain-100 Silver, 38" Color="Silver" />  
      <Production.Product ProductID="772"   
                ProductName="Mountain-100 Silver, 42" Color="Silver" />  
      <Production.Product ProductID="773"   
                ProductName="Mountain-100 Silver, 44" Color="Silver" />  
        ...  
    </ProductModel>  
     ...  
```  
  
 제품 하위 범주를 생성하는 중첩된 `ELEMENTS` 쿼리에서 `FOR XML` 지시어를 제거하면 전체 결과가 특성 중심이 됩니다. 그런 다음 중첩 없이 이 쿼리를 작성할 수 있습니다. `ELEMENTS` 를 추가하면 부분적으로 특성 중심이고 요소 중심이기도 한 XML이 생성됩니다. 이 결과는 단일 수준의 FOR XML 쿼리에 의해 생성될 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [중첩 FOR XML 쿼리 사용](use-nested-for-xml-queries.md)  
  
  
