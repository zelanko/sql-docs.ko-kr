---
title: Dimensions (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2703122b67debf0749abcd2ea01114fb6ecaa06
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248141"
---
# <a name="dimensions-mdx"></a>Dimensions(MDX)


  숫자 식 또는 문자열 식으로 지정된 계층을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Number*  
 계층 번호를 지정하는 유효한 숫자 식입니다.  
  
 *Hierarchy_Name*  
 계층 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>Remarks  
 계층 번호가 지정 된 경우는 **차원** 함수 계층 큐브 내에서 0부터 시작 위치가 지정 된 계층 번호를 반환 합니다.  
  
 계층 이름이 지정 되는 **차원** 함수는 지정 된 계층을 반환 합니다. 일반적으로이 문자열 버전을 사용 합니다 **차원** 사용자 정의 함수를 사용 하 여 함수입니다.  
  
> [!NOTE]  
>  합니다 **측정값이** 차원은 항상으로 표시 됩니다 `Dimensions(0)`합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 합니다 **차원** 이름, 수준 수 및 숫자 식과 문자열 식을 모두 사용 하 여 지정 된 계층의 멤버 수를 반환 하는 함수입니다.  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
