---
title: "차단 요소 (ASSL) | Microsoft Docs"
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
apiname: Block Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Block
helpviewer_keywords: Block element
ms.assetid: f45c32ae-e4e0-465a-9564-9ccfb10a858f
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4bed0f3c9cf2a519731cb5103f44070e5f13e6c0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="block-element-assl"></a>Block 요소(ASSL)
  전체 또는 일부의 이진 내용을 포함 한 [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Base64Binary|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[블록](../../../analysis-services/scripting/collections/blocks-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="see-also"></a>관련 항목:  
 [Assembly 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [ClrAssembly 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Files 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/files-element-assl.md)   
 [File 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [ClrAssemblyFile 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [데이터 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
