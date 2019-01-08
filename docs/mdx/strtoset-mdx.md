---
title: StrToSet (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee1e0cbeaa4e33be223e1b777ff243b5c3ef2d01
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524410"
---
# <a name="strtoset-mdx"></a>StrToSet(MDX)


  MDX 형식 문자열에 의해 지정 된 집합을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>인수  
 *Set_Specification*  
 직접 또는 간접적으로 집합을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **StrToSet** 함수는 문자열 식에 지정 된 집합을 반환 합니다. 합니다 **StrToSet** 함수는 대개 다시 MDX 문으로 경우, 또는 MDX 쿼리에 매개 변수가 외부 함수의 집합 사양을 반환 사용자 정의 함수와 함께 사용 됩니다.  
  
-   CONSTRAINED 플래그를 사용 하는 경우 해당 집합 사양에 정규화 되거나 정규화 되지 않은 멤버 이름 또는 괄호로 묶은 정규화 되거나 정규화 되지 않은 멤버 이름이 들어 있는 튜플 집합을 포함 해야 합니다 {}합니다. 이 플래그를 사용하면 지정한 문자열을 통한 삽입 공격 위험을 줄일 수 있습니다. 정규화되거나 정규화되지 않은 멤버 이름으로 직접 확인할 수 없는 문자열을 지정하면 "STRTOSET 함수에서 CONSTRAINED 플래그로 설정한 제한을 위반했습니다"라는 오류가 나타납니다.  
  
-   CONSTRAINED 플래그를 사용하지 않을 경우 지정한 집합 사양은 집합을 반환하는 유효한 MDX 식으로 확인될 수 있습니다.  
  
-   집합과 멤버의 차이를 더 잘 이해하려면 집합 식 사용 및 멤버 식 사용을 참조하십시오.  
  
## <a name="examples"></a>예  
 다음 예제를 사용 하 여 State-province 특성 계층의 멤버 집합을 반환 합니다 **StrToSet** 함수입니다. 해당 집합 사양에서는 유효한 MDX 집합 식이 제공됩니다.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 CONSTRAINED 플래그로 인해 오류가 반환됩니다. 해당 집합 사양에서 올바른 MDX 집합 식을 제공하지만 CONSTRAINED 플래그가 있으므로 집합 사양에 정규화되거나 정규화되지 않은 멤버 이름이 필요합니다.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 Germany 및 Canada의 Reseller Sales Amount 측정값을 반환합니다. 지정된 문자열에 제공된 집합 사양에는 CONSTRAINED 플래그에서 필요로 하는 정규화된 멤버 이름이 들어 있습니다.  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
