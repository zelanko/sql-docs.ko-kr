---
title: XML 스키마 컬렉션에 대한 사용 권한 부여 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- granting permissions [SQL Server], XML schema collections
- ALTER permission
ms.assetid: ffbb829c-3b8f-4e5d-97d9-ab4059aab0db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e009f0fe22156f9a652dd19fceddf02bbc48c247
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530185"
---
# <a name="grant-permissions-on-an-xml-schema-collection"></a>XML 스키마 컬렉션에 대한 사용 권한 부여
  XML 스키마 컬렉션을 만들 권한 및 XML 스키마 컬렉션 개체에 대한 권한을 부여할 수 있습니다.  
  
## <a name="granting-permission-to-create-an-xml-schema-collection"></a>XML 스키마 컬렉션을 만들 권한 부여  
 XML 스키마 컬렉션을 만들려면 다음 권한이 필요합니다.  
  
-   보안 주체는 데이터베이스 수준에서 CREATE XML SCHEMA COLLECTION 권한이 필요합니다.  
  
-   XML 스키마 컬렉션이 관계형 스키마 범위이므로 보안 주체는 관계형 스키마에 대한 ALTER 권한도 필요합니다.  
  
 다음 권한을 사용하여 보안 주체는 서버의 데이터베이스에서 관계형 스키마에 XML 스키마 컬렉션을 만들 수 있습니다.  
  
-   서버에 대한 CONTROL 권한  
  
-   서버에 대한 ALTER ANY DATABASE 권한  
  
-   데이터베이스에 대한 ALTER 권한  
  
-   데이터베이스의 CONTROL 권한  
  
-   데이터베이스의 ALTER ANY SCHEMA 권한 및 CREATE XML SCHEMA COLLECTION 권한  
  
-   관계형 스키마에 대한 ALTER 또는 CONTROL 권한 및 데이터베이스의 CREATE XML SCHEMA COLLECTION 권한  
  
 권한의 마지막 메서드는 다음 예에서 사용됩니다.  
  
 관계형 스키마의 소유자는 해당 스키마에 만들어진 XML 스키마 컬렉션의 소유자가 됩니다. 이 소유자에게는 XML 스키마 컬렉션에 대한 모든 권한이 있습니다. 따라서 이 소유자는 XML 스키마 컬렉션을 수정하거나 xml 열을 형식화하거나 XML 스키마 컬렉션을 삭제할 수 있습니다.  
  
## <a name="granting-permissions-on-an-xml-schema-collection-object"></a>XML 스키마 컬렉션 개체에 대한 권한 부여  
 XML 스키마 컬렉션에는 다음 권한이 허용됩니다.  
  
-   ALTER XML SCHEMA COLLECTION 문을 사용하여 기존 XML 스키마 컬렉션의 내용을 수정할 때는 ALTER 권한이 필요합니다.  
  
-   CONTROL 권한을 사용하면 사용자는 XML 스키마 컬렉션에서 모든 작업을 수행할 수 있습니다.  
  
-   한 보안 주체에서 다른 보안 주체로 XML 스키마 컬렉션의 소유권을 이전하는 데는 TAKE OWNERSHIP 권한이 필요합니다.  
  
-   REFERENCES 권한은 보안 주체가 테이블, 뷰 및 매개 변수에서 XML 스키마 컬렉션을 사용하여 `xml` 유형 열을 형식화하거나 제약하도록 권한을 부여합니다. REFERENCES 권한은 하나의 XML 스키마 컬렉션이 다른 컬렉션을 참조할 때도 필요합니다.  
  
-   보안 주체가 컬렉션에 대해 ALTER, REFERENCES 또는 CONTROL 권한 중 하나를 가진 경우 VIEW DEFINITION 권한을 사용하면 보안 주체가 XML_SCHEMA_NAMESPACE 또는 카탈로그 뷰를 통해 XML 스키마 컬렉션의 내용을 쿼리할 수 있습니다.  
  
