---
title: CurrentStorageMode 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b8a2b612e50b072c4b12caac321e75957ea3c952
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="currentstoragemode-element-assl"></a>CurrentStorageMode 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  부모 요소에 대한 현재 저장소 모드를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*ROLAP*|  
|카디널리티|0-1: 한 번만 나타나거나 전혀 나타나지 않을 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[차원](../../../analysis-services/scripting/objects/dimension-element-assl.md), [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **CurrentStorageMode** 요소는 자동 관리 캐싱을 위해 현재 사용 중인 저장소 모드를 나타내며 부모 요소의 모든 특성에 적용됩니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*MOLAP*|부모가 MOLAP(다차원 OLAP) 저장소를 사용합니다.|  
|*ROLAP*|부모가 ROLAP(관계형 OLAP) 저장소를 사용합니다.|  
|*HOLAP*|부모가 HOLAP(하이브리드 OLAP) 저장소를 사용합니다.<br /><br /> 참고:이 값은 적합만 [파티션](../../../analysis-services/scripting/objects/partition-element-assl.md) 부모 요소입니다.|  
  
 허용된 된 값에 해당 하는 열거 **CurrentStorageMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.StorageMode>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
