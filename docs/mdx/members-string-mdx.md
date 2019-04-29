---
title: Members (String) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 302445cadc829de35eca28db2888aaa01673ca75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048456"
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
  
## <a name="remarks"></a>Remarks  
 합니다 **Members (String)** 함수 이름이 지정 된 단일 멤버를 반환 합니다. 일반적으로 사용 합니다 **Members (String)** 를 제공 하는 외부 함수를 사용 하 여 함수를 **Members (String)** 함수 멤버를 식별 하는 문자열 및 **Members (String)**  함수는 지정 된이 멤버에 대 한 값을 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 **Members (String)** 지정된 된 문자열을 유효한 멤버로 변환할 함수 및 문자열에 지정 된 멤버에 대 한 기본 측정값을 반환 합니다. 지정된 문자열은 작은따옴표 안에 있습니다. 기본 측정값은 Reseller Sales Amount 측정값입니다.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
