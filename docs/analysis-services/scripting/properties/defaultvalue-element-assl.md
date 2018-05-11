---
title: DefaultValue 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2a7c0b31a8d749438689c03b56eeb75e2b07888e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="defaultvalue-element-assl"></a>DefaultValue 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  연결된 된 읽기 전용 기본 값이 포함 된 [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ServerProperty>  
   ...  
   <DefaultValue>   </DefaultValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|모든 simpleType|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 읽기 전용 설치 기본값을 포함 하는이 요소는 **ServerProperty** 의 현재 인스턴스에 대 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 기본값은 인스턴스에 의해 제공되며 일반적으로 변경할 수 없습니다.  
  
 부모에 해당 하는 요소 **DefaultValue** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ServerProperties 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Server 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
