---
title: KpiID 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 51255fa38b69633653afb92b3d1b08ab1ef66a5b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="kpiid-element-assl"></a>KpiID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  연결 하는 식별자 (ID)를 포함 한 [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 인 요소는 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PerspectiveKpi>  
      ...  
   <KpiID>...</KpiID>  
   ...  
</PerspectiveKpi>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[PerspectiveKpi](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **KpiID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.PerspectiveKpi>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성(ASSL)](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
