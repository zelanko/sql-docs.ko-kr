---
title: '예제: ELEMENT 지시어 지정 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ELEMENT directive
ms.assetid: 80dd5d1f-fa90-4f97-a186-8fa3f460a7f3
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f1f6edc1be2171f2165e7fde603d82f46affdc42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090609"
---
# <a name="example-specifying-the-element-directive"></a>예제: ELEMENT 지시어 지정
  이 예에서는 직원 정보를 검색하고 다음과 같이 요소 중심 XML을 생성합니다.  
  
```  
<Employee EmpID=...>  
  <Name>  
    <FName>...</FName>  
    <LName>...</LName>  
  </Name>  
</Employee>  
```  
  
 열 이름에 `ELEMENT` 지시어가 추가된 것을 제외하면 쿼리는 같은 상태로 유지됩니다. 따라서 특성 대신 <`FName`> 및 <`LName`> 요소 자식이 <`Name`> 요소에 추가됩니다. `Employee!1!EmpID` 열은 `ELEMENT` 지시어를 지정하지 않기 때문에 `EmpID`가 <`Employee`> 요소의 특성으로 추가됩니다.  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName!ELEMENT],  
       NULL       as [Name!2!LName!ELEMENT]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
ORDER BY [Employee!1!EmpID],[Name!2!FName!ELEMENT]  
FOR XML EXPLICIT;  
```  
  
 다음은 결과의 일부입니다.  
  
 `<Employee EmpID="1">`  
  
 `<Name>`  
  
 `<FName>Ken</FName>`  
  
 `<LName>Sánchez</LName>`  
  
 `</Name>`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name>`  
  
 `<FName>Terri</FName>`  
  
 `<LName>Duffy</LName>`  
  
 `</Name>`  
  
 `</Employee>`  
  
 `...`  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 EXPLICIT 모드 사용](use-explicit-mode-with-for-xml.md)  
  
  