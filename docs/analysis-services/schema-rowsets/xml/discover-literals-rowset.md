---
title: DISCOVER_LITERALS 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ed865f22291b3e2e47c4934e455e0e75795d35cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030354"
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자에서 지원되는 데이터 형식 및 값을 포함한 리터럴 정보를 반환합니다.  
  
 호출 하는 경우는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드는 **DISCOVER_LITERALS** 열거 값은 [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) 요소는 **Discover** 메서드가 반환 되는 **DISCOVER_LITERALS** 행 집합입니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_LITERALS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LiteralName**|**DBTYPE_WSTR**||행에 설명된 리터럴의 이름입니다.<br /><br /> 예를 들어: **DBLITERAL_LIKE_PERCENT**|  
|**LiteralValue**|**DBTYPE_WSTR**||실제 리터럴 값입니다.<br /><br /> 예를 들어 경우 **LiteralName** 은 **DBLITERAL_LIKE_PERCENT** 및 백분율 문자 (**%**) LIKE 절 값의에서 0 개 이상의 문자 일치 **LiteralValue** 열은 "**%**"입니다.|  
|**LiteralInvalidChars**|**DBTYPE_WSTR**||리터럴에 유효하지 않은 문자입니다.<br /><br /> 예를 들어 테이블 이름에 숫자 문자 이외의 무엇이 든 포함할 수, 하는 경우이 문자열은 "**0123456789**"입니다.|  
|**LiteralInvalidStartingChars**|**DBTYPE_WSTR**||리터럴의 첫 문자로 유효하지 않은 문자입니다. 리터럴이 모든 유효한 문자로 시작할 수, 하는 경우 이것이 **null**합니다.|  
|**LiteralMaxLength**|**DBTYPE_I4**||리터럴의 최대 문자 수입니다. 최대값이 없거나 최대값을 알 수 없으면 값은 -1입니다.|  
|**LiteralNameEnumValue**|**DBTYPE_I4**|||  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_LITERALS** 다음 테이블의 열에 행 집합으로 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**LiteralName**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS 행 집합 & #40; XMLA & #41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
