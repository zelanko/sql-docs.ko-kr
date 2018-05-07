---
title: IsGeneration (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ISGENERATION
dev_langs:
- kbMDX
helpviewer_keywords:
- IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b40d895af5298cf3538280a3875363401819930d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="isgeneration-mdx"></a>IsGeneration(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버가 지정한 세대에 속하는지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Generation_Number*  
 지정된 멤버가 평가되는 기준 세대를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 **IsGeneration** 함수에서 반환 **true** 지정된 된 멤버의 지정 된 세대 번호에 있으면 합니다. 그렇지 않으면 함수가 반환 **false**합니다. 또한 지정 된 멤버가 빈 멤버 이면로 평가 되 면는 **IsGeneration** 함수에서 반환 **false**합니다.  
  
 세대 인덱싱을 위해 리프 멤버는 세대 인덱스 0입니다. 리프가 아닌 멤버의 세대 인덱스는 지정된 멤버에 대한 모든 자식 멤버의 합집합에서 가장 높은 세대 인덱스를 가져와서 1을 더하는 방식으로 결정됩니다. 리프가 아닌 멤버의 세대 인덱스의 결정 방법으로 인해 리프가 아닌 특정 멤버는 둘 이상의 세대에 속할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 [Date].[Fiscal].CurrentMember가 두 번째 세대에 속하는 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
