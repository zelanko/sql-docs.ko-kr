---
title: 기본적으로 Null 값을 포함하는 열 | Microsoft 문서
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
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ada1d2f79b74455a8fcd885362c9efc3fb286e71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173066"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>기본적으로 Null 값을 포함하는 열
  기본적으로 열에 Null 값이 있으면 특성, 노드 또는 요소가 없습니다. 다음 쿼리에서와 같이 ELEMENTS 지시어를 사용하여 요소 중심 XML을 요청하고 NULL 값에 대해 요소 추가를 요청하도록 XSINIL을 지정하면 이 기본 동작을 덮어쓸 수 있습니다.  
  
```  
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 다음은 결과를 보여 줍니다. XSINIL을 지정하지 않으면 <`Middle`> 요소가 없습니다.  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 PATH 모드 사용](use-path-mode-with-for-xml.md)  
  
  