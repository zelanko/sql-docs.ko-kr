---
title: "ProactiveCachingObjectNotificationBinding 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ProactiveCachingObjectNotificationBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: ProactiveCachingObjectNotificationBinding data type
ms.assetid: b3cf5fb6-6121-4f25-8de6-f171792c440d
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ab6c427eb4b138c7883083527fd5643b76471798
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="proactivecachingobjectnotificationbinding-data-type-assl"></a>ProactiveCachingObjectNotificationBinding 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]정보를 나타내는 추상 파생된 데이터 형식을 정의 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 지정 된 테이블 및 뷰 또는 테이블 및 뷰의 기존 데이터 바인딩을 통해 식별 된 데이터 원본 변경에 대 한 요소 캐시 재작성이 필요한입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingObjectNotificationBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingObjectNotificationBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|파생 데이터 형식|[ProactiveCachingInheritedBinding](../../../analysis-services/scripting/data-type/proactivecachinginheritedbinding-data-type-assl.md), [ProactiveCachingTablesBinding](../../../analysis-services/scripting/data-type/proactivecachingtablesbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[NotificationTechnique](../../../analysis-services/scripting/properties/notificationtechnique-element-assl.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 에 대 한 자세한 내용은 **ProactiveCachingBinding** 테이블의 상속 계층을 포함 하 여 **ProactiveCachingBinding** 형식 참조 [ProactiveCachingBinding 데이터 Type&#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md).  
  
 에 대 한 자세한 내용은 **바인딩** 유형의 Analysis Services Scripting Language (ASSL) 개체 테이블을 포함 하 여는 **바인딩** 유형과의 상속 계층 구조 **바인딩**  형식 참조 [바인딩 데이터 형식 &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하십시오. [데이터 원본 및 바인딩 &#40; SSAS 다차원 &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ProactiveCachingObjectNotificationBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
