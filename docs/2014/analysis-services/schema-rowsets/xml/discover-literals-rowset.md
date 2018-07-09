---
title: DISCOVER_LITERALS 행 집합 | Microsoft Docs
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
api_name:
- DISCOVER_LITERALS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6bd59dfdc385775f0846a1a0f9de41f7d3bf2750
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259969"
---
# <a name="discoverliterals-rowset"></a>DISCOVER_LITERALS 행 집합
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자에서 지원되는 데이터 형식 및 값을 포함한 리터럴 정보를 반환합니다.  
  
 호출 하는 경우는 [검색](../../xmla/xml-elements-methods-discover.md) 메서드를 `DISCOVER_LITERALS` 열거 값을 [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) 요소를 `Discover` 메서드가 반환 되는 `DISCOVER_LITERALS` 행 집합입니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_LITERALS` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`LiteralName`|`DBTYPE_WSTR`||행에 설명된 리터럴의 이름입니다.<br /><br /> 예: `DBLITERAL_LIKE_PERCENT`|  
|`LiteralValue`|`DBTYPE_WSTR`||실제 리터럴 값입니다.<br /><br /> 예를 들어, `LiteralName`이 `DBLITERAL_LIKE_PERCENT`이고 퍼센트 문자(`%`)가 LIKE 절에서 0개 이상의 문자와 대응하면 `LiteralValue` 열의 값은 "`%`"입니다.|  
|`LiteralInvalidChars`|`DBTYPE_WSTR`||리터럴에 유효하지 않은 문자입니다.<br /><br /> 예를 들어, 테이블 이름에 숫자 문자 이외의 무엇이든 포함할 수 있으면 이 문자열은 "`0123456789`"입니다.|  
|`LiteralInvalidStartingChars`|`DBTYPE_WSTR`||리터럴의 첫 문자로 유효하지 않은 문자입니다. 리터럴이 모든 유효한 문자로 시작할 수 있으면 이것은 `null`입니다.|  
|`LiteralMaxLength`|`DBTYPE_I4`||리터럴의 최대 문자 수입니다. 최대값이 없거나 최대값을 알 수 없으면 값은 -1입니다.|  
|`LiteralNameEnumValue`|`DBTYPE_I4`|||  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DISCOVER_LITERALS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`LiteralName`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_KEYWORDS 행 집합 &#40;XMLA&#41;](discover-keywords-rowset-xmla.md)  
  
  
