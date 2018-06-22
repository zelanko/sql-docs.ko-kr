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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 12cbd6c1a2723cfc0d9e5b68ff4a484878c82a74
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090755"
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
|파생 요소|[데이터](../objects/data-element-assl.md) 요소의 [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) 유형 ([파일](../collections/files-element-assl.md) 컬렉션 [ClrAssembly](assembly-data-type-assl.md) 형식)|  
  
## <a name="see-also"></a>관련 항목  
 [Assembly 요소 &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [파일 요소 &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  