---
title: XML 열에서 뷰 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cc4890077c25e98ebff0832423f6d1f0aaabdc46
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889219"
---
# <a name="create-views-over-xml-columns"></a>XML 열에서 뷰 만들기
  사용할 수는 `xml` 뷰를 만들려면 유형 열입니다. 다음 예에서는 뷰를 만듭니다에서 값을는 `xml` 형식 열이 사용 하 여 검색 됩니다 합니다 `value()` 메서드의 `xml` 데이터 형식입니다.  
  
```  
-- Create the table.  
CREATE TABLE T (  
    ProductID          int primary key,   
    CatalogDescription xml)  
GO  
-- Insert sample data.  
INSERT INTO T values(1,'<ProductDescription ProductID="1" ProductName="SomeName" />')  
GO  
-- Create view (note the value() method used to retrieve ProductName   
-- attribute value from the XML).  
CREATE VIEW MyView AS   
  SELECT ProductID,  
         CatalogDescription.value('(/ProductDescription/@ProductName)[1]', 'varchar(40)') AS PName  
  FROM T  
GO   
```  
  
 뷰에 대해 다음 쿼리를 실행합니다.  
  
```  
SELECT *   
FROM   MyView  
```  
  
 다음은 결과입니다.  
  
```  
ProductID   PName        
----------- ------------  
1           SomeName   
```  
  
 사용에 대 한 다음 사항에 유의 합니다 `xml` 뷰를 만들 데이터 형식:  
  
-   xml 데이터 형식은 구체화된 뷰에서 만들 수 있습니다. 구체화된 뷰는 XML 데이터 형식의 메서드를 기반으로 할 수 없습니다. 하지만 기본 테이블에 있는 xml 유형의 열과는 다른 XML 스키마 컬렉션으로 캐스팅할 수 있습니다.  
  
-   `xml` 분산형 분할 뷰에서 데이터 형식을 사용할 수 없습니다.  
  
-   뷰에 대해 실행하는 SQL 조건자는 뷰 정의의 XQuery에 밀어넣지 못합니다.  
  
-   뷰의 XML 데이터 형식 메서드는 업데이트할 수 없습니다.  
  
  
