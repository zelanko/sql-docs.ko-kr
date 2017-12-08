---
title: "파일 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
apiname: File Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: File
helpviewer_keywords: File element
ms.assetid: 21c70707-d2f8-4040-9acb-cbce23076bcc
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a5d37a6ace9b56fe9bf5ae808c9a89bf49b6c568
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="file-element-assl"></a>File 요소(ASSL)
  구성 하는 파일 중 하나를 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Files>  
   <File xsi:type="ClrAssemblyFile">...</File>  
</Files>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[파일](../../../analysis-services/scripting/collections/files-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **파일** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ClrAssemblyFile>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Server 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Database 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Assemblies 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Assembly 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [ClrAssembly 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [데이터 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
