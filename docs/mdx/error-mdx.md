---
title: "오류 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR
dev_langs:
- kbMDX
helpviewer_keywords:
- Error function
ms.assetid: 2caac19b-b297-443e-9299-648ef88a5039
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b439b8b6d6c36cf500ad5f089a24034e7d2404fb
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

