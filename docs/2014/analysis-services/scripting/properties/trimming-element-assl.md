---
title: Trimming 요소 (ASSL) | Microsoft Docs
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
- Trimming Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Trimming
helpviewer_keywords:
- Trimming element
ms.assetid: 8b3bbf89-8309-4d00-9aea-a5918f0c7027
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d34a2b559dfcace0a8334916f66031b130763182
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326543"
---
# <a name="trimming-element-assl"></a>Trimming 요소(ASSL)
  데이터 원본의 데이터가 잘리는 방법을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataItem>  
   ...  
   <Trimming>...</Trimming>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*오른쪽*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*왼쪽*|데이터가 왼쪽에서 잘립니다.|  
|*오른쪽*|데이터가 오른쪽에서 잘립니다.|  
|*LeftRight*|데이터가 왼쪽과 오른쪽에서 잘립니다.|  
|*없음*|데이터가 잘리지 않습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Trimming`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.Trimming>입니다.  
  
 부모에 해당 하는 요소가 `Trimming` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DataItem>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
