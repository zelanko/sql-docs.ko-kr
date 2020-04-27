---
title: XSD 주석 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9e50cc418ef1fa2076b3207d7d3429694f160a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013552"
---
# <a name="xsd-annotations-sqlxml-40"></a>XSD 주석(SQLXML 4.0)
  다음 표에서는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 도입된 XSD 주석과 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에 도입된 XDR 주석을 비교하여 보여 줍니다.  
  
|XSD 주석|설명|항목 링크|XDR 주석|  
|--------------------|-----------------|----------------|--------------------|  
|`sql:encode`|XML 요소나 특성이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB 열에 매핑된 경우 참조 URI를 요청할 수 있습니다. 이 URI는 나중에 BLOB 데이터를 반환하는 데 사용할 수 있습니다.|[Sql: encoding &#40;SQLXML 4.0&#41;를 사용 하 여 BLOB 데이터에 대 한 URL 참조 요청](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|`url-encode`|  
|`sql:guid`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성된 GUID 값을 사용할지 아니면 해당 열의 updategram에 제공된 값을 사용할지를 지정할 수 있습니다.|[sql:identity 및 sql:guid 주석 사용](using-the-sql-identity-and-sql-guid-annotations.md)|지원되지 않음|  
|`sql:hide`|스키마에 지정된 요소나 특성을 결과 XML 문서에서 숨깁니다.|[sql:hide를 사용하여 요소 및 특성 숨기기](hiding-elements-and-attributes-by-using-sql-hide.md)|지원되지 않음|  
|`sql:identity`|IDENTITY 형식의 데이터베이스 열에 매핑되는 모든 노드에 지정할 수 있습니다. 이 주석에 지정하는 값은 데이터베이스의 해당되는 IDENTITY 형식 열이 업데이트되는 방법을 정의합니다.|[sql:identity 및 sql:guid 주석 사용](using-the-sql-identity-and-sql-guid-annotations.md)|지원되지 않음|  
|`sql:inverse`|Updategram 논리에 ** \<sql: relationship>** 를 사용 하 여 지정 된 부모-자식 관계의 해석을 반전 하도록 지시 합니다.|[Sql: relationship에 sql: 역 특성 지정 &#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|지원되지 않음|  
|`sql:is-constant`|어느 테이블에도 매핑되지 않는 XML 요소를 만듭니다. 이 요소는 쿼리 출력에 나타납니다.|[Sql: is 상수 &#40;SQLXML 4.0&#41;를 사용 하 여 상수 요소를 만듭니다.](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|동일|  
|`sql:key-fields`|테이블의 행을 고유하게 식별하는 열을 지정할 수 있습니다.|[Sql: 키-필드 &#40;SQLXML 4.0&#41;를 사용 하 여 키 열 식별](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|동일|  
|`sql:limit-field`<br /><br /> `sql:limit-value`|제한 값을 기준으로 반환되는 값을 제한할 수 있습니다.|[Sql: limit 필드 및 sql: limit 값을 사용 하 여 값 필터링 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)|동일|  
|`sql:mapped`|스키마 항목을 결과에서 제외할 수 있습니다.|[Sql: mapped &#40;SQLXML 4.0&#41;를 사용 하 여 결과 XML 문서에서 스키마 요소 제외](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|`map-field`|  
|`sql:max-depth`|스키마에 지정된 재귀 관계의 깊이를 지정할 수 있습니다.|[sql:max-depth를 사용하여 재귀 관계의 깊이 지정](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|지원되지 않음|  
|`sql:overflow-field`|오버플로 데이터가 포함된 데이터베이스 열을 식별합니다.|[Sql: 오버플로 필드 &#40;SQLXML 4.0&#41;를 사용 하 여 사용 되지 않은 데이터를 검색 합니다.](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)|동일|  
|`sql:prefix`|유효한 XML ID, IDREF 및 IDREFS를 만들고 ID, IDREF 및 IDREFS 값 앞에 문자열을 추가합니다.|[Sql: prefix &#40;SQLXML 4.0&#41;를 사용 하 여 유효한 ID, IDREF 및 IDREFS 유형 특성 만들기](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|동일|  
|`sql:relationship`|XML 요소 사이의 관계를 지정합니다. 관계는 `parent`, `child`, `parent-key` 및 `child-key` 특성을 사용하여 설정합니다.|[Sql: relationship &#40;SQLXML 4.0&#41;를 사용 하 여 관계 지정](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|다음과 같이 특성 이름이 다름<br /><br /> `key-relation`<br /><br /> `foreign-relation`<br /><br /> `key`<br /><br /> `foreign-key`|  
|`sql:use-cdata`|XML 문서의 특정 요소에 사용될 CDATA 섹션을 지정할 수 있습니다.|[Sql: use-cdata &#40;SQLXML 4.0&#41;를 사용 하 여 CDATA 섹션 만들기](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|동일|  
  
> [!NOTE]  
>  XSD 기본 `targetNamespace` 특성은 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] XDR 매핑 스키마에 도입된 `target-namespace` 주석을 대체합니다.  
  
## <a name="see-also"></a>참고 항목  
 [TargetNamespace 특성 &#40;사용 하 여 대상 네임 스페이스 지정&#41;SQLXML 4.0](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
