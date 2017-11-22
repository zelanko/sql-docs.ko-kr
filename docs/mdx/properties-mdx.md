---
title: "속성 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Properties
dev_langs: kbMDX
helpviewer_keywords: Properties function
ms.assetid: 2d8442c5-30c4-4fd1-99ea-9845b6533e41
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c4275d4bcfdb057a1b5d6b42c263ae0720cd9725
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="properties-mdx"></a>Properties(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>주의  
 **속성** 함수는 지정 된 멤버 속성에 대 한 지정된 된 멤버의 값을 반환 합니다. 멤버 속성와 같은 기본 멤버 속성 중 하나일 수 있습니다 **이름**, **ID**, **키**, 또는 **캡션**, 사용자 정의 멤버 속성이 될 수도 있습니다. 자세한 내용은 참조 [내장 멤버 속성 &#40; Mdx&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) 및 [사용자 정의 멤버 속성 &#40; Mdx&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 기본적으로 값은 문자열로 변환됩니다. 경우 **형식화** 반환 값은 강력한 형식이 지정 된 합니다.  
  
-   속성 유형이 기본인 경우 함수는 원래 유형의 멤버를 반환합니다.  
  
-   속성 유형이 사용자 정의 인 경우 반환 값의 형식이의 반환 값의 형식과 동일는 **MemberValue** 함수입니다.  
  
> [!NOTE]  
>  Properties ('Key')는 복합 키를 제외하고 Key0과 동일한 결과를 반환합니다. Properties ('Key')는 복합 키에 대해 Null을 반환합니다. 키를 사용 하 여*x* 예에서 설명한 것 처럼 복합 키에 대 한 구문입니다. Properties ('Key0'), Properties ('Key1'), Properties ('Key2') 등이 전체적으로 복합 키를 구성합니다.  
  
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
  
 다음 예제에서는 키의 사용을 보여 줍니다.*x* 속성입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [멤버 속성 &#40;를 사용 하 여 Mdx&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
