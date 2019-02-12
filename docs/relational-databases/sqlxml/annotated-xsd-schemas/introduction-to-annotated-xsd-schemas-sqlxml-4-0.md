---
title: 주석이 추가 된 XSD 스키마 (SQLXML 4.0) 소개 | Microsoft 문서
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- mapping schema [SQLXML], about mapping schema
- views [SQLXML]
- valid XSD schemas [SQLXML]
- annotations [SQLXML]
- XSD schemas [SQLXML], creating XML views
- annotated XSD schemas, creating XML views
- minimum XSD schema
- annotated XSD schemas, examples
- XML views [SQLXML]
ms.assetid: 15282db1-65c4-43be-bdb7-e9ef49cb33a2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b9b5b2356e7f244ec7fc07e28ea50dee9fd8e104
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013354"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>주석이 추가된 XSD 스키마 소개(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD(XML 스키마 정의) 언어를 사용하여 관계형 데이터의 XML 뷰를 만들 수 있습니다. 그런 다음 XPath(XML Path Language) 쿼리를 사용하여 뷰를 쿼리할 수 있습니다. 이는 CREATE VIEW 문을 사용하여 뷰를 만들고 뷰에 대해 SQL 쿼리를 지정하는 것과 유사합니다.  
  
 XML 스키마는 XML 문서의 구조뿐만 아니라 문서 내의 데이터에 대한 다양한 제약 조건을 설명합니다. 스키마에 대해 XPath 쿼리를 지정하면 XPath 쿼리가 실행되는 스키마에 따라 반환되는 XML 문서의 구조가 결정됩니다.  
  
 XSD 스키마에서  **\<xsd: schema >** 전체 스키마를 포함 하는 요소, 모든 요소 선언에 포함 되어야 합니다는  **\<xsd: schema >** 요소입니다. 네임 스페이스를 정의 하는 특성을 설명할 수 있는 스키마 및 속성으로 스키마에 사용 되는 네임 스페이스는  **\<xsd: schema >** 요소.  
  
 유효한 XSD 스키마를 포함 해야 합니다는  **\<xsd: schema >** 요소는 다음과 같이 정의 합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 합니다  **\<xsd: schema >** 요소에서 XML 스키마 네임 스페이스 사양에서 파생 됩니다 http://www.w3.org/2001/XMLSchema합니다.  
  
## <a name="annotations-to-the-xsd-schema"></a>XSD 스키마에 주석 추가  
 데이터베이스에 대한 매핑을 설명하는 주석을 XSD 스키마에 추가하여 데이터베이스를 쿼리하고 결과를 XML 문서 형식으로 반환할 수 있습니다. 주석을 사용하여 XSD 스키마를 데이터베이스 테이블 및 열에 매핑할 수 있습니다. XSD 스키마로 생성된 XML 뷰에 대해 XPath 쿼리를 지정하여 데이터베이스를 쿼리하고 결과를 XML 형식으로 얻을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0의 XSD 스키마 언어는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]에서 주석이 추가된 XDR(XML-Data Reduced) 스키마 언어에 도입된 주석을 지원합니다. 주석이 추가된 XDR은 SQLXML 4.0에서 더 이상 사용되지 않습니다.  
  
 관계형 데이터베이스 컨텍스트에서는 임의의 XSD 스키마를 관계형 저장소에 매핑하는 것이 유용합니다. 이를 수행하는 한 가지 방법은 XSD 스키마에 주석을 추가하는 것입니다. 주석이 지정 된 XSD 스키마 라고 하는 *매핑 스키마*, XML 데이터가 관계형 저장소에 매핑되는 방법에 대 한 정보를 제공 하는 합니다. 매핑 스키마는 궁극적으로 관계형 데이터에 대한 XML 뷰로 생각할 수 있습니다. 이러한 매핑을 사용하여 관계형 데이터를 XML 문서로 검색할 수 있습니다.  
  
## <a name="namespace-for-annotations"></a>주석에 대한 네임스페이스  
 XSD 스키마에서 주석은 네임 스페이스를 사용 하 여 지정 된 **urn: 스키마-microsoft-com:mapping-스키마**합니다. 네임 스페이스를 지정 하는 가장 쉬운 방법은 지정 방법은 다음 예제 에서처럼 합니다  **\<xsd: schema >** 태그입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 사용된 네임스페이스 접두사는 임의로 지정되었습니다. 이 설명서에서는 합니다 **sql** 접두사는 주석 네임 스페이스를 나타내고을 구별 하기이 네임 스페이스의 주석을 다른 네임 스페이스에서 사용 됩니다.  
  
## <a name="example-of-an-annotated-xsd-schema"></a>주석이 추가된 XSD 스키마 예  
 다음 예제에서는 XSD 스키마는의 구성 된  **\<Person.Contact >** 요소입니다. 합니다  **\<직원 >** 요소에는 **ContactID** 특성 및  **\<FirstName >** 하 고  **\< LastName >** 자식 요소:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <xsd:element name="Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     type="xsd:string" />   
        <xsd:element name="LName"  
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 해당 요소와 특성을 데이터베이스 테이블 및 열에 매핑하기 위해 이 XSD 스키마에 주석을 추가합니다.  
  
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
        <xsd:attribute name="ConID"   
                       sql:field="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 매핑 스키마에는  **\<연락처 >** 요소를 사용 하 여 샘플 AdventureWorks 데이터베이스의 Person.Contact 테이블에 매핑되는 **sql: relation** 주석입니다. ConID, FName 및 LName 특성을 사용 하 여 Person.Contact 테이블의 ContactID, FirstName 및 LastName 열에 매핑되는 **sql: field** 주석입니다.  
  
 주석이 추가된 이 XSD 스키마는 관계형 데이터에 대한 XML 뷰를 제공합니다. 이 XML 뷰는 XPath 언어를 사용하여 쿼리할 수 있습니다. SQL 쿼리에서 행 집합을 반환하는 것과는 달리 XPath 쿼리에서는 XML 문서를 결과로 반환합니다.  
  
> [!NOTE]  
>  매핑 스키마에서 지정된 관계형 값(예: 테이블 이름 및 열 이름)의 대/소문자 구분은 SQL Server에서 대/소문자 구분 데이터 정렬 설정을 사용하고 있는지 여부에 따라 결정됩니다. 자세한 내용은 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="other-resources"></a>기타 리소스  
 XSD(XML 스키마 정의 언어), XPath(XML Path Language) 및 XSLT(Extensible Stylesheet Language Transformations)에 대한 자세한 내용은 다음 웹 사이트를 참조하십시오.  
  
-   XML Schema Part 0: Primer, W3C 권장 사항 (http://www.w3.org/TR/xmlschema-0/)  
  
-   XML Schema Part 1: 구조, W3C 권장 사항 (http://www.w3.org/TR/xmlschema-1/)  
  
-   XML Schema Part 2: datatypes, W3C 권장 사항 (http://www.w3.org/TR/xmlschema-2/)  
  
-   XML 경로 언어 (XPath) (http://www.w3.org/TR/xpath)  
  
-   XSL 변환 (XSLT) (http://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>관련 항목  
 [주석 스키마 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [주석이 추가 된 XDR 스키마 &#40;SQLXML 4.0에서에서 사용 되지 않음&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
