---
title: "= (같음) (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- =
dev_langs:
- kbMDX
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 5e1f3b58-a646-4fc1-a3f1-19090a5437b7
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9e446cf812f57a3cc3df74728b74c072d1b089bc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="-equal-to-mdx"></a>=(같음)(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나의 MDX 식의 값이 다른 MDX 식의 값과 같은지 확인하는 비교 연산을 수행합니다.  
  
> [!NOTE]  
>  사용 하 여 개체를 비교 하려면는 [IS &#40; Mdx&#41; ](../mdx/is-mdx.md) 연산자입니다. 예를 들어 쿼리 축에 있는 현재 멤버가 특정 멤버인지 확인할 때 IS 연산자를 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>매개 변수  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 조건을 기반으로 하는 부울 값입니다.  
  
-   **true 이면** 첫 번째 매개 변수의 값이 두 번째 매개 변수 값과 동일 합니다.  
  
-   **false** 경우 첫 번째 매개 변수 값의 두 번째 매개 변수 값과 같지 않습니다.  
  
-   **true 이면** 경우 매개 변수가 모두 null이 또는 하나의 매개 변수가 null이 고 다른 매개 변수는 0입니다.  
  
## <a name="examples"></a>예  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

