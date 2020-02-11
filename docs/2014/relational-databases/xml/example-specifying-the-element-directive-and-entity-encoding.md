---
title: '예제: ELEMENT 지시어 및 엔터티 인코딩 지정 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENT directive
- entity encoding [XML]
ms.assetid: 50cda5c1-7293-4080-93b3-872e3b8d484e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28e0e9f808820acc1959ccc11266174e5610600c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63287234"
---
# <a name="example-specifying-the-element-directive-and-entity-encoding"></a>예제: ELEMENT 지시어 및 엔터티 인코딩 지정
  이 예에서는 **ELEMENT** 및 **XML** 지시어 간의 차이점을 보여 줍니다. **ELEMENT** 지시어는 데이터를 엔터티화하지만 **XML** 지시어는 그렇지 않습니다. \<Summary> 요소는 쿼리에서 할당된 XML인 `<Summary>This is summary description</Summary>`입니다.  
  
 다음 쿼리를 살펴보십시오.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription!ELEMENT]  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        NULL,  
       '<Summary>This is summary description</Summary>'  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 다음은 결과입니다. 요약 설명이 결과에 엔터티화되어 있습니다.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription><Summary>This is summary description</Summary></SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 이제 **XML** 지시어 대신 열 이름에 `Summary!2!SummaryDescription!XML`ELEMENT **지시어인** 을 지정하면 엔터티화 없이 요약 설명을 받게 됩니다.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <Summary>This is summary description</Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 다음 쿼리에서는 정적 XML 값을 할당하는 대신 **xml** 유형의 **query()** 메서드를 사용하여 **xml** 유형의 CatalogDescription 열에서 제품 모델의 요약 설명을 검색합니다. 결과는 **xml** 유형으로 알려져 있기 때문에 엔터티화가 적용되지 않습니다.  
  
```  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
       (SELECT CatalogDescription.query('  
            declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
          /pd:ProductDescription/pd:Summary'))  
FROM     Production.ProductModel  
WHERE    CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],Tag  
FOR XML EXPLICIT  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 EXPLICIT 모드 사용](use-explicit-mode-with-for-xml.md)  
  
  
