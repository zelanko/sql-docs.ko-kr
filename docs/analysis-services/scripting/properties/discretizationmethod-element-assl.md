---
title: "DiscretizationMethod 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DiscretizationMethod Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DiscretizationMethod
helpviewer_keywords: DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b084caccf3b44cc6b43021551f227f61c0de0e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="discretizationmethod-element-assl"></a>DiscretizationMethod 요소(ASSL)
  불연속화에 사용할 방법을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **DiscretizationMethod** 요소의 값은 **DimensionAttribute** 또는 **ScalarMiningStructureColumn** 에 대한 값을 불연속화하거나 특정 그룹 집합으로 구성하는 방법을 결정합니다. 불연속화 방법에 대 한 자세한 내용은 참조 [분할 방법 &#40; 데이터 마이닝 속성 &#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md)합니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|*자동*|마이닝 구조 열의 AUTOMATIC 불연속화 메서드와 같습니다.|  
|*EqualAreas*|마이닝 구조 열의 EQUAL_AREAS 불연속화 메서드와 같습니다.|  
|*클러스터*|마이닝 구조 열의 CLUSTERS 불연속화 메서드와 같습니다.|  
|*임계값*|마이닝 구조 열의 THRESHOLDS 불연속화 메서드와 같습니다.|  
|*EqualRanges*|마이닝 구조 열의 EQUAL_RANGES 불연속화 메서드와 같습니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거 **DiscretizationMethod** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DiscretizationMethod>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
