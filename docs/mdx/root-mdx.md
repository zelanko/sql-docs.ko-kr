---
title: Root (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c2301f44cbdac4505bef95d590ce206c8b6b509
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742772"
---
# <a name="root-mdx"></a>Root(MDX)


  구성 된 튜플을 반환 된 **모든** 큐브, 차원 또는 튜플의 현재 범위 내에서 각 특성 계층 멤버입니다. 범위에 대 한 자세한 내용은 참조 [SCOPE 문 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)합니다.  
  
> [!NOTE]  
>  특성 계층에 없는 경우는 **모든** 멤버를 튜플에 해당 계층에 대 한 기본 멤버를 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>인수  
 *Dimension_Name*  
 차원 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 차원 이름과 튜플 식이 모두 지정 하는 경우는 **루트** 함수를 포함 하는 튜플을 반환는 **모든** 멤버 (또는 기본 멤버 경우는 **모든** 멤버가 존재 하지 않으면) 큐브에서 각 특성 계층입니다. 튜플의 멤버 순서는 특성 계층이 큐브 내에서 정의된 순서에 따릅니다.  
  
 차원 이름이 지정 된 경우는 **루트** 함수를 포함 하는 튜플을 반환는 **모든** 멤버 (또는 기본 멤버 경우는 **모든** 멤버가 존재 하지 않으면) 각 특성 계층의 지정된 된 차원의 현재 멤버의 컨텍스트를 기반 합니다. 튜플의 멤버 순서는 특성 계층이 차원 내에서 정의된 순서에 따릅니다.  
  
> [!NOTE]  
>  계층 이름이 지정 되는 **튜플** 함수는 지정 된 계층 이름에서 차원 이름을 선택 합니다.  
  
 튜플 식이 지정 되는 **루트** 함수는 지정 된 튜플의 교차 부분을 포함 하는 튜플을 반환 및 **모든** 지정 된 튜플에 명시적으로 포함 된 다른 모든 차원 특성의 멤버입니다.  
  
## <a name="examples"></a>예  
 포함 하는 튜플을 반환 하는 다음 예제는 **모든** 멤버 (또는 기본 경우는 **모든** 존재 하지 않습니다)는 Adventure Works 큐브에서 각 계층입니다.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 포함 하는 튜플을 반환 하는 다음 예제는 **모든** 멤버 (또는 기본 경우는 **모든** 멤버가 존재 하지 않으면) 각 계층에서 이러한 기본 멤버와 교차 하는 Measures 차원의 지정된 된 멤버의 값과 Adventure Works 큐브의 Date 차원에 있습니다.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 다음 예에서는 지정 된 튜플 멤버를 포함 하는 튜플을 반환 (2001 년 7 월 1과 함께 **모든** 멤버 (또는 기본 경우는 **모든** 멤버가 존재 하지 않으면) 각 날짜에 지정 되지 않은 계층에서 차원의 Adventure Works 큐브의 값 이러한 멤버와 교차 하는 Measures 차원의 지정된 된 멤버에 대 한 합니다.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
