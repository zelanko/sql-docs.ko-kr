---
title: ErrorConfiguration 요소 (XMLA) | Microsoft Docs
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
- http://schemas.microsoft.com/analysisservices/2003/engine#ErrorConfiguration
- urn:schemas-microsoft-com:xml-analysis#ErrorConfiguration
- microsoft.xml.analysis.errorconfiguration
helpviewer_keywords:
- ErrorConfiguration element
ms.assetid: 5e350f5f-3a14-49b4-80c0-208c61f336d5
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1ce9cf2dc862f187c1a9f9cb9e3403e01ade0cfa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092484"
---
# <a name="errorconfiguration-element-xmla"></a>ErrorConfiguration 요소(XMLA)
  중에 발생할 수 있는 오류를 처리 하기 위한 설정을 지정는 [일괄 처리](../xml-elements-commands/batch-element-xmla.md) 또는 [프로세스](../xml-elements-commands/process-element-xmla.md) 작업 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Batch> <!-- or Process -->  
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
</Batch>  
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
|부모 요소|[Batch](../xml-elements-commands/batch-element-xmla.md), [Process](../xml-elements-commands/process-element-xmla.md)|  
|자식 요소|[KeyDuplicate](../../scripting/properties/keyduplicate-element-assl.md), [KeyErrorAction](../../scripting/objects/action-element-assl.md), [KeyErrorLimit](../../scripting/properties/keyerrorlimit-element-assl.md), [KeyErrorLimitAction](../../scripting/properties/keyerrorlimitaction-element-assl.md), [KeyErrorLogFile](../../scripting/objects/file-element-assl.md), [ KeyNotFound](../../scripting/properties/keynotfound-element-assl.md), [NullKeyConvertedToUnknown](../../scripting/properties/nullkeyconvertedtounknown-element-assl.md), [NullKeyNotAllowed](../../scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 구조는 ASSL(Analysis Services Scripting Language)에서 `ErrorConfiguration` 요소의 구조와 같습니다. 에 대 한 자세한 내용은 `ErrorConfiguration` 요소 참조 [ErrorConfiguration 요소 &#40;ASSL&#41;](../../scripting/objects/errorconfiguration-element-assl.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  