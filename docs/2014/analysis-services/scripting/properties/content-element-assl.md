---
title: 콘텐츠 요소 (ASSL) | Microsoft Docs
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
api_name:
- Content Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Content
helpviewer_keywords:
- Content element
ms.assetid: 221addef-2f88-49c5-b8f5-9eee330497a9
caps.latest.revision: 42
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd9e3c237d8009ac153e8c69033ce9cce958aba3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267479"
---
# <a name="content-element-assl"></a>Content 요소(ASSL)
  에 있는 열의 내용을 설명 합니다 [MiningStructure](../objects/miningstructure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 열거는 마이닝 구조 열에 나타난 내용의 유형을 설명하며 마이닝 알고리즘 공급자의 필요에 따라 확장될 수 있습니다. 콘텐츠 형식에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../data-mining/content-types-data-mining.md)을 참조하세요.  
  
 다음 표에 나열된 값은 일반적으로 모든 마이닝 알고리즘 공급자에서 지원됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*불연속*|열에 불연속 값이 있습니다.|  
|*연속*|열의 값이 연속 숫자 데이터 집합을 정의합니다.|  
|*불연속화*|열의 값이 연속 열에서 파생된 값의 그룹(또는 버킷)을 나타냅니다.|  
|*정렬*|열의 값이 정렬된 집합을 정의합니다.|  
|*순환*|열의 값이 정렬된 순환 집합을 정의합니다.|  
|*확률*|열 값에 포함 된 열에 확률을 지정 합니다 [ClassifiedColumns](../collections/columns-element-assl.md) 부모 요소의 `ScalarMiningStructureColumn`합니다.|  
|*Variance*|열의 값이 부모 `ClassifiedColumns`의 `ScalarMiningStructureColumn` 요소에 포함된 열에 분산을 지정합니다.|  
|*StdDev*|열의 값이 부모 `ClassifiedColumns`의 `ScalarMiningStructureColumn` 요소에 포함된 열에 표준 편차를 지정합니다.|  
|*ProbabilityVariance*|열의 값이 부모 `ClassifiedColumns`의 `ScalarMiningStructureColumn` 요소에 포함된 열에 확률 분산을 지정합니다.|  
|*ProbabilityStdDev*|열의 값이 부모 `ClassifiedColumns`의 `ScalarMiningStructureColumn` 요소에 포함된 열에 확률 표준 편차를 지정합니다.|  
|*지원*|열의 값이 부모 `ClassifiedColumns`의 `ScalarMiningStructureColumn` 요소에 포함된 열에 지원 정보를 지정합니다. **참고:** 이 열은 타사 마이닝 알고리즘 공급자에 대 한 표준의 일부로 제공 됩니다. **참고:** Microsoft에서 제공 하는 알고리즘의이 열에 대 한 사용 권한이 없습니다. <br /><br /> 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.|  
|*키*|열이 키 열입니다. **참고:** 이 내용 유형은 키 열에만 적용 됩니다. 합니다 `IsKey` 로 설정 된 `True`합니다.|  
  
 이러한 표준 값 외에도 알고리즘 공급자에 포함 된 마이닝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 표에 값을 지원 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|*키 시퀀스*|열이 키 열이고, 열의 값이 이벤트 시퀀스를 나타냅니다. **참고:** 이 내용 유형은 키 열에만 적용 됩니다. 합니다 `IsKey` 로 설정 된 `True`합니다.|  
|*Key Time*|열이 키 열이고, 열의 값이 시간 측정 단위를 나타냅니다. **참고:** 이 내용 유형은 키 열에만 적용 됩니다. 합니다 `IsKey` 로 설정 된 `True`합니다.|  
|*시퀀스*|열의 값이 이벤트 시퀀스를 나타냅니다.|  
|*Time*|열의 값이 시간 측정 단위를 나타냅니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Content`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ClassifiedColumns 요소 &#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
