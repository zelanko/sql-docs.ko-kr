---
title: CoalesceEmpty (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COALESCEEMPTY
dev_langs: kbMDX
helpviewer_keywords: CoalesceEmpty function
ms.assetid: c00dd739-44bc-4af6-9871-c7e1e3f3e5ba
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d02d253d39a605405df747b49fd0a762913030f1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  빈 셀 값을 비어 있지 않은 특정 셀 값으로 변환합니다. 지정된 셀 값은 숫자이거나 문자열일 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>인수  
 *Numeric_Expression1*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression2*  
 유효한 숫자 식으로서, 일반적으로 지정된 숫자 값입니다.  
  
 *String_Expression1*  
 문자열을 반환하는 셀 좌표의 유효한 문자열 식으로서, 일반적으로 MDX 식입니다.  
  
 *String_Expression2*  
 첫 번째 문자열 식에서 반환되는 NULL을 대체하는 유효한 문자열 식으로서, 일반적으로 지정된 문자열 값입니다.  
  
## <a name="remarks"></a>주의  
 하나 이상의 숫자 식이 지정 된 된 **CoalesceEmpty** 함수는 비어 있지 않은 값으로 확인 될 수 있는 (왼쪽에서 오른쪽) 첫 번째 숫자 식의 숫자 값을 반환 합니다. 모든 지정된 숫자 식이 비어 있지 않은 값으로 확인될 수 없으면 함수가 빈 셀 값을 반환합니다. 일반적으로 두 번째 숫자 식의 값은 첫 번째 숫자 식에서 반환되는 NULL을 대체하는 숫자 값입니다.  
  
 문자열 식이 하나 이상 지정된 경우 이 함수는 비어 있지 않은 값으로 확인될 수 있는 첫 번째 문자열 식(왼쪽에서 오른쪽의 순서로)의 문자열 값을 반환합니다. 모든 지정된 문자열 식이 비어 있지 않은 값으로 확인될 수 없으면 함수가 빈 셀 값을 반환합니다. 일반적으로 두 번째 문자열 식의 값은 첫 번째 문자열 식에서 반환되는 NULL을 대체하는 문자열 값입니다.  
  
 **CoalesceEmpty** 함수에는 동일한 형식의 값만 사용할 수 있습니다. 즉, 지정된 모든 값 식이 숫자 데이터 형식이나 빈 셀 값으로 계산되거나 지정된 모든 값 식이 문자열 데이터 형식 또는 빈 셀 값으로 계산되어야 합니다. 이 함수에 대한 단일 셀에는 숫자 및 문자열 식이 모두 포함될 수 없습니다.  
  
 빈 셀에 대한 자세한 내용은 OLE DB 설명서를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제 쿼리에서 **Adventure Works** 큐브. 이 예에서는 각 제품의 주문 수량과 범주별 주문 수량의 비율을 반환합니다. **CoalesceEmpty** 함수를 사용 하면 계산된 멤버의 서식을 지정할 때 null 값 영 (0)로 표현 됩니다.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
