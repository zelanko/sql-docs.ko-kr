---
description: Properties(MDX)
title: 속성 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbdae47b3ede8ad2b22258e83a69b4f2776115d9
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192343"
---
# <a name="properties-mdx"></a>Properties(MDX)


  멤버 속성 값을 포함하는 문자열 또는 강력한 형식의 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Property_Name*  
 멤버 속성 이름의 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 **Properties** 함수는 지정 된 멤버 속성에 대해 지정 된 멤버의 값을 반환 합니다. 멤버 속성은 **NAME**, **ID**, **KEY**또는 **CAPTION**과 같은 기본 멤버 속성 이거나 사용자 정의 멤버 속성 일 수 있습니다. 자세한 내용은 mdx&#41;&#40;[내장 멤버 속성 &#40;mdx&#41;](/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 및 [사용자 정의 멤버 속성 ](/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)을 참조 하세요.  
  
 기본적으로 값은 문자열로 변환됩니다. **형식화** 된 경우 반환 값은 강력한 형식입니다.  
  
-   속성 유형이 기본인 경우 함수는 원래 유형의 멤버를 반환합니다.  
  
-   속성 유형이 사용자 정의 인 경우 반환 값의 유형은 **Membervalue** 함수의 반환 값 유형과 동일 합니다.  
  
> [!NOTE]  
>  Properties ('Key')는 복합 키를 제외하고 Key0과 동일한 결과를 반환합니다. Properties ('Key')는 복합 키에 대해 Null을 반환합니다. 예제에 나와 있는 것 처럼 복합 키에 대해 키*x* 구문을 사용 합니다. Properties ('Key0'), Properties ('Key1'), Properties ('Key2') 등이 전체적으로 복합 키를 구성합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 기본 멤버 속성과 사용자 정의 멤버 속성을 모두 반환합니다. 이때 TYPED 인수를 사용하여 Day Name 멤버 속성에 대한 강력한 형식의 값을 반환합니다.  
  
```  
WITH MEMBER Measures.MemberName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Name')  
MEMBER Measures.MemberVal AS   
   [Date].[Calendar].[July 1, 2003].Properties('Member_Value')  
MEMBER Measures.MemberKey AS   
   [Date].[Calendar].[July 1, 2003].Properties('Key')  
MEMBER Measures.MemberID AS   
   [Date].[Calendar].[July 1, 2003].Properties('ID')  
MEMBER Measures.MemberCaption AS   
   [Date].[Calendar].[July 1, 2003].Properties('Caption')  
MEMBER Measures.DayName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name', TYPED)  
MEMBER Measures.DayNameTyped AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name')  
MEMBER Measures.DayofWeek AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Week')  
MEMBER Measures.DayofMonth AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Month')  
MEMBER Measures.DayofYear AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Year')  
  
SELECT {Measures.MemberName  
   , Measures.MemberVal  
   , Measures.MemberKey  
   , Measures.MemberID  
   , Measures.MemberCaption  
   , Measures.DayName  
   , Measures.DayNameTyped  
   , Measures.DayofWeek  
   , Measures.DayofMonth  
   , Measures.DayofYear  
   }  ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 키*x* 속성을 사용 하는 방법을 보여 줍니다.  
  
```  
WITH   
MEMBER Measures.MemberKey AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key')  
MEMBER Measures.MemberKey0 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key0')  
MEMBER Measures.MemberKey1 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key1')  
  
SELECT {Measures.MemberKey  
   , Measures.MemberKey0  
   , Measures.MemberKey1     
   }  ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX&#41;&#40;멤버 속성 사용 ](/analysis-services/multidimensional-models/mdx/mdx-member-properties)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
