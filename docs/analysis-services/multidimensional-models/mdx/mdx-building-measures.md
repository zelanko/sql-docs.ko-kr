---
title: MDX로 측정값 작성 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2095d3bde254a59c5b2edbe8ebb117854ab7777
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026100"
---
# <a name="mdx-building-measures"></a>측정값 MDX 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX에서 측정값은 테이블 형식 모델의 값을 반환하기 위해 식을 계산하여 확인되는 명명된 DAX 식입니다. 이러한 정의에는 놀랄 만한 개념이 포함되어 있습니다. MDX 쿼리에서 측정값을 구성하고 사용할 수 있으면 테이블 형식 데이터에 대한 상당한 조작 기능을 활용할 수 있습니다.  
  
> [!WARNING]  
>  측정값은 테이블 형식 모델에서만 정의할 수 있습니다. 데이터베이스가 다차원 모드로 설정된 경우 측정값을 만들면 오류가 생성됩니다.  
  
 MDX 쿼리의 일부로 정의되는 측정값을 만들어서 해당 범위가 쿼리로 제한되도록 하려면 WITH 키워드를 사용합니다. 그런 다음 MDX SELECT 문 내에서 측정값을 사용할 수 있습니다. 이 방식을 사용할 경우 WITH 키워드를 사용하여 만든 계산 멤버는 SELECT 문을 배포하지 않아도 변경할 수 있습니다. 그러나 MDX 식에서 측정값을 참조하는 방법은 DAX 식에서와는 다릅니다. 측정값을 참조하려면 측정값을 [측정값] 차원의 멤버로 지정해야 합니다. 다음 MDX 예를 참조하십시오.  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 위 MDX 식을 실행하면 다음 데이터가 반환됩니다.  
  
||Total Sales Amount||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>관련 항목:  
 [MEMBER 문 & #40; 만들기 Mdx& #41;](../../../mdx/mdx-data-definition-create-member.md)   
 [MDX 함수 참조 & #40; Mdx& #41;](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT 문 & #40; Mdx& #41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
