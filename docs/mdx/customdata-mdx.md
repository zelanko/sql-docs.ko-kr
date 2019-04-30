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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248318"
---
# <a name="customdata-mdx"></a>CustomData(MDX)


  값을 반환 합니다 **CustomData** 연결 문자열 속성이 정의 되지 않으면 **null**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>반환 값  
 합니다 **CustomData** 함수를 검색할 수 있습니다 합니다 **CustomData** 연결 문자열 속성 및 구성와 같은 MDX (Multidimensional Expressions) 함수 및 문에서 사용할 설정을 전달 합니다. [UserName (MDX)](../mdx/username-mdx.md) 하 고 [CALL 문 (MDX)](../mdx/mdx-data-manipulation-call.md)합니다. 예를 들어이 함수 수 동적 보안 식에서 문자열 값에 대 한 허용/거부 집합 멤버를 선택 하 여 **CustomData** 연결 문자열 속성입니다.  
  
## <a name="example"></a>예제  
 다음 쿼리에서 반환한 값을 표시 합니다 **CustomData** 계산된 측정값에서 함수:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
