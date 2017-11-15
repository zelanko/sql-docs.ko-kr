---
title: "예제: 직원 정보 검색 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: EXPLICIT mode
ms.assetid: 63cd6569-2600-485b-92b4-1f6ba09db219
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf27c767ea76c1577ac3c0e12dd1195c9ed34969
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="example-retrieving-employee-information"></a>예제: 직원 정보 검색
  이 예에서는 각 직원에 대한 직원 ID와 직원 이름을 검색합니다. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 employeeID는 Employee 테이블의 BusinessEntityID 열로부터 가져올 수 있습니다. 직원 이름은 Person 테이블로부터 가져올 수 있습니다. BusinessEntityID 열을 사용하면 테이블을 조인할 수 있습니다.  
  
 FOR XML EXPLICIT 변환으로 다음과 같이 XML을 생성한다고 가정해 보십시오.  
  
```  
<Employee EmpID="1" >  
  <Name FName="Ken" LName="Sánchez" />  
</Employee>  
...  
```  
  
 계층에 두 수준이 있기 때문에 두 개의 `SELECT` 쿼리를 작성하고 UNION ALL을 적용합니다. 이 쿼리는 <`Employee`> 요소에 대한 값과 해당 특성을 검색하는 첫 번째 쿼리입니다. 이 쿼리는 <`Employee`> 요소에 대한 `1` 값으로 `Tag`을 할당하고 최상위 요소이기 때문에 `Parent`에는 NULL을 할당합니다.  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID AS [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 다음은 두 번째 쿼리입니다. 이 쿼리는 <`Name`> 요소에 대한 값을 검색합니다. 이 쿼리는 <`Name`> 요소에 대한 `2` 값으로 `Tag`를 할당하고 <`Employee`>를 부모로 지정하는 `1` 태그 값으로 `Parent`을 할당합니다.  
  
```  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 이러한 쿼리를 `UNION AL`과 조합하고 `FOR XML EXPLICIT`를 적용하고 필요한 `ORDER BY` 절을 지정합니다. 먼저 `BusinessEntityID` 로 행 집합을 정렬하고 이름에 있는 NULL 값이 먼저 표시되도록 이름으로도 정렬해야 합니다. FOR XML 절 없이 다음 쿼리를 실행하면 범용 테이블이 생성되는 것을 볼 수 있습니다.  
  
 마지막 쿼리는 다음과 같습니다.  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
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
ORDER BY [Employee!1!EmpID],[Name!2!FName]  
FOR XML EXPLICIT;  
```  
  
 다음은 결과의 일부입니다.  
  
 `<Employee EmpID="1">`  
  
 `<Name FName="Ken" LName="Sánchez" />`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name FName="Terri" LName="Duffy" />`  
  
 `</Employee>`  
  
 `...`  
  
 첫 번째 `SELECT` 는 결과 행 집합에 대해 열 이름을 지정합니다. 이러한 이름은 두 개의 열 그룹을 형성합니다. 열 이름에서 `Tag` 값이 `1`인 그룹은 `Employee`를 요소로, `EmpID`는 특성으로 식별합니다. 다른 열 그룹에는 열에 `Tag` 값 `2`가 있으며 <`Name`>을 요소로, `FName` 및 `LName`은 특성으로 식별합니다.  
  
 다음 테이블은 쿼리에 의해 생성된 부분 행 집합을 보여 줍니다.  
  
 `Tag Parent  Employee!1!EmpID Name!2!FName Name!2!LName`  
  
 `--- ------  ---------------- ------------ ------------`  
  
 `1   NULL    1                NULL         NULL`  
  
 `2   1       1                Ken          Sánchez`  
  
 `1   NULL    2                NULL         NULL`  
  
 `2   1       2                Terri        Duffy`  
  
 `1   NULL    3                NULL         NULL`  
  
 `2   1       3                Roberto      Tamburello`  
  
 `...`  
  
 이 테이블은 범용 테이블의 행을 처리하여 결과 XML 트리를 생성하는 방법을 보여 줍니다.  
  
 첫 번째 행은 `Tag` 값 `1`을 식별합니다. 따라서 `Tag` 값 `1` 이 있는 열 그룹은 `Employee!1!EmpID`로 식별됩니다. 이 열은 `Employee`를 요소 이름으로 식별합니다. 그런 다음 `EmpID` 특성이 포함된 <`Employee`> 요소가 생성됩니다. 이러한 특성에는 해당 열 값이 할당됩니다.  
  
 두 번째 행에는 `Tag` 값 `2`가 포함됩니다. 따라서 열 이름에 `Tag` 값 `2` 가 포함된 열 그룹 `Name!2!FName`및 `Name!2!LName`이 식별됩니다. 이러한 열 이름은 `Name`을 요소 이름으로 식별합니다. `FName` 및 `LName` 특성이 포함된 <`Name`> 요소가 생성됩니다. 이러한 특성에는 해당 열 값이 할당됩니다. 이 행은 `1`을 `Parent`로 식별합니다. 이 요소 자식은 이전 <`Employee`> 요소에 추가됩니다.  
  
 이러한 프로세스는 행 집합의 남은 열에 대해 반복됩니다. FOR XML EXPLICIT에서 행 집합을 순서대로 처리하고 원하는 XML을 생성하기 위해서는 범용 테이블의 행을 정렬하는 것이 중요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
