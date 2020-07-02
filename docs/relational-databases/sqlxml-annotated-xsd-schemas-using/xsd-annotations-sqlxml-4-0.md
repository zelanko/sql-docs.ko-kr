---
title: XSD 주석 (SQLXML)
description: SQL Server 2000 (4.x)에 도입 된 XDR 주석과 비교 하 여 SQL Server 2005 (4.x)에 도입 된 XSD 주석 (SQLXML 4.0)의 목록을 봅니다.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2ab06c27a9d3fa7cf60c3eb59ad0030e6099fa5c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724744"
---
# <a name="xsd-annotations-sqlxml-40"></a>XSD 주석(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  다음 표에서는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 도입된 XSD 주석과 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에 도입된 XDR 주석을 비교하여 보여 줍니다.  
  
|XSD 주석|설명|항목 링크|XDR 주석|  
|--------------------|-----------------|----------------|--------------------|  
|**sql:encode**|XML 요소나 특성이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB 열에 매핑된 경우 참조 URI를 요청할 수 있습니다. 이 URI는 나중에 BLOB 데이터를 반환하는 데 사용할 수 있습니다.|[Sql: encoding &#40;SQLXML 4.0&#41;를 사용 하 여 BLOB 데이터에 대 한 URL 참조 요청](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|**url-인코드**|  
|**sql: guid**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성된 GUID 값을 사용할지 아니면 해당 열의 updategram에 제공된 값을 사용할지를 지정할 수 있습니다.|[sql:identity 및 sql:guid 주석 사용](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|지원되지 않음|  
|**sql:hide**|스키마에 지정된 요소나 특성을 결과 XML 문서에서 숨깁니다.|[sql:hide를 사용하여 요소 및 특성 숨기기](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)|지원되지 않음|  
|**sql:identity**|IDENTITY 형식의 데이터베이스 열에 매핑되는 모든 노드에 지정할 수 있습니다. 이 주석에 지정하는 값은 데이터베이스의 해당되는 IDENTITY 형식 열이 업데이트되는 방법을 정의합니다.|[sql:identity 및 sql:guid 주석 사용](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|지원되지 않음|  
|**sql:inverse**|을 사용 하 여 지정 된 부모-자식 관계의 해석을 반전 하도록 updategram 논리에 지시 **\<sql:relationship>** 합니다.|[Sql: relationship에 sql: 역 특성 지정 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|지원되지 않음|  
|**sql:is-constant**|어느 테이블에도 매핑되지 않는 XML 요소를 만듭니다. 이 요소는 쿼리 출력에 나타납니다.|[Sql: is 상수 &#40;SQLXML 4.0&#41;를 사용 하 여 상수 요소를 만듭니다.](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|동일|  
|**sql:key-fields**|테이블의 행을 고유하게 식별하는 열을 지정할 수 있습니다.|[Sql: 키-필드 &#40;SQLXML 4.0&#41;를 사용 하 여 키 열 식별](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|동일|  
|**sql:limit-field**<br /><br /> **sql:limit-value**|제한 값을 기준으로 반환되는 값을 제한할 수 있습니다.|[Sql: limit 필드 및 sql: limit 값을 사용 하 여 값 필터링 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)|동일|  
|**sql:mapped**|스키마 항목을 결과에서 제외할 수 있습니다.|[Sql: mapped &#40;SQLXML 4.0&#41;를 사용 하 여 결과 XML 문서에서 스키마 요소 제외](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|**지도-필드**|  
|**sql:max-depth**|스키마에 지정된 재귀 관계의 깊이를 지정할 수 있습니다.|[sql:max-depth를 사용하여 재귀 관계의 깊이 지정](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|지원되지 않음|  
|**sql:overflow-field**|오버플로 데이터가 포함된 데이터베이스 열을 식별합니다.|[Sql: 오버플로 필드 &#40;SQLXML 4.0&#41;를 사용 하 여 사용 되지 않은 데이터를 검색 합니다.](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)|동일|  
|**sql:prefix**|유효한 XML ID, IDREF 및 IDREFS를 만들고 ID, IDREF 및 IDREFS 값 앞에 문자열을 추가합니다.|[Sql: prefix &#40;SQLXML 4.0&#41;를 사용 하 여 유효한 ID, IDREF 및 IDREFS 유형 특성 만들기](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|동일|  
|**sql:relationship**|XML 요소 사이의 관계를 지정합니다. **부모**, **자식**, **부모 키**및 **자식 키** 특성은 관계를 설정 하는 데 사용 됩니다.|[Sql: relationship &#40;SQLXML 4.0&#41;를 사용 하 여 관계 지정](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|다음과 같이 특성 이름이 다름<br /><br /> **키-관계**<br /><br /> **외래-관계**<br /><br /> **key**<br /><br /> **외래 키**|  
|**sql:use-cdata**|XML 문서의 특정 요소에 사용될 CDATA 섹션을 지정할 수 있습니다.|[Sql: use-cdata &#40;SQLXML 4.0&#41;를 사용 하 여 CDATA 섹션 만들기](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|동일|  
  
> [!NOTE]  
>  XSD 네이티브 **targetNamespace** 특성은 XDR 매핑 스키마에 정의 된 **대상 네임 스페이스** 주석을 대체 합니다 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] .  
  
## <a name="see-also"></a>참고 항목  
 [TargetNamespace 특성 &#40;사용 하 여 대상 네임 스페이스 지정&#41;SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
