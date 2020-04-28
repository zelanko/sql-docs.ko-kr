---
title: StrToTuple (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 232d1e94892165430867ec5217f8c87ccd625b48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036707"
---
# <a name="strtotuple-mdx"></a>StrToTuple(MDX)


  MDX 형식 문자열에 의해 지정 된 튜플을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>인수  
 *Tuple_Specification*  
 직접 또는 간접적으로 튜플을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 **Strtotuple** 함수는 지정 된 집합을 반환 합니다. **Strtotuple** 함수는 일반적으로 외부 함수에서 다시 MDX 문으로 튜플 사양을 반환 하는 사용자 정의 함수와 함께 사용 됩니다.  
  
-   CONSTRAINED 플래그를 사용할 경우 튜플 사양에는 정규화되거나 정규화되지 않은 멤버 이름을 포함해야 합니다. 이 플래그를 사용하면 지정한 문자열을 통한 삽입 공격 위험을 줄일 수 있습니다. 정규화 되거나 정규화 되지 않은 멤버 이름으로 직접 확인할 수 없는 문자열을 제공 하는 경우 "STRTOTUPLE 함수에서 제한 된 플래그에 의해 적용 된 제한을 위반 했습니다." 라는 오류가 나타납니다.  
  
-   CONSTRAINED 플래그를 사용하지 않을 경우 지정한 튜플은 튜플을 반환하는 유효한 MDX 식으로 확인될 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 2004년에 대한 Bayern 멤버의 Reseller Sales Amount 측정값을 반환합니다. 제공되는 튜플 사양에는 유효한 MDX 튜플 식이 포함됩니다.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 2004년에 대한 Bayern 멤버의 Reseller Sales Amount 측정값을 반환합니다. 제공되는 튜플 사양에는 CONSTRAINED 플래그에 필요한 정규화된 멤버 이름이 포함됩니다.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 2004년에 대한 Bayern 멤버의 Reseller Sales Amount 측정값을 반환합니다. 제공되는 튜플 사양에는 유효한 MDX 튜플 식이 포함됩니다.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 CONSTRAINED 플래그로 인해 오류가 반환됩니다. 지정된 튜플 사양에 유효한 MDX 튜플 식이 들어 있지만 CONSTRAINED 플래그가 있으므로 튜플 사양에 정규화되거나 정규화되지 않은 멤버 이름이 필요합니다.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
