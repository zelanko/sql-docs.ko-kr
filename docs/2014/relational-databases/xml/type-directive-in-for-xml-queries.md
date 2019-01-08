---
title: FOR XML 쿼리의 TYPE 지시어 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bafe35efbcc1f5dae7cea0775464deac3c8ed7f8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351082"
---
# <a name="type-directive-in-for-xml-queries"></a>FOR XML 쿼리의 TYPE 지시어
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대 한 지원 합니다 [xml &#40;TRANSACT-SQL&#41; ](/sql/t-sql/xml/xml-transact-sql) 선택적으로 FOR XML 쿼리 결과가 반환 되도록 요청할 수 있습니다 `xml` TYPE 지시어를 지정 하 여 데이터 형식입니다. 그러면 서버에서 FOR XML 쿼리 결과를 처리할 수 있습니다. 에 대해 XQuery를 지정 결과를 할당을 예는 `xml` 변수를 입력 하거나 작성 [중첩 FOR XML 쿼리](use-nested-for-xml-queries.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 TYPE 지시어를 사용하거나 `xml` 데이터 형식을 사용하여 SQL 테이블 열과 출력 매개 변수에서 XML 인스턴스 데이터 값을 반환하는 FOR XML 쿼리와 같은 여러 서버 구문의 결과로 XML 데이터 형식 인스턴스 데이터를 클라이언트에 반환합니다. 클라이언트 애플리케이션 코드에서 ADO.NET 공급자가 이 XML 데이터 형식 정보를 서버에서 이진 인코딩으로 보내도록 요청합니다. 그러나 TYPE 지시어 없이 FOR XML을 사용하면 XML 데이터가 문자열 유형으로 반환됩니다. 클라이언트 공급자는 항상 두 XML 유형 중 하나를 처리할 수 있습니다. TYPE 지시어가 없는 최상위 FOR XML은 커서와 함께 사용할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 TYPE 지시어를 FOR XML 쿼리와 함께 사용하는 방법을 보여 줍니다.  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>FOR XML 쿼리 결과를 xml 유형으로 검색  
 다음 쿼리에서는 `Contacts` 테이블에서 고객 연락처 정보를 검색합니다. `TYPE`에 `FOR XML` 지시어가 지정되어 있으므로 결과는 `xml` 유형으로 반환됩니다.  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 다음은 결과의 일부입니다.  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>xml 유형 변수에 FOR XML 쿼리 결과 할당  
 다음 예에서는 FOR XML 결과가 `xml` 유형 변수 `@x`에 할당됩니다. 와 같은 연락처 정보를 검색 하는 쿼리를 `BusinessEntityID`, `FirstName`를 `LastName`, 및 추가에서 전화 번호와는 `AdditionalContactInfo` 열의 `xml``TYPE`합니다. `FOR XML` 절은 `TYPE` 지시어를 지정하므로 XML은 `xml` 유형으로 반환되며 변수에 할당됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>FOR XML 쿼리 결과 쿼리  
 FOR XML 쿼리가 XML을 반환하므로 FOR XML 쿼리에서 반환한 XML 결과에 `xml`, `query()` 등의 `value()` 유형 메서드를 적용할 수 있습니다.  
  
 다음 쿼리에서는 `xml` 데이터 형식의 `query()` 메서드를 사용하여 `FOR XML` 쿼리 결과를 쿼리합니다. 자세한 내용은 [query&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](/sql/t-sql/xml/query-method-xml-data-type)를 참조하세요.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 내부 `SELECT ... FOR XML` 쿼리는 외부 `SELECT`가 `query()` 메서드를 `xml` 유형에 적용하는 `xml` 유형 결과를 반환합니다. 지정된 `TYPE` 지시어에 유의하십시오.  
  
 다음은 결과입니다.  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 다음 쿼리에서는 `xml` 데이터 형식의 `value()` 메서드를 사용하여 `SELECT...FOR XML` 쿼리가 반환한 XML 결과에서 값을 검색합니다. 자세한 내용은 [value&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](/sql/t-sql/xml/value-method-xml-data-type)를 참조하세요.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 `value()` 메서드의 XQuery 경로 식이 `BusinessEntityID` 가 `1`인 고객 연락처의 첫 번째 전화 번호를 검색합니다.  
  
> [!NOTE]  
>  TYPE 지시어를 지정하지 않으면 FOR XML 쿼리 결과가 `nvarchar(max)` 형식으로 반환됩니다.  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>INSERT, UPDATE 및 DELETE(Transact-SQL DML)에 FOR XML 쿼리 결과 사용  
 다음 예에서는 DML(데이터 조작 언어) 문에 FOR XML 쿼리를 사용할 수 있는 방법을 보여 줍니다. 예에서 `FOR XML`은 `xml` 유형의 인스턴스를 반환합니다. `INSERT` 문은 이 XML을 테이블에 삽입합니다.  
  
```  
CREATE TABLE T1(intCol int, XmlCol xml);  
GO  
INSERT INTO T1   
VALUES(1, '<Root><ProductDescription ProductModelID="1" /></Root>');  
GO  
  
CREATE TABLE T2(XmlCol xml)  
GO  
INSERT INTO T2(XmlCol)   
SELECT (SELECT XmlCol.query('/Root')   
        FROM T1   
        FOR XML AUTO,TYPE);   
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML&#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
