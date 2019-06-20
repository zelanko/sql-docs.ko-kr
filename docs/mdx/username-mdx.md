---
title: UserName (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f8c08855d70d6a880607cc4310e6adcabbf7d9ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298027"
---
# <a name="username-mdx"></a>UserName(MDX)


  현재 연결의 도메인 이름과 사용자 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Remarks  
 반환되는 값은 다음 형식의 문자열입니다.  
  
 *domain-name\user-name*  
  
## <a name="example"></a>예제  
 다음 예에서는 쿼리를 실행하는 사용자의 이름을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
