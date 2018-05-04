---
title: 주석이 추가 된 XSD 스키마 (SQLXML 4.0) 쿼리에서 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f01b4ac920c98ebe180ee6b5f54e6601af1f8748
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>쿼리에 주석이 추가된 XSD 스키마 사용(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  템플릿에 XDR 스키마에 대한 XPath 쿼리를 지정하는 방식으로 주석이 추가된 스키마에 대해 쿼리를 지정하여 데이터베이스에서 데이터를 검색할 수 있습니다.  
  
 **\<sql:xpath-쿼리 >** 요소를 사용 하면 주석이 추가 된 스키마에서 정의 된 XML 뷰에 대해 XPath 쿼리를 지정할 수 있습니다. 대상 XPath 쿼리를 실행할 수는 주석이 추가 된 스키마를 사용 하 여 식별 됩니다는 **매핑 스키마** 특성에는  **\<sql:xpath-쿼리 >** 요소입니다.  
  
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
  
 그러면 SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만들어서 사용하여 템플릿 파일의 일부로 쿼리를 실행할 수 있습니다. 자세한 내용은 참조 [주석이 추가 된 XDR 스키마 &#40;SQLXML 4.0에서 더 이상 사용&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)합니다.  
  
## <a name="using-inline-mapping-schemas"></a>인라인 매핑 스키마 사용  
 주석이 추가된 스키마를 템플릿에 직접 포함한 다음 이 템플릿에 인라인 스키마에 대한 XPath 쿼리를 지정할 수 있습니다. 이 템플릿은 Updategram일 수도 있습니다.  
  
 템플릿에는 여러 개의 인라인 스키마가 포함될 수 있습니다. 서식 파일에 포함 된 인라인 스키마를 사용 하려면 지정 된 **id** 고유 값으로 특성을  **\<xsd: schema >** 요소와 다음 사용 하 여 **#idvalue**인라인 스키마를 참조 하도록 합니다. **id** 특성은의 동작과 동일는 **그것이** ({:-microsoft-com:xml-sql} id) XDR 스키마에서 사용 됩니다.  
  
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
  
 이 템플릿에서는 두 개의 XPath 쿼리도 지정합니다. 각각의  **\<xpath 쿼리 >** 요소를 지정 하 여 매핑 스키마를 고유 하 게 식별 된 **매핑 스키마** 특성입니다.  
  
 템플릿에 인라인 스키마를 지정 하는 경우는 **sql: 매핑은-스키마** 에 주석만 지정 해야 합니다는  **\<xsd: schema >** 요소입니다. **sql: 매핑은-스키마** 는 부울 값 (0 = false, 1 = true). 인라인 스키마는 **sql: 매핑은-스키마 = "1"** 주석이 추가 된 인라인 스키마로 처리 되 고 XML 문서에 반환 되지 않습니다.  
  
 **sql: 매핑은-스키마** 주석은 템플릿 네임 스페이스에 속한 **:-microsoft-com:xml-sql**합니다.  
  
 이 예를 테스트하려면 로컬 디렉터리에 템플릿(InlineSchemaTemplate.xml)을 지정한 다음 SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만들어서 사용하여 템플릿을 실행합니다. 자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 지정 하는 것 외에도 **매핑 스키마** 특성에  **\<sql:xpath-쿼리 >** 요소 (이 경우 XPath 쿼리) 템플릿 또는  **\< updg:sync >** 요소 updategram에서 다음을 수행할 수 있습니다.  
  
-   지정 된 **매핑 스키마** 특성을  **\<루트 >** 템플릿의 요소 (전역 선언). 그러면이 매핑 스키마에 있는 더 명시적 모든 XPath 및 updategram 노드에서 사용할 기본 스키마가 됩니다 **매핑 스키마** 주석입니다.  
  
-   지정 된 **매핑 스키마** ADO를 사용 하 여 특성 **명령** 개체입니다.  
  
 **매핑 스키마** 에 지정 된 특성의  **\<xpath 쿼리 >** 또는  **\<updg:sync >** 요소에 최대 precedence; ADO **명령** 개체 우선 순위가 가장 낮습니다.  
  
 서식 파일에 XPath 쿼리를 지정 하 고 XPath 쿼리가 실행 되는 매핑 스키마를 지정 하지 않으면 XPath 쿼리 처리 됩니다는 **dbobject** 형식 쿼리 합니다. 예를 들어 다음 템플릿을 참조하십시오.  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 이 템플릿에서는 XPath 쿼리만 지정하고 매핑 스키마는 지정하지 않습니다. 따라서이 쿼리는 취급는 **dbobject** 형식 쿼리는 Production.ProductPhoto가 테이블 이름 및 @ProductPhotoID= '100'이 ID 값이 100 인 제품 사진을 찾는 조건자 인 합니다. @LargePhoto 값을 검색할 열이입니다.  
  
  
