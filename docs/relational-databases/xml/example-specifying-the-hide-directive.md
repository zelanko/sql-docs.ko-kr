---
title: '예제: HIDE 지시어 지정 | Microsoft 문서'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HIDE directive
ms.assetid: 87504d87-1cbd-412a-9041-47884b6efcec
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b71fa8a58aa2e18e2de3cb24da42cf8c470c40f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33013440"
---
# <a name="example-specifying-the-hide-directive"></a>예제: HIDE 지시어 지정
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 예에서는 **HIDE** 지시어 사용 방법을 보여 줍니다. 이 지시어는 쿼리에 의해 반환된 범용 테이블의 행을 정렬하기 위한 특성은 쿼리가 반환하게 하고 최종 결과 XML 문서에는 그 특성이 포함되지 않게 하려는 경우에 유용합니다.  
  
 다음 쿼리는 이러한 XML을 생성합니다.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
           <Summary> element from XML stored in CatalogDescription column  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 이 쿼리는 원하는 XML을 생성합니다. 이 쿼리는 열 이름의 Tag 값으로 1과 2가 포함된 두 열 그룹을 식별합니다.  
  
 이 쿼리는 [xml](../../t-sql/xml/query-method-xml-data-type.md) 데이터 형식의 **query() 메서드(xml 데이터 형식)** 를 사용하여 요약 설명을 검색하기 위해 **xml** 유형의 CatalogDescription 열을 쿼리합니다. 이 쿼리는 또한 [xml](../../t-sql/xml/value-method-xml-data-type.md) 데이터 형식의 **value() 메서드(xml 데이터 형식)** 를 사용하여 CatalogDescription 열로부터 ProductModelID 값을 검색합니다. 이 값은 결과 XML에 필요하지 않지만 결과 행 집합을 정렬하는 데 필요합니다. 따라서 열 이름 `[Summary!2!ProductModelID!HIDE]`에는 **HIDE** 지시어가 포함됩니다. 이 열이 SELECT 문에 포함되지 않은 경우 `[ProductModel!1!ProdModelID]` xml `[Summary!2!SummaryDescription]` 유형인 **및** 으로 행 집합을 정렬해야 하며 ORDER BY에서는 **xml** 유형의 열을 사용할 수 없습니다. 따라서 추가 `[Summary!2!ProductModelID!HIDE]` 열이 추가된 다음 ORDER BY 절에 지정됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID     as [ProductModel!1!ProdModelID],  
        Name               as [ProductModel!1!Name],  
        NULL               as [Summary!2!ProductModelID!hide],  
        NULL               as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
        CatalogDescription.value('  
         declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       (/PD:ProductDescription/@ProductModelID)[1]', 'int'),  
        CatalogDescription.query('  
         declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /pd:ProductDescription/pd:Summary')  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],[Summary!2!ProductModelID!hide]  
FOR XML EXPLICIT  
go  
```  
  
 다음은 결과입니다.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" xmlns="">  
        <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike. Performance-enhancing options include the innovative HL Frame, super-smooth front suspension, and traction for all terrain. </p1:p>  
      </pd:Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
