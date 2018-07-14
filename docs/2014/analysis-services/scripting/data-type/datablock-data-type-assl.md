---
title: DataBlock 데이터 형식 (ASSL) | Microsoft Docs
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
- DataBlock Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataBlock
helpviewer_keywords:
- DataBlock data type
ms.assetid: 4192b388-613a-472b-881c-f9c02215aa81
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 167af587de6f06d283ec29f8afbc0fedb2ebc99e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211963"
---
# <a name="datablock-data-type-assl"></a>DataBlock 데이터 형식(ASSL)
  이진 내용을 저장 하는 데 사용 되는 데이터 블록의 컬렉션을 나타내는 기본 데이터 형식을 정의 [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataBlock>  
   <Blocks>...</Blocks>  
</DataBlock>  
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
|자식 요소|[블록](../collections/blocks-element-assl.md)|  
|파생 요소|[데이터](../objects/data-element-assl.md) 요소의 [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) 형식 ([파일](../collections/files-element-assl.md) 모음인 [ClrAssembly](assembly-data-type-assl.md) 형식)|  
  
## <a name="see-also"></a>관련 항목  
 [Assembly 요소 &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [파일 요소 &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [블록 요소 &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
