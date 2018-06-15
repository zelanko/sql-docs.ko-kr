---
title: position 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c0afc659ea30da13a520c04c3d9f7efbdfaf8681
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077930"
---
# <a name="context-functions---position-xquery"></a>컨텍스트 함수-위치 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 처리 중인 항목의 시퀀스 내에서 컨텍스트 항목의 위치를 나타내는 정수 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], **fn:position()** 상황별 조건자의 경우에만 사용할 수 있습니다. 특히 사용 시 대괄호([ ])로 묶어야 합니다. 이 함수와 비교하면 정적 유형 유추 중에 카디널리티가 감소하지 않습니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>1. position() XQuery 함수를 사용하여 처음 두 개 제품 기능 검색  
 다음 쿼리는 제품 모델 카탈로그 설명에서 처음 두 개 기능, 즉 <`Features`> 요소의 처음 두 개 자식 요소를 검색합니다. 추가 기능이 있을 경우 <`there-is-more/`> 요소를 결과에 추가합니다.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **네임 스페이스** 키워드는 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 쿼리 본문에 사용 되는 네임 스페이스 접두사를 정의 합니다.  
  
-   쿼리 본문에는 XML을 생성 한 \<제품 > 요소와 **ProductModelID** 및 **ProductModelName** 특성 및 자식 요소로 반환 된 제품 기능이 있는 합니다.  
  
-   **position ()** 함수를 사용 하는 조건자에서의 위치를 결정 하는 \<기능 > 컨텍스트에서 자식 요소입니다. 이것이 첫 번째 기능이거나 두 번째 기능인 경우 반환됩니다.  
  
-   IF 문이 추가 \<여기는 더 / > 요소를 두 개 이상의 기능 제품 카탈로그에 있는 경우 결과입니다.  
  
-   일부 제품 모델만 해당 카탈로그 설명이 테이블에 저장되어 있으므로 WHERE 절을 사용하여 CatalogDescriptions가 NULL인 행을 무시합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
…  
```  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
