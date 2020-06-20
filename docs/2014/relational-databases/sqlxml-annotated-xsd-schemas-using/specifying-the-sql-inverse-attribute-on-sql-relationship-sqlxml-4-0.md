---
title: 'Sql: relationship에 sql: 역 특성 지정 (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- bulk load [SQLXML]
- inverse attribute
- relationships [SQLXML], inverse orders
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- updategrams [SQLXML], relationships
- sql:inverse
ms.assetid: 08904cbd-9c86-493d-90c3-f5e1d13ce59d
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b0781102371b98cced72a5a0edee70c9567c372
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003066"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>sql:relationship에 sql:inverse 특성 지정(SQLXML 4.0)
  `sql:inverse` 특성은 XSD 스키마를 대량 로드용이나 updategram에서 사용할 경우에만 유용합니다. `sql:inverse`요소에 특성을 지정할 수 있습니다 **\<sql:relationship>** . Updategram에서 updategram 논리는 스키마를 해석하여 updategram 작업으로 업데이트되는 테이블 및 열을 결정합니다. 스키마에 지정하는 부모-자식 관계에 따라 레코드가 수정(삽입 또는 삭제)되는 순서가 결정됩니다.  
  
 부모-자식 관계가 해당 데이터베이스 열 간의 기본 키/외래 키 관계의 역순으로 지정된 XSD 스키마가 있는 경우 기본 키/외래 키 위반 때문에 삽입 또는 삭제 Updategram 작업이 실패합니다. 이러한 경우 `sql:inverse` 요소에 특성이 지정 되 고 ( `sql:inverse="true"` ) **\<sql:relationship>** updategram 논리는 스키마에 지정 된 부모-자식 관계의 해석을 반대 합니다.  
  
 `sql:inverse` 특성은 부울 값(0=false, 1=true)을 사용합니다. 허용되는 값은 0, 1, true 및 false입니다.  
  
 주석을 사용 하는 작업 예제는 `sql:inverse` [Updategram에서 주석이 추가 된 매핑 스키마 지정](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Sql: relationship &#40;SQLXML 4.0&#41;를 사용 하 여 관계 지정](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
