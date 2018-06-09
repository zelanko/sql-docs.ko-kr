---
title: CustomData (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 172915d99b231490cbdca24f70d1d38da27a1d3d
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739308"
---
# <a name="customdata-mdx"></a>CustomData(MDX)


  값을 반환 된 **CustomData** 연결 문자열 속성이 정의 되지 않으면 **null**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>반환 값  
 **CustomData** 함수를 검색할 수는 **CustomData** 연결 문자열 속성 및 구성 설정을 같은 MDX (Multidimensional Expressions) 함수 및 문에서 사용할 전달할 [UserName (MDX)](../mdx/username-mdx.md) 및 [CALL 문 (MDX)](../mdx/mdx-data-manipulation-call.md)합니다. 예를 들어이 함수 사용할 수는 동적 보안 식에서 문자열 값에 대 한 허용/거부 집합 멤버를 선택 하 고 **CustomData** 연결 문자열 속성입니다.  
  
## <a name="example"></a>예제  
 반환 된 값을 표시 하는 다음 쿼리는 **CustomData** 계산된 측정값에서 함수:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
