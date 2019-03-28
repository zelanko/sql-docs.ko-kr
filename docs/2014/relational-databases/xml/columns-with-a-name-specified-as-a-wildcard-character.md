---
title: 이름이 와일드카드 문자로 지정된 열 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1ec180247a3df15af58f95e041a0c426a35cdb4
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532815"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>이름이 와일드카드 문자로 지정된 열
  지정된 열 이름이 와일드카드 문자(\*)이면 열 이름이 지정되지 않은 경우처럼 열 내용이 삽입됩니다. 이 열이 비-`xml` 유형 열이면 다음 예에서와 같이 열 내용이 텍스트 노드로 삽입됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 다음은 결과입니다.  
  
 `<row EmpID="1">KenJS??nchez</row>`  
  
 열이 `xml` 유형일 경우 해당 XML 트리가 삽입됩니다. 예를 들어 다음 쿼리는 Instructions 열에 대해 XQuery에서 반환한 XML이 포함된 열 이름에 "*"를 지정합니다.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
GO  
```  
  
 다음은 결과입니다. XQuery에서 반환한 XML이 래핑 요소 없이 삽입됩니다.  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location LocationID="10">...</MI:Location>`  
  
 `<MI:Location LocationID="20">...</MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 PATH 모드 사용](use-path-mode-with-for-xml.md)  
  
  
