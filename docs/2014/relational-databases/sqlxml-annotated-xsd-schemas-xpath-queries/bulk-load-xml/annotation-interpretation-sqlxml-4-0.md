---
title: 주석 해석 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ba4c9e6506b67802a8a9571df80ff4db7d2b3934
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091466"
---
# <a name="annotation-interpretation-sqlxml-40"></a>주석 해석(SQLXML 4.0)
  이 섹션의 항목에서는 XML 대량 로드가 XSD 스키마의 주석을 해석하는 방법에 대해 설명합니다. 여기서 설명하는 동작은 XDR 스키마의 주석에도 적용됩니다.  
  
> [!NOTE]  
>  이 항목의 내용은 XML 대량 로드에서 처리 시 사용하는 주석에 대해서만 설명합니다. SQLXML 4.0에서 지 원하는 XSD 스키마에 대 한 주석 목록은 전체 참조 [XSD 스키마에서 주석을 사용 하 여 &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)합니다. XDR 스키마에 대 한 지원 되는 주석 목록, 참조 [주석이 추가 된 XDR 스키마 &#40;SQLXML 4.0에서 더 이상 사용&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [sql: relationship 및 키 순서 지정 규칙 &#40;SQLXML 4.0&#41;](annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 XML 대량 로드에서 `sql:relationship` 주석이 해석되는 방법에 대해 설명합니다.  
  
 [sql: 매핑된 &#40;SQLXML 4.0&#41;](annotation-interpretation-sql-mapped.md)  
 XML 대량 로드에서 `sql:mapped` 주석이 해석되는 방법에 대해 설명합니다.  
  
 [sql:-필드 및 sql:-값 &#40;SQLXML 4.0&#41;](annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 XML 대량 로드에서 `sql:limit-field` 및 `sql:limit-value` 주석이 해석되는 방법에 대해 설명합니다.  
  
 [sql:overflow-필드 &#40;SQLXML 4.0&#41;](annotation-interpretation-sql-overflow-field.md)  
 XML 대량 로드에서 `sql:overflow` 주석이 해석되는 방법에 대해 설명합니다.  
  
 [기타 주석 &#40;SQLXML 4.0&#41;](annotation-interpretation-other-annotations.md)  
 XML 대량 로드에서 다음 주석이 해석 되는 방법에 대해 설명: `sql:id-prefix`, `sql:use-cdata`, `sql:url-encode`, `sql:is-mapping-schema`, `sql:key-fields`합니다.  
  
  