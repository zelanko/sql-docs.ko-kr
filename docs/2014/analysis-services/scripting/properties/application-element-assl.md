---
title: 응용 프로그램 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Application Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Application
helpviewer_keywords:
- Application element
ms.assetid: dfd780ad-f643-4a1c-b58b-34271ae91240
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b4a9b82bef51b02d65c934a6b8adbbbdb30e2e4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200393"
---
# <a name="application-element-assl"></a>Application 요소(ASSL)
  연결 된 응용 프로그램을 식별 하는 [동작](../objects/action-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <Application>...</Application>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../objects/action-element-assl.md) 또는 해당 파생 된 요소 중 하나: [DrillThroughAction](../data-type/action-data-type-assl.md)하십시오 [ReportAction](../data-type/reportaction-data-type-assl.md), [StandardAction](../data-type/standardaction-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Application` 요소는 클라이언트 응용 프로그램에서 특정 클라이언트 응용 프로그램에 적용되는 동작을 확인하는 데 사용할 수 있습니다. 클라이언트 응용 프로그램에서는 이 요소 값을 계산해야 합니다.  
  
 부모에 해당 하는 요소가 `Application` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Actions 요소 &#40;ASSL&#41;](../collections/actions-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
