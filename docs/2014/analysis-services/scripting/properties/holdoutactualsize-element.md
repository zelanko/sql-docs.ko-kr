---
title: HoldoutActualSize 요소 | Microsoft Docs
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
- HoldoutActualSize
helpviewer_keywords:
- HoldoutActualSize element
ms.assetid: 606a6674-cedb-4cee-82d0-26589f084dd9
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fe781b9e3381a97d9ad75440dac40e281881419f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093395"
---
# <a name="holdoutactualsize-element"></a>HoldoutActualSize 요소
  처리를 수행한 테스트 집합이 들어 있는 홀드 아웃 파티션의 실제 크기를 나타냅니다는 [MiningStructure](../objects/miningstructure-element-assl.md) 요소입니다. 데이터 집합의 나머지 사례는 학습에 사용됩니다. 이 속성은 읽기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutActualSize>...</ddl100_100:HoldoutActualSize>  
   ...  
</MiningStructure  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|일기 전용 정수 값입니다.|  
|기본값|해당 사항 없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 값 `HoldoutActualSize` 값에 대 한 원본 데이터에 따라 달라 집니다 [HoldoutMaxCases](holdoutmaxcases-element.md), [HoldoutMaxPercent](holdoutmaxpercent-element.md), 및 [HoldoutSeed](holdoutseed-element.md)합니다. 따라서 `HoldoutActualSize`에 대한 값은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 나머지 구조를 처리한 후에 사용할 수 있습니다.  
  
 부모에 해당 하는 요소 `HoldoutActualSize` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 마이닝 구조에서 홀드아웃 파티션의 사용을 지원하지 않았습니다. 따라서 홀드아웃 매개 변수 `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` 또는 `HoldoutActualSize` 중 하나를 포함하는 ASSL([!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Scripting Language) 문은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 사용할 수 없습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 ASSL 문의 이러한 홀드아웃 매개 변수 중 하나를 사용하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)   
 [HoldoutMaxCases 요소](holdoutmaxcases-element.md)   
 [HoldoutMaxPercent 요소](holdoutmaxpercent-element.md)   
 [HoldoutSeed 요소](holdoutseed-element.md)  
  
  