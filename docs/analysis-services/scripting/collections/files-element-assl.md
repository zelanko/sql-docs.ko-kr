---
title: "파일 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
apiname: Files Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Files
helpviewer_keywords: Files element
ms.assetid: 8a1327cb-1f60-42a7-b8ef-213d45a63e55
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f7727da9a239596dfe0e6ffddd5e8bd783a3a64e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="files-element-assl"></a>Files 요소(ASSL)
  컬렉션을 포함 [파일](../../../analysis-services/scripting/objects/file-element-assl.md) 구성 하는 요소는 [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 요소입니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md) 형식의 [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|자식 요소|[파일](../../../analysis-services/scripting/objects/file-element-assl.md) 형식의 [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Server 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Database 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Assemblies 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [데이터 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
