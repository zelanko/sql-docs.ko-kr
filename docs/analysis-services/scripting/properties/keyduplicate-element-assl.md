---
title: KeyDuplicate 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b236a148c28d8e4135bcc6b5bff0592934abc6f1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="keyduplicate-element-assl"></a>KeyDuplicate 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  결정 방법을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 처리 하는 동안 발생 한 중복 키 오류를 처리 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyDuplicate>...</KeyDuplicate>  
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
 중복 키 오류는 차원 처리 중에 특성 키가 한 번 이상 발견된 경우에만 발생합니다. 특성 키는 고유해야 하므로 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 중복 레코드를 삭제합니다. 일반적으로 중복 키 오류는 특성 간 관계와 같은 차원의 디자인에 결함이 있음을 나타냅니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*IgnoreError*|오류를 무시하고 처리를 계속합니다.|  
|*ReportAndContinue*|오류를 보고하고 처리를 계속합니다.|  
|*ReportAndStop*|오류를 보고하고 처리를 중지합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **KeyDuplicate** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ErrorOption>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
