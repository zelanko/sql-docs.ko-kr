---
title: SkippedLevels 요소 (XMLA) | Microsoft Docs
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
- SkippedLevels Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#SkippedLevels
- microsoft.xml.analysis.skippedlevels
- urn:schemas-microsoft-com:xml-analysis#SkippedLevels
helpviewer_keywords:
- SkippedLevels element
ms.assetid: 4887b557-0ffc-4f42-b6b9-c98ad1208ca5
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a916a64b9dc327e05355bd682e06beaa95c29e94
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="skippedlevels-element-xmla"></a>SkippedLevels 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]부모를 나타내는 특성 멤버가 건너뛰는 수준의 수를 포함 [특성](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute>  
   ...  
   <SkippedLevels>...</SkippedLevels>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|0|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 **SkippedLevels** 요소는 부모 **Attribute** 요소에서 정의하는 특성 멤버가 건너뛰는 수준의 수를 결정합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 &#40; 삽입 XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
