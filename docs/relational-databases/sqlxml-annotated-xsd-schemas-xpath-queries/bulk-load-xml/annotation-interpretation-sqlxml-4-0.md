---
title: 주석 해석 (SQLXML)
description: SQLXML 4.0의 XML 대량 로드가 XSD 및 XDR 스키마의 주석을 해석 하는 방법에 대해 알아봅니다.
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9dabbbce21727203e9e7641587490ba03876727f
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84884416"
---
# <a name="annotation-interpretation-sqlxml-40"></a>주석 해석(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 섹션의 항목에서는 XML 대량 로드가 XSD 스키마의 주석을 해석하는 방법에 대해 설명합니다. 여기서 설명하는 동작은 XDR 스키마의 주석에도 적용됩니다.  
  
> [!NOTE]  
>  이 항목의 내용은 XML 대량 로드에서 처리 시 사용하는 주석에 대해서만 설명합니다. SQLXML 4.0에서 지원 되는 XSD 스키마에 대 한 전체 주석 목록은 [Xsd 스키마에서 주석 사용 &#40;sqlxml 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)을 참조 하세요. XDR 스키마에 대해 지원 되는 주석 목록은 [SQLXML 4.0&#41;에서 사용 되지 &#40;주석이 추가 된 Xdr 스키마 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [sql: relationship 및 키 순서 지정 규칙 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 **Sql: relationship** 주석이 XML 대량 로드에서 해석 되는 방법에 대해 설명 합니다.  
  
 [sql: 매핑된 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 **Sql: mapped** 주석이 XML 대량 로드에서 해석 되는 방법에 대해 설명 합니다.  
  
 [sql: limit 필드 및 sql: limit 값 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 **Sql: limit 필드** 및 **sql: LIMIT 값** 주석이 XML 대량 로드에서 해석 되는 방법에 대해 설명 합니다.  
  
 [sql: 오버플로 필드 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 **Sql: 오버플로** 주석이 XML 대량 로드에서 해석 되는 방법에 대해 설명 합니다.  
  
 [SQLXML 4.0 &#40;다른 주석&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 XML 대량 로드에서 다음 주석을 해석 하는 방법에 대해 설명 합니다. **sql: id-접두사**, **sql: use-cdata**, **sql: url-인코드**, **sql:-매핑-스키마**, **sql: 키-필드**.  
  
  
