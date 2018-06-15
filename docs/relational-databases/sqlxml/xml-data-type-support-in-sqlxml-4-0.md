---
title: xml 데이터 형식 지원 SQLXML 4.0에서 | Microsoft Docs
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
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 68cb00ced8f77b5921be07a3f6383d4436f0bade
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973228"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>SQLXML 4.0의 xml 데이터 형식 지원
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 XML 데이터를 사용 하 여 입력의 **xml** 데이터 형식입니다. 이 항목에서는 SQLXML 4.0의 인스턴스를 인식 하는 방법에 대 한 정보는 **xml** 데이터 형식과 구현 지원 합니다.  
  
## <a name="working-with-xml-data-types"></a>xml 데이터 형식 작업  
 구현 하는 SQL 테이블을 사용 하는 방법에 대 한 자세한 **xml** 데이터 형식 열을 다음과 같은 예가 제공 됩니다.  
  
|태스크|예제|항목|  
|----------|-------------|-----------|  
|매핑하고 포함 하는 방법 한 **xml** XML 보기에서 열|"XML 요소를 XML 데이터 형식 열에 매핑"|[테이블 및 열에 XSD 요소와 특성의 기본 매핑이 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|데이터를 삽입 하는 방법 한 **xml** updategram으로 열|"XML 데이터 형식 열에 데이터 삽입"|[XML Updategram을 사용 하 여 데이터 삽입 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|에 대 한 XML 데이터 대량 로드는 **xml** 열|"xml 데이터 형식 열에 대량 로드"|[XML 대량 로드 예 & #40; SQLXML 4.0 & #41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>지침 및 제한 사항  
  
-   **\<xsd: 모든 >** 포함 하 여 열에 매핑할 수 없습니다는 **xml** 데이터 형식입니다. 이 시나리오를 통해 제공 됩니다에 대 한 SQLXML에서 지원은 **sql:overflow-필드** 주석입니다. 매핑하는 또 다른 방법은 **xml** 데이터 형식 필드의 요소로 **: anytype**합니다. 이 해결 방법은 위의 테이블에 나와 있는 "XML 요소를 XML 데이터 형식 열에 매핑" 예에서 보여 줍니다.  
  
-   내용에 대 한 XPath 쿼리 **xml** 데이터 형식 열이 지원 되지 않습니다.  
  
-   사용 하는 **xml** 지원 되지 않습니다는 주석에서 데이터 형식 열 (같은 **sql: relationship** 및 **sql:-필드**)에 허용 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류를 SQLXML 4.0을 구현 하는 중간 계층 구성 요소에 의해 포착 되지 것입니다. 이는 SQLXML에 SQL 유형 정보가 필요 없기 때문에 발생합니다. 이 동작은 BLOB 및 이진 유형과 같은 다른 데이터 형식에 대한 SQLXML 동작과 비슷합니다.  
  
-   매핑 **xml** 열 XSD 스키마에 대해서만 지원 됩니다. XDR 스키마 매핑을 지원 하지 않는 **xml** 열입니다.  
  
-   SQLXML 4.0에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공되는 XML 구문 분석 지원을 사용합니다. **xml** 열 하거나 형식화 된 XML 또는 형식화 되지 않은 XML로 매핑할 수 있습니다. 두 경우 모두 SQLXML 4.0에서는 입력 XML의 유효성을 검사하지 않습니다.  입력 XML이 유효하지 않거나 잘못 작성된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 이를 SQLXML에 보고하고 서버에서 반환하는 관련 오류 정보를 사용자에게 전달합니다.  
  
-   SQLXML 4.0에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공되는 DTD에 대한 제한된 지원을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 DTD를 고려한 **xml** 데이터에는 기본값을 제공 하 고 엔터티 참조를 해당 확장 대체를 사용할 수 있는 데이터를 입력 합니다. SQLXML에서는 XML 데이터를 서버에 내부 DTD를 포함한 "있는 그대로" 전달합니다. 타사 도구를 사용하여 DTD를 XML 스키마(XSD) 문서로 변환하고 인라인 XML 스키마가 있는 데이터를 데이터베이스에 로드할 수 있습니다.  
  
-   SQLXML 4.0은 보존 하지 않습니다 XML 선언 처리 명령 (예:)의 동작에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. XML 선언에 대 한 지시어로 취급 됩니다 대신는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 파서와 해당 특성 (예: 버전, 인코딩 및 독립 실행형)이 손실에 데이터를 변환한 후의 **xml** 데이터 형식입니다. XML 데이터는 내부적으로 UCS-2로 저장됩니다. XML 인스턴스의 다른 모든 처리 명령은 유지 됩니다. 에 허용 되는 **xml** 열을 SQLXML에서 지원 될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
