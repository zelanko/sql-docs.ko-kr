---
title: RequiresRestart 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c5e4166ee8df1557270ec3bc54fe3c3339122667
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="requiresrestart-element-assl"></a>RequiresRestart 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  와 연결 된 읽기 전용 값을 포함 한 [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) 결정를 인스턴스에 변경 내용을 적용 하기 위해 다시 시작 해야 하는지 여부를 서버 속성의 값을 변경 해야 하는 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ServerProperty>  
   ...  
   <RequiresRestart>...</RequiresRestart>  
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
 부모에 해당 하는 요소 **RequiresRestart** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ServerProperties 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Server 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
