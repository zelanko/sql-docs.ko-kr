---
title: ClrAssemblyFile 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: db7ec0dea32fd0fbe0c0584b75fb42b783629daa
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="clrassemblyfile-data-type-assl"></a>ClrAssemblyFile 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  구성 하는 파일 중 하나를 나타내는 기본 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] **어셈블리** ([ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 요소).  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ClrAssemblyFile>  
   <Name>...</Name>  
      <Type>...</Type>  
      <Data>...</Data>  
</ClrAssemblyFile>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[데이터](../../../analysis-services/scripting/objects/data-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [유형](../../../analysis-services/scripting/properties/type-element-clrassemblyfile-assl.md)|  
|파생 요소|[파일](../../../analysis-services/scripting/objects/file-element-assl.md) ([파일](../../../analysis-services/scripting/collections/files-element-assl.md) 컬렉션 [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md))|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ClrAssemblyFile>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Server 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Assemblies 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Assembly 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [DataBlock 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
