---
title: X쿼리의 문자열 검색 | 마이크로 소프트 문서
description: XQuery에서 문자열 검색 예제를 보고 XML 문서에서 텍스트를 검색하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- strings [SQL Server], search
- XML [SQL Server], searching text
- searches [SQL Server], XML documents
- XQuery, string search
ms.assetid: edc62024-4c4c-4970-b5fa-2e54a5aca631
author: rothja
ms.author: jroth
ms.openlocfilehash: 33f68a55cb627099150ec14941fe5de81de53fc8
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388058"
---
# <a name="string-search-in-xquery"></a>XQuery에서 문자열 검색
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 XML 문서에서 텍스트를 검색하는 방법을 보여 주는 예제 쿼리를 제공합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-find-feature-descriptions-that-contain-the-word-maintenance-in-the-product-catalog"></a>A. 제품 카탈로그에서 "maintenance"라는 단어가 포함된 기능 설명 찾기  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    for $f in /p1:ProductDescription/p1:Features/*  
     where contains(string($f), "maintenance")  
     return  
           $f ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 이전 `where` 쿼리에서 FLOWR 식은 `for` 식의 결과를 필터링하고 **contains()** 조건을 충족하는 요소만 반환합니다.  
  
 다음은 결과입니다.  
  
```  
<p1:Maintenance     
      xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
 <p1:NoOfYears>10</p1:NoOfYears>  
 <p1:Description>maintenance contact available through your   
               dealer or any AdventureWorks retail store.</p1:Description>  
</p1:Maintenance>  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버&#41;&#40;XML 데이터](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
