---
title: StrToValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cad8fec605a56a60cfcc7024739225e474fd42f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036693"
---
# <a name="strtovalue-mdx"></a>StrToValue(MDX)


  MDX (Multidimensional Expressions) 형식 문자열에 의해 지정 된 숫자 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>인수  
 *MDX_Expression*  
 직접 또는 간접적으로 단일 셀로 확인되는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 **Strtovalue** 함수는 MDX 식에 의해 지정 된 숫자 값을 반환 합니다. **Strtovalue** 함수는 일반적으로 사용자 정의 함수와 함께 사용 되어 외부 함수의 mdx 식을 단일 셀로 확인 될 수 있는 mdx 문에 다시 반환 합니다.  
  
-   CONSTRAINED 플래그를 사용할 경우 MDX 식에는 스칼라 값만 들어 있어야 합니다. CONSTRAINED 플래그를 사용하면 지정한 문자열을 통한 삽입 공격 위험을 줄일 수 있습니다. 스칼라 값에 직접 확인할 수 없는 MDX 식이 제공 되는 경우 "STRTOVALUE 함수에서 제약 조건이 적용 된 제한을 위반 했습니다." 라는 오류가 나타납니다.  
  
-   CONSTRAINED 플래그를 사용하지 않을 경우에는 원하는 만큼 복잡한 MDX 식을 지정할 수 있습니다. 단, 해당 식은 단일 셀을 반환하는 유효한 MDX 식으로 확인되어야 합니다.  
  
> [!NOTE]  
>  MDX 식의 결과를 숫자 값으로 반환하면 값이 텍스트로 저장되어 있는데 반환되는 값에 대해 산술 연산을 수행하려는 경우에 유용합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **Strtovalue** 함수를 사용 하 여 각 자전거의 무게를 값으로 반환 합니다.  
  
```  
WITH MEMBER Measures.x AS   
StrToValue   
   ([Product].[Product].CurrentMember.Properties ('Weight')  
   ,CONSTRAINED  
   )  
SELECT Measures.x ON 0  
,[Product].[Product].[Product].Members ON 1  
FROM [Adventure Works]  
WHERE [Product].[Product Categories].[Bikes]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
