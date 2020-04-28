---
title: Members (문자열) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05df2d0a846af30d46e702c1d5489945d57c9115
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68001498"
---
# <a name="members-string-mdx"></a>Members(문자열)(MDX)


  문자열 식으로 지정된 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Name*  
 멤버 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
 **Members (String)** 함수는 이름이 지정 된 단일 멤버를 반환 합니다. 일반적으로 members **(string)** 함수를 외부 함수와 함께 사용 하 여 멤버 **(문자열)** 함수에 멤버를 식별 하는 문자열을 제공 하 고 **members (string)** 함수는이 지정 된 멤버의 값을 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **Members (String)** 함수를 사용 하 여 지정 된 문자열을 유효한 멤버로 변환한 다음 문자열에 지정 된 멤버의 기본 측정값을 반환 합니다. 지정된 문자열은 작은따옴표 안에 있습니다. 기본 측정값은 Reseller Sales Amount 측정값입니다.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
