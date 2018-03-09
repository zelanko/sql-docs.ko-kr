---
title: "계정 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Accounts Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Accounts
helpviewer_keywords: Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 68975a4da8425a423f38bed174c180ea5d27299b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="accounts-element-assl"></a>Accounts 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]에 정의 된 계정 유형의 컬렉션을 포함 한 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.  
  
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
|부모 요소|[데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|자식 요소|[계정](../../../analysis-services/scripting/objects/account-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 차원, 해당 [형식](../../../analysis-services/scripting/properties/type-element-dimension-assl.md) 로 설정 된 *계정*, Income, Expense 등 계정 유형을 지정 하는 특성을 보유할 수 있으며 등의 차원 멤버에 의해 표현 합니다. 계정 유형을 사용 합니다 [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md) 요소를 가진 [AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md) 로 설정 된 *ByAccount*, 집계 함수를 사용 하는 경우를 확인 하려면 해당 차원의 멤버를 집계 합니다. **Accounts** 요소는 계정 유형 및 각 계정 유형에 사용해야 하는 집계 함수를 나타내는 **Account** 요소의 컬렉션을 보유합니다.  
  
 집계 함수에서 사용 되는 기본값과에서 다른 경우 계정 유형이 나열 되어야 합니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 각 계정 유형에 대 한 합니다.  
  
 올바른 계정 유형 집합은 고정되어 있습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.AccountCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [AccountType 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)   
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
