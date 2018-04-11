---
title: 이름이 있는 열 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8a73ca9c3e77d73ea885ecb70e25fc2018663690
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="columns-with-a-name"></a>이름이 있는 열
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  다음은 이름이 있는 행 집합 열이 대/소문자를 구분하여 결과 XML에 매핑되는 특정 조건입니다.  
  
-   열 이름이 @ 기호로 시작하는 경우  
  
-   열 이름이 @ 기호로 시작하지 않는 경우  
  
-   열 이름이 @ 기호로 시작하지 않고 슬래시 기호(/)를 포함하는 경우  
  
-   여러 열이 같은 접두사를 공유하는 경우  
  
-   하나의 열에 다른 이름이 있는 경우  
  
## <a name="column-name-starts-with-an-at-sign-"></a>열 이름이 @ 기호로 시작하는 경우  
 열 이름이 @ 기호로 시작하고 슬래시 기호(/)를 포함하지 않는 경우 해당 열 값을 갖는 `row` 요소의 특성이 만들어집니다. 예를 들어 다음 쿼리는 2개의 열(@PmId, Name)로 구성된 행 집합을 반환합니다. 결과 XML에서 **PmId** 특성이 해당 `row` 요소에 추가되고 ProductModelID의 값이 여기에 할당됩니다.  
  
```  
  
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
  
```  
  
 다음은 결과입니다.  
  
```  
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 특성은 같은 수준에서 요소 노드, 텍스트 노드 등 다른 노드 유형 앞에 와야 합니다. 다음 쿼리는 오류를 반환합니다.  
  
```  
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign-"></a>열 이름이 @ 기호로 시작하지 않는 경우  
 열 이름이 @ 기호로 시작하지 않고 XPath 노드 테스트 중 하나가 아니며 슬래시 기호(/)를 포함하지 않는 경우 기본적으로 `row` 행 요소의 하위 요소인 XML 요소가 생성됩니다.  
  
 다음 쿼리는 결과인 열 이름을 지정합니다. 따라서 `result` 요소 자식이 `row` 요소에 추가됩니다.  
  
```  
SELECT 2+2 as result  
for xml PATH  
```  
  
 다음은 결과입니다.  
  
```  
<row>  
  <result>4</result>  
</row>  
```  
  
 다음 쿼리는 **xml** 유형의 Instructions 열에 대해 지정된 XQuery에서 반환하는 XML에 대해 열 이름 ManuWorkCenterInformation을 지정합니다. 따라서 `ManuWorkCenterInformation` 요소가 `row` 요소의 자식으로 추가됩니다.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
 다음은 결과입니다.  
  
```  
<row>  
  <ProductModelID>7</ProductModelID>  
  <Name>HL Touring Frame</Name>  
  <ManuWorkCenterInformation>  
    <MI:Location ...LocationID="10" ...></MI:Location>  
    <MI:Location ...LocationID="20" ...></MI:Location>  
     ...  
  </ManuWorkCenterInformation>  
</row>  
```  
  
## <a name="column-name-does-not-start-with-an-at-sign--and-contains-a-slash-mark-"></a>열 이름이 @ 기호로 시작하지 않고 슬래시 기호(/)를 포함하는 경우  
 열 이름이 @ 기호로 시작하지 않지만 슬래시 기호(/)를 포함할 경우 열 이름은 XML 계층을 나타냅니다. 예를 들어 열 이름이 "Name1/Name2/Name3.../Name***n*** "이면 각 Name***i*** 는 현재 행 요소(i=1인 경우)에 중첩된 요소 이름을 나타내거나 이름이 Name***i-1***인 요소 아래의 요소 이름을 나타냅니다. Namen***n*** 이 '@'으로 시작하는 경우 Name***n-1*** 요소의 특성에 매핑됩니다.  
  
 예를 들어 다음 쿼리는 이름, 중간 이름 및 성을 포함하는 복잡한 요소 EmpName으로 표현되는 직원 ID와 이름을 반환합니다.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 PATH 모드에서 XML을 생성할 때 열 이름이 경로로 사용됩니다. 직원 ID 값을 포함하는 열 이름이 '\@'로 시작하므로 **EmpID** 특성이 `row` 요소에 추가됩니다. 다른 모든 열에는 계층을 나타내는 열 이름에 슬래시 기호('/')가 있습니다. 결과 XML은 `row` 요소 아래에 `EmpName` 자식을 포함하고 `EmpName` 자식은 `First`, `Middle` 및 `Last` 요소 자식을 갖습니다.  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 직원 중간 이름은 Null이며 기본적으로 Null 값이 매핑할 요소나 특성이 없습니다. NULL 값에 대해 요소를 생성하려는 경우 이 쿼리에서와 같이 ELEMENTS 지시어와 XSINIL을 함께 지정할 수 있습니다.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 다음은 결과입니다.  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
      EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 기본적으로 PATH 모드는 요소 중심의 XML을 생성하므로 PATH 모드 쿼리에 ELEMENTS 지시어를 지정하면 아무 영향도 미치지 않습니다. 그러나 이전 예에서와 같이 ELEMENTS 지시어를 XSINIL과 함께 사용하면 Null 값에 대한 요소를 생성하는 데 유용합니다.  
  
 다음 쿼리에서는 ID와 이름 외에 직원 주소를 검색합니다. 주소 열에 대한 열 이름에 있는 각 경로대로 `Address` 요소 자식이 `row` 요소에 추가되고 주소 정보가 `Address` 요소의 요소 자식으로 추가됩니다.  
  
```  
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 다음은 결과입니다.  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
</row>  
```  
  
## <a name="several-columns-share-the-same-path-prefix"></a>여러 열이 같은 경로 접두사를 공유하는 경우  
 이어지는 여러 열이 같은 경로 접두사를 공유할 경우 같은 이름으로 함께 그룹화됩니다. 다른 네임스페이스 접두사가 사용되면 같은 네임스페이스로 바인딩되더라도 경로가 다르다고 간주됩니다. 이전 쿼리에서 FirstName, MiddleName 및 LastName 열은 동일한 EmpName 접두사를 공유하므로 `EmpName` 요소의 자식으로 추가됩니다. 이전 예제에서 `Address` 요소를 만들던 것도 이와 같은 경우입니다.  
  
## <a name="one-column-has-a-different-name"></a>하나의 열에 다른 이름이 있는 경우  
 이름이 다른 열이 중간에 나타나면 다음의 수정된 쿼리에서와 같이 그룹화가 해제됩니다. 쿼리는 FirstName 열과 MiddleName 열 사이에 주소 열을 추가하여 이전 쿼리에 지정된 대로 FirstName, MiddleName 및 LastName의 그룹화를 해제합니다.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 그 결과 쿼리는 두 개의 `EmpName` 요소를 생성합니다. 첫 번째 `EmpName` 요소는 `FirstName` 요소 자식을 포함하고 두 번째 `EmpName` 요소는 `MiddleName` 및 `LastName` 요소 자식을 포함합니다.  
  
 다음은 결과입니다.  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
  <EmpName>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
