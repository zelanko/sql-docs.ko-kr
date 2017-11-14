---
title: "NullKeyNotAllowed 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- NullKeyNotAllowed Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NullKeyNotAllowed
helpviewer_keywords:
- NullKeyNotAllowed element
ms.assetid: 4ece99eb-954b-4da1-add4-dd9efd5fff0a
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 834a0e3728c99d41db1e7871e2c95eec96d1b922
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*ReportAndContinue*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 Null 값이 허용되지 않는 키 열에 Null 값이 발견되면 Null 키 오류가 발생하고 처리하는 동안 해당 레코드를 삭제합니다. 경우에이 오류가 발생 하는 반면는 [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md) 에 대 한 요소는 **DataItem** 의 상위 항목은 **ErrorConfiguration** 로 설정 된 부모  *오류*합니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*IgnoreError*|오류를 무시하고 처리를 계속합니다.|  
|*ReportAndContinue*|오류를 보고하고 처리를 계속합니다.|  
|*ReportAndStop*|오류를 보고하고 처리를 중지합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **NullKeyNotAllowed** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ErrorOption>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ErrorConfiguration 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)  
  
  

