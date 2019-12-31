---
title: 테이블/열에 대 한 사용자 지정 XSD 매핑 (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5fafcd918dda0001c316fd68cae3b19e6cd805a3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257430"
---
# <a name="custom-xsd-mappings-to-tablescolumns-sqlxml"></a>테이블/열에 대 한 사용자 지정 XSD 매핑 (SQLXML)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD 스키마를 사용하여 관계형 데이터베이스의 XML 뷰를 제공할 때는 스키마의 요소 및 특성을 데이터베이스의 테이블 및 열에 매핑해야 합니다. 데이터베이스 테이블/뷰의 행은 XML 문서의 요소에 매핑됩니다. 데이터베이스의 열 값은 특성 또는 요소에 매핑됩니다.  
  
 XPath 쿼리는 주석이 추가된 XSD 스키마에 대해 지정되며 스키마의 요소 및 특성에 대한 데이터는 매핑되는 테이블 및 열에서 검색됩니다. 데이터베이스에서 단일 값을 얻으려면 XSD 스키마에 지정된 매핑에 관계 및 필드 사양이 모두 있어야 합니다. 요소/특성의 이름이 매핑되는 테이블/뷰 또는 열 이름과 다른 경우 **sql: relation** 및 **sql: field** annotation을 사용 하 여 XML 문서의 요소 또는 특성과 데이터베이스의 테이블 (뷰) 또는 열 간의 매핑을 지정 합니다.  
  
## <a name="sql-relation"></a>sql-relation  
 **Sql: relation** 주석이 추가 되어 XSD 스키마의 XML 노드를 데이터베이스 테이블에 매핑합니다. 테이블 이름 (뷰)은 **sql: relation** 주석의 값으로 지정 됩니다.  
  
 요소에 **sql: relation** 을 지정 하는 경우이 주석의 범위는 해당 요소의 복합 형식 정의에 설명 된 모든 특성 및 자식 요소에 적용 되므로 주석을 작성 하는 바로 가기를 제공 합니다.  
  
 **Sql: relation** 주석은에서 유효한 식별자가 XML에서 유효 하지 않은 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에도 유용 합니다. 예를 들어 "Order Details"는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 유효한 테이블 이름이지만 XML에서는 유효하지 않습니다. 이러한 경우 **sql: relation** 주석을 사용 하 여 매핑을 지정할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 **Sql 필드** 주석은 요소나 특성을 데이터베이스 열에 매핑합니다. **Sql: field** 주석이 추가 되어 스키마의 XML 노드를 데이터베이스 열에 매핑합니다. 빈 콘텐츠 요소에는 **sql: field** 를 지정할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예를 실행 하기 위한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)을 참조 하세요.  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. sql:relation 및 sql:field 주석 지정  
 이 예에서 XSD 스키마는 ** \<FName>** 및 ** \<LName>** 자식 요소와 **ContactID** 특성을 포함 하는 복합 형식의 ** \<Contact>** 요소로 구성 됩니다.  
  
 **Sql: relation** 주석은 ** \<contact>** 요소를 AdventureWorks 데이터베이스의 Person. contact 테이블에 매핑합니다. **Sql: field** annotation은 ** \<FName>** 요소를 FirstName 열에 매핑하고 ** \<LName>** 요소를 LastName 열에 매핑합니다.  
  
 **ContactID** 특성에는 주석이 지정 되지 않습니다. 따라서 이름이 같은 열에 특성을 매핑하는 기본 매핑이 수행됩니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 MySchema-annotated.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. MySchema-annotated.xml을 저장한 디렉터리와 같은 디렉터리에 MySchema-annotatedT.xml 이름으로 파일을 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(MySchema-annotated.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
