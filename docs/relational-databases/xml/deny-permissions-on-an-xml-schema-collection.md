---
title: "XML 스키마 컬렉션에 대한 사용 권한 거부 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: denying permissions [SQL Server], XML server collections
ms.assetid: e2b300b0-e734-4c43-a4da-c78e6e5d4fba
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15783b9d7a5e578e50aad8c351108fc949d90ad2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="deny-permissions-on-an-xml-schema-collection"></a>XML 스키마 컬렉션에 대한 사용 권한 거부
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 새 XML 스키마 컬렉션을 만들거나 기존 스키마 컬렉션을 사용할 권한을 거부할 수 있습니다.  
  
## <a name="denying-permission-to-create-an-xml-schema-collection"></a>XML 스키마 컬렉션을 만드는 권한 거부  
 다음과 같은 방법으로 XML 스키마 컬렉션을 만드는 권한을 거부할 수 있습니다.  
  
-   관계형 스키마에 대한 ALTER 권한을 거부합니다.  
  
-   관계형 스키마 및 포함된 모든 개체에 대한 모든 사용 권한을 거부하려면 관계형 스키마에 대한 CONTROL 권한을 거부합니다.  
  
-   데이터베이스에 대한 ALTER ANY SCHEMA를 거부합니다. 이 경우 보안 주체가 데이터베이스의 어떤 위치에도 XML 스키마 컬렉션을 만들 수 없습니다. 데이터베이스에 대한 ALTER 또는 CONTROL 권한을 거부하면 데이터베이스의 모든 개체에 대한 모든 사용 권한이 거부됩니다.  
  
## <a name="denying-permissions-on-an-xml-schema-collection-object"></a>XML 스키마 컬렉션 개체에 대한 사용 권한 거부  
 다음은 기존 XML 스키마 컬렉션 및 결과에 대해 거부할 수 있는 사용 권한입니다.  
  
-   ALTER 권한을 거부하면 XML 스키마 컬렉션의 내용을 수정하는 보안 주체의 권한이 거부됩니다.  
  
-   CONTROL 권한을 거부하면 XML 스키마 컬렉션에 대한 작업을 수행하는 보안 주체의 권한이 거부됩니다.  
  
-   REFERENCES 권한을 거부하면 XML 스키마 컬렉션을 사용하여 xml 유형 열 및 매개 변수를 입력하거나 제한하는 보안 주체의 권한이 거부됩니다. 또한 다른 XML 스키마 컬렉션에서 이 XML 스키마 컬렉션을 참조하는 보안 주체의 권한이 거부됩니다.  
  
-   VIEW DEFINITION 권한을 거부하면 XML 스키마 컬렉션의 내용을 보는 보안 주체의 권한이 거부됩니다.  
  
-   EXECUTE 권한을 거부하면 XML 스키마 컬렉션에 의해 입력되거나 제한되는 열, 변수 및 매개 변수에 값을 삽입하거나 업데이트하는 보안 주체의 권한이 거부됩니다. 또한 같은 xml 유형 열 및 변수의 값을 쿼리하는 보안 주체의 권한이 거부됩니다.  
  
## <a name="examples"></a>예  
 다음 예의 시나리오에서는 XML 스키마 권한의 작동 방식을 보여 줍니다. 각 예에서는 필요한 테스트 데이터베이스, 관계형 스키마 및 로그인을 만듭니다. 이러한 로그인에는 필요한 XML 스키마 컬렉션 권한이 부여됩니다. 각 예에서는 종료 시 필요한 정리를 수행합니다.  
  
### <a name="a-preventing-a-user-from-creating-an-xml-schema-collection"></a>1. 사용자가 XML 스키마 컬렉션을 만드는 것을 방지  
 사용자가 XML 스키마 컬렉션을 만들 수 없게 하는 방법 중 하나는 관계형 스키마에 대한 ALTER 권한을 거부하는 것입니다. 이는 다음 예에서 확인할 수 있습니다.  
  
 이 예에서는 `TestLogin1`이라는 사용자와 데이터베이스를 만듭니다. 또한 데이터베이스에 `dbo` 스키마 외에 관계형 스키마를 만듭니다. 처음에는 사용자가 `CREATE XML SCHEMA` 권한을 사용하여 데이터베이스의 모든 위치에 스키마 컬렉션을 만들 수 있습니다. 그런 다음 관계형 스키마 중 하나에 대한 사용자의 `ALTER` 권한을 거부합니다. 이렇게 하면 사용자가 해당 관계형 스키마에 XML 스키마 컬렉션을 만들 수 없습니다.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
GO  
-- Now deny permission from TestLogin1 to alter myOtherDBSchema.  
setuser  
GO  
DENY ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
GO  
-- Now TestLogin1 cannot create xml schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
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
  
### <a name="b-denying-permissions-on-an-xml-schema-collection"></a>2. XML 스키마 컬렉션에 대한 사용 권한 거부  
 다음 예에서는 로그인에 대해 기존 XML 스키마 컬렉션에 대한 특정 권한을 거부할 수 있는 방법을 보여 줍니다. 이 예에서 테스트 로그인은 기존 XML 스키마 컬렉션에 대한 REFERENCES 권한이 거부됩니다.  
  
 이 예에서는 `TestLogin1`이라는 사용자와 데이터베이스를 만듭니다. 또한 데이터베이스에 `dbo` 스키마 외에 관계형 스키마를 만듭니다. 처음에는 사용자가 `CREATE XML SCHEMA` 권한을 사용하여 데이터베이스의 모든 위치에 스키마 컬렉션을 만들 수 있습니다.  
  
 XML 스키마 컬렉션에 대한 `REFERENCES` 권한을 통해 `TestLogin1` 은 테이블에 `xml` 유형의 열을 만들 때 스키마를 사용할 수 있습니다. XML 스키마 컬렉션에 대한 `REFERENCES` 권한이 거부되면 `TestLogin1` 은 XML 스키마 컬렉션을 사용할 수 없습니다.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, the following  
-- permission is required.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant permission to TestLogin1 to create a table and reference the XML schema collection.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also needs REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on the schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection   
TO TestLogin1  
GO  
  
--TestLogin1 can use the schema.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
-- Drop the table.  
DROP TABLE T  
GO  
-- Now deny REFERENCES permission to TestLogin1 on the schema created previously.  
SETUSER  
GO  
DENY REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection TO TestLogin1  
  
GO  
-- Now TestLogin1 cannot create xml schema collection  
SETUSER 'TestLogin1'  
GO  
-- Following statement fails. TestLogin1 does not have REFERENCES   
-- permission on the XML schema collection.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
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
  
## <a name="see-also"></a>참고 항목  
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 스키마 컬렉션&#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)   
 [DENY 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
