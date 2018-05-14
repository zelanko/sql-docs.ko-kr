---
title: AccountType 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5258ff60c8dfafefbf81f87d3538c396c085ccac
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="accounttype-element-assl"></a>AccountType 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  에 정의 된 계정 유형의 이름을 포함 한 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[계정](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Income*|수입 계정입니다.|  
|*Expense*|지출 계정입니다.|  
|*Flow*|현금 흐름 계정입니다.|  
|*Balance*|잔액 계정입니다.|  
|*Asset*|자산 계정입니다.|  
|*Liability*|부채 계정입니다.|  
|*통계*|통계 계정입니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거 **AccountType** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AccountTypes>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 계정 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
