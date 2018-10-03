---
title: StorageLocation 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- StorageLocation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StorageLocation
helpviewer_keywords:
- StorageLocation element
ms.assetid: ecf8852f-56a1-4fcf-b0d8-d7eebb75e4ed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 45ba999d7cd7de44eaf6a9abaec55ff796dcc800
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079273"
---
# <a name="storagelocation-element-assl"></a>StorageLocation 요소(ASSL)
  부모 요소의 내용에 대한 파일 시스템 저장소 위치를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube><!-- or MeasureGroup, Partition -->  
      ...  
   <StorageLocation>...</StorageLocation>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|기본값|  
|------------------------|-------------------|  
|[Cube](../objects/cube-element-assl.md)|없음|  
|[측정값 그룹](../objects/group-element-assl.md)|`StorageLocation` 부모 요소의 `Cube` 값입니다.|  
|[파티션](../objects/partition-element-assl.md)|`StorageLocation` 부모 요소의 `MeasureGroup` 값입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../objects/cube-element-assl.md)하십시오 [MeasureGroup](../objects/group-element-assl.md), [파티션](../objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델에서 `StorageLocation`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MeasureGroup> 및 <xref:Microsoft.AnalysisServices.Partition>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
