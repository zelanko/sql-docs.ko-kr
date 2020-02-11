---
title: 'Sql: relationship (SQLXML)에서 sql: 역 특성 설정'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9da456ddb234ed4ec8e0d2a0f2ad8e8ad7250682
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246845"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>sql:relationship에 sql:inverse 특성 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Sql: 역함수** 특성은 XSD 스키마를 대량 로드 또는 updategram에 사용 하는 경우에만 유용 합니다. Sql: **역** 특성은 ** \<sql: relationship>** 요소에 지정할 수 있습니다. Updategram에서 updategram 논리는 스키마를 해석하여 updategram 작업으로 업데이트되는 테이블 및 열을 결정합니다. 스키마에 지정하는 부모-자식 관계에 따라 레코드가 수정(삽입 또는 삭제)되는 순서가 결정됩니다.  
  
 부모-자식 관계가 해당 데이터베이스 열 간의 기본 키/외래 키 관계의 역순으로 지정된 XSD 스키마가 있는 경우 기본 키/외래 키 위반 때문에 삽입 또는 삭제 Updategram 작업이 실패합니다. 이러한 경우 sql: ** \<relationship>** 요소에 **sql: 역** 특성이 지정 되 고 (**sql: 역 = "true"**) updategram 논리는 스키마에 지정 된 부모-자식 관계의 해석을 반대 합니다.  
  
 **Sql: 역** 특성은 부울 값 (0 = false, 1 = true)을 사용 합니다. 허용되는 값은 0, 1, true 및 false입니다.  
  
 **Sql: 역** 주석을 사용 하는 작업 예제는 [Updategram에서 주석이 추가 된 매핑 스키마 지정](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Sql: relationship &#40;SQLXML 4.0&#41;를 사용 하 여 관계 지정](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
