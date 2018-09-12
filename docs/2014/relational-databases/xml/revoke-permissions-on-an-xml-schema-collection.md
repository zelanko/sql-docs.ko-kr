---
title: XML 스키마 컬렉션에 대한 사용 권한 취소 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- revoking permissions [SQL Server]
ms.assetid: 4e542b70-2d56-4a65-8a39-96a1ed477ca6
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3c5cadf833a479b5a6678dd8c8aa03e8d54150e
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890219"
---
# <a name="revoke-permissions-on-an-xml-schema-collection"></a>XML 스키마 컬렉션에 대한 사용 권한 취소
  XML 스키마 컬렉션을 만드는 권한은 다음 중 하나를 사용하여 취소할 수 있습니다.  
  
-   관계형 스키마에 대한 ALTER 권한을 취소합니다. 그러면 보안 주체가 관계형 스키마에서 XML 스키마 컬렉션을 만들 수 없습니다. 하지만 보안 주체는 동일 데이터베이스의 다른 관계형 스키마에서 여전히 같은 작업을 수행할 수 있습니다.  
  
-   데이터베이스에서 보안 주체에 대한 ALTER ANY SCHEMA 권한을 취소합니다. 그러면 보안 주체가 데이터베이스의 어느 곳에서도 XML 스키마 컬렉션을 만들 수 없습니다.  
  
-   데이터베이스에서 보안 주체에 대한 CREATE XML SCHEMA COLLECTION 또는 ALTER XML SCHEMA COLLECTION 권한을 취소합니다. 그러면 보안 주체가 데이터베이스 내에서 XML 스키마 컬렉션을 가져올 수 없습니다. 데이터베이스에서 ALTER 또는 CONTROL 권한을 취소해도 같은 효과가 있습니다.  
  
## <a name="revoking-permissions-on-an-existing-xml-schema-collection-object"></a>기존 XML 스키마 컬렉션 개체에 대한 사용 권한 취소  
 다음은 XML 스키마 컬렉션 및 결과에서 취소할 수 있는 권한입니다.  
  
-   ALTER 권한을 취소하면 보안 주체의 XML 스키마 컬렉션 콘텐츠 수정 기능이 취소됩니다.  
  
-   TAKE OWNERSHIP 권한을 취소하면 보안 주체의 XML 스키마 컬렉션 소유권 전달 기능이 취소됩니다.  
  
-   REFERENCES 권한을 취소하면 XML 스키마 컬렉션을 사용하여 테이블 및 뷰에 있는 xml 유형의 열 및 매개 변수를 형식화하거나 제한하는 보안 주체의 기능이 취소됩니다. 또한 다른 XML 스키마 컬렉션에서 이 스키마 컬렉션을 참조하는 권한이 취소됩니다.  
  
-   VIEW DEFINITION 권한을 취소하면 보안 주체의 XML 스키마 컬렉션의 콘텐츠를 보는 기능이 취소됩니다.  
  
-   EXECUTE 권한을 취소하면 XML 컬렉션에 의해 형식화되었거나 제한된 변수, 매개 변수 및 열에 있는 값을 삽입 또는 업데이트하는 보안 주체의 기능이 취소됩니다. 또한 이러한 **xml** 유형의 열, 변수 또는 매개 변수를 쿼리하는 기능이 취소됩니다.  
  
## <a name="examples"></a>예  
 다음 예의 시나리오에서는 XML 스키마 권한의 작동 방식을 보여 줍니다. 각 예에서는 필요한 테스트 데이터베이스, 관계형 스키마 및 로그인을 만듭니다. 이러한 로그인에는 필요한 XML 스키마 컬렉션 권한이 부여됩니다. 각 예에서는 종료 시 필요한 정리를 수행합니다.  
  
### <a name="a-revoking-permissions-to-create-an-xml-schema-collection"></a>1. XML 스키마 컬렉션을 만드는 권한 취소  
 이 예에서는 로그인 계정과 예제 데이터베이스를 만듭니다. 또한 데이터베이스에 관계형 스키마를 추가합니다. 초기에 로그인 계정에는 관계형 스키마에 대한 ALTER 권한과 XML 스키마 컬렉션을 만들기 위한 다른 필수 권한이 부여됩니다. 이 예에서는 데이터베이스에 있는 관계형 스키마 중 하나에 대한 ALTER 권한을 취소합니다. 이렇게 하면 로그인 계정이 XML 스키마 컬렉션을 만들 수 없습니다.  
  
```  
setuser  
go  
create login TestLogin1 with password='SQLSvrPwd1'  
go  
create database SampleDBForSchemaPermissions  
go  
use SampleDBForSchemaPermissions  
go  
-- Create another relational schema in the db (in addition to dbo schema)  
CREATE SCHEMA myOtherDBSchema  
go  
CREATE USER TestLogin1  
go  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed  
-- CREATE XML SCHEMA is a database level permission  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
go  
-- Now TestLogin1 can import an XML schema collection in both relational schemas.  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- TestLogin1 can create XML schema collection in myOtherDBSchema relational schema  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- Let us drop XML schema collections from both relational schemas  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
go  
DROP XML SCHEMA COLLECTION dbo.myTestSchemaCollection  
go  
-- now REVOKE permission from TestLogin1 to alter myOtherDBSchema  
setuser  
go  
REVOKE ALTER ON SCHEMA::myOtherDBSchema FROM TestLogin1  
go  
-- now TestLogin1 cannot create xml schema collection in myOtherDBSchema  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- TestLogin1 can still create XML schema collections in dbo  
-- It cannot create XML schema collections anywhere in the database  
-- if we REVOKE CREATE XML SCHEMA COLLECTION permission  
SETUSER  
go  
REVOKE CREATE XML SCHEMA COLLECTION FROM TestLogin1  
go  
  
setuser 'TestLogin1'  
go  
-- the following now should fail  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- Final cleanup  
SETUSER  
go  
USE master  
go  
DROP DATABASE SampleDBForSchemaPermissions  
go  
DROP LOGIN TestLogin1  
Go  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터&#40;SQL Server&#41;](xml-data-sql-server.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](compare-typed-xml-to-untyped-xml.md)   
 [XML 스키마 컬렉션&#40;SQL Server&#41;](xml-schema-collections-sql-server.md)   
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
