---
title: ErrorConfiguration 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 730f48adee4d459c453f49f742f611f6d985771e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191753"
---
# <a name="errorconfiguration-element-xmla"></a>ErrorConfiguration 요소(XMLA)
  하는 동안 발생할 수 있는 오류를 처리 하기 위한 설정을 지정 된 [일괄 처리](../xml-elements-commands/batch-element-xmla.md) 또는 [프로세스](../xml-elements-commands/process-element-xmla.md) 작업 합니다.  
  
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
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Batch](../xml-elements-commands/batch-element-xmla.md), [Process](../xml-elements-commands/process-element-xmla.md)|  
|자식 요소|[KeyDuplicate](../../scripting/properties/keyduplicate-element-assl.md), [KeyErrorAction](../../scripting/objects/action-element-assl.md), [KeyErrorLimit](../../scripting/properties/keyerrorlimit-element-assl.md)를 [KeyErrorLimitAction](../../scripting/properties/keyerrorlimitaction-element-assl.md)를 [KeyErrorLogFile](../../scripting/objects/file-element-assl.md)합니다 [ KeyNotFound](../../scripting/properties/keynotfound-element-assl.md)하십시오 [NullKeyConvertedToUnknown](../../scripting/properties/nullkeyconvertedtounknown-element-assl.md), [NullKeyNotAllowed](../../scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 구조는 ASSL(Analysis Services Scripting Language)에서 `ErrorConfiguration` 요소의 구조와 같습니다. 에 대 한 자세한 내용은 합니다 `ErrorConfiguration` 요소를 참조 하세요 [ErrorConfiguration 요소 &#40;ASSL&#41;](../../scripting/objects/errorconfiguration-element-assl.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
