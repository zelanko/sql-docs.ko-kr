---
title: 오류 (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 774bcd1a0093350b3eb3cbf8cac4f4eeae188ed1
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579655"
---
# <a name="error-mdx"></a>Error(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  오류를 발생시킵니다. 지정된 오류 메시지를 제공할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>인수  
 *Error_Text*  
 반환할 오류 메시지가 들어 있는 유효한 문자열 식입니다.  
  
## <a name="examples"></a>예  
 다음 쿼리를 사용 하는 방법을 보여 줍니다는 **오류** 함수는 계산된 측정값 내:  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
