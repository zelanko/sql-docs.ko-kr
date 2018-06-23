---
title: ProactiveCachingInheritedBinding 데이터 형식 (ASSL) | Microsoft Docs
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
- ProactiveCachingInheritedBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingInheritedBinding data type
ms.assetid: 913fa19f-1ecb-4fca-897e-12f0fb02cf8b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 97013002cc5fd57e8239ee1f4b1769d52279c5af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079139"
---
# <a name="proactivecachinginheritedbinding-data-type-assl"></a>ProactiveCachingInheritedBinding 데이터 형식(ASSL)
  정보를 나타내는 파생된 데이터 형식을 정의 [ProactiveCaching](../objects/proactivecaching-element-assl.md) 테이블 및 뷰의 캐시를 다시 작성 해야 하는 기존 데이터 바인딩을 통해 식별 된 데이터 원본 변경 내용에 대 한 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingInheritedBinding>  
   <!-- This element has no child elements that extend ProactiveCachingObjectNotificationBinding -->  
</ProactiveCachingInheritedBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[ProactiveCachingObjectNotificationBinding](binding-data-type-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|InclusionThresholdSetting|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 자세한 내용은 `ProactiveCachingBinding` 테이블의 상속 계층을 포함 하 여 `ProactiveCachingBinding` 형식 참조 [ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](proactivecachingbinding-data-type-assl.md)합니다.  
  
 에 대 한 자세한 내용은 `Binding` 유형의 Analysis Services Scripting Language (ASSL) 개체 테이블을 포함 하 여는 `Binding` 유형과의 상속 계층 구조 `Binding` 형식 참조 [바인딩 데이터 형식 &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하세요. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ProactiveCachingInheritedBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  