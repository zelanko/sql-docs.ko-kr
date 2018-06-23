---
title: AccountType 요소 (ASSL) | Microsoft Docs
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
- AccountType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AccountType
helpviewer_keywords:
- AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ff7203d2882689b21a6ab3171880c26a8d385f7b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181896"
---
# <a name="accounttype-element-assl"></a>AccountType 요소(ASSL)
  에 정의 된 계정 유형의 이름을 포함 한 [데이터베이스](../objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[계정](../objects/account-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*수입*|수입 계정입니다.|  
|*비용*|지출 계정입니다.|  
|*흐름*|현금 흐름 계정입니다.|  
|*잔액*|잔액 계정입니다.|  
|*자산*|자산 계정입니다.|  
|*책임*|부채 계정입니다.|  
|*통계*|통계 계정입니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `AccountType`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.AccountTypes>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소 계정 &#40;ASSL&#41;](../collections/accounts-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  