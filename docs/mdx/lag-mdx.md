---
title: Lag (MDX) | Microsoft Docs
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
- LAG
dev_langs:
- kbMDX
helpviewer_keywords:
- Lag function
ms.assetid: 08c704ea-35d8-44ee-abe5-93bd24b99906
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eedeae82c5b7566f0c59a6876fc6743c61794de0
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="lag-mdx"></a>Lag(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  멤버 수준에서 지정한 위치 번호만큼 지정한 멤버의 앞에 있는 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *인덱스*  
 지정한 멤버와의 간격을 나타내는 멤버 위치 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 수준 내의 멤버 위치는 특성 계층의 일반적인 순서에 따라 결정됩니다. 위치를 나타내는 번호는 0부터 시작합니다.  
  
 지정한 간격이 0 바이트인 경우는 **지연** 함수는 지정 된 멤버를 반환 합니다.  
  
 지정한 간격이 음수 이면이 **지연** 함수는 이후 멤버를 반환 합니다.  
  
 `Lag(1)`해당 하는 [PrevMember](../mdx/prevmember-mdx.md) 함수입니다. `Lag(-1)`해당 하는 [NextMember](../mdx/nextmember-mdx.md) 함수입니다.  
  
 **지연** 함수는 비슷합니다는 [발생할](../mdx/lead-mdx.md) 함수와 **발생할** 반대 방향으로 함수를 찾습니다는 **지연** 함수입니다. 즉, `Lag(n)`은 `Lead(-n)`과 동일합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 2001년 12월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 2002년 3월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

