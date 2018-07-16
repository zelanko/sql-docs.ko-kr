---
title: Mode 요소 (XMLA) | Microsoft Docs
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
- Mode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c90d67995e6775c035265db57c2b55380ad0fe76
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267649"
---
# <a name="mode-element-xmla"></a>Mode 요소(XMLA)
  부모에서 사용할 모드를 식별 [잠금](../xml-elements-commands/lock-element-xmla.md) 지정된 된 개체에서 잠금을 만들 때 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[잠금을](../xml-elements-commands/lock-element-xmla.md), [잠금 해제](../xml-elements-commands/unlock-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모 `Lock` 요소는 `Mode` 요소를 사용하여 개체에 만들 잠금 유형을 결정합니다. 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*CommitShared*|공유 잠금은 지정된 개체에서 설정됩니다. 동일한 개체에서 다른 공유 잠금을 만들 수도 있습니다.<br /><br /> 공유 잠금을 방지와 같은 쓰기 작업을 포함 하는 트랜잭션을 [Execute](../xml-elements-methods-execute.md) 실행 하는 메서드 호출은 [Alter](../xml-elements-commands/alter-element-xmla.md) 공유 잠금을 제거할 때까지 커밋에서 지정된 된 개체에서 명령을 합니다. 공유 잠금을 같은 읽기 작업을 포함 하는 트랜잭션을 해도 [검색](../xml-elements-methods-discover.md) 메서드 호출 또는 `Execute` 실행 하는 메서드 호출을 [문](../xml-elements-commands/statement-element-xmla.md) 커밋 명령을 합니다.|  
|*CommitExclusive*|지정된 개체에서 배타적 잠금이 설정됩니다. 동일한 개체에서 다른 공유 잠금 또는 배타적 잠금을 만들 수 없습니다.<br /><br /> 배타적 잠금을 설정하면 배타적 잠금을 제거할 때까지 지정된 개체에서 읽기 또는 쓰기 작업을 포함하는 트랜잭션을 커밋하지 못합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [ID 요소 &#40;XMLA&#41;](id-element-xmla.md)   
 [개체 요소 &#40;XMLA&#41;](object-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