-   `xml` 유형 열, 변수 및 매개 변수를 형식화하거나 제약하는 XML 스키마 컬렉션에 대해 보안 주체가 삽입하거나 업데이트한 값의 유효성을 검사하려면 EXECUTE 권한이 필요합니다. 이 권한은 이러한 열 및 변수에 저장된 XML을 쿼리할 때도 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예의 시나리오에서는 XML 스키마 권한의 작동 방식을 보여 줍니다. 각 예에서는 필요한 테스트 데이터베이스, 관계형 스키마 및 로그인을 만듭니다. 이러한 로그인에는 필요한 XML 스키마 컬렉션 권한이 부여됩니다. 각 예에서는 종료 시 필요한 정리를 수행합니다.  
  
### <a name="a-granting-permissions-to-create-an-xml-schema-collection"></a>1. XML 스키마 컬렉션을 만들 권한 부여  
 다음 예에서는 보안 주체가 XML 스키마 컬렉션을 만들 수 있도록 권한을 부여하는 방법을 보여 줍니다. 이 예에서는 `TestLogin1`이라는 테스트 사용자와 예제 데이터베이스를 만듭니다. `TestLogin1` 은 관계형 스키마에 대해 `ALTER` 권한을 부여받고 데이터베이스에 대해 `CREATE XML SCHEMA COLLECTION` 권한을 부여받습니다. 이러한 권한을 통해 `TestLogin1` 은 예제 XML 스키마 컬렉션을 성공적으로 만듭니다.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Execute CREATE XML SCHEMA COLLECTION.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="root" type="xsd:byte"/>  
</xsd:schema>'  
GO  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="b-granting-permission-to-use-an-existing-xml-schema-collection"></a>2. 기존 XML 스키마 컬렉션을 사용할 권한 부여  
 다음 예에서는 XML 스키마 컬렉션에 대한 권한 모델을 보여 줍니다. XML 스키마 컬렉션을 만들고 사용하는 데 다른 권한이 필요한지 설명합니다.  
  
 이 예에서는 테스트 데이터베이스와 `TestLogin1`이라는 로그인을 만듭니다. `TestLogin1` 은 데이터베이스에 XML 스키마 컬렉션을 만듭니다. 이 로그인은 테이블을 만들고 XML 스키마 컬렉션을 사용하여 형식화된 xml 열을 만듭니다. 그런 다음 데이터를 삽입하고 쿼리합니다. 이러한 모든 단계에는 코드에 표시된 대로 필요한 스키마 권한이 있어야 합니다.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Create a table by using the collection to type an XML column.   
