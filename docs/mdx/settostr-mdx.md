---
title: SetToStr (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e0a2db653917d53ac25c290bd6dc14f3afe2cd09
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="settostr-mdx"></a>SetToStr(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 집합에 해당하는 MDX 형식 문자열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 이 함수를 사용하여 집합의 문자열 표현을 구문 분석을 위해 외부 함수에 전송할 수 있습니다. 반환되는 문자열은 중괄호로 {}로 묶이고 집합 내의 각 항목은 쉼표로 구분됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Geography.Country 특성 계층의 모든 멤버를 포함하는 문자열을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

