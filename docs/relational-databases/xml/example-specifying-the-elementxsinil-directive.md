---
title: '예제: ELEMENTXSINIL 지시어 지정 | Microsoft Docs'
description: SQL에서 ELEMENTXSINIL 지시어를 지정하여 xsi:nil 특성이 true인 NULL 값에 XML 요소를 생성하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTXSINIL directive
ms.assetid: bbcb6f9e-a51b-4775-9795-947c9d6d758f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64e44b8f84f2ff4b908556b31b6088a6a2c77c55
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632505"
---
# <a name="example-specifying-the-elementxsinil-directive"></a>예제: ELEMENTXSINIL 지시어 지정
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  요소 중심 XML을 검색하기 위해 ELEMENT 지시어를 지정할 때 열에 NULL 값이 있으면 EXPLICIT 모드에서 해당 요소가 생성되지 않습니다. **xsi:nil** 특성이 TRUE 값으로 설정된 경우 NULL 값에 대한 요소를 생성하도록 요청하기 위해 선택적으로 ELEMENTXSINIL 지시어를 지정할 수 있습니다.  
  
 다음 쿼리는 직원 주소가 포함된 XML을 생성합니다. `AddressLine2` 및 `City` 열에서 열 이름은 `ELEMENTXSINIL` 지시어를 지정합니다. 이렇게 하면 행 집합에서 `AddressLine2` 및 `City` 열에 있는 NULL 값에 대한 요소가 생성됩니다.  
  
```sql
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

```xml
<Employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          EmpID="1"
          AddressID="249">
  <Address AddressID="249">
    <AddressLine1>4350 Minute Dr.</AddressLine1>
    <AddressLine2 xsi:nil="true" />
    <City>Minneapolis</City>
  </Address>
</Employee>
...
```
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
