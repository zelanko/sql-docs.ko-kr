---
title: HoldoutMaxCases 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutMaxCases
helpviewer_keywords:
- HoldoutMaxCases element
ms.assetid: 58d94d10-e11e-4368-b3b8-dff23e1947cd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aaf0629b51abf7e8dc4fe6efa5ac6b18a2f166b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136813"
---
# <a name="holdoutmaxcases-element"></a>HoldoutMaxCases 요소
  테스트 집합이 들어 있는 홀드 아웃 파티션에 사용 되는 데이터 원본의 최대 사례 수를 지정 된 [MiningStructure](../objects/miningstructure-element-assl.md) 요소입니다. 데이터 집합의 나머지 사례는 학습에 사용됩니다. 0 값은 테스트 집합으로 홀드아웃할 수 있는 사례 수에 대한 제한이 없음을 나타냅니다.  
  
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
|부모 요소|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `HoldoutMaxPercent` 및 `HoldoutMaxCases` 모두에 대한 값을 지정하면 알고리즘이 테스트 집합을 두 값 중 작은 값으로 제한합니다.  
  
 `HoldoutMaxCases`가 기본값 0으로 설정되고 `HoldoutMaxPercent`에 대한 값이 설정되지 않은 경우 알고리즘은 전체 데이터 집합을 학습에 사용합니다.  
  
 새 속성 `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, 또는 `HoldoutActualSize` 으로만 사용할 수 있는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상. 따라서 구문 설명에 표시된 대로 새 네임스페이스로 이러한 속성에 접두사를 지정해야 합니다. 그렇지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 마이닝 구조에서 홀드아웃 파티션의 사용을 지원하지 않았습니다. 따라서 홀드아웃 매개 변수 `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` 또는 `HoldoutActualSize` 중 하나를 포함하는 ASSL([!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Scripting Language) 문은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 사용할 수 없습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 ASSL 문의 이러한 홀드아웃 매개 변수 중 하나를 사용하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
 부모에 해당 하는 요소가 `HoldoutMaxCases` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)   
 [HoldoutMaxPercent 요소](holdoutmaxpercent-element.md)   
 [HoldoutSeed 요소](holdoutseed-element.md)   
 [HoldoutActualSize 요소](holdoutactualsize-element.md)  
  
  
