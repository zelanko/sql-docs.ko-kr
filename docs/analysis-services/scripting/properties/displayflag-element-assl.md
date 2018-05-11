---
title: DisplayFlag 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d4a65524e6e7dd94ba7fad989d4bbf71e0e11abd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="displayflag-element-assl"></a>DisplayFlag 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  사용자 인터페이스 구성 요소는 연결 된 표시 해야 하는지 여부를 나타내는 읽기 전용 힌트를 포함 [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ServerProperty>  
   ...  
   <DisplayFlag>...</DisplayFlag>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **DisplayFlag** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ServerProperties 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Server 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
