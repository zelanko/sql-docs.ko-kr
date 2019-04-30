---
title: xml 데이터 형식 지원 SQLXML 4.0에서 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1a0fa49a1dac16ed366c66c72f7d800ccc4aed8e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232711"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>SQLXML 4.0의 xml 데이터 형식 지원
  부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식의 지원 XML을 사용 하 여 데이터를 `xml` 데이터 형식입니다. 이 항목에서는 SQLXML 4.0에서 `xml` 데이터 형식의 인스턴스를 인식하고 이러한 인스턴스에 대한 지원을 구현하는 방법에 대해 설명합니다.  
  
## <a name="working-with-xml-data-types"></a>xml 데이터 형식 작업  
 SQL 테이블을 사용하여 `xml` 데이터 형식 열을 구현하는 방법에 대한 자세한 내용은 다음 예를 참조하십시오.  
  
|태스크|예제|항목|  
|----------|-------------|-----------|  
|XML 뷰에서 `xml` 열을 매핑하고 포함하는 방법|"XML 요소를 XML 데이터 형식 열에 매핑"|[기본 매핑의 XSD 요소 및 특성 테이블 및 열을 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|Updategram을 사용하여 `xml` 열에 데이터를 삽입하는 방법|"XML 데이터 형식 열에 데이터 삽입"|[XML Updategram을 사용 하 여 데이터를 삽입 합니다. &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|`xml` 열에 XML 데이터 대량 로드|"xml 데이터 형식 열에 대량 로드"|[XML 대량 로드 예 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>지침 및 제한 사항  
  
-   **\<xsd: 모든 >** 포함 하는 열에 매핑할 수 없습니다는 `xml` 데이터 형식입니다. SQLXML에서는 `sql:overflow-field` 주석을 통해 이 문제를 해결할 수 있습니다. 또는 `xml` 데이터 형식 필드를 `xsd:anyType`의 요소로 매핑하여 이 문제를 해결할 수도 있습니다. 이 해결 방법은 위의 테이블에 나와 있는 "XML 요소를 XML 데이터 형식 열에 매핑" 예에서 보여 줍니다.  
  
-   `xml` 데이터 형식 열의 내용에 대한 XPath 쿼리는 지원되지 않습니다.  
  
-   `xml` 데이터 형식 열이 지원되지 않거나(예: `sql:relationship` 및 `sql:key-fields`) 허용되지 않는 주석에서 이를 사용하면 SQLXML 4.0을 구현하는 중간 계층 구성 요소에 의해 포착되지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류가 발생합니다. 이는 SQLXML에 SQL 유형 정보가 필요 없기 때문에 발생합니다. 이 동작은 BLOB 및 이진 유형과 같은 다른 데이터 형식에 대한 SQLXML 동작과 비슷합니다.  
  
-   `xml` 열 매핑은 XSD 스키마에서만 지원됩니다. XDR 스키마에서는 `xml` 열 매핑이 지원되지 않습니다.  
  
-   SQLXML 4.0에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공되는 XML 구문 분석 지원을 사용합니다. `xml` 열은 형식화된 XML이나 형식화되지 않은 XML로 매핑될 수 있습니다. 두 경우 모두 SQLXML 4.0에서는 입력 XML의 유효성을 검사하지 않습니다.  입력 XML이 유효하지 않거나 잘못 작성된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 이를 SQLXML에 보고하고 서버에서 반환하는 관련 오류 정보를 사용자에게 전달합니다.  
  
-   SQLXML 4.0에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공되는 DTD에 대한 제한된 지원을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 기본값을 제공하고 엔터티 참조를 해당 확장 형식으로 바꾸는 데 사용할 수 있는 `xml` 데이터 형식 데이터의 내부 DTD를 허용합니다. SQLXML에서는 XML 데이터를 서버에 내부 DTD를 포함한 "있는 그대로" 전달합니다. 타사 도구를 사용하여 DTD를 XML 스키마(XSD) 문서로 변환하고 인라인 XML 스키마가 있는 데이터를 데이터베이스에 로드할 수 있습니다.  
  
-   SQLXML 4.0은 보존 하지 않습니다 XML 선언 처리 명령 (예:)의 동작에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 대신 XML 선언은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 파서에 대한 지시어로 처리되며 해당 특성(version, encoding 및 standalone)은 데이터가 `xml` 데이터 형식으로 변환된 다음 삭제됩니다. XML 데이터는 내부적으로 UCS-2로 저장됩니다. 다른 모든 XML 인스턴스 처리 명령은 보존됩니다. 따라서 이러한 처리 명령은 `xml` 열에서 허용되고 SQLXML에서 지원될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터&#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  
