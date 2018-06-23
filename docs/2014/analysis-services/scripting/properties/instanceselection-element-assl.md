---
title: InstanceSelection 요소 (ASSL) | Microsoft Docs
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
- InstanceSelection Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4b36f0c3c5d29c88c499dea6e70ab4dd0cee1b42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093851"
---
# <a name="instanceselection-element-assl"></a>InstanceSelection 요소(ASSL)
  목록의 예상 항목 수를 기반으로 항목 목록의 표시 방법을 제안하는 힌트를 클라이언트 응용 프로그램에 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|선택 목록을 표시하지 않습니다. 사용자가 직접 값을 입력합니다.|  
|*드롭다운*|항목 수가 드롭다운 목록에 표시할 수 있을 만큼 적습니다.|  
|*목록*|항목 수가 드롭다운 목록에 표시하기에는 너무 많지만 필터링이 필요한 정도는 아닙니다.|  
|*FilteredList*|항목 수가 많아 표시할 항목을 사용자가 필터링해야 합니다.|  
|*MandatoryFilter*|항목 수가 너무 많아 표시 항목을 항상 필터링해야 합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `InstanceSelection`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.InstanceSelection>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  