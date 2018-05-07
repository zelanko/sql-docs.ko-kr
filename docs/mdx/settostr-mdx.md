---
title: SetToStr (MDX) | Microsoft Docs
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
- SETTOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToStr function
ms.assetid: b761e002-26cd-460e-b424-fb8e306746fa
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 3c1cfc97d793e6614b9b2bfb8e24616581be66b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="settostr-mdx"></a>SetToStr(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정된 집합에 해당하는 MDX 형식 문자열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 이 함수를 사용하여 집합의 문자열 표현을 구문 분석을 위해 외부 함수에 전송할 수 있습니다. 반환 되는 문자열은 중괄호로 묶여 {}, 쉼표로 구분 하 여 집합의 각 항목입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Geography.Country 특성 계층의 모든 멤버를 포함하는 문자열을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
