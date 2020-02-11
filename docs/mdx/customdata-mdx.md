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
ms.openlocfilehash: d2884e23cbee78acacdb72e386f0e99610e9629f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135834"
---
# <a name="customdata-mdx"></a>CustomData(MDX)


  정의 된 경우 **CustomData** 연결 문자열 속성의 값을 반환 합니다. 그렇지 않으면 **null**입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Return Value  
 **CustomData** 함수는 **CustomData** 연결 문자열 속성을 검색 하 고 mdx (Multidimensional Expressions) 함수 및 문 (예: [UserName (mdx)](../mdx/username-mdx.md) 및 [CALL Statement (mdx))](../mdx/mdx-data-manipulation-call.md)에 사용할 구성 설정을 전달할 수 있습니다. 예를 들어 동적 보안 식에서이 함수를 사용 하 여 **CustomData** 연결 문자열 속성의 문자열 값에 대해 허용/거부 집합 멤버를 선택할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 쿼리는 계산 된 측정값에서 **CustomData** 함수에 의해 반환 된 값을 표시 합니다.  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
