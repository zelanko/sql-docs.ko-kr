---
title: 콘텐츠 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e0efd6cc31b00c4029e88adab40b56aa88f50dc8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="content-element-assl"></a>Content 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  에 있는 열의 내용을 설명는 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 열거는 마이닝 구조 열에 나타난 내용의 유형을 설명하며 마이닝 알고리즘 공급자의 필요에 따라 확장될 수 있습니다. 콘텐츠 형식에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](../../../analysis-services/data-mining/content-types-data-mining.md)을 참조하세요.  
  
 다음 표에 나열된 값은 일반적으로 모든 마이닝 알고리즘 공급자에서 지원됩니다.  
  
|Value|Description|  
|-----------|-----------------|  
|*불연속*|열에 불연속 값이 있습니다.|  
|*연속*|열의 값이 연속 숫자 데이터 집합을 정의합니다.|  
|*분했습니다*|열의 값이 연속 열에서 파생된 값의 그룹(또는 버킷)을 나타냅니다.|  
|*정렬*|열의 값이 정렬된 집합을 정의합니다.|  
|*순환*|열의 값이 정렬된 순환 집합을 정의합니다.|  
|*확률*|열에 대 한 값에 포함 된 열에 확률을 지정 된 [ClassifiedColumns](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md) 부모 **ScalarMiningStructureColumn**합니다.|  
|*Variance*|에 포함 된 열에 대 한 분산을 지정 하는 열에 대 한 값은 **ClassifiedColumns** 부모 **ScalarMiningStructureColumn**합니다.|  
|*StdDev*|에 포함 된 열에 대 한 표준 편차를 지정 하는 열에 대 한 값은 **ClassifiedColumns** 부모 **ScalarMiningStructureColumn**합니다.|  
|*ProbabilityVariance*|열에 대 한 값에 포함 된 열에 확률 분산을 지정 된 **ClassifiedColumns** 부모 **ScalarMiningStructureColumn**합니다.|  
|*ProbabilityStdDev*|에 포함 된 열에 확률 표준 편차를 지정 하는 열에 대 한 값은 **ClassifiedColumns** 부모 **ScalarMiningStructureColumn**합니다.|  
|*지원*|에 포함 된 열에 대 한 지원 정보를 지정 하는 열에 대 한 값은 **ClassifiedColumns** 부모 **ScalarMiningStructureColumn**합니다.<br /><br /> 참고:이 열 타사 마이닝 알고리즘 공급자에 대 한 표준의 일부로 제공 됩니다. Microsoft에서 제공 하는 알고리즘 되지 않도록이 열의 사용 합니다.|  
|*Key*|열이 키 열입니다.<br /><br /> 참고:이 콘텐츠 유형에는 키 열에만 적용 됩니다.는 **IsKey** 로 설정 된 **True**합니다.|  
  
 이러한 표준 값 외에도 마이닝 알고리즘 공급자에 포함 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 다음 표에서 값을 지원 합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|*키 시퀀스*|열이 키 열이고, 열의 값이 이벤트 시퀀스를 나타냅니다.<br /><br /> 참고:이 콘텐츠 유형에는 키 열에만 적용 됩니다.는 **IsKey** 로 설정 된 **True**합니다.|  
|*Key Time*|열이 키 열이고, 열의 값이 시간 측정 단위를 나타냅니다.<br /><br /> 참고:이 콘텐츠 유형에는 키 열에만 적용 됩니다.는 **IsKey** 로 설정 된 **True**합니다.|  
|*시퀀스*|열의 값이 이벤트 시퀀스를 나타냅니다.|  
|*Time*|열의 값이 시간 측정 단위를 나타냅니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거 **콘텐츠** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ClassifiedColumns 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
