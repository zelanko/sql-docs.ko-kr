---
title: "OnlineMode 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: OnlineMode Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: OnlineMode
helpviewer_keywords: OnlineMode element
ms.assetid: 0bbac4e2-002f-4be4-8dd6-ccd7034f5f93
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4c8a38c9882484335fefdfe1e7b8f155b27a84fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="onlinemode-element-assl"></a>OnlineMode 요소(ASSL)
  캐시를 다시 작성하기 시작할 때 바로 데이터베이스를 다시 온라인 상태로 만들지, 아니면 캐시를 다시 작성한 후에만 데이터베이스를 다시 온라인 상태로 만들지를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <OnlineMode>...</OnlineMode>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*직접 실행*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*직접 실행*|캐시를 다시 작성하기 시작할 때 바로 데이터베이스를 다시 온라인 상태로 만듭니다.|  
|*OnCacheComplete*|캐시를 다시 작성한 후에만 데이터베이스를 다시 온라인 상태로 만듭니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **OnlineMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ProactiveCaching>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ProactiveCaching 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
  
