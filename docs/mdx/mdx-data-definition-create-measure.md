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
manager: kfile
ms.openlocfilehash: aa895099420b022cf15d7cd3a91472511c1100e3
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741440"
---
# <a name="mdx-data-definition---create-measure"></a>MDX 데이터 정의-측정값 만들기


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
  
## <a name="remarks"></a>Remarks  
 *Measure_Name* 대괄호로 묶어야 합니다.  
  
 CREATE MEASURE 문은 MDX 스크립트 정의;만 사용할 수 있습니다. 참조 [MdxScript 요소 &#40;ASSL&#41;](../analysis-services/scripting/objects/mdxscript-element-assl.md)합니다.  
  
 또한 단일 쿼리에서 사용할 계산 멤버를 정의할 수 있습니다. 단일 쿼리로 제한된 계산 멤버를 정의하려면 SELECT 문에서 WITH 절을 사용합니다. 자세한 내용은 참조 [MDX로 측정값 만들기](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
