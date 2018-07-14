---
title: ProactiveCachingQueryBinding 데이터 형식 (ASSL) | Microsoft Docs
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
- ProactiveCachingQueryBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingQueryBinding data type
ms.assetid: c1b06e50-9e68-40db-bdab-fc2cb3a8ff64
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c93fc223e66910dde5e532ecf20e89497227f6d3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263499"
---
# <a name="proactivecachingquerybinding-data-type-assl"></a>ProactiveCachingQueryBinding 데이터 형식(ASSL)
  정보를 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 테이블 및 뷰의 캐시 재작성이 필요한 지정 된 쿼리의 실행을 통해 식별 된 데이터 원본 변경 내용에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingQueryBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <RefreshInterval>...</RefreshInterval>  
   <QueryNotification>...</QueryNotification>  
</ProactiveCachingQueryBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[ProactiveCachingBinding](binding-data-type-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[QueryNotification](../objects/querynotification-element-assl.md), [RefreshInterval](../properties/refreshinterval-element-assl.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 자세한 내용은 합니다 `ProactiveCachingBinding` 상속 계층의 테이블을 포함 하 여 형식이 `ProactiveCachingBinding` 참조 하십시오 [ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 에 대 한 자세한 내용은 합니다 `Binding` 형식, Analysis Services Scripting Language (ASSL) 개체 테이블을 비롯 한는 `Binding` 형식과 상속 계층 `Binding` 참조 하십시오 [바인딩 데이터 형식 &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩 개요를 보려면 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
