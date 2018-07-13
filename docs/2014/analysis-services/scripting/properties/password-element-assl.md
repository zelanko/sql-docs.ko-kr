---
title: Password 요소 (ASSL) | Microsoft Docs
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
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 99d7eabdd66e6c7f036389b4825c5926873367b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197743"
---
# <a name="password-element-assl"></a>Password 요소(ASSL)
  에 대 한 사용자 계정의 암호를 포함 합니다 [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 값 합니다 `Password` 값 뿐만 아니라 요소를 [계정](account-element-impersonationinfo-assl.md) 요소인 경우 가장 용도로 사용 됩니다 값을 [ImpersonationMode](impersonationmode-element-assl.md) 에서 파생 된 모든 요소에 대 한 요소를 `ImpersonationInfo` 데이터 유형이 설정 되어 *ImpersonateAccount*합니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 서버 관리자 역할 멤버만 `Password` 요소에 빈 값을 제공할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [DataSourceImpersonationInfo 요소 &#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
