---
title: 요소 (ImpersonationInfo) (ASSL) 계정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Account Element (ImpersonationInfo)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f454e39a7c4ec4911f38ff070f94fcbe50a34c74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190373"
---
# <a name="account-element-impersonationinfo-assl"></a>Account 요소(ImpersonationInfo)(ASSL)
  에 대 한 사용자 계정의 이름을 포함 합니다 [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 값 합니다 `Account` 값 뿐만 아니라 요소를 [암호](password-element-assl.md) 요소인 경우 가장 용도로 사용 됩니다 값을 [ImpersonationMode](impersonationmode-element-assl.md) 에서 파생 된 모든 요소에 대 한 요소를 `ImpersonationInfo` 데이터 유형이 설정 되어 *ImpersonateAccount*합니다.  
  
## <a name="see-also"></a>관련 항목  
 [DataSourceImpersonationInfo 요소 &#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
