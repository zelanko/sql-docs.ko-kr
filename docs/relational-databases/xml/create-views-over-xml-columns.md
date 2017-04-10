---
title: "XML 열에서 뷰 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "뷰 [SQL Server의 XML]"
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# XML 열에서 뷰 만들기
  **xml** 유형 열을 사용하여 뷰를 만들 수 있습니다. 다음 예에서는 **xml** 데이터 형식의 **value()** 메서드를 사용하여 `xml` 유형 열의 값을 검색하는 뷰를 만듭니다.  
  
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
  
 다음은 **xml** 데이터 형식을 사용하여 뷰를 만드는 방법에 대한 설명입니다.  
  
-   xml 데이터 형식은 구체화된 뷰에서 만들 수 있습니다. 구체화된 뷰는 XML 데이터 형식의 메서드를 기반으로 할 수 없습니다. 하지만 기본 테이블에 있는 xml 유형의 열과는 다른 XML 스키마 컬렉션으로 캐스팅할 수 있습니다.  
  
-   분산형 분할 뷰에서는 **xml** 데이터 형식을 사용할 수 없습니다.  
  
-   뷰에 대해 실행하는 SQL 조건자는 뷰 정의의 XQuery에 밀어넣지 못합니다.  
  
-   뷰의 XML 데이터 형식 메서드는 업데이트할 수 없습니다.  
  
  