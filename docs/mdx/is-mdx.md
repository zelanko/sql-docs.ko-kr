---
title: IS (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS
dev_langs:
- kbMDX
helpviewer_keywords:
- IS operator
ms.assetid: dc8c0b91-3bb1-49e5-8d70-57545baaa8e0
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 97183b67350b6d3db613bb8bc8e957642bf5bb76
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="is-mdx"></a>IS(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  두 개체 식에 대해 논리 비교를 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Expression1*  
 MDX 개체 참조를 반환하는 유효한 MDX 식입니다.  
  
 *Expression2*  
 MDX 개체 참조를 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 하는 부울 값 **true** 두 인수는 같은 개체;를 참조 하는 경우 이렇게 하지 않으면 **false**합니다. 경우는 **NULL** 연산자 반환 키워드를 지정 **true** 경우 *Expression1* 은 **null**, 그렇지 않으면 **false**합니다.  
  
## <a name="remarks"></a>주의  
 **IS** 연산자는 대개 튜플 및 멤버가 지 확인 idempotent 값과 동일을 있음을 의미 합니다.  
  
## <a name="examples"></a>예  
 사용 하는 방법을 보여 주는 다음 예제는 **IS** 연산자 축에 있는 현재 멤버가 특정 멤버 인지 확인 하려면:  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

