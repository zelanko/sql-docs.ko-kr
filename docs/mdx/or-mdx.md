---
title: OR (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae6b6602d7968bb444dcf4838537bb000b97dd53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278256"
---
# <a name="or-mdx"></a>OR(MDX)


  두 숫자 식에 논리 분리를 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>매개 변수  
 Expression1  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
 Expression2  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 하는 부울 값 **true** 인수 중 하나 또는 둘 다로 평가 되 면 **true**이 고, 그렇지 않으면 **false**합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **또는** 연산자는 두 인수가 모두 부울 값으로 처리 (0으로 **false**이 고, 그렇지 않으면 **true**) 연산자는 논리 분리를 수행 하기 전에 합니다. 다음 표에서 설명 하는 방법을 **또는** 연산자로 논리 분리를 수행 합니다.  
  
|*Expression1*|*Expression2*|반환 값|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>예제  
 다음 쿼리는 "MARRIED OR MALE" 이면 Customer 차원의 Gender 계층에 있는 현재 멤버가 Male Customer 차원의 Marital Status 계층에 있는 현재 멤버가 Married 인; 문자열을 반환 하는 계산된 측정값을 포함 그렇지 않으면 "UNMARRIED 또는 FEMALE" 문자열을 반환 합니다.  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
