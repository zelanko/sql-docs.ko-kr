---
title: 이름이 XPath 노드 테스트인 열 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
- XPath node test
ms.assetid: b48adccd-3b6b-486a-b326-20f57170186f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c6d2ed88feef80027a7c52c89b3fe891d8f589c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096143"
---
# <a name="columns-with-the-name-of-an-xpath-node-test"></a>이름이 XPath 노드 테스트인 열
  열 이름이 XPath 노드 테스트 중 하나일 경우 다음 표에서와 같이 내용이 매핑됩니다. 열 이름이 XPath 노드 테스트이면 내용이 해당 노드로 매핑됩니다. 열의 SQL 형식이 `xml`, 오류가 반환 됩니다.  
  
|열 이름|동작|  
|-----------------|--------------|  
|text()|이름이 text()인 열의 경우 열의 문자열 값이 텍스트 노드로 추가됩니다.|  
|comment()|이름이 comment()인 열의 경우 열의 문자열 값이 XML 주석으로 추가됩니다.|  
|node()|이름이 node()인 열의 경우 열 이름이 와일드카드 문자(*)일 때와 결과가 같습니다.|  
|processing-instruction(name)|이름이 처리 명령인 열의 경우 열의 문자열 값이 처리 명령 대상 이름의 PI 값으로 추가됩니다.|  
  
 다음 쿼리에서는 노드 테스트를 열 이름으로 사용하는 방법을 보여 줍니다. 쿼리는 결과 XML에 텍스트 노드와 주석을 추가합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
        'Example of using node tests such as text(), comment(), processing-instruction()'                as "comment()",  
        'Some PI'                   as "processing-instruction(PI)",  
        'Employee name and address data' as "text()",  
        'middle name is optional'        as "EmpName/text()",  
        FirstName                        as "EmpName/First",   
        MiddleName                       as "EmpName/Middle",   
        LastName                         as "EmpName/Last",  
        AddressLine1                     as "Address/AddrLine1",  
        AddressLine2                     as "Address/AddrLIne2",  
        City                             as "Address/City"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P   
    ON P.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS BAE  
    ON BAE.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BAE.AddressID = A.AddressID  
WHERE  E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 다음은 결과입니다.  
  
 `<row EmpID="1">`  
  
 `<!--Example of using node tests such as text(), comment(), processing-instruction() -->`  
  
 `<?PI Some PI?>`  
  
 `Employee name and address data`  
  
 `<EmpName>middle name is optional`  
  
 `<First>Ken</First>`  
  
 `<Last>Sánchez</Last>`  
  
 `</EmpName>`  
  
 `<Address>`  
  
 `<AddrLine1>4350 Minute Dr.</AddrLine1>`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</row>`  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 PATH 모드 사용](use-path-mode-with-for-xml.md)  
  
  
