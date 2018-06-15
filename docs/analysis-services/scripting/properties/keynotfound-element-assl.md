---
title: KeyNotFound 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bfce07b37bd43b18c769212f7647ec311fec4fa3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033684"
---
# <a name="keynotfound-element-assl"></a>KeyNotFound 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  지정 방법을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 참조 무결성 오류가 발생할 때 응답 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyNotFound>...</KeyNotFound>  
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
 참조 무결성 오류는 종속 테이블의 외래 키 값과 일치하는 항목이 부모 테이블에 없는 경우에 발생합니다. 이러한 오류는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 팩트 테이블에서 해당 차원의 차원 테이블에 존재하지 않는 외래 키 값을 참조하는 차원을 처리하는 경우 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 파티션에 포함된 차원의 주 차원 테이블에서 연결된 다른 차원 테이블에 존재하지 않는 키 값을 참조할 때 해당 파티션을 처리하는 경우에 발생합니다. 부모 자식 계층 및 부모 특성이 있는 차원의 경우 파티션에 포함된 차원의 주 차원 테이블이 동일한 차원 테이블에 존재하지 않는 키 값을 참조하는 경우에도 참조 무결성 오류가 발생할 수 있습니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*IgnoreError*|오류를 무시하고 처리를 계속합니다.|  
|*ReportAndContinue*|오류를 보고하고 처리를 계속합니다.|  
|*ReportAndStop*|오류를 보고하고 처리를 중지합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **KeyNotFound** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ErrorOption>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
