---
title: HoldoutMaxPercent 요소 | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c2b6c560d497bb1f5a54e704063459505d71229
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032884"
---
# <a name="holdoutmaxpercent-element"></a>HoldoutMaxPercent 요소
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  테스트 집합이 들어 있는 홀드 아웃 파티션에 사용할 수 있는 데이터 원본의 최대 사례 비율을 지정 된 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다. 나머지 사례는 학습에 사용됩니다. 0 값은 테스트 집합으로 홀드아웃할 수 있는 사례 수에 대한 제한이 없음을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxPercent>...</ddl100_100:HoldoutMaxPercent>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|0에서 99 사이의 정수입니다.|  
|기본값|30|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **HoldoutMaxPercent** 및 **HoldoutMaxCases**모두에 대한 값을 지정하면 알고리즘이 테스트 집합을 두 값 중 작은 값으로 제한합니다.  
  
 **HoldoutMaxCases** 가 기본값 0으로 설정되고 **HoldoutMaxPercent**에 대한 값이 설정되지 않은 경우 알고리즘은 전체 데이터 집합을 학습에 사용합니다.  
  
 새 속성 **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, 또는 **HoldoutActualSize** 에서만사용할수[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 및 이후 버전입니다. 따라서 구문 설명에 표시된 대로 새 네임스페이스를 사용하여 이러한 속성에 접두사를 지정해야 합니다. 그렇지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 마이닝 구조에서 홀드아웃 파티션의 사용을 지원하지 않았습니다. 따라서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 홀드 아웃 매개 변수 중 하나를 포함 하는 ASSL (Scripting Language) 문은 **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, 또는 **HoldoutActualSize**에 사용할 수 없는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 ASSL 문의 이러한 홀드아웃 매개 변수 중 하나를 사용하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
 부모에 해당 하는 요소 **HoldoutMaxPercent** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxCases 요소](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)   
 [HoldoutSeed 요소](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [HoldoutActualSize 요소](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  
