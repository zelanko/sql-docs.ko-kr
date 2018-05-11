---
title: IsKey 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2c8093c4b7eb14280d67604ed09c862bfeca7c2d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="iskey-element-assl"></a>IsKey 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  열에 사례에 대 한 키를 제공 하는지 여부를 나타냅니다는 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <IsKey>...</IsKey>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 하나 이상의 열이 중첩된 테이블 구조의 각 수준에 대해 키 열로 지정될 수 있습니다.  
  
 부모에 해당 하는 요소 **IsKey** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
