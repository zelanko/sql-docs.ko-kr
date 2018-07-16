---
title: xml 데이터 형식에 대한 FOR XML 지원 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 14010ca375afdf5166f737a27e33f8ed3fc42c49
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37327347"
---
# <a name="for-xml-support-for-the-xml-data-type"></a>xml 데이터 형식에 대한 FOR XML 지원
  FOR XML 쿼리 열을 지정 하는 경우 `xml` 형식 SELECT 절에서 열 값은 ELEMENTS 지시어를 지정 하는 여부에 관계 없이 반환된 된 XML의 요소로 매핑됩니다. `xml` 유형의 열에 있는 XML 선언은 직렬화되지 않습니다.  
  
 예를 들어 다음 쿼리는 검색 고객 연락처 정보 등을 `BusinessEntityID`, `FirstName`, 및 `LastName` 열 및 전화 번호를 `AdditionalContactInfo` 열의 `xml` 형식입니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 열 값에서 검색 된 추가 연락 정보 값을 제외 하 고 특성으로 반환 된 쿼리는 ELEMENTS 지시어를 지정 하지 않으므로는 `xml` 유형 열입니다. 이러한 값은 요소로 반환됩니다.  
  
 다음은 결과의 일부입니다.  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</PhoneNumber>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</PhoneNumber>`  
  
```  
</Person.Person>  
...  
```  
  
 XQuery에 의해 생성된 XML 열에 대한 열 별칭을 지정하면 XQuery에 의해 생성되는 XML에 래퍼 요소를 추가하는 데 해당 별칭이 사용됩니다. 예를 들어 다음 쿼리는 `MorePhoneNumbers`를 열 별칭으로 지정합니다.  
  
```  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 XQuery에 의해 반환된 XML은 다음 부분 결과에 표시된 것과 같이 <`MorePhoneNumbers`> 요소에 래핑됩니다.  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</MorePhoneNumbers>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</MorePhoneNumbers>`  
  
```  
</Person.Person>  
...  
```  
  
 쿼리에서 ELEMENTS 지시어를 지정하면 BusinessEntityID, LastName 및 FirstName이 결과 XML에 요소로 반환됩니다.  
  
 다음 예에서는 FOR XML 처리 논리가 XML 데이터에 있는 모든 XML 선언을 직렬화 하지 않음을 보여 줍니다는 `xml` 형식 열:  
  
```  
create table t(i int, x xml)  
go  
insert into t values(1, '<?xml version="1.0" encoding="UTF-8" ?>  
                             <Root SomeID="10" />')  
select i, x  
from   t  
for xml auto;  
```  
  
 다음은 결과입니다. 결과에서 XML 선언 <`?xml version="1.0" encoding="UTF-8" ?`>은 직렬화되지 않습니다.  
  
```  
<root>  
  <t i="1">  
    <x>  
      <Root SomeID="10" />  
    </x>  
  </t>  
</root>  
```  
  
## <a name="returning-xml-from-a-user-defined-function"></a>사용자 정의 함수로부터 XML 반환  
 FOR XML 쿼리를 사용하여 다음 중 하나를 반환하는 사용자 정의 함수로부터 XML을 반환할 수 있습니다.  
  
-   단일 `xml` 유형 열이 포함된 테이블  
  
-   인스턴스는 `xml` 형식  
  
 다음 사용자 정의 함수를 단일 열 테이블을 반환 하는 예를 들어 `xm`유형의:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.MyUDF (@ProudctModelID int)  
RETURNS @T TABLE  
  (  
     ProductDescription xml  
  )  
AS  
BEGIN  
  INSERT @T  
     SELECT CatalogDescription.query('  
declare namespace PD="http://www.adventure-works.com/schemas/products/description";  
                    //PD:ProductDescription  ')  
     FROM Production.ProductModel  
     WHERE ProductModelID = @ProudctModelID  
  RETURN  
END;  
```  
  
 사용자 정의 함수를 실행하고 함수로 반환된 테이블을 쿼리할 수 있습니다. 이 예제에서는 테이블을 쿼리하여 반환 된 XML에 할당 되는 `xml` 형식 변수입니다.  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 이 예는 사용자 정의 함수의 또 다른 예입니다. 이 사용자 정의 함수는 `xml` 유형의 인스턴스를 반환합니다. 이 예에서 사용자 정의 함수는 스키마 네임스페이스가 지정되어 있기 때문에 형식화된 XML 인스턴스를 반환합니다.  
  
```  
DROP FUNCTION dbo.MyUDF;  
GO  
CREATE FUNCTION MyUDF (@ProductModelID int)   
RETURNS xml ([Production].[ProductDescriptionSchemaCollection])  
AS  
BEGIN  
  declare @x xml  
  set @x =   ( SELECT CatalogDescription  
          FROM Production.ProductModel  
          WHERE ProductModelID = @ProductModelID )  
  return @x  
END;  
```  
  
 사용자 정의 함수로 반환된 XML은 다음과 같이 `xml` 유형의 변수에 할당될 수 있습니다.  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>관련 항목  
 [다양한 SQL Server 데이터 형식에 대한 FOR XML 지원](for-xml-support-for-various-sql-server-data-types.md)  
  
  
