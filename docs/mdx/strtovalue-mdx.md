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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036693"
---
# <a name="strtovalue-mdx"></a>StrToValue(MDX)


  MDX 형식 문자열에 의해 지정 된 숫자 값을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>인수  
 *MDX_Expression*  
 직접 또는 간접적으로 단일 셀로 확인되는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **StrToValue** 함수는 MDX 식에서 지정한 숫자 값을 반환 합니다. 합니다 **StrToValue** 함수는 대개 외부 함수의 MDX 식을 단일 셀으로 확인 될 수 있는 MDX 문에으로 다시 돌아가려면 사용자 정의 함수와 함께 사용 됩니다.  
  
-   CONSTRAINED 플래그를 사용할 경우 MDX 식에는 스칼라 값만 들어 있어야 합니다. CONSTRAINED 플래그를 사용하면 지정한 문자열을 통한 삽입 공격 위험을 줄일 수 있습니다. MDX 식을 제공 스칼라 값으로 직접 확인할 수 없는 경우 다음 오류가 표시 됩니다. "CONSTRAINED 설정한 제한을 위반 했습니다 STRTOVALUE 함수에서 플래그."  
  
-   CONSTRAINED 플래그를 사용하지 않을 경우에는 원하는 만큼 복잡한 MDX 식을 지정할 수 있습니다. 단, 해당 식은 단일 셀을 반환하는 유효한 MDX 식으로 확인되어야 합니다.  
  
> [!NOTE]  
>  MDX 식의 결과를 숫자 값으로 반환하면 값이 텍스트로 저장되어 있는데 반환되는 값에 대해 산술 연산을 수행하려는 경우에 유용합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 **StrToValue** 값으로 각 자전거의 무게를 반환 하는 함수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
