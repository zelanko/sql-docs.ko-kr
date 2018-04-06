---
title: Levels (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Levels
dev_langs:
- kbMDX
helpviewer_keywords:
- Levels function
ms.assetid: 1a989cc9-8aa8-4ec3-b5e9-795d6fa84983
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1898b87749b8ae2921e71d391f8bbae3374d893b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="levels-mdx"></a>Levels(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  차원 또는 계층에서의 위치가 숫자 식에 의해 지정되거나 이름이 문자열 식에 의해 지정되는 수준을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Number*  
 수준 번호를 지정하는 유효한 숫자 식입니다.  
  
 *Level_Name*  
 수준 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 수준 번호를 지정 하는 경우는 **수준** 함수는 지정 된 0부터 시작 위치와 관련 된 수준을 반환 합니다.  
  
 수준 이름이 지정 되는 **수준** 함수는 지정 된 수준을 반환 합니다.  
  
> [!NOTE]  
>  사용자 정의 함수에 대해서는 문자열 식 구문을 사용합니다.  
  
## <a name="examples"></a>예  
 다음 예제는 설명의 각는 **수준** 함수 구문을 합니다.  
  
### <a name="numeric"></a>숫자  
 다음 예에서는 Country 수준을 반환합니다.  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 다음 예에서는 Country 수준을 반환합니다.  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
