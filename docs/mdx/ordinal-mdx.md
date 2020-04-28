---
title: 서 수 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b22cc6d5a609f8e1f585ccc1229e0e1cd67e1796
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055642"
---
# <a name="ordinal-mdx"></a>Ordinal(MDX)


  수준과 관련된 서수 값(0부터 시작)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>인수  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Ordinal** 함수는 쿼리 결과에서 각 특정 셀의 서 수 위치에 따라 여러 계층 수준에서 서로 다른 값을 조건부로 표시 하기 위해 **IIF** 및 **currentmember** 함수와 함께 사용 되는 경우가 많습니다. 예를 들어 **서 수** 함수를 사용 하 여 특정 수준에서 계산을 수행 하 고 다른 수준에서 "N/a"의 기본값을 표시할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Calendar 계층에 있는 Calendar Quarter 수준의 서수를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
