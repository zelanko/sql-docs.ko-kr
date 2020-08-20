---
description: SCOPE 문(MDX)
title: SCOPE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c9f6738b2d7e0764e750b25f09001b7e9d3864a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483866"
---
# <a name="mdx-scripting---scope"></a>MDX 스크립팅 - SCOPE


  지정된 MDX 문의 범위를 지정된 하위 큐브로 제한합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>인수  
 *Subcube_Expression*  
 유효한 MDX 식입니다.  
  
 *MDX_Statement*  
 유효한 MDX 식입니다.  
  
 *Common_Grain_Members*  
 세분성이 동일한 멤버로 평가되는 유효한 MDX 문입니다.  
  
 *single_tuple*  
 단일 튜플입니다.  
  
## <a name="remarks"></a>설명  
 SCOPE 문은 하나 이상의 MDX 문을 실행하여 영향을 받는 하위 큐브를 결정합니다. MDX 문이 SCOPE 문 내로 제한되지 않는 이상 MDX 문의 암시적 범위는 전체 큐브입니다.  
  
> [!NOTE]  
>  숨겨진 멤버는 SCOPE 문에서 노출됩니다.  
  
 범위 문은 **MDX 호환성** 설정에 관계 없이 "구멍"을 노출 하는 하위 큐브를 만듭니다. 예를 들어 `Scope( Customer.State.members )` 문은 주는 포함하지 않지만 보이지 않는 자리 표시자 멤버가 삽입된 국가 또는 지역의 주를 포함할 수 있습니다.  
  
 SCOPE 문 내에서 만든 명명된 집합과 계산 멤버는 SCOPE 문에 의해 영향을 받지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예는 놀이 Works 샘플 솔루션의 MDX 계산 스크립트에서 현재 범위를 회계 연도 2005 및 sales amount quota 측정값의 회계 분기로 정의한 다음 **ParallelPeriod** 함수를 사용 하 여 현재 범위에 있는 셀에 값을 할당 합니다. 그런 다음이 예에서는 다른 SCOPE 문을 사용 하 여 범위를 수정한 다음 [이 (MDX)](../mdx/this-mdx.md) 함수를 사용 하 여 다른 할당을 수행 합니다.  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 스크립팅 문&#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
