---
title: ProactiveCachingIncrementalProcessingBinding 데이터 형식 (ASSL) | Microsoft Docs
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
- ProactiveCachingIncrementalProcessingBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingIncrementalProcessingBinding data type
ms.assetid: f49c0c96-4277-417b-9660-d77a4faebd00
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad1107d1ad2e135e65b2ef4f05fd2e85d799123c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247723"
---
# <a name="proactivecachingincrementalprocessingbinding-data-type-assl"></a>ProactiveCachingIncrementalProcessingBinding 데이터 형식(ASSL)
  에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 합니다 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 캐시를 다시 작성 프로세스의 상태에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingIncrementalProcessingBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <RefreshInterval>...</ RefreshInterval >  
   <IncrementalProcessingNotification>...</ IncrementalProcessingNotification >  
</ProactiveCachingIncrementalProcessingBinding>  
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
|자식 요소|[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md), [RefreshInterval](../properties/refreshinterval-element-assl.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 자세한 내용은 합니다 `ProactiveCachingBinding` 상속 계층의 테이블을 포함 하 여 형식이 `ProactiveCachingBinding` 참조 하십시오 [ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 에 대 한 자세한 내용은 합니다 `Binding` 형식, Analysis Services Scripting Language (ASSL) 개체 테이블을 비롯 한는 `Binding` 형식과 상속 계층 `Binding` 참조 하십시오 [바인딩 데이터 형식 &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩 개요를 보려면 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ProactiveCachingIncrementalProcessingBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
