---
title: DISCOVER_ENUMERATORS 행 집합 | Microsoft Docs
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
- DISCOVER_ENUMERATORS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2c4eb36f93faba7f32352de41d5c6fde4e0dac2c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184358"
---
# <a name="discoverenumerators-rowset"></a>DISCOVER_ENUMERATORS 행 집합
  특정 데이터 원본에 대해 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자에서 지원하는 열거자의 이름, 데이터 형식 및 열거 값 목록을 반환합니다. XMLA 공급자는 인식된 모든 열거 상수를 게시합니다.  
  
 호출 하는 경우는 [Discover](../../xmla/xml-elements-methods-discover.md) 사용 하 여 메서드는 `DISCOVER_ENUMERATORS` 열거 값은 [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) 요소는 `Discover` 메서드가 반환 되는 `DISCOVER_ENUMERATORS` 스키마 행 집합.  
  
## <a name="rowset-columns"></a>행 집합 열  
 각 열거자에 대해 열거에는 각 값마다 하나씩 여러 요소가 있습니다. 각 열거자를 나타내는 행 집합은 플랫 형식이며, 같은 열거에 속하는 요소들에 대해 열거자의 이름이 반복될 수 있습니다.  
  
 `DISCOVER_ENUMERATORS` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`EnumName`|`DBTYPE_WSTR`||일련의 값을 포함하는 열거자의 이름입니다.|  
|`EnumDescription`|`DBTYPE_WSTR`||열거자의 지역화 가능한 설명입니다. 수 `NULL`합니다.|  
|`EnumType`|`DBTYPE_WSTR`||열거 값의 데이터 형식입니다.|  
|`ElementName`|`DBTYPE_WSTR`||열거자 집합에 있는 값 요소 중 하나의 이름입니다.<br /><br /> 예: `TDP`|  
|`ElementDescription`|`DBTYPE_WSTR`||(옵션) 요소의 지역화 가능한 설명입니다. 수 `NULL`합니다.|  
|`ElementValue`|`DBTYPE_WSTR`||요소의 값입니다. 수 `NULL`합니다.<br /><br /> 예: `01`|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DISCOVER_ENUMERATORS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`EnumName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  