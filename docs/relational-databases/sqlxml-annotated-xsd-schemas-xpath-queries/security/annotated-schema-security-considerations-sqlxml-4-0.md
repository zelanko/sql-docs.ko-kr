---
title: 주석이 추가 된 스키마 보안 고려 사항 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87af92866658e2fa5b4f8648e2a22dbf3d1cb13f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75252507"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>주석 스키마 보안 고려 사항(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  다음은 주석 스키마를 사용하기 위한 보안 지침입니다.  
  
-   매핑 스키마에서는 기본 매핑 사용을 사용하지 마십시오. 기본 매핑은 기본적으로 요소 이름을 테이블 이름에 매핑하고 특성 이름을 열 이름에 매핑하므로 결과 XML 문서에서 데이터베이스 정보(테이블 및 열 이름)가 공개됩니다. 따라서 XML 문서를 보는 모든 사용자가 데이터베이스의 테이블 및 열 정보에 액세스할 수 있으므로 보안 문제가 발생할 수 있습니다. 이러한 위험을 방지하려면 스키마에 임의의 요소 및 특성 이름을 지정하고 주석을 사용하여 이를 명시적으로 테이블 및 열에 매핑하십시오. XSD 스키마를 만들 때 기본 매핑을 사용 하는 방법에 대 한 자세한 내용은 [SQLXML 4.0&#41;&#40;테이블 및 열에 대 한 Xsd 요소 및 특성의 기본 매핑 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)을 참조 하세요.  
  
-   주석을 사용하여 명시적 매핑을 지정하면 테이블 이름 및 열 이름과 같은 데이터베이스 정보가 공개됩니다. 따라서 이러한 스키마가 공개되지 않도록 해야 합니다.  
  
-   재귀를 사용 하 여 매핑 스키마에 대해 지정 된 것과 같은 특정 쿼리 ( **최대 깊이** 주석 집합을 더 높은 값으로 지정)는 실행 하는 데 시간이 더 오래 걸릴 수 있습니다. 선택적으로 명령 제한 시간 속성을 설정 하 여 제한 시간을 지정할 수 있습니다 (초 단위). 다음은 그 예입니다.  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [SQLXML 4.0의 주석이 추가된 XSD 스키마](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
