---
title: ImpersonationInfoSecurity 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ImpersonationInfoSecurity Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ImpersonationInfoSecurity element
ms.assetid: 583fec36-90ef-4d6a-9888-ece6ae865c53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4aaf5aee83f6aa6102aeeb9488ddb7a75c4af540
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224914"
---
# <a name="impersonationinfosecurity-element-assl"></a>ImpersonationInfoSecurity 요소(ASSL)
  제공 되는 보안 자격 증명에 변경 된 경우를 나타내는 읽기 전용 값이 포함 된 [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationInfoSecurity>...</ImpersonationInfoSecurity>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*PasswordRemoved*|제공된 보안 자격 증명에서 암호 정보가 제거되었습니다.|  
|*Unchanged*|제공된 보안 자격 증명이 변경되지 않았습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `ImpersonationInfoSecurity`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ImpersonationInfoSecurity>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