--TestLogin1 must have permission to create a table.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also must have REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- Now user can create a table and use the XML schema collection to create   
-- a typed XML column.  
SETUSER 'TestLogin1'  
GO  
CREATE TABLE MyTestTable (xmlCol xml (dbo.myTestSchemaCollection))  
GO  
-- To insert data in the table, the user needs EXECUTE permission on the XML schema collection.  
-- GRANT EXECUTE permission to TestLogin2 on the xml schema collection.  
SETUSER  
GO  
GRANT EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection   
TO TestLogin1  
GO  
-- TestLogin1 does not own the dbo schema. This user must have INSERT permission.  
GRANT INSERT TO TestLogin1  
GO  
-- Now the user can insert data into the table.  
SETUSER 'TestLogin1'  
GO  
INSERT INTO MyTestTable VALUES('  
<telephone xmlns="http://schemas.adventure-works.com/Additional/ContactInfo">111-1111</telephone>  
')  
GO  
-- To query the table, TestLogin1 must have permissions: SELECT on the table and EXECUTE on the XML schema collection.  
SETUSER  
GO  
GRANT SELECT TO TestLogin1  
GO  
-- TestLogin1 already has EXECUTE permission on the schema (granted before inserting a record in the table).  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- To show that the user must have EXECUTE permission to query, revoke the  
-- previously granted permission and return the query.  
SETUSER  
GO  
REVOKE EXECUTE ON XML SCHEMA COLLECTION::myTestSchemaCollection to TestLogin1  
Go  
-- Now TestLogin1 cannot execute the query.  
SETUSER 'TestLogin1'  
GO  
SELECT xmlCol.query('declare default element namespace "http://schemas.adventure-works.com/Additional/ContactInfo" /telephone[1]')  
FROM MyTestTable  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="c-granting-alter-permission-on-an-xml-schema-collection"></a>3. XML 스키마 컬렉션에 대한 ALTER 권한 부여  
 사용자가 데이터베이스에서 기존 XML 스키마 컬렉션을 수정하려면 ALTER 권한이 있어야 합니다. 다음 예에서는 `ALTER` 권한을 부여하는 방법을 보여 줍니다.  
  
```  
SETUSER  
GO  
USE master  
GO  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
CREATE USER TestLogin1  
GO  
-- Grant permission to the user.  
SETUSER  
GO  
-- User must have ALTER permission on the relational schema in the database.  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- User also must have permission to create XML schema collections in the database.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
-- Now user can execute the previous CREATE XML SCHEMA COLLECTION statement.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
  <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"    
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant ALTER permission to TestLogin1.  
setuser  
GO  
GRANT ALTER ON XML SCHEMA COLLECTION::myTestSchemaCollection TO TestLogin1  
GO  
-- TestLogin1 should be able to add components to the collection.  
SETUSER 'TestLogin1'  
GO  
ALTER XML SCHEMA COLLECTION myTestSchemaCollection ADD '  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns="http://schemas.adventure-works.com/Additional/ContactInfo"   
elementFormDefault="qualified">  
 <xsd:element name="pager" type="xsd:string"/>  
</xsd:schema>  
'  
Go  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="d-granting-take-ownership-permission-on-an-xml-schema-collection"></a>4. XML 스키마 컬렉션에 대한 TAKE OWNERSHIP 권한 부여  
 다음 예에서는 XML 스키마 소유권을 한 사용자에서 다른 사용자로 이전하는 방법을 보여 줍니다. 보다 유용한 예로 만들기 위해 사용자는 서로 다른 기본 관계형 스키마에서 작업을 수행합니다.  
  
 이 예에서는 다음을 수행합니다.  
  
-   `dbo` 및 `myOtherDBSchema`라는 두 개의 관계형 스키마로 데이터베이스를 만듭니다.  
  
-   `TestLogin1` 및 `TestLogin2`의 두 사용자를 만듭니다. `TestLogin2` 는 `myOtherDBSchema` 관계형 스키마의 소유자가 됩니다.  
  
-   `TestLogin1` 은 `dbo` 관계형 스키마에 XML 스키마 컬렉션을 만듭니다.  
  
-   `TestLogin1` 이 그런 다음 XML 스키마 컬렉션에 대한 `TAKE OWNERSHIP` 권한을 `TestLogin2`에게 부여합니다.  
  
-   `TestLogin2` 는 XML 스키마 컬렉션의 관계형 스키마를 변경하지 않고 `myOtherDBSchema`에서 XML 스키마 컬렉션의 소유자가 됩니다.  
  
```  
CREATE LOGIN TestLogin1 with password='SQLSvrPwd1'  
GO  
CREATE LOGIN TestLogin2 with password='SQLSvrPwd2'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
-- Create users in the database. Note TestLogin2's default schema is  
-- myOtherDBSchema.  
CREATE USER TestLogin1  
GO  
CREATE USER TestLogin2 WITH DEFAULT_SCHEMA=myOtherDBSchema  
GO  
-- TestLogin2 will own myOtherDBSchema relational schema.  
ALTER AUTHORIZATION ON SCHEMA::myOtherDBSchema TO TestLogin2  
GO  
  
-- For TestLogin1 to create XML schema collection, the following  
-- permission is required.  
GRANT CREATE XML SCHEMA COLLECTION   
TO TestLogin1  
GO  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
GO  
-- Now TestLogin1 can create an XML schema collection.  
setuser 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
  
<xsd:element name="AdditionalContactInfo" >  
 <xsd:complexType mixed="true" >  
    <xsd:sequence>  
      <xsd:any processContents="strict"   
               namespace="http://schemas.adventure-works.com/Contact/Record   
                          http://schemas.adventure-works.com/AdditionalContactTypes"  
               minOccurs="0" maxOccurs="unbounded" />  
    </xsd:sequence>  
 </xsd:complexType>  
</xsd:element>  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
  
-- Grant TAKE OWNERSHIP to TestLogin2.  
SETUSER  
GO  
GRANT TAKE OWNERSHIP ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Verify the owner. Note the UserName and Principal_id is null.   
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections   
      JOIN sys.schemas   
      ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- TestLogin2 can take ownership now.  
setuser 'TestLogin2'  
GO  
ALTER AUTHORIZATION ON XML SCHEMA COLLECTION::dbo.myTestSchemaCollection   
TO TestLogin2  
GO  
-- Note that although TestLogin2 is the owner,the XML schema collection   
-- is still in dbo.  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
      sys.schemas.name as RelSchemaName,*   
FROM sys.xml_schema_collections JOIN sys.schemas   
     ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
  
-- TestLogin2 moves the collection from dbo to myOtherDBSchema relational schema.  
-- TestLogin2 already has all necessary permissions.  
-- 1) TestLogin2 owns the destination relational schema so he can alter it.  
-- 2) TestLogin2 owns the XML schema collection (therefore, has CONTROL permission).  
ALTER SCHEMA myOtherDBSchema  
TRANSFER XML SCHEMA COLLECTION::dbo.myTestSchemaCollection  
GO  
  
