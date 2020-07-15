---
title: ALTER XML SCHEMA COLLECTION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_XML_SCHEMA_COLLECTION_TSQL
- ALTER XML SCHEMA COLLECTION
dev_langs:
- TSQL
helpviewer_keywords:
- schema collections [SQL Server], altering
- xml_schema_namespace function
- adding schema components
- ALTER XML SCHEMA COLLECTION statement
- XML schemas [SQL Server], adding
- XML schema collections [SQL Server], modifying
- schema collections [SQL Server], adding components
- XML schema collections [SQL Server], adding components
- importing schemas
- XML schema collections [SQL Server], altering
- schema collections [SQL Server], modifying
- multiple schema namespaces
ms.assetid: e311c425-742a-4b0d-b847-8b974bf66d53
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 832b8a0c0d66a1e9754366e7735ebbac84b3ac7b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895556"
---
# <a name="alter-xml-schema-collection-transact-sql"></a>ALTER XML SCHEMA COLLECTION(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  기존 XML 스키마 컬렉션에 새 스키마 구성 요소를 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER XML SCHEMA COLLECTION [ relational_schema. ]sql_identifier ADD 'Schema Component'  
```  
  
## <a name="arguments"></a>인수  
 *relational_schema*  
 관계형 스키마 이름을 식별합니다. 지정하지 않으면 기본 관계형 스키마가 사용됩니다.  
  
 *sql_identifier*  
 XML 스키마 컬렉션의 SQL 식별자입니다.  
  
 **‘** 스키마 구성 요소 **’**   
 삽입할 스키마 구성 요소입니다.  
  
## <a name="remarks"></a>설명  
 ALTER XML SCHEMA COLLECTION을 사용하여 XML 스키마 컬렉션에 네임스페이스가 없는 새 XML 스키마를 추가하거나 컬렉션의 기존 네임스페이스에 새 구성 요소를 추가할 수 있습니다.  
  
 다음 예에서는 `MyColl` 컬렉션에 있는 `https://MySchema/test_xml_schema` 기존 네임스페이스에 새 \<element>를 추가합니다.  
  
```  
-- First create an XML schema collection.  
CREATE XML SCHEMA COLLECTION MyColl AS '  
   <schema   
    xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="https://MySchema/test_xml_schema">  
      <element name="root" type="string"/>   
  </schema>'  
-- Modify the collection.   
ALTER XML SCHEMA COLLECTION MyColl ADD '  
  <schema xmlns="http://www.w3.org/2001/XMLSchema"   
         targetNamespace="https://MySchema/test_xml_schema">   
     <element name="anotherElement" type="byte"/>   
 </schema>';  
```  
  
 `ALTER XML SCHEMA`는 `<anotherElement>` 요소를 이전에 정의한 네임스페이스인 `https://MySchema/test_xml_schema`에 추가합니다.  
  
 컬렉션에 추가하려는 구성 요소 중 일부가 이미 동일한 컬렉션에 있는 구성 요소를 참조하는 경우에는 `<import namespace="referenced_component_namespace" />`를 사용해야 합니다. 그러나 `<xsd:import>`의 현재 스키마 네임스페이스는 사용할 수 없으므로 현재 스키마 네임스페이스와 동일한 대상 네임스페이스의 구성 요소를 자동으로 가져옵니다.  
  
 컬렉션을 제거하려면 [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)을 사용합니다.  
  
 스키마 컬렉션에 이미 lax 유효성 검사 와일드카드 또는 **xs:anyType** 형식의 요소가 포함되어 있는 경우 새 전역 요소, 형식 또는 특성 선언을 스키마 컬렉션에 추가하면 해당 스키마 컬렉션의 제한을 받는 모든 저장된 데이터에 대해 유효성 재검사가 수행됩니다.  
  
## <a name="permissions"></a>사용 권한  
 XML SCHEMA COLLECTION을 변경하려면 해당 컬렉션에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-xml-schema-collection-in-the-database"></a>A. 데이터베이스에 XML 스키마 컬렉션 만들기  
 다음 예에서는 XML 스키마 컬렉션 `ManuInstructionsSchemaCollection`을 만듭니다. 이 컬렉션에는 스키마 네임스페이스가 하나만 있습니다.  
  
