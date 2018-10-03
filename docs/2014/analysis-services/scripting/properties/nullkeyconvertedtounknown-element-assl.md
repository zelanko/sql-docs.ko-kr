---
title: NullKeyConvertedToUnknown 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NullKeyConvertedToUnknown Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullKeyConvertedToUnknown
helpviewer_keywords:
- NullKeyConvertedToUnknown element
ms.assetid: 1a6cde33-01ba-4095-b464-16d1ad3c6905
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6aaf78e4081b0f2fe04bf9b4037639f5b86f5311
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121723"
---
# <a name="nullkeyconvertedtounknown-element-assl"></a>NullKeyConvertedToUnknown 요소(ASSL)
  Null 변환 오류가 발생할 때 수행할 동작을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*IgnoreError*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 키 열에 Null 값이 있으며 이 값이 `Unknown` 멤버로 해석되는 경우 Null 변환 오류가 발생합니다. 경우에이 오류가 발생 하는 반면를 [NullProcessing](nullprocessing-element-assl.md) 요소를 [DataItem](../data-type/dataitem-data-type-assl.md) 의 상위 항목을 `ErrorConfiguration` 부모 요소가로 설정 되어 *UnknownMember*합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*IgnoreError*|오류를 무시하고 처리를 계속합니다.|  
|*ReportAndContinue*|오류를 보고하고 처리를 계속합니다.|  
|*ReportAndStop*|오류를 보고하고 처리를 중지합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `NullKeyConvertedToUnknown`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ErrorOption>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ErrorConfiguration 요소 &#40;ASSL&#41;](../objects/errorconfiguration-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
