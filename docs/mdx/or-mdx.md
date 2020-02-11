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
ms.openlocfilehash: 45063e9f2aca6a924289d4d52434535d16c9a08e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055713"
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
  
## <a name="return-value"></a>Return Value  
 둘 중 하나 또는 둘 다가 **true**로 평가 되는 경우 **true** 를 반환 하는 부울 값입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 **OR** 연산자는 연산자가 논리 분리를 수행 하기 전에 두 인수를 모두 부울 값 (0, 0, 0, **0, 0)으로**처리 **합니다.** 다음 표에서는 **OR** 연산자가 논리 분리를 수행 하는 방법을 보여 줍니다.  
  
|*Expression1*|*Expression2*|Return Value|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**허위**|**true**|  
|**허위**|**true**|**true**|  
|**허위**|**허위**|**허위**|  
  
## <a name="example"></a>예제  
 다음 쿼리는 Customer 차원의 성별 계층에 있는 현재 멤버가 남성 이거나 Customer 차원의 결혼 상태 계층에 있는 현재 멤버가 결혼 된 경우 "결혼 또는 남성" 문자열을 반환 하는 계산 측정값을 포함 합니다. 그렇지 않으면 "UNMARRIED 또는 여성" 문자열을 반환 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
