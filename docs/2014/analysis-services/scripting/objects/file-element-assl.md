---
title: 파일 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- File
helpviewer_keywords:
- File element
ms.assetid: 21c70707-d2f8-4040-9acb-cbce23076bcc
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 645882666ba82f965fddff9e1c886e97ff092a90
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082551"
---
# <a name="file-element-assl"></a>File 요소(ASSL)
  구성 하는 파일 중 하나를 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] [ClrAssembly](../data-type/assembly-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Files>  
   <File xsi:type="ClrAssemblyFile">...</File>  
</Files>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[파일](../collections/files-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소 `Files` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ClrAssemblyFile>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [서버 요소 &#40;ASSL&#41;](server-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](database-element-assl.md)   
 [Assemblies 요소 &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Assembly 요소 &#40;ASSL&#41;](assembly-element-assl.md)   
 [ClrAssembly 데이터 형식 &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [데이터 요소 &#40;ASSL&#41;](data-element-assl.md)   
 [DataBlock 데이터 형식 &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](block-element-assl.md)   
 [ComAssembly 데이터 형식 &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  