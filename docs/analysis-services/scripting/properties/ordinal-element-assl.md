---
title: Ordinal 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 88c2409d42fc23f017989218d8ea87172d1b8d3d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="ordinal-element-assl"></a>Ordinal 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  키 및 번역과 같은 컬렉션에서 바인딩할 서수를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Ordinal>...</Ordinal>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|**0**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **AttributeBinding** 및 **CubeAttributeBinding** 요소가 들어는 [형식](../../../analysis-services/scripting/properties/type-element-binding-assl.md) 속성으로 설정 되어 *키* 또는 *번역* 다시 데이터 원본 뷰에서 열의 컬렉션에 바인딩되는 특성에 바인딩될 수 있습니다. 값은 **서 수** 요소는 열을 결정는 **AttributeBinding** 또는 **CubeAttributeBinding** 해당 컬렉션에 대 한 참조입니다.  
  
 부모에 해당 하는 요소 **서** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributeBinding> 및 <xref:Microsoft.AnalysisServices.CubeAttributeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
