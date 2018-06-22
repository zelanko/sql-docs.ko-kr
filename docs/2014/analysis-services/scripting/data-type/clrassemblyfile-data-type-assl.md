---
title: ClrAssemblyFile 데이터 형식 (ASSL) | Microsoft Docs
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
- ClrAssemblyFile Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssemblyFile
helpviewer_keywords:
- ClrAssemblyFile data type
ms.assetid: 91074677-c149-483b-a56d-0e35d959d9eb
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b542c4193d80fa80cc9aed6663f41e102266000b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081941"
---
# <a name="clrassemblyfile-data-type-assl"></a>ClrAssemblyFile 데이터 형식(ASSL)
  구성 하는 파일 중 하나를 나타내는 기본 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] `Assembly` ([ClrAssembly](assembly-data-type-assl.md) 요소).  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ClrAssemblyFile>  
   <Name>...</Name>  
      <Type>...</Type>  
      <Data>...</Data>  
</ClrAssemblyFile>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[데이터](../objects/data-element-assl.md), [이름](../properties/name-element-assl.md), [유형](../properties/type-element-clrassemblyfile-assl.md)|  
|파생 요소|[파일](../objects/file-element-assl.md) ([파일](../collections/files-element-assl.md) 컬렉션 [ClrAssembly](assembly-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ClrAssemblyFile>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [서버 요소 &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Assemblies 요소 &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Assembly 요소 &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [DataBlock 데이터 형식 &#40;ASSL&#41;](datablock-data-type-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 데이터 형식 &#40;ASSL&#41;](comassembly-data-type-assl.md)   
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  