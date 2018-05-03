---
title: Mode 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Mode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e5f6f3e46a86d8db07d2ce13a84007f2c36af267
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mode-element-xmla"></a>Mode 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에서 사용할 모드를 식별 [잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) 지정된 된 개체에서 잠금을 만들 때의 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [잠금 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모 **잠금** 요소 사용 하 여는 **모드** 요소는 개체에 만들 잠금 유형을 결정 하도록 합니다. 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*CommitShared*|공유 잠금은 지정된 개체에서 설정됩니다. 동일한 개체에서 다른 공유 잠금을 만들 수도 있습니다.<br /><br /> 공유 잠금을 설정와 같은 쓰기 작업을 포함 하는 트랜잭션을 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드 호출이 실행 되는 [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) 커밋되지는 공유 잠금이 제거 될 때까지 지정된 된 개체에서 명령을 합니다. 와 같은 읽기 작업을 포함 하는 트랜잭션을 한 공유 잠금을 사용 해도 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드 호출 또는 **Execute** 메서드 호출이 실행 되는 [문을](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) 명령에서 커밋하고 있습니다.|  
|*CommitExclusive*|지정된 개체에서 배타적 잠금이 설정됩니다. 동일한 개체에서 다른 공유 잠금 또는 배타적 잠금을 만들 수 없습니다.<br /><br /> 배타적 잠금을 설정하면 배타적 잠금을 제거할 때까지 지정된 개체에서 읽기 또는 쓰기 작업을 포함하는 트랜잭션을 커밋하지 못합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ID 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Object 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
