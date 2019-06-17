---
title: 속성 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c29d9b29078d6097b512acb93ff47eef018592c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278447"
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
  
## <a name="remarks"></a>Remarks  
 합니다 **속성** 함수에는 지정한 멤버 속성에 대 한 지정된 된 멤버의 값을 반환 합니다. 멤버 속성 같은 내장 멤버 속성 중 하나가 될 수 있습니다 **이름을**를 **ID**를 **키**, 또는 **캡션**, 될 수도 있습니다는 사용자 정의 멤버 속성입니다. 자세한 내용은 [내장 멤버 속성 &#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) 하 고 [사용자 정의 멤버 속성 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 기본적으로 값은 문자열로 변환됩니다. 하는 경우 **형식화 된** 반환 값은 강력한 형식이 지정 됩니다.  
  
-   속성 유형이 기본인 경우 함수는 원래 유형의 멤버를 반환합니다.  
  
-   속성 형식이 사용자 정의 인 경우 반환 값의 형식이 반환 값의 형식과 동일 합니다 **MemberValue** 함수입니다.  
  
> [!NOTE]  
>  Properties ('Key')는 복합 키를 제외하고 Key0과 동일한 결과를 반환합니다. Properties ('Key')는 복합 키에 대해 Null을 반환합니다. 키를 사용 하 여*x* 예제에 나온 것 처럼 복합 키에 대 한 구문입니다. Properties ('Key0'), Properties ('Key1'), Properties ('Key2') 등이 전체적으로 복합 키를 구성합니다.  
  
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
  
 다음 예제에서는 키의 사용을 보여 줍니다*x* 속성입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [멤버 속성 사용&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
