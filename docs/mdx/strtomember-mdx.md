---
description: StrToMember(MDX)
title: StrToMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68d2d99bb51412a98919d1ab1626c7a86bd86245
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386809"
---
# <a name="strtomember-mdx"></a>StrToMember(MDX)


  MDX 형식 문자열에 의해 지정 된 멤버를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>인수  
 *Member_Name*  
 직접 또는 간접적으로 멤버를 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 **Strtomember** 함수는 문자열 식에 지정 된 멤버를 반환 합니다. **Strtomember** 함수는 일반적으로 외부 함수에서 다시 mdx 문으로 멤버 사양을 반환 하거나 mdx 쿼리가 매개 변수화 될 때 사용자 정의 함수와 함께 사용 됩니다.  
  
-   CONSTRAINED 플래그를 사용할 경우 멤버 이름은 정규화되거나 정규화되지 않은 멤버 이름으로 직접 확인될 수 있어야 합니다. 이 플래그를 사용하면 지정한 문자열을 통한 삽입 공격 위험을 줄일 수 있습니다. 정규화 되거나 정규화 되지 않은 멤버 이름으로 직접 확인할 수 없는 문자열을 제공 하는 경우 "STRTOMEMBER 함수에서 제한 된 플래그에 의해 적용 된 제한을 위반 했습니다." 라는 오류가 나타납니다.  
  
-   CONSTRAINED 플래그를 사용하지 않을 경우 지정된 멤버는 멤버 이름으로 직접 확인되거나 이름으로 확인되는 MDX 식으로 확인될 수 있습니다.  
  
-   집합과 멤버의 차이를 더 잘 이해하려면 집합 식 사용 및 멤버 식 사용을 참조하십시오.  
  
## <a name="examples"></a>예제  
 다음 예에서는 **Strtomember** 함수를 사용 하 여 시/도 특성 계층의 Bayern 멤버에 대 한 대리점 Sales Amount 측정값을 반환 합니다. 지정된 문자열은 정규화된 멤버 이름을 제공합니다.  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 **Strtomember** 함수를 사용 하 여 Bayern 멤버에 대 한 대리점 Sales Amount 측정값을 반환 합니다. 멤버 이름 문자열은 정규화되지 않은 멤버 이름만 제공하므로 해당 쿼리는 Reseller Sales와 교차하지 않는 Customer 차원의 Customer Geography 계층에서 발생하는 지정된 멤버의 첫 번째 인스턴스를 반환합니다. 결과가 예상대로 나타나도록 하려면 정규화된 이름을 지정하는 것이 좋습니다.  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 **Strtomember** 함수를 사용 하 여 시/도 특성 계층의 Bayern 멤버에 대 한 대리점 Sales Amount 측정값을 반환 합니다. 지정된 멤버 이름 문자열은 정규화된 멤버 이름으로 확인됩니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
