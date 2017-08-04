---
title: Ordinal (MDX) | Microsoft Docs
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
- Ordinal
dev_langs:
- kbMDX
helpviewer_keywords:
- Ordinal function
ms.assetid: 9d416c39-da4a-4f0d-8d85-a76af5df0a87
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b848698799bc0c620d9592e90f508f01ac279f6f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ordinal-mdx"></a>Ordinal(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  수준과 관련된 서수 값(0부터 시작)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>인수  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **서 수** 함수와 함께에서 자주 사용 되는 **IIF** 및 **CurrentMember** 쿼리 결과 있는 각 특정 셀의 서 수 위치에 따라 조건부로 각 계층 수준 서로 다른 값을 표시 하는 함수입니다. 예를 들어, 사용할 수는 **서** 특정 수준에서 계산을 수행 하 고 다른 수준의 기본값은 "n/A"를 표시 하는 함수입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Calendar 계층에 있는 Calendar Quarter 수준의 서수를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

