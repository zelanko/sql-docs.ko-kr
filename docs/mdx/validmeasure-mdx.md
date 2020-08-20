---
description: ValidMeasure(MDX)
title: 유효한 측정값 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd2bc2385a3445076636fb1b4001120463d1cd89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494835"
---
# <a name="validmeasure-mdx"></a>ValidMeasure(MDX)


  지정된 튜플에 대한 결과를 반환할 때 적용할 수 없는 차원을 All 수준 또는 기본 멤버(집계할 수 없는 경우)에 강제로 적용하여 큐브의 측정값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 유효 **측정값** 함수는 튜플이 반환 하는 값을 갖는 측정값의 측정값 그룹과 관계가 없는 특성을 무시 하 고 튜플의 값을 반환 합니다. 특성은 다음 두 가지 이유로 측정값과 무관할 수 있습니다.  
  
-   특성의 차원이 튜플에서 측정값의 측정값 그룹과 관계가 없습니다.  
  
-   특성의 차원이 측정값의 측정값 그룹과 관계가 없지만 세분성 특성이 키 특성이 아니며 세분성 특성이 튜플에 있는 특성과 직접적인 관계가 없습니다.  
  
 이 함수로 지정 된 동작은 기본 서버 쪽 동작으로 서, 측정값 그룹 개체의 **IgnoreUnrelatedDimensions** 속성에 의해 제어 됩니다.  
  
 튜플의 멤버가 All 멤버가 아니며 세분성이 있는 지정한 튜플의 각 특성에 대해 각 해당 특성의 현재 좌표는 다음과 같이 이동됩니다.  
  
-   지정된 특성 멤버에 연관된 특성은 현재 멤버와 함께 존재하는 멤버로 이동됩니다.  
  
-   지정한 특성 멤버에 연관시키는 특성은 All 멤버(또는 계층을 집계할 수 없는 경우 기본 멤버)로 이동됩니다.  
  
-   연관되지 않은 특성은 측정값에 따라 All 멤버로 이동됩니다.  
  
## <a name="example"></a>예제  
 다음 쿼리에서는 ValidMeasure 함수를 사용하여 IgnoreUnrelatedDimensions 속성의 동작을 재정의할 수 있는 방법을 보여 줍니다. Adventure Works 큐브에서 Sales Targets 측정값 그룹에는 False로 설정된 IgnoreUnrelatedDimensions 집합이 있습니다. MDX 스크립트에는 아래로 Month 레벨에 값을 할당하는 계산도 있지만, Date 차원은 Calendar Quarter 세분성에서 이 측정값 그룹에 조인하기 때문에 기본적으로 Sales Quota 측정값은 Calendar Quarter 아래에서 null을 반환합니다. 계산 측정값에서 ValidMeasure 함수를 사용하여 IgnoreUnrelatedDimensions가 True로 설정된 것처럼 Sales Quota 측정값이 작동하게 할 수 있으며 Sales Quota가 현재 Calendar Quarter의 값을 표시하도록 할 수 있습니다.  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 마찬가지로, Sales Targets 측정값 그룹은 Promotion 차원과 전혀 관계가 없으므로 Promotion에 있는 모든 계층의 All Member는 null을 반환합니다. 이 경우에도 ValidMeasure를 사용하여 이 동작을 변경할 수 있습니다.  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
