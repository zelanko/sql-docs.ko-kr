---
title: "HoldoutMaxCases 요소 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: HoldoutMaxCases
helpviewer_keywords: HoldoutMaxCases element
ms.assetid: 58d94d10-e11e-4368-b3b8-dff23e1947cd
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 67171b2144cbfcd6680b2c2f90f4f83e0f40ab8e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="holdoutmaxcases-element"></a>HoldoutMaxCases 요소
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]테스트 집합이 들어 있는 홀드 아웃 파티션에 사용 되는 데이터 원본의 최대 사례 수를 지정 된 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다. 데이터 집합의 나머지 사례는 학습에 사용됩니다. 0 값은 테스트 집합으로 홀드아웃할 수 있는 사례 수에 대한 제한이 없음을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxCases>...</ddl100_100:HoldoutMaxCases>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|0보다 큰 정수입니다.|  
|기본값|0|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 **HoldoutMaxPercent** 및 **HoldoutMaxCases**모두에 대한 값을 지정하면 알고리즘이 테스트 집합을 두 값 중 작은 값으로 제한합니다.  
  
 **HoldoutMaxCases** 가 기본값 0으로 설정되고 **HoldoutMaxPercent**에 대한 값이 설정되지 않은 경우 알고리즘은 전체 데이터 집합을 학습에 사용합니다.  
  
 새 속성 **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, 또는 **HoldoutActualSize** 에서만사용할수[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 및 이후 버전입니다. 따라서 구문 설명에 표시된 대로 새 네임스페이스로 이러한 속성에 접두사를 지정해야 합니다. 그렇지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 마이닝 구조에서 홀드아웃 파티션의 사용을 지원하지 않았습니다. 따라서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 홀드 아웃 매개 변수 중 하나를 포함 하는 ASSL (Scripting Language) 문은 **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, 또는 **HoldoutActualSize**에 사용할 수 없는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 ASSL 문의 이러한 홀드아웃 매개 변수 중 하나를 사용하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
 부모에 해당 하는 요소 **HoldoutMaxCases** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxPercent 요소](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutSeed 요소](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [HoldoutActualSize 요소](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  
