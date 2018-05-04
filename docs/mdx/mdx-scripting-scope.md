---
title: SCOPE 문 (MDX) | Microsoft Docs
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
- SCOPE
dev_langs:
- kbMDX
helpviewer_keywords:
- scope [MDX]
- SCOPE statement
ms.assetid: ceab459d-b601-4468-b3fc-4f5bb4a1805f
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 7cb864de089645a137676d7d8607e988e084939e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-scripting---scope"></a>MDX 스크립팅-범위
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>주의  
 SCOPE 문은 하나 이상의 MDX 문을 실행하여 영향을 받는 하위 큐브를 결정합니다. MDX 문이 SCOPE 문 내로 제한되지 않는 이상 MDX 문의 암시적 범위는 전체 큐브입니다.  
  
> [!NOTE]  
>  숨겨진 멤버는 SCOPE 문에서 노출됩니다.  
  
 SCOPE 문을에 관계 없이 "구멍"을 노출 하는 하위 큐브를 만듭니다.는 **MDX Compatibility** 설정 합니다. 예를 들어 `Scope( Customer.State.members )` 문은 주는 포함하지 않지만 보이지 않는 자리 표시자 멤버가 삽입된 국가 또는 지역의 주를 포함할 수 있습니다.  
  
 SCOPE 문 내에서 만든 명명된 집합과 계산 멤버는 SCOPE 문에 의해 영향을 받지 않습니다.  
  
## <a name="example"></a>예제  
 Adventure Works 예제 솔루션에서 MDX 계산 스크립트에서 다음 예제에서는 2005 회계 연도의 판매 할당액 측정값에 회계 분기와 현재 범위를 정의 하 고 사용 하 여 현재 범위에 있는 셀에 값을 할당 한 다음는 **ParallelPeriod** 함수입니다. 이 예제에서는 다음 다른 SCOPE 문을 사용 하 여 범위를 수정 하 고 다음 사용 하 여 다른 할당을 수행 된 [This (MDX)](../mdx/this-mdx.md) 함수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 스크립팅 문 & #40; Mdx& #41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
