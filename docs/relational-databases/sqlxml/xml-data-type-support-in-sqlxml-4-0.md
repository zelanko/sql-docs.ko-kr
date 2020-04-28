---
title: SQLXML 4.0의 xml 데이터 형식 지원
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4c56efd6c79b7ce7d74af621963f4b12e734d5f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75252166"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>SQLXML 4.0의 xml 데이터 형식 지원
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  부터은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]xml [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 사용 하 **여 xml 형식의** 데이터를 지원 합니다. 이 항목에서는 SQLXML 4.0에서 **xml** 데이터 형식의 인스턴스를 인식 하 고이에 대 한 지원을 구현 하는 방법에 대 한 정보를 제공 합니다.  
  
## <a name="working-with-xml-data-types"></a>xml 데이터 형식 작업  
 **Xml** 데이터 형식 열을 구현 하는 SQL 테이블을 사용 하는 방법에 대해 자세히 알아보려면 다음 예를 제공 합니다.  
  
|작업|예제|항목|  
|----------|-------------|-----------|  
|Xml 뷰에 **xml** 열을 매핑하고 포함 하는 방법|"XML 요소를 XML 데이터 형식 열에 매핑"|[SQLXML 4.0 &#40;테이블 및 열에 대 한 XSD 요소 및 특성의 기본 매핑&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Updategram을 사용 하 여 **xml** 열에 데이터를 삽입 하는 방법|"XML 데이터 형식 열에 데이터 삽입"|[XML Updategrams &#40;SQLXML 4.0&#41;를 사용 하 여 데이터 삽입](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|**Xml 열에** xml 데이터 대량 로드|"xml 데이터 형식 열에 대량 로드"|[XML 대량 로드 예 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>지침 및 제한 사항  
  
-   **xsd: 모든>xml 데이터 형식을 포함 하는 열에 매핑할 수 없습니다. \<** **xml** SQLXML에서이 시나리오에 대 한 지원은 **sql: 오버플로 필드** 주석을 통해 제공 됩니다. 또 다른 해결 방법은 **xml** 데이터 형식 필드를 **xsd: anyType**의 요소로 매핑하는 것입니다. 이 해결 방법은 위의 테이블에 나와 있는 "XML 요소를 XML 데이터 형식 열에 매핑" 예에서 보여 줍니다.  
  
-   **Xml** 데이터 형식 열의 내용에 대 한 XPath 쿼리는 지원 되지 않습니다.  
  
-   지원 되지 않는 주석을 사용 하는 xml 데이터 형식 열 (예: **sql: relationship** 및 **sql: 키-필드**) 또는 허용 된 **xml** 데이터 형식 열 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 사용 하면 SQLXML 4.0을 구현 하는 중간 계층 구성 요소에서 오류가 발생 하지 않습니다. 이는 SQLXML에 SQL 유형 정보가 필요 없기 때문에 발생합니다. 이 동작은 BLOB 및 이진 유형과 같은 다른 데이터 형식에 대한 SQLXML 동작과 비슷합니다.  
  
-   **Xml** 열 매핑은 XSD 스키마에 대해서만 지원 됩니다. XDR 스키마는 **xml** 열 매핑을 지원 하지 않습니다.  
  
-   SQLXML 4.0에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공되는 XML 구문 분석 지원을 사용합니다. **Xml** 열은 형식화 된 xml 또는 형식화 되지 않은 xml로 매핑될 수 있습니다. 두 경우 모두 SQLXML 4.0에서는 입력 XML의 유효성을 검사하지 않습니다.  입력 XML이 유효하지 않거나 잘못 작성된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 이를 SQLXML에 보고하고 서버에서 반환하는 관련 오류 정보를 사용자에게 전달합니다.  
  
-   SQLXML 4.0에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공되는 DTD에 대한 제한된 지원을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** 데이터 형식 데이터의 내부 DTD를 허용 합니다 .이 데이터를 사용 하 여 기본 값을 제공 하 고 엔터티 참조를 해당 확장 내용으로 바꿀 수 있습니다. SQLXML에서는 XML 데이터를 서버에 내부 DTD를 포함한 "있는 그대로" 전달합니다. 타사 도구를 사용하여 DTD를 XML 스키마(XSD) 문서로 변환하고 인라인 XML 스키마가 있는 데이터를 데이터베이스에 로드할 수 있습니다.  
  
-   SQLXML 4.0는의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]동작에 따라 XML 선언 처리 명령 (예:)을 유지 하지 않습니다. 대신 xml 선언은 xml 파서에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 지시어로 처리 되며, 데이터를 **xml** 데이터 형식으로 변환한 후에는 해당 특성 (버전, 인코딩 및 독립 실행형)이 손실 됩니다. XML 데이터는 내부적으로 UCS-2로 저장됩니다. XML 인스턴스의 다른 모든 처리 명령은 유지 됩니다. 이러한 열은 **xml** 열에서 허용 되며 SQLXML에서 지원할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
