---
title: 요소 (ASSL) 계정 | Microsoft Docs
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
- Accounts Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Accounts
helpviewer_keywords:
- Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 94e167c6eb804f3372fab6974403f0303f21a13a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277969"
---
# <a name="accounts-element-assl"></a>Accounts 요소(ASSL)
  에 정의 된 계정 유형의 컬렉션을 포함 한 [데이터베이스](../objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database>  
   ...  
   <Accounts>  
      <Account>...</Account>  
   </Accounts>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음(컬렉션)|  
|기본값|없음(컬렉션)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[데이터베이스](../objects/database-element-assl.md)|  
|자식 요소|[계정](../objects/account-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 차원입니다 [형식](../properties/type-element-dimension-assl.md) 로 설정 된 *계정*, Income, Expense 등 계정 유형을 지정 하는 특성을 포함할 수 있으며 등의 차원 멤버에 의해 표현 합니다. 계정 유형에 사용 됩니다 [측정값](../objects/measure-element-assl.md) 요소인입니다 [AggregationFunction](../properties/aggregatefunction-element-assl.md) 로 설정 된 *ByAccount*, 집계 함수 사용 시기를 확인 하려면 해당 차원의 멤버를 집계 합니다. `Accounts` 요소는 계정 유형 및 각 계정 유형에 사용해야 하는 집계 함수를 나타내는 `Account` 요소의 컬렉션을 보유합니다.  
  
 집계 함수를 사용 하 여 기본값과에서 다른 경우 계정 유형이 나열 되어야 합니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 각 계정 유형에 대 한 합니다.  
  
 올바른 계정 유형 집합은 고정되어 있습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AccountCollection>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [AccountType 요소 &#40;ASSL&#41;](../properties/accounttype-element-assl.md)   
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
