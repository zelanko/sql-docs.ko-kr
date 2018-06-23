---
title: DISCOVER_KEYWORDS 행 집합 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DISCOVER_KEYWORDS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: df7fd7c6bf7dbe9ebd0bb9057b5c82dc351afab3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088709"
---
# <a name="discoverkeywords-rowset-xmla"></a>DISCOVER_KEYWORDS 행 집합(XMLA)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자에 예약된 키워드에 대한 정보를 반환합니다.  
  
 호출 하는 경우는 [Discover](../../xmla/xml-elements-methods-discover.md) 사용 하 여 메서드는 `DISCOVER_KEYWORDS` 열거 값은 [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) 요소는 `Discover` 메서드가 반환 되는 `DISCOVER_KEYWORDS` 행 집합.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_KEYWORDS` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Keyword`|`DBTYPE_WSTR`||공급자에서 예약된 모든 키워드 목록입니다.<br /><br /> 예: `AND`|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DISCOVER_KEYWORDS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`Keyword`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_LITERALS 행 집합](discover-literals-rowset.md)  
  
  