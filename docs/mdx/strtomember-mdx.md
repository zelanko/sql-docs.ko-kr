---
title: StrToMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37c76d6e1e7ffe9bc40d785952b5c456ab1fc6fa
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743052"
---
# <a name="strtomember-mdx"></a>StrToMember(MDX)


  MDX(Multidimensional Expression) 형식 문자열에 의해 지정된 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>인수  
 *Member_Name*  
 직접 또는 간접적으로 멤버를 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>Remarks  
 **StrToMember** 함수는 문자열 식에 지정 된 멤버를 반환 합니다. **StrToMember** 함수는 대개 다시 MDX 문으로 경우, 또는 MDX 쿼리에 매개 변수가 외부 함수의 멤버 사양을 반환 사용자 정의 함수와 함께 사용 됩니다.  
  
-   CONSTRAINED 플래그를 사용할 경우 멤버 이름은 정규화되거나 정규화되지 않은 멤버 이름으로 직접 확인될 수 있어야 합니다. 이 플래그를 사용하면 지정한 문자열을 통한 삽입 공격 위험을 줄일 수 있습니다. 다음과 같은 오류가 표시 되는 문자열이 제공 정규화 되거나 정규화 되지 않은 멤버 이름으로 직접 확인할 수 없는 경우: "설정한 제한을 CONSTRAINED 플래그 STRTOMEMBER 함수에서 위반 했습니다."  
  
-   CONSTRAINED 플래그를 사용하지 않을 경우 지정된 멤버는 멤버 이름으로 직접 확인되거나 이름으로 확인되는 MDX 식으로 확인될 수 있습니다.  
  
-   집합과 멤버의 차이를 더 잘 이해하려면 집합 식 사용 및 멤버 식 사용을 참조하십시오.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용 하 여 State-province 특성 계층의 Bayern 멤버에 대 한 Reseller Sales Amount 측정값을 반환 된 **StrToMember** 함수입니다. 지정된 문자열은 정규화된 멤버 이름을 제공합니다.  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 사용 하 여 Bayern 멤버에 대 한 Reseller Sales Amount 측정값을 반환 하는 다음 예제는 **StrToMember** 함수입니다. 멤버 이름 문자열은 정규화되지 않은 멤버 이름만 제공하므로 해당 쿼리는 Reseller Sales와 교차하지 않는 Customer 차원의 Customer Geography 계층에서 발생하는 지정된 멤버의 첫 번째 인스턴스를 반환합니다. 결과가 예상대로 나타나도록 하려면 정규화된 이름을 지정하는 것이 좋습니다.  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 사용 하 여 State-province 특성 계층의 Bayern 멤버에 대 한 Reseller Sales Amount 측정값을 반환 된 **StrToMember** 함수입니다. 지정된 멤버 이름 문자열은 정규화된 멤버 이름으로 확인됩니다.  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 CONSTRAINED 플래그로 인해 오류가 반환됩니다. 지정된 멤버 이름 문자열에는 정규화된 멤버 이름으로 확인되는 유효한 MDX 멤버 식이 들어 있지만 CONSTRAINED 플래그가 있으므로 멤버 이름 문자열에 정규화되거나 정규화되지 않은 멤버 이름이 필요합니다.  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