SELECT user_name(sys.xml_schema_collections.principal_id) as UserName,   
       sys.schemas.name as RelSchemaName,*   
FROM   sys.xml_schema_collections JOIN sys.schemas   
       ON sys.schemas.schema_id=sys.xml_schema_collections.schema_id  
GO  
-- Final cleanup   
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
DROP LOGIN TestLogin2  
go   
```  
  
### <a name="e-granting-view-definition-permission-on-an-xml-schema-collection"></a>5. XML 스키마 컬렉션에 대한 VIEW DEFINITION 권한 부여  
 다음 예에서는 XML 스키마 컬렉션에 대한 VIEW DEFINITION 권한을 부여하는 방법을 보여 줍니다.  
  
```  
SETUSER  
GO  
USE master  
GO  
IF EXISTS( SELECT * FROM sysdatabases WHERE name='permissionsDB' )  
   DROP DATABASE permissionsDB  
GO  
IF EXISTS( SELECT * FROM sys.sql_logins WHERE name='schemaUser' )  
   DROP LOGIN schemaUser  
GO  
CREATE DATABASE permissionsDB  
GO  
CREATE LOGIN schemaUser WITH PASSWORD='Pass#123',DEFAULT_DATABASE=permissionsDB  
GO  
GRANT CONNECT SQL TO schemaUser  
GO  
USE permissionsDB  
GO  
CREATE USER schemaUser WITH DEFAULT_SCHEMA=dbo  
GO  
CREATE XML SCHEMA COLLECTION MySC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns"  
xmlns:ns="http://ns">  
  
   <simpleType name="ListOfIntegers">  
      <list itemType="integer"/>  
   </simpleType>  
  
   <element name="root" type="ns:ListOfIntegers"/>  
  
   <element name="gRoot" type="gMonth"/>  
  
</schema>  
'  
GO  
-- schemaUser cannot see the contents of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
  
-- Grant schemaUser VIEW DEFINITION and REFERENCES permissions  
-- on the XML schema collection.  
SETUSER  
GO  
GRANT VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
GRANT REFERENCES ON XML SCHEMA COLLECTION::dbo.MySC TO schemaUser  
GO  
-- Now schemaUser can see the content of the collection.  
SETUSER 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
-- Revoke schemaUser VIEW DEFINITION permissions  
-- on the XML schema collection.  
SETUSER  
GO  
REVOKE VIEW DEFINITION ON XML SCHEMA COLLECTION::dbo.MySC FROM schemaUser  
GO  
-- Now schemaUser cannot see the contents of   
-- the collection.  
setuser 'schemaUser'  
GO  
SELECT XML_SCHEMA_NAMESPACE(N'dbo',N'MySC')  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터&#40;SQL Server&#41;](xml-data-sql-server.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](compare-typed-xml-to-untyped-xml.md)   
 [XML 스키마 컬렉션&#40;SQL Server&#41;](xml-schema-collections-sql-server.md)   
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
