---
title: ImpersonationMode 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ImpersonationMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ImpersonateMode
helpviewer_keywords:
- ImpersonateMode element
ms.assetid: 160fdcb2-ac9f-4c5a-a0eb-a5f7669166b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87a68d6ef1035d7caf1d787d9ab44578d17c5489
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105151"
---
# <a name="impersonationmode-element-assl"></a>ImpersonationMode 요소(ASSL)
  파생 된 요소에 대 한 가장 방법을 나타내는 값을 포함 합니다 [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationMode>...</ImpersonationMode>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*기본값*|  
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
|*기본값*|부모가 가장이 사용되는 컨텍스트에 대해 가장 적합한 가장 방법을 사용합니다.|  
|*ImpersonateAccount*|부모가 부모 요소에 지정된 사용자 계정의 자격 증명을 사용합니다.|  
|*ImpersonateAnonymous*|부모가 익명 사용자의 자격 증명을 사용합니다.|  
|*ImpersonateCurrentUser*|부모가 현재 사용자의 자격 증명을 사용합니다.|  
|*ImpersonateServiceAccount*|인스턴스와 연결 된 서비스 계정의 자격 증명을 사용 하는 부모 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `ImpersonationMode`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ImpersonationLevel>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
