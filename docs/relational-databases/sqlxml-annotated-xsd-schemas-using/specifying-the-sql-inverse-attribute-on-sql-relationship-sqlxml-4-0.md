---
title: "Sql: relationship (SQLXML 4.0)에 sql: inverse 특성 지정 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90a2021f9fb72a22870c834730b50c9aa27af796
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>sql:relationship에 sql:inverse 특성 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]**sql: inverse** 특성은 사용한 경우에 XSD 스키마는 대량 로드 용이나 updategram에서 유용 합니다. **sql: inverse** 특성에 지정할 수 있습니다는  **\<sql: relationship >** 요소입니다. Updategram에서 updategram 논리는 스키마를 해석하여 updategram 작업으로 업데이트되는 테이블 및 열을 결정합니다. 스키마에 지정하는 부모-자식 관계에 따라 레코드가 수정(삽입 또는 삭제)되는 순서가 결정됩니다.  
  
 부모-자식 관계가 해당 데이터베이스 열 간의 기본 키/외래 키 관계의 역순으로 지정된 XSD 스키마가 있는 경우 기본 키/외래 키 위반 때문에 삽입 또는 삭제 Updategram 작업이 실패합니다. 이러한 경우에는 **sql: inverse** 특성이 지정 된 (**sql: inverse = "true"**)에  **\<sql: relationship >** 요소 및 updategram 논리 반대로 스키마에 지정 된 부모-자식 관계의 해석 합니다.  
  
 **sql: inverse** 특성은 부울 값 (0 = false, 1 = true). 허용되는 값은 0, 1, true 및 false입니다.  
  
 사용 하 여 작업 예제에 대 한는 **sql: inverse** 주석을 참조 [Updategram에 주석이 추가 된 매핑 스키마 지정](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Sql: relationship을 사용 하 여 관계 &#40;를 지정합니다. SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
