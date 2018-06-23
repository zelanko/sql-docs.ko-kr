---
title: 계정 요소 (ASSL) | Microsoft Docs
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
- Account Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Account
helpviewer_keywords:
- Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0a99dbaee6e1eaec95385295cf1842ffcc336adf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185945"
---
# <a name="account-element-assl"></a>Account 요소(ASSL)
  내의 계정 유형에 대 한 세부 정보를 포함 한 [데이터베이스](database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Accounts>  
   <Account>  
      <AccountType>...</AccountType>  
      <AggregationFunction>...</AggregationFunction>  
            <Aliases>...</Aliases>  
            <Annotations>...</Annotations>  
   </Account>  
</Accounts>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[계정](../collections/accounts-element-assl.md)|  
|자식 요소|[AccountType](../properties/accounttype-element-assl.md), [AggregationFunction](../properties/aggregationfunction-element-assl.md), [별칭](../collections/aliases-element-assl.md), [주석](../collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 차원, 해당 [형식](../properties/type-element-dimension-assl.md) 로 설정 된 *계정* 차원의 멤버만 Income, Expense 등 계정 유형을 지정 하 고 표시 되 면 특성이 하나씩 있을 수 있습니다. 계정 유형을 사용 합니다 [측정값](measure-element-assl.md) 요소를 가진 [AggregationFunction](../properties/aggregatefunction-element-assl.md) 로 설정 된 *ByAccount*, 집계 함수를 사용 하는 경우를 확인 하려면 해당 차원의 멤버를 집계 합니다. `Account` 요소는 단일 계정 유형 및 해당 측정값에 사용되어야 하는 집계 함수를 나타냅니다.  
  
 집계 함수에서 사용 되는 기본값과에서 다른 경우 계정 유형이 나열 되어야 합니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 각 계정 유형에 대 한 합니다.  
  
 올바른 계정 유형 집합은 고정되어 있습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Account>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Database 요소 &#40;ASSL&#41;](database-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  