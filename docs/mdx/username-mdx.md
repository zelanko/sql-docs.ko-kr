---
title: UserName (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 887af13c84fd06ead5a36564c0dda740a5f6d0b0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581355"
---
# <a name="username-mdx"></a>UserName(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  현재 연결의 도메인 이름과 사용자 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Remarks  
 반환되는 값은 다음 형식의 문자열입니다.  
  
 *도메인 이름 \ 사용자 이름*  
  
## <a name="example"></a>예제  
 다음 예에서는 쿼리를 실행하는 사용자의 이름을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
