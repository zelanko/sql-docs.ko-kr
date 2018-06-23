---
title: 테이블 및 열 (SQLXML 4.0)에 XSD 요소와 특성의 기본 매핑이 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XSD schemas [SQLXML], mapping attributes and elements
- mapping schema [SQLXML], default mapping
- element mapping [SQLXML], default mapping
- element mapping [SQLXML]
- table mapping [SQLXML]
- annotated XSD schemas, mapping attributes and elements
- table/view mapping [SQLXML]
- column mapping [SQLXML]
- attribute mapping [SQLXML], default mapping
- default schema mapping
- table mapping [SQLXML], default mapping
- testing XPath query against schema
- xml data type [SQL Server], SQLXML
- table/view mapping [SQLXML], default mapping
- element/attribute mapping [SQLXML]
ms.assetid: 9a18e92a-6cfb-4a14-993a-663a95aabb63
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cbed4eee82d0bd7d57b7e4073d1f78f9150f9e6c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088340"
---
# <a name="default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-40"></a>테이블 및 열에 대한 XSD 요소 및 특성의 기본 매핑(SQLXML 4.0)
  기본적으로 주석이 추가된 XSD 스키마에서 복합 유형의 요소는 지정된 데이터베이스에 있는 같은 이름의 테이블(뷰)에 매핑되고 단순 유형의 요소 또는 특성은 테이블에 있는 같은 이름의 열에 매핑됩니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 참조 [SQLXML 예 실행에 대 한 요구 사항](../sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-default-mapping"></a>1. 기본 매핑 지정  
 이 예에서는 XSD 스키마에 주석이 지정되지 않습니다. **\<Person.Contact >** 요소는 복합 유형 및, 따라서 기본적으로 AdventureWorks 데이터베이스의 Person.Contact 테이블에 매핑합니다. 모든 특성 (ContactID, FirstName, LastName)은  **\<Person.Contact >** 요소는 단순 유형이 고 기본적으로 Person.Contact 테이블에서 같은 이름의 열에 매핑됩니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID"  type="xsd:string" />   
       <xsd:attribute name="FirstName"   type="xsd:string" />   
       <xsd:attribute name="LastName"    type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 MySchema.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 MySchema.xml을 저장한 디렉터리와 같은 디렉터리에 MySchemaT.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="MySchema.xml">  
            /Person.Contact  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(MySchema.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<?xml version="1.0" encoding="UTF-8" ?>  
<ROOT>  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong"/>  
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel"/>  
   ...  
</ROOT>  
```  
  
### <a name="b-mapping-an-xml-element-to-a-database-column"></a>2. XML 요소를 데이터베이스 열에 매핑  
 이 예에서는 주석이 사용되지 않기 때문에 기본 매핑이 수행합니다. **\<Person.Contact >** 요소는 복합 유형 및 데이터베이스에 같은 이름의 테이블에 매핑됩니다. 요소  **\<FirstName >** 및  **\<LastName >** 및 **EmployeeID** 특성은 단순 유형이 고, 따라서에 매핑됩니다는 같은 이름의 열입니다. 이 예와 이전 예의 유일한 차이점은 요소가 FirstName 및 LastName 필드 매핑에 사용된다는 것입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="FirstName" type="xsd:string" />   
        <xsd:element name="LastName" type="xsd:string" />   
      </xsd:sequence>  
      <xsd:attribute name="ContactID" type="xsd:integer" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 MySchemaElements.xml로 저장합니다.  
  
2.  다음 템플릿(MySchemaElementsT.xml)을 만들어 이전 단계에서 사용한 디렉터리와 같은 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="MySchemaElements.xml">  
            /Person.Contact  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchemaElements.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1">  
    <FirstName>Gustavo</FirstName>  
    <LastName>Achong</LastName>  
  </Person.Contact>  
   ...  
</ROOT>  
```  
  
### <a name="c-mapping-an-xml-element-to-an-xml-data-type-column"></a>3. XML 요소를 XML 데이터 형식 열에 매핑  
 이 예에서는 주석이 사용되지 않기 때문에 기본 매핑이 수행합니다. **\<Production.ProductModel >** 요소는 복합 유형 및 데이터베이스에 같은 이름의 테이블에 매핑됩니다. **ProductModelID** 특성은 단순 유형의 이며, 따라서 동일한 이름의 열에 매핑됩니다. 이 예와 이전 예의 유일한 차이점은는  **\<지침 >** 요소를 사용 하는 열에 매핑된다는 `xml` 데이터 형식을 사용 하 여는 `xsd:anyType` 유형입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Instructions" type="xsd:anyType" />   
      </xsd:sequence>  
      <xsd:attribute name="ProductModelID" type="xsd:integer" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 `xml` 데이터 형식은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입되었습니다.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 MySchemaXmlAnyElements.xml로 저장합니다.  
  
2.  다음 템플릿(MySchemaXmlAnyElementsT.xml)을 만들어 이전 단계에서 사용한 디렉터리와 같은 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="MySchemaXmlAnyElements.xml">  
            /Production.ProductModel[@ProductModelID=7]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchemaXmlAnyElements.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductModel ProductModelID="7">  
    <Instructions>  
      <root xmlns="http:  
//schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstru  
ctions">  
...  
      </root>  
    <Instructions>  
  </Production.ProductModel>  
</ROOT>  
```  
  
## <a name="see-also"></a>관련 항목  
 [주석 스키마 보안 고려 사항 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [XML 데이터&#40;SQL Server&#41;](../xml/xml-data-sql-server.md)   
 [SQLXML 4.0의 xml 데이터 형식 지원](../sqlxml/xml-data-type-support-in-sqlxml-4-0.md)  
  
  