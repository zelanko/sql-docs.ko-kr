---
title: XML for Analysis (XMLA) 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec0d843ac46cbcf5d032d1f93190869fd5a37cb2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241283"
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) 참조
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 클라이언트 응용 프로그램 및 Analysis Services 인스턴스 간의 모든 통신을 처리 하는 XML for Analysis (XMLA) 프로토콜을 사용 합니다. 가장 기본적인 수준에서 ADOMD.NET과 AMO 같은 기타 클라이언트 라이브러리는 XMLA에서 요청을 생성하고 응답을 디코딩하여 XMLA를 독점적으로 사용하는 Analysis Services 인스턴스의 매개자 역할을 합니다.  
  
 다차원 형식과 테이블 형식에서 검색 및 데이터 조작을 지원, XMLA 사양의 일반적으로 액세스 가능한 두 가지 메서드를 정의 [Discover](xml-elements-methods-discover.md) 하 고 [Execute](xml-elements-methods-execute.md), 및 XML 요소 및 데이터 형식의 컬렉션입니다. XML은 느슨하게 연결된 클라이언트 및 서버 아키텍처를 허용하므로 두 메서드 모두 XML 형식으로 들어오고 나가는 정보를 처리합니다. Analysis Services는 XMLA 1.1 사양과 호환되지만 `Discover` 및 `Execute` 메서드에서 주석으로 구현되는 데이터 정의 및 조작 기능을 포함하도록 해당 사양을 확장합니다. 확장된 XML 구문을 ASSL(Analysis Services Scripting Language)이라고 합니다. ASSL은 충돌 없이 XMLA 사양을 기반으로 작성됩니다. XMLA 기반 상호 운용성은 XMLA만 사용하건 XMLA와 ASSL을 모두 사용하건 간에 보장됩니다.  
  
 프로그래머는 솔루션 요구 사항에 XML, SOAP 및 HTTP 같은 표준 프로토콜이 지정되어 있는 경우 XMLA를 프로그래밍 인터페이스로 사용할 수 있습니다. 프로그래머와 관리자는 서버에서 정보를 검색하거나 명령을 실행하기 위해 임시로 XMLA를 사용할 수도 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[XML 요소 &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)|XMLA 사양의 요소를 설명합니다.|  
|[XML 데이터 형식 &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)|XMLA 사양의 데이터 형식을 설명합니다.|  
|[XML for Analysis 호환성 &#40;XMLA&#41;](xml-for-analysis-compliance-xmla.md)|XMLA 1.1 사양과의 호환성 수준에 대해 설명합니다.|  
  
## <a name="related-sections"></a>관련 섹션  
 [분석을 사용 하 여 개발 Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [XML for Analysis 스키마 행 집합](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [ADOMD.NET을 사용하여 개발](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [Analysis Management Objects를 사용 하 여 개발 &#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft OLAP 아키텍처 이해](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
