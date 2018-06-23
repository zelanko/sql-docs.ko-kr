---
title: NotificationTechnique 요소 (ASSL) | Microsoft Docs
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
- NotificationTechnique Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- NotificationTechnique element
ms.assetid: 80c43de3-f147-4bf5-bb85-da9d182ce415
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f1216ed87ac9fd24265dbcb33d13ba831997b73c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078893"
---
# <a name="notificationtechnique-element-assl"></a>NotificationTechnique 요소(ASSL)
  지정 여부 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 외부 클라이언트 응용 프로그램의 알림을 처리 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingBinding>  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*클라이언트*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProactiveCachingBinding](../data-type/binding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*클라이언트*|외부 클라이언트 응용 프로그램이 알림을 처리합니다.|  
|*Server*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 알림을 처리합니다.|  
  
 부모에 해당 하는 요소 `NotificationTechnique` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ProactiveCachingBinding>합니다.  
  
 AMO(Analysis Management Objects) 개체 모델에서 `NotificationTechnique`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.NotificationTechnique>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)  
  
  