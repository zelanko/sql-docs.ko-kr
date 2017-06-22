---
title: "xml 데이터 형식에 대한 FOR XML 지원 | Microsoft 문서"
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
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9fcd42a40be7da666ed66dc7eb05600b081457ea
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="for-xml-support-for-the-xml-data-type"></a>xml 데이터 형식에 대한 FOR XML 지원
  FOR XML 쿼리가 SELECT 절에서 **xml** 유형의 열을 지정하는 경우 ELEMENTS 지시어를 지정했는지 여부에 관계없이 열 값은 반환된 XML의 요소로 매핑됩니다. **xml** 유형의 열에 있는 XML 선언은 직렬화되지 않습니다.  
  
 예를 들어 다음 쿼리는 `BusinessEntityID`xml `FirstName`유형의 `LastName` 열에서 `AdditionalContactInfo` , **및** 열과 전화 번호와 같은 고객 연락 정보를 검색합니다.  
  
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
  
 쿼리는 ELEMENTS 지시어를 지정하지 않기 때문에 **xml** 유형의 열로부터 검색된 추가 연락 정보 값을 제외하면 열 값이 특성으로 반환됩니다. 이러한 값은 요소로 반환됩니다.  
  
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
  
 다음 예에서는 FOR XML 처리 논리가 **xml** 유형 열의 XML 데이터에 있는 모든 XML 선언을 직렬화하지 않음을 보여 줍니다.  
  
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
  
-   단일 **xml** 유형 열이 포함된 테이블  
  
-   **xml** 유형의 인스턴스  
  
 예를 들어 다음 사용자 정의 함수는 **xml**유형의 단일 열이 포함된 테이블을 반환합니다.  
  
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
  
 사용자 정의 함수를 실행하고 함수로 반환된 테이블을 쿼리할 수 있습니다. 이 예에서 테이블 쿼리를 통해 반환된 XML은 **xml** 유형의 변수에 할당됩니다.  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 이 예는 사용자 정의 함수의 또 다른 예입니다. 이 사용자 정의 함수는 **xml** 유형의 인스턴스를 반환합니다. 이 예에서 사용자 정의 함수는 스키마 네임스페이스가 지정되어 있기 때문에 형식화된 XML 인스턴스를 반환합니다.  
  
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
  
 사용자 정의 함수로 반환된 XML은 다음과 같이 **xml** 유형의 변수에 할당될 수 있습니다.  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>참고 항목  
 [다양한 SQL Server 데이터 형식에 대한 FOR XML 지원](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
