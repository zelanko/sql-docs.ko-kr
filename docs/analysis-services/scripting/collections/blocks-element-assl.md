---
title: 차단 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2372c7b95ac16a6151b335908c94d6d37c90e93c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="blocks-element-assl"></a>Blocks 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  이진 내용을 나타내는 이진 데이터 블록의 컬렉션을 포함 한 [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Data xsi:type="DataBlock">  
   ...  
   <Blocks>  
      <Block>...</Block>  
   </Blocks>  
   ...  
</File>  
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
|부모 요소|[데이터](../../../analysis-services/scripting/objects/data-element-assl.md) 형식의 [DataBlock](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)|  
|자식 요소|[블록](../../../analysis-services/scripting/objects/block-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **블록** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ClrAssemblyFile>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Assembly 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [ClrAssembly 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [파일 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/files-element-assl.md)   
 [File 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [ClrAssemblyFile 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [데이터 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks 요소](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [컬렉션 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
