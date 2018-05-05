---
title: XSD 스키마 (SQLXML 4.0)에 주석 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f3e44d91a958441e421259b7257df49f14883eb0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>XSD 스키마에 주석 사용(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0의 XSD 스키마 언어는 XDR(XML-Data Reduced) 스키마 언어에 도입된 주석과 비슷한 방식으로 주석을 지원합니다. XSD에는 XDR에서는 지원되지 않은 추가 주석도 도입되었습니다.  
  
 이러한 주석은 XSD 스키마 내에서 XML-관계형 매핑을 지정하는 데 사용됩니다. 여기에는 XSD 스키마의 요소 및 특성을 데이터베이스의 테이블(뷰) 및 열에 매핑하는 작업이 포함됩니다.  
  
 주석을 지정하지 않으면 기본 매핑이 수행됩니다. 기본적으로 복합 유형의 XSD 요소는 지정된 데이터베이스의 테이블(뷰) 이름에 매핑되며 단순 유형의 요소 또는 특성은 같은 이름의 열에 매핑됩니다.  
  
 XSD 스키마는 간단히 말해 관계형 데이터의 XML 뷰이므로 이러한 주석을 사용하면 XML의 계층 관계를 지정하여 데이터베이스의 관계를 나타낼 수 있습니다.  
  
 이 섹션에서는 XSD 스키마에서 사용할 수 있는 주석에 대해 설명하고 사용 예를 제공합니다.  
  
> [!NOTE]  
>  이 섹션에 있는 모든 예는 각 예에서 설명된 주석이 추가된 XSD 스키마에 대해 간단한 XPath 쿼리를 지정합니다. 이 섹션에서는 사용자가 XPath 언어에 대해 잘 알고 있다고 가정합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [XSD 주석 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
 XSD 스키마에서 사용할 수 있는 주석, 이러한 주석에 대한 설명, 그리고 이러한 주석에 해당하는 XDR 주석을 나열합니다.  
  
 [테이블 및 열에 XSD 요소와 특성의 기본 매핑이 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 기본 매핑 및 이와 관련된 태스크의 예를 설명합니다.  
  
 [테이블 및 열에 XSD 요소와 특성의 명시적 매핑 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 사용한 명시적 매핑에 대해 설명 된 **sql: relation** 및 **sql: field** 주석, 예제를 제공 합니다.  
  
 [Sql: relationship을 사용 하 여 관계 지정 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql: relationship** 주석입니다.  
  
 [Sql: inverse Attribute on sql: relationship 지정 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 설명의 **sql: inverse** 주석입니다.  
  
 [Sql 사용 하 여 상수 요소 만들기:은 상수 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql:은 상수** 주석입니다.  
  
 [결과 XML 문서를 사용 하 여 sql에서 스키마 요소 제외: 매핑된 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 에 대해 설명 하 고 예를 제공 된 **sql: 매핑된** 주석입니다.  
  
 [사용 하 여 값 필터링-필드 및 sql:-값 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql:-필드** 및 **sql:-값** 주석입니다.  
  
 [Sql: 사용 하 여 키 열 식별-필드 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql:-필드** 주석입니다.  
  
 [대상 Namespace를 사용 하 여 targetNamespace 특성 지정 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **targetNamespace** 특성입니다.  
  
 [유효한 ID, IDREF 및 IDREFS 유형 특성을 사용 하 여 sql: prefix 만드는 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql: prefix** 주석입니다.  
  
 [데이터 형식 강제 변환 및 sql: datatype 주석 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql: datatype** 주석입니다.  
  
 [XSD 데이터 형식을 XPath 데이터 형식에 매핑 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)  
 XSD, XDR 및 XPath 데이터 형식을 비교하고 연관된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환을 나열하는 표를 제공합니다.  
  
 [Sql:use 사용 하 여 CDATA 섹션 만들기-cdata &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql:use-데이터** 주석입니다.  
  
 [Sql 사용 하 여 BLOB 데이터에 대 한 URL 참조 요청: 인코딩할 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql: 인코딩할** 주석입니다.  
  
 [사용 되지 않은 데이터를 사용 하 여 sql:overflow 검색-필드 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)  
 에 대해 설명 하 고 예를 제공 된 **sql:overflow-필드** 주석입니다.  
  
 [sql:hide를 사용하여 요소 및 특성 숨기기](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)  
 에 대해 설명 하 고 예를 제공 된 **sql: hide** 주석입니다.  
  
 [sql:identity 및 sql:guid 주석 사용](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)  
 에 대해 설명 하 고 예를 제공 된 **sql: identity** 및 **sql: guid** 주석입니다.  
  
 [sql:max-depth를 사용하여 재귀 관계의 깊이 지정](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 에 대해 설명 하 고 예를 제공 된 **sql:max-깊이** 주석입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [주석 스키마 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
