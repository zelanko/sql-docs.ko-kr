---
title: XML 스키마 컬렉션(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- XSD schemas [SQL Server]
- xml_schema_namespace function
- XML schema collections [SQL Server], about XML schema collections
- metadata [SQL Server], XML schema collections
- queries [XML in SQL Server], XML schema collections
- schema collections [SQL Server]
- schemas [SQL Server], XML
- XML [SQL Server], schema collections
- XML schema collections [SQL Server]
- schema collections [SQL Server], about XML schema collections
ms.assetid: 659d41aa-ccec-4554-804a-722a96ef25c2
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8c4b1492f003a8535e53909b9a89c1a0555a7ff6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="xml-schema-collections-sql-server"></a>XML 스키마 컬렉션 [SQL Server]
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [xml&#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md) 항목에 설명된 것과 같이 SQL Server는 **xml** 데이터 형식을 통해 XML 데이터에 대한 네이티브 저장소를 제공합니다. 선택적으로 XML 스키마 컬렉션을 통해 **xml** 유형의 열 또는 변수와 XSD 스키마를 연결할 수 있습니다. XML 스키마 컬렉션은 가져온 XML 스키마를 저장하고 다음을 수행하는 데 사용됩니다.  
  
-   XML 인스턴스 유효성 검사  
  
-   데이터베이스에 저장될 때 XML 데이터 형식화  
  
 XML 스키마 컬렉션은 데이터베이스에 있는 테이블과 같은 메타데이터 엔터티입니다. 스키마 컬렉션은 생성, 수정 및 삭제할 수 있습니다. [CREATE XML SCHEMA COLLECTION(Transact-SQL)](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) 문에 지정된 스키마는 새로 만든 XML 스키마 컬렉션 개체에 자동으로 가져와집니다. [ALTER XML SCHEMA COLLECTION(Transact-SQL)](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) 문을 사용하여 추가 스키마 또는 스키마 구성 요소를 데이터베이스에 있는 기존 컬렉션 개체로 가져올 수 있습니다.  
  
 [형식화된 XML과 형식화되지 않은 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md) 항목에 설명된 것과 같이 스키마가 연결된 열 또는 변수에 저장된 XML은 스키마가 인스턴스 데이터에 대해 필요한 데이터 형식 정보를 제공하기 때문에 **형식화된** XML이라고 부릅니다. SQL Server는 이 유형 정보를 사용하여 데이터 저장소를 최적화합니다.  
  
 쿼리 프로세싱 엔진은 또한 유형 검사 및 쿼리와 데이터 수정 최적화를 위해 스키마를 사용합니다.  
  
 또한 SQL Server는 형식화된 **xml**의 경우 연결된 XML 스키마 컬렉션을 사용하여 XML 인스턴스의 유효성을 검사합니다. XML 인스턴스가 스키마로 컴파일되는 경우 데이터베이스에서 인스턴스를 해당 유형 정보와 함께 시스템에 저장할 수 있습니다. 그렇지 않으면 인스턴스가 거부됩니다.  
  
 내장 함수 XML_SCHEMA_NAMESPACE를 사용하여 데이터베이스에 저장된 스키마 컬렉션을 검색할 수 있습니다. 자세한 내용은 [저장된 XML 스키마 컬렉션 보기](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)를 참조하세요.  
  
 또한 XML 스키마 컬렉션을 사용하여 XML 변수, 매개 변수 및 열을 형식화할 수 있습니다.  
  
##  <a name="ddl"></a> 스키마 컬렉션 관리 DDL  
 데이터베이스에서 XML 스키마 컬렉션을 만들고 이를 **xml** 유형의 변수 및 열과 연결할 수 있습니다. 데이터베이스에 있는 스키마 컬렉션을 관리하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다음 DDL 문을 제공합니다.  
  
-   [CREATE XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)은 데이터베이스에 스키마 구성 요소를 가져옵니다.  
  
-   [ALTER XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)은 기존 XML 스키마 컬렉션의 스키마 구성 요소를 수정합니다.  
  
-   [DROP XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)은 전체 XML 스키마 컬렉션 및 모든 해당 구성 요소를 삭제합니다.  
  
 XML 스키마 컬렉션과 여기에 포함되는 스키마를 사용하려면 먼저 CREATE XML SCHEMA COLLECTION 문을 사용하여 컬렉션과 스키마를 만들어야 합니다. 스키마 컬렉션을 만든 다음에는 **xml** 유형의 변수와 열을 만들고 스키마 컬렉션과 연결할 수 있습니다. 스키마 컬렉션을 만든 다음에는 여러 스키마 구성 요소가 메타데이터에 포함됩니다. 또한 ALTER XML SCHEMA COLLECTION을 사용하여 기존 스키마에 더 많은 구성 요소를 추가하거나 기존 컬렉션에 새로운 스키마를 추가할 수 있습니다.  
  
 스키마 컬렉션을 삭제하려면 DROP XML SCHEMA COLLECTION 문을 사용합니다. 이렇게 하면 컬렉션에 포함된 모든 스키마가 삭제되고 컬렉션 개체가 제거됩니다. 스키마 컬렉션을 삭제하려면 [DROP XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)에 기술된 조건을 충족해야 합니다.  
  
##  <a name="components"></a> 스키마 구성 요소 이해  
 CREATE XML SCHEMA COLLECTION 문을 사용하면 여러 스키마 구성 요소를 데이터베이스로 가져옵니다. 스키마 구성 요소에는 스키마 요소, 특성 및 유형 정의가 포함됩니다. DROP XML SCHEMA COLLECTION 문을 사용하면 전체 컬렉션을 제거합니다.  
  
 CREATE XML SCHEMA COLLECTION은 여러 시스템 테이블에 스키마 구성 요소를 저장합니다.  
  
 예를 들어 다음 스키마를 고려해 보십시오.  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            targetNamespace="uri:Cust_Orders2"  
            xmlns="uri:Cust_Orders2" >  
  <xsd:attribute name="SomeAttribute" type="xsd:int" />  
  <xsd:complexType name="SomeType" />  
  <xsd:complexType name="OrderType" >  
    <xsd:sequence>  
      <xsd:element name="OrderDate" type="xsd:date" />  
      <xsd:element name="RequiredDate" type="xsd:date" />  
      <xsd:element name="ShippedDate" type="xsd:date" />  
    </xsd:sequence>  
    <xsd:attribute name="OrderID" type="xsd:ID" />  
    <xsd:attribute name="CustomerID"  />  
    <xsd:attribute name="EmployeeID"  />  
  </xsd:complexType>  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order" type="OrderType"  
                     maxOccurs="unbounded" />  
       </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
      <xsd:attribute name="OrderIDList" type="xsd:IDREFS" />  
  </xsd:complexType>  
  <xsd:element name="Customer" type="CustomerType" />  
</xsd:schema>  
```  
  
 이전 스키마는 데이터베이스에 저장할 수 있는 여러 유형의 구성 요소를 보여 줍니다. 여기에는 `SomeAttribute`, `SomeType`, `OrderType`, `CustomerType`, `Customer`, `Order`, `CustomerID`, `OrderID`, `OrderDate`, `RequiredDate`및 `ShippedDate`이(가) 포함됩니다.  
  
### <a name="component-categories"></a>구성 요소 범주  
 데이터베이스에 저장되는 스키마 구성 요소는 다음 범주로 구분됩니다.  
  
-   ELEMENT  
  
-   ATTRIBUTE  
  
-   TYPE(간단하거나 복잡한 유형)  
  
-   ATTRIBUTEGROUP  
  
-   MODELGROUP  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
-   **SomeAttribute** 는 ATTRIBUTE 구성 요소입니다.  
  
-   **SomeType**, **OrderType**및 **CustomerType** 은 TYPE 구성 요소입니다.  
  
-   **Customer** 는 ELEMENT 구성 요소입니다.  
  
 데이터베이스로 스키마를 가져올 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 스키마 자체는 저장하지 않습니다. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 여러 개별 구성 요소를 저장합니다. 즉, \<Schema> 태그는 저장되지 않으며 이 태그 내에 정의된 구성 요소만 보관됩니다. 모든 스키마 요소는 보관되지 않습니다. \<Schema> 태그에 해당 구성 요소의 기본 동작을 지정하는 특성이 포함된 경우 이러한 특성은 다음 표에 설명된 것과 같이 가져오기 프로세스 중에 태그 내에 있는 스키마 구성 요소로 이동됩니다.  
  
|특성 이름|동작|  
|--------------------|--------------|  
|**attributeFormDefault**|아직 제공되지 않았고 값이 **attributeFormDefault** 특성의 값으로 설정된 스키마의 모든 특성 선언에 적용된 **form** 특성입니다.|  
|**elementFormDefault**|아직 제공되지 않았고 값이 **elementFormDefault** 특성의 값으로 설정된 스키마의 모든 요소 선언에 적용된 **form** 특성입니다.|  
|**blockDefault**|아직 제공되지 않았고 값이 **blockDefault** 특성의 값으로 설정된 모든 요소 선언 및 유형 정의에 적용된 **block** 특성입니다.|  
|**finalDefault**|아직 제공되지 않았고 값이 **finalDefault** 특성의 값으로 설정된 모든 요소 선언 및 유형 정의에 적용된 **final** 특성입니다.|  
|**targetNamespace**|대상 네임스페이스에 속하는 구성 요소에 대한 정보는 메타데이터에 저장됩니다.|  
  
##  <a name="perms"></a> XML 스키마 컬렉션에 대한 사용 권한  
 다음을 수행하는 데 필요한 권한이 있어야 합니다.  
  
-   XML 스키마 컬렉션 생성/로드  
  
-   XML 스키마 컬렉션 수정  
  
-   XML 스키마 컬렉션 삭제  
  
-   XML 스키마 컬렉션을 사용하여 **xml** 유형의 열, 변수 및 매개 변수를 형식화하거나 이를 테이블 또는 열 제약 조건에 사용  
  
 SQL Server 보안 모델에서는 모든 개체에 대한 CONTROL 권한이 허용됩니다. 이 사용 권한의 피부여자는 개체에 대한 모든 기타 사용 권한을 얻습니다. 개체의 소유자는 또한 개체에 대한 모든 사용 권한을 가집니다.  
  
 개체에 대한 CONTROL 권한의 소유자 및 피부여자는 해당 개체에 대한 모든 사용 권한을 부여할 수 있습니다. 소유자가 아니고 CONTROL 권한이 없는 사용자도 WITH GRANT OPTION이 지정된 경우에는 개체에 대한 사용 권한을 계속 부여할 수 있습니다. 예를 들어 WITH GRANT OPTION을 통해 사용자 A에게 XML 스키마 컬렉션 S에 대한 REFERENCES 권한이 있지만 S에 대한 다른 사용 권한이 없다고 가정해 보십시오. 이 경우 사용자 A는 사용자 B에게 스키마 컬렉션 S에 대한 REFERENCES 권한을 부여할 수 있습니다.  
  
 보안 모델에서는 또한 사용 권한을 통해 XML 스키마 컬렉션을 만들고 사용하거나 한 사용자에서 다른 사용자로 소유권을 전송할 수 있습니다. 다음 항목에서는 XML 스키마 컬렉션 권한에 대해 설명합니다.  
  
-   [XML 스키마 컬렉션에 대한 사용 권한 부여](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)  
  
     이 항목에서는 XML 스키마 컬렉션을 만들기 위한 사용 권한을 부여하고 XML 스키마 컬렉션 개체에 대한 사용 권한을 부여하는 방법에 대해 설명합니다.  
  
-   [XML 스키마 컬렉션에 대한 사용 권한 취소](../../relational-databases/xml/revoke-permissions-on-an-xml-schema-collection.md)  
  
     이 항목에서는 사용 권한 취소를 사용하여 XML 스키마 컬렉션이 생성되지 않도록 방지하고 XML 스키마 컬렉션 개체에서 사용 권한을 취소하는 방법에 대해 설명합니다.  
  
-   [XML 스키마 컬렉션에 대한 사용 권한 거부](../../relational-databases/xml/deny-permissions-on-an-xml-schema-collection.md)  
  
     이 항목에서는 XML 스키마 컬렉션을 만들기 위한 사용 권한을 거부하고 XML 스키마 컬렉션 개체에 대한 사용 권한을 거부하는 방법에 대해 설명합니다.  
  
##  <a name="info"></a> XML 스키마 및 스키마 컬렉션에 대한 정보 가져오기  
 XML 스키마 컬렉션은 sys.xml_schema_collections 카탈로그 뷰에 열거됩니다. XML 스키마 컬렉션 "sys"는 시스템에 의해 정의됩니다. 여기에는 명시적으로 로드할 필요 없이 모든 사용자 정의 XML 스키마 컬렉션에서 사용할 수 있는 미리 정의된 네임스페이스가 포함됩니다. 이 목록에는 xml, xs, xsi, fn 및 xdt에 대한 네임스페이스가 포함됩니다. 두 개의 다른 카탈로그 뷰는 각 XML 스키마 컬렉션 내에서 모든 네임스페이스를 열거하는 sys.xml_schema_namespaces와 각 XML 스키마 내에서 모든 XML 스키마 구성 요소를 열거하는 sys.xml_components입니다.  
  
 기본 제공 함수인 **XML_SCHEMA_NAMESPACE**, *schemaName, XmlSchemacollectionName, namespace-uri*는 **xml** 데이터 형식의 인스턴스를 생성합니다. 이 인스턴스에는 미리 정의된 XML 스키마를 제외하고 XML 스키마 컬렉션에 포함된 스키마에 대한 XML 스키마 조각이 들어 있습니다.  
  
 XML 스키마 컬렉션의 내용은 다음과 같은 방식으로 열거할 수 있습니다.  
  
-   XML 스키마 컬렉션에 적합한 카탈로그 뷰에 Transact-SQL 쿼리를 작성합니다.  
  
-   기본 제공 함수 **XML_SCHEMA_NAMESPACE()** 를 사용합니다. 이 함수의 출력에 **xml** 데이터 형식 메서드를 적용할 수 있습니다. 하지만 기본 XML 스키마는 수정할 수 없습니다.  
  
 이러한 내용은 다음 예에 설명되어 있습니다.  
  
### <a name="example-enumerate-the-xml-namespaces-in-an-xml-schema-collection"></a>예: XML 스키마 컬렉션에 XML 네임스페이스 열거  
 XML 스키마 컬렉션 "myCollection"에 대해 다음 쿼리를 사용합니다.  
  
```  
SELECT XSN.name  
FROM    sys.xml_schema_collections XSC JOIN sys.xml_schema_namespaces XSN  
    ON (XSC.xml_collection_id = XSN.xml_collection_id)  
WHERE    XSC.name = 'myCollection'     
```  
  
### <a name="example-enumerate-the-contents-of-an-xml-schema-collection"></a>예: XML 스키마 컬렉션의 내용 열거  
 다음 문은 관계형 스키마 dbo 내에 있는 XML 스키마 컬렉션 "myCollection"의 내용을 열거합니다.  
  
```  
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection')  
```  
  
 컬렉션 내의 개별 XML 스키마는 **XML_SCHEMA_NAMESPACE()** 에 대한 세 번째 인수로 대상 네임스페이스를 지정하여 **xml**데이터 형식의 인스턴스로 가져올 수 있습니다. 이는 다음 예에서 확인할 수 있습니다.  
  
### <a name="example-output-a-specified-schema-from-an-xml-schema-collection"></a>예: XML 스키마 컬렉션으로부터 지정된 스키마 출력  
 다음 명령문은 관계형 스키마 dbo 내에 있는 XML 스키마 컬렉션 "myCollection"으로부터 대상 네임스페이스가 http://www.microsoft.com/books인 XML 스키마를 출력합니다.  
  
```  
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection',   
N'http://www.microsoft.com/books')  
```  
  
### <a name="querying-xml-schemas"></a>XML 스키마 쿼리  
 XML 스키마 컬렉션에 로드한 XML 스키마를 다음과 같은 방식으로 쿼리할 수 있습니다.  
  
-   XML 스키마 네임스페이스에 대한 카탈로그 뷰에서 Transact-SQL 쿼리를 작성합니다.  
  
-   **xml** 데이터 형식의 열이 포함된 테이블을 만들어서 XML 스키마를 저장하고 이를 XML 유형의 시스템으로 로드합니다. **xml** 데이터 형식의 메서드를 사용하여 XML 열을 쿼리할 수 있습니다. 또한 이 열에서 XML 인덱스를 작성할 수 있습니다. 하지만 이 접근 방식에서는 응용 프로그램이 XML 열에 저장된 XML 스키마와 XML 유형 시스템 간의 일관성을 유지 관리해야 합니다. 예를 들어 XML 유형 시스템으로부터 XML 스키마 네임스페이스를 삭제하면 일관성 유지를 위해 테이블에서도 삭제해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장된 XML 스키마 컬렉션 보기](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [포함된 스키마를 병합하기 위해 스키마 전처리](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md)   
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
