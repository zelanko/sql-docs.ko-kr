---
title: Generate (MDX) | Microsoft Docs
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
- GENERATE
dev_langs:
- kbMDX
helpviewer_keywords:
- Generate function
ms.assetid: 696a229d-c2f1-47b7-9dca-7b0a6b547d9b
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e78dec45044cc29e375b9116886b183013c74ef1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="generate-mdx"></a>Generate(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  한 집합을 다른 집합의 각 멤버에 적용하고 결과 집합을 합집합으로 결합시킵니다. 또는 집합에 대해 문자열 식을 계산하여 생성된 연결 문자열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *String_Expression*  
 유효한 문자열 식으로서, 일반적으로 지정된 집합에 있는 각 튜플의 현재 멤버 이름(CurrentMember.Name)입니다.  
  
 *구분 기호*  
 문자열 식으로 표현된 유효한 구분 기호입니다.  
  
## <a name="remarks"></a>주의  
 두 번째 집합을 지정 하는 경우는 **생성** 함수는 첫 번째 집합의 각 튜플에 두 번째 집합의 튜플을 적용 하 여 생성 된 집합을 반환*,* 다음 결과 조인 공용 구조체에 의해 가져오거나 설정 합니다. 경우 **모든** 지정 된 경우 함수는 결과 집합에 중복을 유지 합니다.  
  
 문자열 식이 지정 되는 **생성** 함수는 첫 번째 집합의 각 튜플에 대해 지정 된 문자열 식을 계산 하 여 생성 된 문자열을 반환*,* 계산한 다음 결과 연결 합니다. 연결된 문자열에서 각 결과를 구분하여 문자열을 구분할 수도 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="set"></a>Set  
 다음 예에서 [Date].[Calendar Year].[Calendar Year].MEMBERS 집합에 4개의 멤버가 있으므로 쿼리는 Internet Sales Amount 측정값을 포함하는 집합을 4번 반환합니다.  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 ALL을 제거하면 Internet Sales Amount가 한 번만 반환되도록 쿼리가 변경됩니다.  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 가장 일반적으로 사용 **생성** 집합 복잡 한 계산 하는 멤버의 집합에 대해 TopCount와 같은 식에 있습니다. 다음 예제 쿼리에서는 Rows의 각 Calendar Year에 대한 상위 10개의 Product를 표시합니다.  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 다른 상위 10 개의 각 연도 및에 대 한 표시 사용 **생성** 이 결과 얻기 위해 불가피 합니다. 다음 예와 같이 단순히 Calendar Year와 상위 10개의 Product 집합을 Crossjoin하면 매년 상위 10개의 Product가 항상 반복하여 표시됩니다.  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 다음 예제에서는 사용을 보여 줍니다. **생성** 문자열을 반환 합니다.  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  이러한 형태의 **생성** 함수 수 유용할 수 계산을 디버깅할 때 집합의 모든 멤버의 이름을 표시 하는 문자열을 반환할 수 있습니다. 이 집합의 엄격한 MDX 표현 보다 읽기 쉬울 수 있습니다 하는 [SetToStr &#40; Mdx&#41; ](../mdx/settostr-mdx.md) 함수에서 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
