---
title: AggregationPrefix 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AggregationPrefix Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7f7fe7ad16c8949116edb13c7d2c9b5144443dd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293283"
---
# <a name="aggregationprefix-element-assl"></a>AggregationPrefix 요소(ASSL)
  관련 부모 요소 전체에서 집계 이름에 사용할 공통 접두사를 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../objects/cube-element-assl.md)하십시오 [데이터베이스](../objects/database-element-assl.md)를 [MeasureGroup](../objects/group-element-assl.md), [파티션](../objects/partition-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 집계 접두사에서 집계 이름을 생성 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 고 관계형 ROLAP (OLAP) 파티션에 저장 된 집계에 대 한 관계형 데이터베이스의 테이블 이름도 생성 합니다.  
  
 완전히 확장된 집계 이름은 다음 부분으로 구성됩니다.  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 집계 이름의 처음 네 부분은 집계 접두사를 구성합니다. 사용자가 다음과 같이 처음 네 부분을 제공합니다.  
  
-   *DatabasePrefix* 의 값을 나타내는 합니다 `AggregationPrefix` 요소와 연관는 `Database` 요소입니다.  
  
-   *CubePrefix* 의 값을 나타내는 합니다 `AggregationPrefix` 요소와 연관는 `Cube` 요소입니다.  
  
-   *MeasureGroupPrefix* 의 값을 나타내는 합니다 `AggregationPrefix` 요소와 연관는 `MeasureGroup` 요소입니다.  
  
-   *PartitionPrefix* 의 값을 나타내는 합니다 `AggregationPrefix` 요소와 연관는 `Partition` 요소입니다.  
  
 이름의 다섯 번째 부분인 *AggregationID*는 시스템 정의 ID로, 사용자는 이름의 이 부분을 제어할 수 없습니다.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `AggregationPrefix`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup> 및 <xref:Microsoft.AnalysisServices.Partition>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
