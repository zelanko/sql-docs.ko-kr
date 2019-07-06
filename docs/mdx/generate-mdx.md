---
title: Generate (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c965300654f8cbebdf6fbd88699afdd512632488
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597440"
---
# <a name="generate-mdx"></a>Generate(MDX)


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
  
## <a name="remarks"></a>Remarks  
 두 번째 집합을 지정 합니다 **생성** 함수는 첫 번째 집합의 각 튜플에 두 번째 집합의 튜플을 적용 하 여 생성 된 집합을 반환 하 고 결과 조인한 다음 집합을 union으로 합니다. 하는 경우 **모든** 지정 된 경우 함수에는 결과 집합에 중복 요소가 유지 됩니다.  
  
 문자열 식이 지정 하는 경우는 **생성** 함수는 지정 된 문자열 식을 첫 번째 집합의 각 튜플에 대해 계산한 다음 결과 연결 하 여 생성 된 문자열을 반환 합니다. 연결된 문자열에서 각 결과를 구분하여 문자열을 구분할 수도 있습니다.  
  
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
  
 가장 일반적으로 사용 **생성** 집합 복잡 한 계산 하는 멤버 집합에 대해 TopCount와 같은 식에 있습니다. 다음 예제 쿼리에서는 Rows의 각 Calendar Year에 대한 상위 10개의 Product를 표시합니다.  
  
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
  
 다른 상위 10 개의 각 연도에 표시 됩니다 사용 **생성** 해야만이 결과 얻을 수 있습니다. 다음 예와 같이 단순히 Calendar Year와 상위 10개의 Product 집합을 Crossjoin하면 매년 상위 10개의 Product가 항상 반복하여 표시됩니다.  
  
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
  
### <a name="string"></a>문자열  
 다음 예제에서는 사용을 보여 줍니다 **생성** 문자열을 반환 합니다.  
  
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
>  이러한 형태의 합니다 **생성** 함수 유용할 수 있습니다 계산을 디버깅할 때 집합의 모든 멤버의 이름을 표시 하는 문자열을 반환할 수 있습니다. 이 집합의 엄격한 MDX 표현 보다 읽기 쉬울 수 있습니다 하는 [SetToStr &#40;MDX&#41; ](../mdx/settostr-mdx.md) 함수에서 반환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