```  
-- Create a sample database in which to load the XML schema collection.  
CREATE DATABASE SampleDB;  
GO  
USE SampleDB;  
GO  
CREATE XML SCHEMA COLLECTION ManuInstructionsSchemaCollection AS  
N'<?xml version="1.0" encoding="UTF-16"?>  
<xsd:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   xmlns          ="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
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
  
-- Use it. Create a typed xml variable. Note the collection name   
-- that is specified.  
DECLARE @x xml (ManuInstructionsSchemaCollection);  
GO  
--Or create a typed xml column.  
CREATE TABLE T (  
        i int primary key,   
        x xml (ManuInstructionsSchemaCollection));  
GO  
-- Clean up.  
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
DECLARE @MySchemaCollection nvarchar(max);  
SET @MySchemaCollection  = N' copy the schema collection here';  
CREATE XML SCHEMA COLLECTION AS @MySchemaCollection;   
```  
  
 이 예에서 변수는 `nvarchar(max)` 형식입니다. 변수는 **xml** 데이터 형식일 수도 있으며, 이 경우 문자열로 암시적으로 변환됩니다.  
  
 자세한 내용은 [저장된 XML 스키마 컬렉션 보기](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)를 참조하세요.  
  
 **xml** 유형 열에 스키마 컬렉션을 저장할 수 있습니다. 이 경우 XML 스키마 컬렉션을 만들려면 다음 단계를 수행합니다.  
  
1.  SELECT 문을 사용하여 열에서 스키마 컬렉션을 검색하고 검색된 스키마 컬렉션을 **xml** 형식이나 **varchar** 형식의 변수에 할당합니다.  
  
2.  CREATE XML SCHEMA COLLECTION 문에 변수 이름을 지정합니다.  
  
 CREATE XML SCHEMA COLLECTION은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인식되는 스키마 구성 요소만 저장합니다. XML 스키마의 모든 내용이 데이터베이스에 저장되지는 않습니다. 따라서 XML 스키마 컬렉션을 제공된 방식과 똑같이 되돌리려면 XML 스키마를 데이터베이스 열 또는 컴퓨터의 다른 폴더에 저장하는 것이 좋습니다.  
  
### <a name="b-specifying-multiple-schema-namespaces-in-a-schema-collection"></a>B. 스키마 컬렉션에 여러 개의 스키마 네임스페이스 지정  
 XML 스키마 컬렉션을 만들 때 XML 스키마를 여러 개 지정할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
CREATE XML SCHEMA COLLECTION N'  
<xsd:schema>....</xsd:schema>  
<xsd:schema>...</xsd:schema>';  
```  
  
 다음 예에서는 두 개의 XML 스키마 네임스페이스를 포함하는 XML 스키마 컬렉션 `ProductDescriptionSchemaCollection`을 만듭니다.  
  
```  
CREATE XML SCHEMA COLLECTION ProductDescriptionSchemaCollection AS   
'<xsd:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"  
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
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
 <xs:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    elementFormDefault="qualified"   
    xmlns:mstns="https://tempuri.org/XMLSchema.xsd"   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" >  
    <xs:import   
namespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" />  
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
GO   
-- Clean up  
DROP XML SCHEMA COLLECTION ProductDescriptionSchemaCollection;  
GO  
```  
  
### <a name="c-importing-a-schema-that-does-not-specify-a-target-namespace"></a>C. 대상 네임스페이스를 지정하지 않는 스키마 가져오기  
 **targetNamespace** 특성이 포함되지 않은 스키마를 컬렉션으로 가져오는 경우 이 컬렉션의 구성 요소는 다음 예와 같이 빈 문자열 대상 네임스페이스와 연결됩니다. 컬렉션으로 가져온 하나 이상의 스키마를 연결하지 않으면 잠재적으로 관련이 없는 여러 개의 스키마 구성 요소가 기본 빈 문자열 네임스페이스에 연결되게 됩니다.  
  
```  
-- Create a collection that contains a schema with no target namespace.  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  xmlns:ns="http://ns">  
<element name="e" type="dateTime"/>  
</schema>';  
GO  
-- query will return the names of all the collections that   
--contain a schema with no target namespace  
SELECT sys.xml_schema_collections.name   
FROM   sys.xml_schema_collections   
JOIN   sys.xml_schema_namespaces   
ON     sys.xml_schema_collections.xml_collection_id =   
       sys.xml_schema_namespaces.xml_collection_id   
WHERE  sys.xml_schema_namespaces.name='';  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [DROP XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
