---
title: "예제: ELEMENTXSINIL 지시어 지정 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ELEMENTXSINIL directive
ms.assetid: bbcb6f9e-a51b-4775-9795-947c9d6d758f
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42f40e0a22457f365e27a6f1560bd2f496366294
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="example-specifying-the-elementxsinil-directive"></a>예제: ELEMENTXSINIL 지시어 지정
  요소 중심 XML을 검색하기 위해 ELEMENT 지시어를 지정할 때 열에 NULL 값이 있으면 EXPLICIT 모드에서 해당 요소가 생성되지 않습니다. **xsi:nil** 특성이 TRUE 값으로 설정된 경우 NULL 값에 대한 요소를 생성하도록 요청하기 위해 선택적으로 ELEMENTXSINIL 지시어를 지정할 수 있습니다.  
  
 다음 쿼리는 직원 주소가 포함된 XML을 생성합니다. `AddressLine2` 및 `City` 열에서 열 이름은 `ELEMENTXSINIL` 지시어를 지정합니다. 이렇게 하면 행 집합에서 `AddressLine2` 및 `City` 열에 있는 NULL 값에 대한 요소가 생성됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID  as [Employee!1!EmpID],  
       BEA.AddressID as [Employee!1!AddressID],  
       NULL        as [Address!2!AddressID],  
       NULL        as [Address!2!AddressLine1!ELEMENT],  
       NULL        as [Address!2!AddressLine2!ELEMENTXSINIL],  
       NULL        as [Address!2!City!ELEMENTXSINIL]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       BEA.AddressID,  
       A.AddressID,  
       AddressLine1,   
       AddressLine2,  
       City   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BEA.AddressID = A.AddressID  
ORDER BY [Employee!1!EmpID],[Address!2!AddressID]  
FOR XML EXPLICIT;  
```  
  
 다음은 결과의 일부입니다.  
  
 `<Employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `EmpID="1" AddressID="249">`  
  
 `<Address AddressID="249">`  
  
 `<AddressLine1>4350 Minute Dr.</AddressLine1>`  
  
 `<AddressLine2 xsi:nil="true" />`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</Employee>`  
  
 `...`  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  

