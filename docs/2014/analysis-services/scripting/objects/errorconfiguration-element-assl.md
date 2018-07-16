---
title: ErrorConfiguration 요소 (ASSL) | Microsoft Docs
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
- ErrorConfiguration Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ErrorConfiguration
helpviewer_keywords:
- ErrorConfiguration element
ms.assetid: e8363ec2-fbbf-48f6-a55d-01793afa759c
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e36d41d9788b7c65079f7aff7a97d72dd44d8e17
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316933"
---
# <a name="errorconfiguration-element-assl"></a>ErrorConfiguration 요소(ASSL)
  부모 요소가 처리될 때 발생할 수 있는 오류 처리에 대한 설정을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, MiningStructure, Partition -->  
   ...  
   <ErrorConfiguration>  
      <KeyErrorLimit>...</KeyErrorLimit>  
      <KeyErrorLogFile>...</KeyErrorLogFile>  
      <KeyErrorAction>...</KeyErrorAction>  
      <KeyErrorLimitAction>...</KeyErrorLimitAction>  
      <KeyNotFound>...</KeyNotFound>  
      <KeyDuplicate>...</KeyDuplicate>  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
      <NullKeyNotAllowed>...<NullKeyNotAllowed>  
   </ErrorConfiguration>  
   ...  
</Cube >  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](cube-element-assl.md), [차원](dimension-element-assl.md)합니다 [MeasureGroup](group-element-assl.md)를 [MiningStructure](miningstructure-element-assl.md), [파티션](partition-element-assl.md)|  
|자식 요소|[KeyDuplicate](../properties/keyduplicate-element-assl.md), [KeyErrorAction](action-element-assl.md), [KeyErrorLimit](../properties/keyerrorlimit-element-assl.md)를 [KeyErrorLimitAction](../properties/keyerrorlimitaction-element-assl.md)를 [KeyErrorLogFile](file-element-assl.md)합니다 [ KeyNotFound](../properties/keynotfound-element-assl.md)하십시오 [NullKeyConvertedToUnknown](../properties/nullkeyconvertedtounknown-element-assl.md), [NullKeyNotAllowed](../properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ErrorConfiguration>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
