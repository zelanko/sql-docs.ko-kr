---
title: CREATE XML SCHEMA COLLECTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE XML SCHEMA COLLECTION
- CREATE_XML_SCHEMA_COLLECTION_TSQL
- CREATE XML SCHEMA
- CREATE_XML_SCHEMA_TSQL
- COLLECTION
- COLLECTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML SCHEMA COLLECTION statement
- importing schema components
- schema collections [SQL Server], creating
- multiple schema namespaces
- XML schema collections [SQL Server], creating
ms.assetid: 350684e8-b3f6-4b58-9dbc-0f05cc776ebb
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c3389c617104ca45a39d151a908bff8701aad723
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38064291"
---
# <a name="create-xml-schema-collection-transact-sql"></a>CREATE XML SCHEMA COLLECTION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  스키마 구성 요소를 데이터베이스로 가져옵니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE XML SCHEMA COLLECTION [ <relational_schema>. ]sql_identifier AS Expression  
```  
  
## <a name="arguments"></a>인수  
 *relational_schema*  
 관계형 스키마 이름을 식별합니다. 지정하지 않으면 기본 관계형 스키마가 사용됩니다.  
  
 *sql_identifier*  
 XML 스키마 컬렉션의 SQL 식별자입니다.  
  
 *식*  
 문자열 상수 또는 스칼라 변수입니다. **varchar**, **varbinary**, **nvarchar** 또는 **xml** 유형입니다.  
  
## <a name="remarks"></a>Remarks  
 [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)을 사용하여 컬렉션에 있는 기존 네임스페이스에 새 구성 요소를 추가하거나 컬렉션에 새 네임스페이스를 추가할 수도 있습니다.  
  
 컬렉션을 제거하려면 [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)을 사용합니다.  
  
## <a name="permissions"></a>Permissions  
 XML SCHEMA COLLECTION을 만들려면 다음 사용 권한이 하나 이상 필요합니다.  
  
-   서버에 대한 CONTROL 권한  
  
-   서버에 대한 ALTER ANY DATABASE 권한  
  
-   데이터베이스에 대한 ALTER 권한  
  
-   데이터베이스의 CONTROL 권한  
  
-   데이터베이스의 ALTER ANY SCHEMA 권한 및 CREATE XML SCHEMA COLLECTION 권한  
  
-   관계형 스키마에 대한 ALTER 또는 CONTROL 권한 및 데이터베이스의 CREATE XML SCHEMA COLLECTION 권한  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-xml-schema-collection-in-the-database"></a>1. 데이터베이스에 XML 스키마 컬렉션 만들기  
 다음 예에서는 XML 스키마 컬렉션 `ManuInstructionsSchemaCollection`을 만듭니다. 이 컬렉션에는 스키마 네임스페이스가 하나만 있습니다.  
  
```  
-- Create a sample database in which to load the XML schema collection.  
CREATE DATABASE SampleDB;  
GO  
USE SampleDB;  
GO  
CREATE XML SCHEMA COLLECTION ManuInstructionsSchemaCollection AS  
N'<?xml version="1.0" encoding="UTF-16"?>  
<xsd:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   xmlns          ="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   elementFormDefault="qualified"   
   attributeFormDefault="unqualified"  
   xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
  
    <xsd:complexType name="StepType" mixed="true" >  
        <xsd:choice  minOccurs="0" maxOccurs="unbounded" >   
            <xsd:element name="tool" type="xsd:string" />  
            <xsd:element name="material" type="xsd:string" />  
            <xsd:element name="blueprint" type="xsd:string" />  
            <xsd:element name="specs" type="xsd:string" />  
            <xsd:element name="diag" type="xsd:string" />  
        </xsd:choice>   
    </xsd:complexType>  
  
    <xsd:element  name="root">  
        <xsd:complexType mixed="true">  
            <xsd:sequence>  
                <xsd:element name="Location" minOccurs="1" maxOccurs="unbounded">  
                    <xsd:complexType mixed="true">  
                        <xsd:sequence>  
                            <xsd:element name="step" type="StepType" minOccurs="1" maxOccurs="unbounded" />  
                        </xsd:sequence>  
                        <xsd:attribute name="LocationID" type="xsd:integer" use="required"/>  
                        <xsd:attribute name="SetupHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="MachineHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LaborHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LotSize" type="xsd:decimal" use="optional"/>  
                    </xsd:complexType>  
                </xsd:element>  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>' ;  
GO  
-- Verify - list of collections in the database.  
SELECT *  
FROM sys.xml_schema_collections;  
-- Verify - list of namespaces in the database.  
SELECT name  
FROM sys.xml_schema_namespaces;  
  
-- Use it. Create a typed xml variable. Note collection name specified.  
DECLARE @x xml (ManuInstructionsSchemaCollection);  
GO  
--Or create a typed xml column.  
CREATE TABLE T (  
        i int primary key,   
        x xml (ManuInstructionsSchemaCollection));  
