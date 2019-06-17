---
title: Axis (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2802422f7d50c0a504a0c42eec940d81e89e66b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181645"
---
# <a name="axis-mdx"></a>Axis(MDX)


  튜플 집합을 지정된 축에 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>인수  
 *Axis_Number*  
 축 번호를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **축** 함수 축 0부터 시작 위치를 사용 하 여 축의 튜플 집합을 반환 합니다. 예를 들어 `Axis(0)`은 COLUMNS 축을 반환하고, `Axis(1)`은 ROWS 축을 반환하는 식으로 진행됩니다. 합니다 **축** 필터 축에 함수를 사용할 수 없습니다. 이 함수를 사용하면 계산 멤버에서 실행될 쿼리의 컨텍스트를 인식하도록 지정할 수 있습니다. 예를 들어 Rows 축에서 선택한 계산 멤버의 합계만 제공하는 계산 멤버가 필요할 수 있습니다. 또한 이 함수를 사용하여 한 축의 정의가 다른 축의 정의에 종속되도록 지정할 수 있습니다. 예를 들어 Columns 축의 첫 번째 항목 값에 따라 Rows 축의 내용을 정렬할 수 있습니다.  
  
> [!NOTE]  
>  축은 이전 축만 참조할 수 있습니다. 예를 들어 `Axis(0)`은 ROW 또는 PAGE 축과 같이 COLUMNS 축이 계산된 다음에만 발생해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예제 쿼리에서는 Axis 함수를 사용하는 방법을 보여 줍니다.  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SETTOSTR(AXIS(1))`  
  
 `SELECT MEASURES.AXISDEMO ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 계산 멤버 내에 Axis 함수를 사용하는 방법을 보여 줍니다.  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SUM(AXIS(1), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.AXISDEMO} ON 0,`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
