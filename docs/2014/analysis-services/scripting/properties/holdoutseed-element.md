---
title: HoldoutSeed 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutSeed
helpviewer_keywords:
- HoldoutSeed element
ms.assetid: 6b608bb3-c075-4744-9722-f5fb9fa1cc7e
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4b17c334a2effbecb24fc3aca41293567f3225ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078642"
---
# <a name="holdoutseed-element"></a>HoldoutSeed 요소
  테스트 집합을 포함 하는 반복 가능한 홀드 아웃 파티션의 초기값을 지정 된 [MiningStructure](../objects/miningstructure-element-assl.md) 요소입니다. 이 초기값은 다시 처리하는 동안 모델 내용이 동일하게 유지되도록 합니다. 지정 되지 않았거나 0으로 설정 하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 마이닝 구조의 이름에 해시 알고리즘을 사용 하 여 초기값을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Long|  
|기본값|0|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 마이닝 구조를 처음 만들면 ID 및 이름이 같습니다. 마이닝 구조의 이름을 변경할 수도 있습니다. 따라서 파티션을 반복할 수 있게 하려면 이름으로 만든 초기값에 따를 필요가 없으며 초기값을 명시적으로 설정해야 합니다.  
  
 그리고 `EXPORT` 문을 사용하여 마이닝 구조의 사본을 만들 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 새로운 마이닝 구조의 이름을 보존하지만 자동으로 새 ID를 생성합니다. 따라서 이름은 같지만 ID가 다른 두 개의 마이닝 구조가 있을 수 있습니다. 이름이 같은 두 개의 마이닝 구조는 동일한 초기값을 가집니다. 그러나 데이터 분할이 원본 데이터에 따라 달라지므로 각 구조에 있는 파티션의 실제 내용은 다를 수 있습니다.  
  
 새 속성 `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, 또는 `HoldoutActualSize` 에 사용할 수 있는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전입니다. 따라서 구문 설명에 표시된 대로 새 네임스페이스로 이러한 속성에 접두사를 지정해야 합니다. 그렇지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
 **참고** 에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 마이닝 구조에서 홀드 아웃 파티션의 사용을 지원 하지 않았습니다. 따라서 홀드아웃 매개 변수 `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` 또는 `HoldoutActualSize`를 포함하는 ASSL([!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Scripting Language) 문은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 사용할 수 없습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 ASSL 문의 이러한 홀드아웃 매개 변수 중 하나를 사용하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
 부모에 해당 하는 요소 `HoldoutSeed` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)   
 [HoldoutActualSize 요소](holdoutactualsize-element.md)   
 [HoldoutMaxPercent 요소](holdoutmaxpercent-element.md)   
 [HoldoutMaxCases 요소](holdoutmaxcases-element.md)  
  
  