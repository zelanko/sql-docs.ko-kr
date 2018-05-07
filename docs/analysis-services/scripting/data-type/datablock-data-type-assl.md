---
title: DataBlock 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7ef74279d2430df004ae00429f559ceb9a5c174e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="datablock-data-type-assl"></a>DataBlock 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소의 이진 내용을 저장하는 데 사용되는 데이터 블록의 컬렉션을 나타내는 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataBlock>  
   <Blocks>...</Blocks>  
</DataBlock>  
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
|자식 요소|[블록](../../../analysis-services/scripting/collections/blocks-element-assl.md)|  
|파생 요소|[ClrAssemblyFile](../../../analysis-services/scripting/objects/data-element-assl.md) 형식의 [Data](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소([ClrAssembly](../../../analysis-services/scripting/collections/files-element-assl.md) 형식의 [Files](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 컬렉션)|  
  
## <a name="see-also"></a>관련 항목:  
 [Assembly 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [File 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [Block 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
