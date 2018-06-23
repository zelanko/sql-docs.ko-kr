---
title: NullKeyNotAllowed 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- NullKeyNotAllowed Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullKeyNotAllowed
helpviewer_keywords:
- NullKeyNotAllowed element
ms.assetid: 4ece99eb-954b-4da1-add4-dd9efd5fff0a
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 235c76fb2b8cad1682fab97f36cb1867d7c82c38
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079845"
---
# <a name="nullkeynotallowed-element-assl"></a>NullKeyNotAllowed 요소(ASSL)
  결정 방법을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 처리 엔진이 처리 도중 발생 한 null 키 오류를 처리 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ErrorConfiguration>  
   ...  
   <NullKeyNotAllowed>...</NullKeyNotAllowed>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*ReportAndContinue*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Null 값이 허용되지 않는 키 열에 Null 값이 발견되면 Null 키 오류가 발생하고 처리하는 동안 해당 레코드를 삭제합니다. 경우에이 오류가 발생 하는 반면는 [NullProcessing](nullprocessing-element-assl.md) 에 대 한 요소는 `DataItem` 의 상위 항목은 `ErrorConfiguration` 로 설정 된 부모 *오류*합니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*IgnoreError*|오류를 무시하고 처리를 계속합니다.|  
|*ReportAndContinue*|오류를 보고하고 처리를 계속합니다.|  
|*ReportAndStop*|오류를 보고하고 처리를 중지합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `NullKeyNotAllowed`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ErrorOption>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ErrorConfiguration 요소 &#40;ASSL&#41;](../objects/errorconfiguration-element-assl.md)  
  
  