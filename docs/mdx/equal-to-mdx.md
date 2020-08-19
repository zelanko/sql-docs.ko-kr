---
description: =(같음)(MDX)
title: = (같음) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5ec3cbcb928926d02dd6597116f8ce9af00bf8e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494936"
---
# <a name="-equal-to-mdx"></a>=(같음)(MDX)


  하나의 MDX 식의 값이 다른 MDX 식의 값과 같은지 확인하는 비교 연산을 수행합니다.  
  
> [!NOTE]  
>  개체를 비교 하려면 [IS &#40;MDX&#41;](../mdx/is-mdx.md) 연산자를 사용 합니다. 예를 들어 쿼리 축에 있는 현재 멤버가 특정 멤버인지 확인할 때 IS 연산자를 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>매개 변수  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 조건을 기반으로 하는 부울 값입니다.  
  
-   첫 번째 매개 변수의 값이 두 번째 매개 변수의 값과 같으면 **true** 입니다.  
  
-   첫 번째 매개 변수의 값이 두 번째 매개 변수의 값과 같지 않으면 **false** 입니다.  
  
-   두 매개 변수가 모두 null 이거나 한 매개 변수가 null이 고 다른 매개 변수가 0 이면 **true** 입니다.  
  
## <a name="examples"></a>예제  
 다음 쿼리에서는 이러한 조건의 예를 보여 줍니다.  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
