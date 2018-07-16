---
title: 요소 (ASSL) 파티션 | Microsoft Docs
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
- Partitions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Partitions
helpviewer_keywords:
- Partitions element
ms.assetid: e41c97ca-da44-48e9-a454-d25ee74209fd
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f54cab2990fcd5f3679da1c83c997921a59e67ac
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185212"
---
# <a name="partitions-element-assl"></a>Partitions 요소(ASSL)
  컬렉션을 포함 [파티션](../objects/partition-element-assl.md) 에서 사용 되는 요소는 [MeasureGroup](../objects/group-element-assl.md) 요소나는 아웃 아웃오브 라인을 구성 하는 파티션 바인딩의 컬렉션 [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup> <!-- or MeasureGroupBinding -->  
   ...  
   <Partitions>  
      <Partition>...</Partition> <!-- parent: MeasureGroup -->  
      <!-- or -->  
      <Partition xsi:type="PartitionBinding">...</Partition> <!-- parent: MeasureGroupBinding -->  
   </Partitions>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MeasureGroup](../objects/group-element-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[측정값 그룹](../objects/group-element-assl.md)|[파티션](../objects/partition-element-assl.md)|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[파티션](../objects/partition-element-assl.md) 형식의 [PartitionBinding](../data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.PartitionCollection>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
