---
title: Persistence 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6c83c4c9c8ded6f3798644193036228a464d06fd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="persistence-element-assl"></a>Persistence 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  바인딩된 원본 데이터의 어떤 부분에는 동적 이며 지정 된 빈도 사용 하 여 업데이트 확인 결정는 [RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Persistence>...</Persistence>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*NotPersisted*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*NotPersisted*|원본 메타데이터, 멤버 및 데이터가 모두 동적입니다.|  
|*메타 데이터*|원본 메타데이터는 정적이지만 멤버와 데이터는 동적입니다.|  
|*모두*|원본 메타데이터, 멤버 및 데이터가 모두 정적입니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **지 속성** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.PersistenceType>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
