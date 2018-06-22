---
title: 큐브 요소 (XMLA) | Microsoft Docs
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
- Cube Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cube
- urn:schemas-microsoft-com:xml-analysis#Cube
- http://schemas.microsoft.com/analysisservices/2003/engine#Cube
helpviewer_keywords:
- Cube element
ms.assetid: 2e8662f4-fb2e-43af-b70a-9e0b5872c9b9
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 3627c62dd8277ff0c86d66f453afd66ad01005c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080929"
---
# <a name="cube-element-xmla"></a>Cube 요소(XMLA)
  부모 나타내는 차원을 포함 하는 큐브를 식별 [개체](object-element-dimension-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Object>  
   ...  
   <Cube>...</Cube>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[개체](object-element-dimension-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Cube` 요소는 `Object` 요소가 나타내는 차원이 있는 큐브 이름을 포함하는 개체 식별자입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Database 요소 &#40;XMLA&#41;](database-element-xmla.md)   
 [요소를 차원 &#40;XMLA&#41;](dimension-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  