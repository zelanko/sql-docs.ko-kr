---
title: XML for Analysis (XMLA) 참조 | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e8c3645175d8d1f3251fd621825f5a542669cbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576765"
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) 참조
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]   

Azure Analysis Services 및 SQL Server Analysis Services 클라이언트 응용 프로그램 및 Analysis Services 인스턴스 간의 통신을 위해 Analysis (XMLA) 프로토콜에 대 한 XML을 사용합니다. 가장 기본적인 수준에서 ADOMD.NET과 AMO 같은 기타 클라이언트 라이브러리는 XMLA에서 요청을 생성하고 응답을 디코딩하여 XMLA를 독점적으로 사용하는 Analysis Services 인스턴스의 매개자 역할을 합니다.  
  
 XMLA 사양의 검색 및 조작을 데이터의 테이블 형식 및 다차원 모드를 지원 하려면 일반적으로 액세스 가능한 두 개의 메서드를 정의 [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) 및 [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md), 및 XML 요소 및 데이터 형식의 컬렉션입니다. XML은 느슨하게 연결된 클라이언트 및 서버 아키텍처를 허용하므로 두 메서드 모두 XML 형식으로 들어오고 나가는 정보를 처리합니다. 

Analysis Services는 XMLA 1.1 사양과 사양에 동시에 주석으로 구현 데이터 정 및 조작 기능을 포함 하도록 확장 된 **Discover** 및 **Execute** 메서드. 확장 된 XML 구문에는 스크립팅 언어 TMSL (Tabular Model) 및 Analysis Services Scripting Language (ASSL)입니다. 

TMSL은 호환성 수준 1200 이상에서 테이블 형식 모델 데이터베이스에 대 한 명령 및 개체 모델 정의 구문입니다. TMSL은 XMLA 프로토콜을 통해 Analysis Services와 통신 합니다. 여기서는 `XMLA.Execute` TMSL의 두 문은 JSON 기반 스크립트 뿐만 아니라 Analysis Services Scripting Language (ASSL XMLA에 대 한)의 기존 XML 기반 스크립트를 허용 하는 h o 합니다. 자세한 내용은 참고 [스크립팅 언어 TMSL (Tabular Model) 참조](../tabular-model-scripting-language-tmsl-reference.md)합니다.

ASSL은 호환성 수준 1103 이하의 테이블 형식 모드 데이터베이스 및 다차원 모델 데이터베이스에 대 한 명령 및 개체 모델 정의 구문입니다. 이 정의 충돌 없이 XMLA 사양을 작성 합니다. XMLA 기반 상호 운용성은 XMLA만 사용하건 XMLA와 ASSL을 모두 사용하건 간에 보장됩니다. 자세한 내용은 참고 [Analysis Services Scripting Language (ASSL XMLA에 대 한)](../scripting/analysis-services-scripting-language-assl-for-xmla.md)합니다.
  
 개발자는 XML, SOAP 및 HTTP와 같은 표준 프로토콜을 지정 하는 솔루션 요구 사항 인터페이스로 XMLA 사용할 수 있습니다. 개발자와 관리자가 사용할 수도 XMLA 임시 트랜잭션이란에 서버에서 정보를 검색 하거나 명령을 실행 합니다. 
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[XML 데이터 형식(XMLA)](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|XMLA 사양의 데이터 형식을 설명합니다.|  
|[XML 요소-명령 (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Execute 메서드를 호출 하는 동안 Command 요소 내에서 사용할 수 있는 요소입니다.|  
|[XML 요소-명령 (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Execute 메서드를 호출 하는 동안 Command 요소 내에서 사용할 수 있는 요소입니다.|  
|[XML 요소-헤더 (XMLA)](../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)| Microsoft Analysis Services에서 구현 되는 헤더 요소입니다.|  
|[XML 요소-속성 (XMLA)](../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)| 속성 정보 및 XMLA 헤더, 메서드, 개체, 명령 및 데이터 형식에 대 한 값을 나타낼 수 있는 요소입니다.|  
|[-방법-XML 요소 (XMLA)를 검색합니다.](../../analysis-services/xmla/xml-elements-methods-discover.md)| Analysis Services의 인스턴스에서 특정 개체에 대 한 정보 또는 사용 가능한 데이터베이스 목록과 같은 정보를 검색합니다.|  
|[XML 요소 방법-실행 (XMLA)](../../analysis-services/xmla/xml-elements-methods-execute.md)| Analysis Services의 인스턴스로 Analysis (XMLA) 명령에 대 한 XML을 보냅니다.|  
|[XML 요소 개체-DiscoverResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)| Discover 메서드 호출에 대 한 응답으로 Analysis Services의 인스턴스에서 반환 되는 정보를 포함 합니다.|  
|[XML 요소 개체-ExecuteResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)| Execute 메서드 호출에 대 한 응답으로 Analysis Services의 인스턴스에서 반환 되는 정보를 포함 합니다.|  
|[XML 요소-개체 (XMLA)](../../analysis-services/xmla/xml-elements-objects.md)| Analysis Services에서 구현 하는 개체입니다.|  
|[XMLA(XML for Analysis) 준수](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|XMLA 1.1 사양과의 호환성 수준에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고자료
 [XML for Analysis 스키마 행 집합](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
 [ADOMD.NET을 사용하여 개발](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 [AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
