---
title: Distribution 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eeea432dcddcca8580cdfcbd6d15ae07293f77fb
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="distribution-element-assl"></a>Distribution 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  어떻게 스칼라 값을 설명 하는 공급자별 값이 포함 된 열에서이 배포 되는 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Distribution>...</Distribution>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Distribution** 요소에 사용 가능한 값(예: *Normal* 또는 *Uniform,* )은 각 마이닝 알고리즘 공급자에 따라 다릅니다. 유효한 **Distribution** 값에 대한 자세한 내용은 마이닝 알고리즘 공급자 설명서를 참조하십시오.  
  
 부모에 해당 하는 요소 **배포** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
