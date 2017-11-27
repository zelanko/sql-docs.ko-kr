---
title: "CREATE MEASURE 문 (MDX) | Microsoft Docs"
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
ms.assetid: f264ba96-cbbe-488b-8ac9-b3056a6e997b
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 97edb823814647bc87b155250cad88dfeb5cf5f5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-measure"></a>MDX 데이터 정의-측정값 만들기
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>주의  
 *Measure_Name* 대괄호로 묶어야 합니다.  
  
 CREATE MEASURE 문은 MDX 스크립트 정의;만 사용할 수 있습니다. 참조 [MdxScript 요소 &#40; ASSL &#41; ](../analysis-services/scripting/objects/mdxscript-element-assl.md).  
  
 또한 단일 쿼리에서 사용할 계산 멤버를 정의할 수 있습니다. 단일 쿼리로 제한된 계산 멤버를 정의하려면 SELECT 문에서 WITH 절을 사용합니다. 자세한 내용은 참조 [MDX로 측정값 만들기](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDX 데이터 정의 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

