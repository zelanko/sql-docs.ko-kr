---
title: 쿼리(SQLXML)에서 추가된 XSD 스키마 사용
description: SQLXML 4.0에서 추가된 XSD 스키마에 대해 XPath 쿼리를 지정하여 데이터베이스에서 데이터를 검색하는 방법을 알아봅니다.
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML]
- inline schemas [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- queries [SQLXML], annotated XSD schemas
- retrieving data
- mapping schema [SQLXML], queries
- multiple inline schemas
- annotated XSD schemas, queries
- XSD schemas [SQLXML], queries
- templates [SQLXML], annotated XSD schemas in queries
ms.assetid: 927a30a2-eae8-420d-851d-551c5f884f3c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9ecd9d65d0f70f7c25328c15bb886ca52122de2
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388688"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>쿼리에 주석이 추가된 XSD 스키마 사용(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  템플릿에 XDR 스키마에 대한 XPath 쿼리를 지정하는 방식으로 주석이 추가된 스키마에 대해 쿼리를 지정하여 데이터베이스에서 데이터를 검색할 수 있습니다.  
  
 sql:xpath-query>요소를 사용하면 추가된 스키마에 의해 정의된 XML 뷰에 대해 XPath 쿼리를 지정할 수 있습니다. ** \<** XPath 쿼리를 실행할 추가된 스키마는 ** \<sql:xpath-query>** 요소의 **매핑 스키마** 특성을 사용하여 식별됩니다.  
  
 템플릿은 하나 이상의 쿼리를 포함하는 유효한 XML 문서입니다. FOR XML 및 XPath 쿼리는 문서 조각을 반환합니다. 템플릿은 문서 조각의 컨테이너 역할을 하며 단일 최상위 요소를 지정하는 방법을 제공합니다.  
  
 이 항목의 예에서는 템플릿을 통해 주석이 추가된 스키마에 대해 XPath 쿼리를 지정하여 데이터베이스에서 데이터를 검색합니다.  
  
 예를 들어 주석이 추가된 다음 스키마를 참조하십시오.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID" type="xsd:string" />   
       <xsd:attribute name="FirstName" type="xsd:string" />   
       <xsd:attribute name="LastName"  type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 이해하기 쉽도록 이 XSD 스키마는 Schema2.xml이라는 파일에 저장됩니다. 따라서 다음 템플릿 파일(Schema2T.xml)에 주석이 추가된 스키마에 대한 XPath 쿼리를 지정할 수 있었습니다.  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql"  
     >  
          Person.Contact[@ContactID="1"]  
</sql:xpath-query>  
```  
  
 그러면 SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만들어서 사용하여 템플릿 파일의 일부로 쿼리를 실행할 수 있습니다. 자세한 내용은 [SQLXML 4.0&#41;에서 사용되지 &#40;비하여 추가된 XDR 스키마를 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)참조하십시오.  
  
## <a name="using-inline-mapping-schemas"></a>인라인 매핑 스키마 사용  
 주석이 추가된 스키마를 템플릿에 직접 포함한 다음 이 템플릿에 인라인 스키마에 대한 XPath 쿼리를 지정할 수 있습니다. 이 템플릿은 Updategram일 수도 있습니다.  
  
 템플릿에는 여러 개의 인라인 스키마가 포함될 수 있습니다. 템플릿에 포함된 인라인 스키마를 사용하려면 ** \<xsd:schema>** 요소에 고유한 값이 있는 **id** 특성을 지정한 다음 **#idvalue** 사용하여 인라인 스키마를 참조합니다. **id** 특성은 XDR 스키마에서 사용되는 sql:id({urn:schemas-microsoft-com:xml-sql}id)와 동작에서 동일합니다. **sql:id**  
  
 예를 들어 다음 템플릿에서는 주석이 추가된 두 개의 인라인 스키마를 지정합니다.  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema1' sql:is-mapping-schema='1'>  
  <xsd:element name='Employees' ms:relation='HumanResources.Employee'>  
    <xsd:complexType>  
      <xsd:attribute name='LoginID'   
                     type='xsd:string'/>  
      <xsd:attribute name='Title'   
                     type='xsd:string'/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema2' sql:is-mapping-schema='1'>  
  <xsd:element name='Contacts' ms:relation='Person.Contact'>  
    <xsd:complexType>  
  
      <xsd:attribute name='ContactID'   
                     type='xsd:string' />  
      <xsd:attribute name='FirstName'   
                     type='xsd:string' />  
      <xsd:attribute name='LastName'   
                     type='xsd:string' />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema1'>  
    /Employees[@LoginID='adventure-works\guy1']  
</sql:xpath-query>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema2'>  
    /Contacts[@ContactID='1']  
</sql:xpath-query>  
</ROOT>  
```  
  
 이 템플릿에서는 두 개의 XPath 쿼리도 지정합니다. 각 ** \<xpath-쿼리>** 요소는 **매핑 스키마** 특성을 지정하여 매핑 스키마를 고유하게 식별합니다.  
  
 템플릿에서 인라인 스키마를 지정할 때 **sql:is-mapping-스키마** 어구는 ** \<xsd:schema>** 요소에도 지정해야 합니다. **sql:is-mapping-스키마는** 부울 값을 사용합니다(0=false, 1=true). **sql:is-mapping-스키마="1"이** 있는 인라인 스키마는 인라인 에이치드 스키마로 처리되며 XML 문서에서 반환되지 않습니다.  
  
 **sql:is-mapping-스키마** 어구는 템플릿 네임스페이스 **항아리에 속합니다:스키마-마이크로소프트-com:xml-sql**.  
  
 이 예를 테스트하려면 로컬 디렉터리에 템플릿(InlineSchemaTemplate.xml)을 지정한 다음 SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만들어서 사용하여 템플릿을 실행합니다. 자세한 내용은 [ADO를 사용하여 SQLXML 4.0 쿼리를 실행합니다.](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)  
  
 sql:xpath-query>요소(XPath 쿼리가 있는 경우) 또는 업데이트 그램의 ** \<updg:sync>** 요소에 **매핑 스키마** 특성을 지정하는 것 외에도 다음을 수행할 수 있습니다. ** \<**  
  
-   템플릿의 ** \<ROOT>** 요소(전역 선언)에서 **매핑 스키마** 특성을 지정합니다. 이 매핑 스키마는 명시적 **매핑 스키마** 추가가 없는 모든 XPath 및 updategram 노드에서 사용되는 기본 스키마가 됩니다.  
  
-   ADO **Command** 개체를 사용하여 **매핑 스키마** 특성을 지정합니다.  
  
 xpath 쿼리>또는 ** \<updg:sync>** 요소에 지정된 **매핑 스키마** 특성이 가장 높은 우선 순위를 가합니다. ** \<** ADO **명령** 개체의 우선 순위가 가장 낮습니다.  
  
 템플릿에서 XPath 쿼리를 지정하고 XPath 쿼리가 실행되는 매핑 스키마를 지정하지 않으면 XPath 쿼리가 **dbobject** 형식 쿼리로 처리됩니다. 예를 들어 다음 템플릿을 참조하십시오.  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 이 템플릿에서는 XPath 쿼리만 지정하고 매핑 스키마는 지정하지 않습니다. 따라서 이 쿼리는 Production.ProductPhoto가 테이블 이름이며 @ProductPhotoID='100'이 ID 값이 100인 제품 사진을 찾는 조건자인 **dbobject** 형식 쿼리로 처리됩니다. @LargePhoto은 값을 검색할 열입니다.  
  
  
