---
title: CREATE MEASURE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 02c6d29bbebcc794e72f4ca960e3d9259de7205b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892140"
---
# <a name="mdx-data-definition---create-measure"></a>MDX 데이터 정의 - CREATE MEASURE


  테이블 형식 모델에 측정값을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>인수  
 *Table_Name*  
 측정값을 만들 테이블의 이름을 지정하는 유효한 문자열 리터럴입니다.  
  
 *Measure_Name*  
 측정값 이름을 지정하는 유효한 문자열 리터럴입니다.  
  
 *DAX_Expression*  
 단일 스칼라 값을 반환하는 유효한 DAX 식입니다.  
  
## <a name="remarks"></a>설명  
 *Measure_Name* 는 괄호로 묶어야 합니다.  
  
 CREATE MEASURE 문은 MDX 스크립트 정의 내 에서만 사용할 수 있습니다. [&#41;&#40;MdxScript 요소 ](https://docs.microsoft.com/bi-reference/assl/objects/mdxscript-element-assl)를 참조 하세요.  
  
 또한 단일 쿼리에서 사용할 계산 멤버를 정의할 수 있습니다. 단일 쿼리로 제한된 계산 멤버를 정의하려면 SELECT 문에서 WITH 절을 사용합니다. 자세한 내용은 [MDX로 측정값 작성](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-building-measures)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 데이터 정의 문은 MDX를 &#40;&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
