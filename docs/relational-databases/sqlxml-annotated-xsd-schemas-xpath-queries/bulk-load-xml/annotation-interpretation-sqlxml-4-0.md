---
title: 주석 해석 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 80db781d32c8d48f9df48c27baa1807eef5a9f7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054393"
---
# <a name="annotation-interpretation-sqlxml-40"></a>주석 해석(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 섹션의 항목에서는 XML 대량 로드가 XSD 스키마의 주석을 해석하는 방법에 대해 설명합니다. 여기서 설명하는 동작은 XDR 스키마의 주석에도 적용됩니다.  
  
> [!NOTE]  
>  이 항목의 내용은 XML 대량 로드에서 처리 시 사용하는 주석에 대해서만 설명합니다. SQLXML 4.0에서 지원 되는 XSD 스키마에 대 한 주석의 전체 목록은 참조 하세요 [XSD 스키마에서 주석을 사용 하 여 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)합니다. XDR 스키마에 대 한 지원 되는 주석 목록은 참조 하세요 [주석이 추가 된 XDR 스키마 &#40;SQLXML 4.0에서 사용 되지 않음&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [sql: relationship 및 키 순서 지정 규칙 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 에 대해 설명 하는 방법을 **sql: relationship** XML 대량 로드에서 주석을 해석 됩니다.  
  
 [sql: 매핑된 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 에 대해 설명 하는 방법을 **sql: 매핑된** XML 대량 로드에서 주석을 해석 됩니다.  
  
 [sql:-필드와-값 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 에 대해 설명 하는 방법을 **sql:-필드** 하 고 **sql:-값** XML 대량 로드에서 주석을 해석 됩니다.  
  
 [sql:overflow-필드 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 에 대해 설명 하는 방법을 **sql:overflow** XML 대량 로드에서 주석을 해석 됩니다.  
  
 [다른 주석은 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 XML 대량 로드에서 다음 주석이 해석 되는 방법에 대해 설명 합니다. **그것이-접두사**, **sql:use-cdata**를 **sql:url-인코딩**, **sql: -매핑-스키마**하십시오 **sql:-필드**합니다.  
  
  
