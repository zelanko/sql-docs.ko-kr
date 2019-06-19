---
title: AddCalculatedMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 18ccf4ad808c15945d82f1ca05616f0da878a7ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201619"
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers(MDX)


  계산 멤버를 지정한 집합에 추가하여 생성된 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 기본적으로 MDX는 집합 함수를 확인할 때 계산 멤버를 제외시킵니다. 합니다 **AddCalculatedMembers** 함수에 지정 된 집합 식을 검사 *Set_Expression,* 하 고 해당 집합의 범위 내에 포함 된 멤버의 형제인 계산된 멤버를 포함 합니다. 식입니다.  
  
> [!NOTE]  
>  이 함수는 1차원 집합 식에서만 사용될 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 함수의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 다음 예제에서는 반환 합니다 `Measures.[Unit Price]` 에 있는 모든 계산된 멤버 외에도 멤버를 **측정값** 차원에서를 **Adventure Works** 큐브.  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
