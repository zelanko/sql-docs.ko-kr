---
title: NullKeyConvertedToUnknown 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c3d101e2577a7e691aae685bcf821979b5640182
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="nullkeyconvertedtounknown-element-assl"></a>NullKeyConvertedToUnknown 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*IgnoreError*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 키 열에 null 값은 있어서로 해석 하는 경우 null 변환 오류가 발생 된 **알 수 없는** 멤버입니다. 경우에이 오류가 발생 하는 반면는 [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md) 에 대 한 요소는 [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) 의 상위 항목은 **ErrorConfiguration** 로 설정 된 부모  *UnknownMember*합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*IgnoreError*|오류를 무시하고 처리를 계속합니다.|  
|*ReportAndContinue*|오류를 보고하고 처리를 계속합니다.|  
|*ReportAndStop*|오류를 보고하고 처리를 중지합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **NullKeyConvertedToUnknown** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ErrorOption>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ErrorConfiguration 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
