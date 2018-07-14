---
title: UserDefinedGroupBinding 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- UserDefinedGroupBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UserDefinedGroupBinding
helpviewer_keywords:
- UserDefinedGroupBinding data type
ms.assetid: 70149929-0ff7-4a67-84bf-e94908ae7611
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a31c1867296ff00d8000b24640dfb44bef034a00
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194323"
---
# <a name="userdefinedgroupbinding-data-type-assl"></a>UserDefinedGroupBinding 데이터 형식(ASSL)
  특성에 대한 사용자 정의 그룹화를 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<UserDefinedGroupBinding>  
   <!-- The following elements extend Binding -->  
      <AttributeID>...</AttributeID>  
      <Groups>...</Groups>  
</UserDefinedGroupBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[바인딩](binding-data-type-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[AttributeID](../properties/id-element-assl.md), [그룹](../collections/groups-element-assl.md)|  
|파생 요소|참조 [바인딩](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `UserDefinedGroupBinding` 자동으로 취급를 [AttributeBinding](attributebinding-data-type-assl.md)해당 [형식](../properties/type-element-binding-assl.md) 로 설정 된 *모든*합니다.  
  
 에 대 한 자세한 내용은 합니다 `Binding` 형식, Analysis Services Scripting Language (ASSL) 개체 테이블을 비롯 한는 `Binding` 형식과 상속 계층 `Binding` 참조 하십시오 [바인딩 데이터 형식 &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩 개요를 보려면 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.UserDefinedGroupBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
