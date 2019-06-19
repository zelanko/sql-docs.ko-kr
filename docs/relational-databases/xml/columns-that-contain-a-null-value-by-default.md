---
title: 기본적으로 Null 값을 포함하는 열 | Microsoft 문서
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
manager: craigg
ms.openlocfilehash: 33acf250b60628869cde6b1c920ee3e86e08259a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175352"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>기본적으로 Null 값을 포함하는 열

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  
