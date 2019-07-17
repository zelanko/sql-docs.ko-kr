---
title: VisualTotals (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a5becd3382f07a9adc89055a253235495a7e50a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125835"
---
# <a name="visualtotals-mdx"></a>VisualTotals(MDX)


  지정된 집합에 있는 자식 멤버의 합계를 동적으로 구하여 생성된 집합을 반환합니다. 결과 집합에서 부모 멤버의 이름에 대한 패턴을 사용할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Pattern*  
 부모 이름의 대체 문자로 별표(*)가 들어 있는 집합의 부모 멤버에 대한 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 지정된 집합 식은 단일 차원 내에 있는 모든 수준의 멤버(일반적으로 상위-하위 관계가 있는 멤버)가 들어 있는 집합을 지정할 수 있습니다. 합니다 **VisualTotals** 함수는 지정된 된 집합의 자식 멤버의 값 합계를 계산 하 고 하며, 결과 합계를 계산할 때 해당 집합에 없는 자식 멤버를 무시 합니다. 합계는 계층 순서로 정렬된 집합에 대해 보이는 값 합계로 계산됩니다. 집합의 멤버 순서가 계층과 맞지 않는 경우 결과는 보이는 값 합계가 아닙니다. 예를 들어 VisualTotals (USA, WA, CA, Seattle)는 WA를 Seattle로 반환하는 것이 아니라 WA, CA 및 Seattle에 대한 값을 반환한 다음 이러한 값의 합계를 USA의 보이는 값 합계로 계산하므로 Seattle의 판매량은 두 번 계산됩니다.  
  
> [!NOTE]  
>  적용 된 **VisualTotals** 무관 측정값 또는 측정값 그룹 세분성 수준 아래에 있는 차원 멤버를 함수로 인해 값을 null로 바뀝니다.  
  
 *패턴*, 합계 레이블의 형식을 지정 하는 작업은 선택 사항입니다. *패턴* 별표 (*)를 사용 하는 부모 이름과 연결 된 결과에 표시 되는 부모 멤버와 문자열의 텍스트의 나머지 부분에 대 한 대체 문자임을 나타내야 합니다. 리터럴 별표를 표시 하려면 별표를 두 개를 사용 하 여 (\*\*).  
  
## <a name="examples"></a>예  
 다음 예에서는 지정된 단일 하위 항목, 즉 7월을 기준으로 2001년 3분기의 보이는 값 합계를 반환합니다.  
  
```  
SELECT VisualTotals  
   ({[Date].[Calendar].[Calendar Quarter].&[2001]&[3]  
      ,[Date].[Calendar].[Month].&[2001]&[7]}) ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 Product 차원에 있는 Category 특성 계층의 [All] 멤버와 해당 자식 항목 네 개 중 두 개를 함께 반환합니다. Internet Sales Amount 측정값의 [All] 멤버에 대해 반환된 합계는 Accessories 및 Clothing 멤버만에 대한 합계입니다. 또한 [All Products] 열의 레이블을 지정하기 위해 패턴 인수가 사용됩니다.  
  
```  
SELECT  
   VisualTotals  
   ({[Product].[Category].[All Products]  
      ,[Product].[Category].[Accessories]  
      ,[Product].[Category].[Clothing]}  
      , '* - Visual Total'  
   ) ON Columns  
, [Measures].[Internet Sales Amount] ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
