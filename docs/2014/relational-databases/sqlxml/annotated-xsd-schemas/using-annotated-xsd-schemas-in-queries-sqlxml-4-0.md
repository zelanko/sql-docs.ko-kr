---
title: 쿼리에 주석이 추가 된 XSD 스키마 사용 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: caee73995b56e248a91872117a51e809c6eea976
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065679"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>쿼리에 주석이 추가된 XSD 스키마 사용(SQLXML 4.0)
  템플릿에 XDR 스키마에 대한 XPath 쿼리를 지정하는 방식으로 주석이 추가된 스키마에 대해 쿼리를 지정하여 데이터베이스에서 데이터를 검색할 수 있습니다.  
  
 **\<sql:xpath-query>** 요소를 사용 하면 주석이 추가 된 스키마에 정의 된 XML 뷰에 대해 XPath 쿼리를 지정할 수 있습니다. XPath 쿼리가 실행 될 주석이 추가 된 스키마는 요소의 특성을 사용 하 여 식별 됩니다 `mapping-schema` **\<sql:xpath-query>** .  
  
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
  
 그러면 SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만들어서 사용하여 템플릿 파일의 일부로 쿼리를 실행할 수 있습니다. 자세한 내용은 [SQLXML 4.0&#41;에서 사용 되지 &#40;주석이 추가 된 XDR 스키마 ](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)를 참조 하세요.  
  
## <a name="using-inline-mapping-schemas"></a>인라인 매핑 스키마 사용  
 주석이 추가된 스키마를 템플릿에 직접 포함한 다음 이 템플릿에 인라인 스키마에 대한 XPath 쿼리를 지정할 수 있습니다. 이 템플릿은 Updategram일 수도 있습니다.  
  
 템플릿에는 여러 개의 인라인 스키마가 포함될 수 있습니다. 템플릿에 포함 된 인라인 스키마를 사용 하려면 요소에 고유한 값을 사용 하 여 **id** 특성을 지정한 **\<xsd:schema>** 다음 **#idvalue** 를 사용 하 여 인라인 스키마를 참조 합니다. **Id** 특성은 XDR 스키마에 사용 되는 **sql: id** ({urn: 스키마-microsoft-com: xml) id)의 동작과 동일 합니다.  
  
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
  
 이 템플릿에서는 두 개의 XPath 쿼리도 지정합니다. 각 요소는 **\<xpath-query>** 특성을 지정 하 여 매핑 스키마를 고유 하 게 식별 합니다 `mapping-schema` .  
  
 템플릿에서 인라인 스키마를 지정 하는 경우 `sql:is-mapping-schema` 에도 요소에 주석을 지정 해야 합니다 **\<xsd:schema>** . `sql:is-mapping-schema`는 부울 값(0=false, 1=true)을 사용합니다. **Sql: is 매핑-schema = "1"** 인 인라인 스키마는 인라인 주석이 추가 된 스키마로 처리 되 고 XML 문서에서 반환 되지 않습니다.  
  
 `sql:is-mapping-schema` 주석은 템플릿 네임스페이스 `urn:schemas-microsoft-com:xml-sql`에 속합니다.  
  
 이 예를 테스트하려면 로컬 디렉터리에 템플릿(InlineSchemaTemplate.xml)을 지정한 다음 SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만들어서 사용하여 템플릿을 실행합니다. 자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 템플릿의 요소에 특성을 지정 하는 것 외에도 `mapping-schema` **\<sql:xpath-query>** (XPath 쿼리가 있을 때) 또는 **\<updg:sync>** updategram의 요소에는 다음을 수행할 수 있습니다.  
  
-   `mapping-schema` **\<ROOT>** 템플릿의 요소 (전역 선언)에 특성을 지정 합니다. 그러면 이 매핑 스키마가 명시적 `mapping-schema` 주석이 없는 모든 XPath 및 Updategram 노드에서 사용할 기본 스키마가 됩니다.  
  
-   ADO `mapping schema` 개체를 사용하여 `Command` 특성을 지정합니다.  
  
 `mapping-schema`또는 요소에 지정 된 특성의 **\<xpath-query>** **\<updg:sync>** 우선 순위가 가장 높습니다. ADO `Command` 개체의 우선 순위가 가장 낮습니다.  
  
 템플릿에서 XPath 쿼리를 지정 하 고 XPath 쿼리가 실행 되는 매핑 스키마를 지정 하지 않으면 XPath 쿼리가 **dbobject** type 쿼리로 처리 됩니다. 예를 들어 다음 템플릿을 참조하십시오.  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 이 템플릿에서는 XPath 쿼리만 지정하고 매핑 스키마는 지정하지 않습니다. 따라서이 쿼리는 **dbobject** 형식 쿼리로 처리 됩니다. 여기서는 Production photo가 테이블 이름이 고 @ProductPhotoID = ' 100 '은 ID 값이 100 인 제품 사진을 찾는 조건자입니다. @LargePhoto값을 검색할 열입니다.  
  
  
