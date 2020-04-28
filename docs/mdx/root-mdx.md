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
ms.openlocfilehash: be687d5cbfd4fdbb706ef5c10778a4f3e3f93197
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68037046"
---
# <a name="root-mdx"></a>Root(MDX)


  큐브, 차원 또는 튜플의 현재 범위 내에 있는 각 특성 계층의 **모든** 멤버로 구성 된 튜플을 반환 합니다. 범위에 대 한 자세한 내용은 [Scope 문 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)를 참조 하세요.  
  
> [!NOTE]  
>  특성 계층에 **All** 멤버가 없으면 튜플은 해당 계층에 대 한 기본 멤버를 포함 합니다.  
  
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
  
## <a name="remarks"></a>설명  
 차원 이름 또는 튜플 식이 모두 지정 되지 않은 경우 **루트** 함수는 큐브의 각 특성 계층에서 **all** 멤버 (또는 **all** 멤버가 없는 경우 기본 멤버)가 들어 있는 튜플을 반환 합니다. 튜플의 멤버 순서는 특성 계층이 큐브 내에서 정의된 순서에 따릅니다.  
  
 차원 이름이 지정 된 경우 **루트** 함수는 현재 멤버의 컨텍스트를 기반으로 지정 된 차원에 있는 각 특성 계층에서 **All** 멤버 ( **all** 멤버가 없는 경우 기본 멤버)가 포함 된 튜플을 반환 합니다. 튜플의 멤버 순서는 특성 계층이 차원 내에서 정의된 순서에 따릅니다.  
  
> [!NOTE]  
>  계층 이름이 지정 된 경우 **튜플** 함수는 지정 된 계층 이름에서 차원 이름을 선택 합니다.  
  
 튜플 식이 지정 된 경우 **루트** 함수는 지정 된 튜플에 대해 명시적으로 포함 되지 않은 다른 모든 차원 특성의 **모든** 멤버와 지정 된 튜플의 교집합을 포함 하는 튜플을 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 어드벤처 큐브의 각 계층에서 **all** 멤버 (또는 **all** 멤버가 없는 경우 기본값)를 포함 하는 튜플을 반환 합니다.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 놀이 Works 큐브의 Date 차원에 있는 각 계층의 **all** 멤버 (또는 **all** 멤버가 없는 경우 기본값)를 포함 하는 튜플을 반환 하 고 이러한 기본 멤버와 교차 하는 측정값 차원의 지정 된 멤버 값을 반환 합니다.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 다음 예에서는 Date dimension 놀이 Works 큐브의 지정 되지 않은 각 계층에서 지정 된 튜플 멤버 (또는 All **멤버가 없는** 경우 기본값)와 함께 지정 된 튜플 멤버 2001 (또는 **all** 멤버가 없는 경우 기본값)를 포함 하는 튜플을 반환 하 고 이러한 멤버와 교차 하는 측정값 차원의 지정 된 멤버 값을 반환 합니다.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
