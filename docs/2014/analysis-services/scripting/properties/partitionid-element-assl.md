---
title: PartitionID 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PartitionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- PartitionID element
ms.assetid: 95e59c73-5ca4-478e-898d-50ffa4bbe794
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eaeb6bccb6465df04347ab3ba9a69584d6d91d86
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185693"
---
# <a name="partitionid-element-assl"></a>PartitionID 요소(ASSL)
  연결 된 [파티션](../objects/partition-element-assl.md) 부모 요소, 바인딩 또는 아웃오브 라인 바인딩 요소.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PartitionBinding>  
   ...  
   <PartitionID>...</PartitionID>  
   ...  
</PartitionBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[PartitionBinding](../data-type/binding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 바인딩 및 아웃오브 라인 바인딩에 대 한 자세한 내용은 참조 하세요. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
