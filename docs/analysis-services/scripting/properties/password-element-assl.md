---
title: Password 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1ae6eed7fd8f98aa026fceaf79efe8b5643660fa
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="password-element-assl"></a>Password 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  에 대 한 사용자 계정의 암호를 포함 된 [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 값은 **암호** 의 값과 함께 요소는 [계정](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md) 요소를 경우 가장 용도로 사용 됩니다 값은 [ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md) 요소에 대 한 파생 된 모든 요소는 **ImpersonationInfo** 데이터 유형이 설정 되어 *ImpersonateAccount*합니다.  
  
 에 대 한 서버 관리자 역할의 구성원만는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대 한 빈 값을 제공할 수는 **암호** 요소  
  
## <a name="see-also"></a>관련 항목:  
 [DataSourceImpersonationInfo 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
