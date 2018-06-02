---
title: 또는 (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 215ed38ef7887d9815c6cf4ac79321b95a367707
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580625"
---
# <a name="or-mdx"></a>OR(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 반환 하는 부울 값 **true** 인수 중 하나 또는 둘 다로 계산 되 면 **true**, 그렇지 않으면 **false**합니다.  
  
## <a name="remarks"></a>Remarks  
 **또는** 연산자는 부울 값으로 두 개의 인수를 처리 (0, 0,으로 **false**, 그렇지 않으면 **true**) 연산자는 논리 분리를 수행 하기 전에. 다음 표에서 설명 방법을 **또는** 연산자로 논리 분리를 수행 합니다.  
  
|*Expression1*|*Expression2*|반환 값|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>예제  
 다음 쿼리에는 Customer 차원의 Gender 계층에 있는 현재 멤버가 Male이거나 Customer 차원의 Marital Status 계층에 있는 현재 멤버가 Married인 경우 “MARRIED OR MALE” 문자열을 반환하고, 그렇지 않으면 “UNMARRIED OR FEMALE” 문자열을 반환하는 계산 측정값이 포함되어 있습니다.  
  
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
  
  
