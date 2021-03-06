---
title: 기본적으로 Null 값을 포함하는 열 | Microsoft 문서
description: SQL에서 ELEMENTS XSINIL 키워드 문구를 사용하여 기본적으로 null 값을 포함하는 열을 처리하는 방법을 알아봅니다.
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d6962f6117a857ed5875d503c259b4d54e8dd84d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775605"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>기본적으로 Null 값을 포함하는 열

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

기본적으로 열에 Null 값이 있으면 특성, 노드 또는 요소가 없습니다. 이 기본 동작은 ELEMENTS XSINIL 키워드 구를 사용하여 재정의할 수 있습니다. 이 구문은 요소 중심 XML을 요청합니다. 이는 반환된 결과에 null 값이 명시적으로 표시됨을 의미합니다. 이러한 요소에는 값이 없습니다.

ELEMENTS XSINIL 구문은 다음 Transact-SQL SELECT 예제에 나와 있습니다.

```sql
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
  AND  E.EmployeeID=1
FOR XML PATH, ELEMENTS XSINIL;
```  
  
 다음은 결과를 보여 줍니다. XSINIL을 지정하지 않으면 <`Middle`> 요소가 없습니다.  
  
```xml
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