GO  
-- Clean up  
DROP TABLE T;  
GO  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
Go  
USE master;  
GO  
DROP DATABASE SampleDB;  
```  
  
 또는 다음과 같이 변수에 스키마 컬렉션을 할당하고 `CREATE XML SCHEMA COLLECTION` 문에 변수를 지정할 수 있습니다.  
  
```  
DECLARE @MySchemaCollection nvarchar(max)  
Set @MySchemaCollection  = N' copy the schema collection here'  
CREATE XML SCHEMA COLLECTION MyCollection AS @MySchemaCollection   
```  
  
 이 예에서 변수는 `nvarchar(max)` 형식입니다. 변수는 **xml** 데이터 형식일 수도 있으며, 이 경우 문자열로 암시적으로 변환됩니다.  
  
 자세한 내용은 [저장된 XML 스키마 컬렉션 보기](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)를 참조하세요.  
  
 **xml** 형식 열에 스키마 컬렉션을 저장할 수 있습니다. 이 경우 XML 스키마 컬렉션을 만들려면 다음을 수행합니다.  
  
1.  SELECT 문을 사용하여 열에서 스키마 컬렉션을 검색하고 검색된 스키마 컬렉션을 **xml** 형식이나 **varchar** 형식의 변수에 할당합니다.  
  
2.  CREATE XML SCHEMA COLLECTION 문에 변수 이름을 지정합니다.  
  
 CREATE XML SCHEMA COLLECTION은 SQL Server에서 이해하는 스키마 구성 요소만 저장합니다. XML 스키마에 있는 모든 사항이 데이터베이스에 저장되는 것은 아닙니다. 따라서 XML 스키마 컬렉션을 제공된 방식과 똑같이 되돌리려면 XML 스키마를 데이터베이스 열 또는 컴퓨터의 다른 폴더에 저장하는 것이 좋습니다.  
  
### <a name="b-specifying-multiple-schema-namespaces-in-a-schema-collection"></a>2. 스키마 컬렉션에 여러 개의 스키마 네임스페이스 지정  
 XML 스키마 컬렉션을 만들 때 XML 스키마를 여러 개 지정할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS N'  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
<!-- Contents of schema here -->    
</xsd:schema>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
<!-- Contents of schema here -->  
</xsd:schema>';  
```  
  
 다음 예에서는 두 개의 XML 스키마 네임스페이스를 포함하는 XML 스키마 컬렉션 `ProductDescriptionSchemaCollection`을 만듭니다.  
  
```  
CREATE XML SCHEMA COLLECTION ProductDescriptionSchemaCollection AS   
'<xsd:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"  
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
    elementFormDefault="qualified"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
    <xsd:element name="Warranty"  >  
        <xsd:complexType>  
            <xsd:sequence>  
                <xsd:element name="WarrantyPeriod" type="xsd:string"  />  
                <xsd:element name="Description" type="xsd:string"  />  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>  
 <xs:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    elementFormDefault="qualified"   
    xmlns:mstns="http://tempuri.org/XMLSchema.xsd"   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" >  
    <xs:import   
namespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" />  
    <xs:element name="ProductDescription" type="ProductDescription" />  
        <xs:complexType name="ProductDescription">  
            <xs:sequence>  
                <xs:element name="Summary" type="Summary" minOccurs="0" />  
            </xs:sequence>  
            <xs:attribute name="ProductModelID" type="xs:string" />  
            <xs:attribute name="ProductModelName" type="xs:string" />  
        </xs:complexType>  
        <xs:complexType name="Summary" mixed="true" >  
            <xs:sequence>  
                <xs:any processContents="skip" namespace="http://www.w3.org/1999/xhtml" minOccurs="0" maxOccurs="unbounded" />  
            </xs:sequence>  
        </xs:complexType>  
</xs:schema>'  
;  
GO -- Clean up  
DROP XML SCHEMA COLLECTION ProductDescriptionSchemaCollection;  
GO  
```  
  
### <a name="c-importing-a-schema-that-does-not-specify-a-target-namespace"></a>3. 대상 네임스페이스를 지정하지 않는 스키마 가져오기  
 **targetNamespace** 특성이 포함되지 않은 스키마를 컬렉션으로 가져오는 경우 이 컬렉션의 구성 요소는 다음 예와 같이 빈 문자열 대상 네임스페이스와 연결됩니다. 컬렉션으로 가져온 하나 이상의 스키마를 연결하지 않으면 잠재적으로 관련되지 않은 여러 스키마 구성 요소가 기본 빈 문자열 네임스페이스와 연결됩니다.  
  
```  
-- Create a collection that contains a schema with no target namespace.  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  xmlns:ns="http://ns">  
<element name="e" type="dateTime"/>  
</schema>';  
go  
-- Query will return the names of all the collections that   
--contain a schema with no target namespace.  
SELECT sys.xml_schema_collections.name   
FROM   sys.xml_schema_collections   
JOIN   sys.xml_schema_namespaces   
ON     sys.xml_schema_collections.xml_collection_id =   
       sys.xml_schema_namespaces.xml_collection_id   
WHERE  sys.xml_schema_namespaces.name='';  
```  
  
### <a name="d-using-an-xml-schema-collection-and-batches"></a>4. XML 스키마 컬렉션 및 일괄 처리 사용  
 스키마 컬렉션은 해당 컬렉션이 생성된 것과 같은 일괄 처리에서 참조할 수 없습니다. 해당 컬렉션이 생성된 것과 같은 일괄 처리에서 컬렉션을 참조하려고 하면 컬렉션이 없다는 오류 메시지가 표시됩니다. 다음 예는 제대로 실행되지만 `GO`를 제거하고 XML 스키마 컬렉션을 참조하여 같은 일괄 처리에 `xml` 변수를 입력하려고 하면 오류가 반환됩니다.  
  
```  
CREATE XML SCHEMA COLLECTION mySC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="string"/>  
</schema>  
';  
GO  
CREATE TABLE T (Col1 xml (mySC));  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)   
 [DROP XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [DROP XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
