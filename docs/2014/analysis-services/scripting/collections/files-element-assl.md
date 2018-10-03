---
title: 파일 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Files Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Files
helpviewer_keywords:
- Files element
ms.assetid: 8a1327cb-1f60-42a7-b8ef-213d45a63e55
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 91fd214a87ea266a1c5849211bd30237b4313b20
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078623"
---
# <a name="files-element-assl"></a>Files 요소(ASSL)
  컬렉션을 포함 [파일](../objects/file-element-assl.md) 구성 하는 요소는 [ClrAssembly](../data-type/assembly-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Assembly xsi:type="ClrAssembly">  
   ...  
   <Files>  
      <File xsi:type="ClrAssemblyFile">...</File>  
   </Files>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[어셈블리](../objects/assembly-element-assl.md) 형식의 [ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|자식 요소|[파일](../objects/file-element-assl.md) 형식의 [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Server 요소 &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Assemblies 요소 &#40;ASSL&#41;](assemblies-element-assl.md)   
 [데이터 요소 &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 데이터 형식 &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](blocks-element-assl.md)   
 [블록 요소 &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 데이터 형식 &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
