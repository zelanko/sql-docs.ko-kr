---
title: Ascendants (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ASCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: df35665a82149bd133e4116d97cb739d70865ac7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="ascendants-mdx"></a>Ascendants(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  멤버 자체를 포함하여 지정한 멤버의 상위 항목 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **Ascendants** 함수 멤버의 계층의 최상위까지 멤버 자체에서 모든 멤버의 상위 항목을 반환; 보다 구체적으로, 지정된 된 멤버에 대 한 계층의 후 위 순회를 수행 하 고 다음 반환 모든 상위 항목 멤버와 관련 된 멤버를 집합에서 자신을 포함 하 합니다. 이 달리는 [상위](../mdx/ancestor-mdx.md) 특정 구성원, 또는 특정 수준에서 상위 항목을 반환 하는 함수입니다.  
  
## <a name="examples"></a>예  
 한에 대 한 대리점 주문 건수를 반환 하는 다음 예제는 `[Sales Territory].[Northwest]` 멤버와 해당 멤버의 모든 상위 항목은 **Adventure Works** 큐브. **상위** 포함 된 집합을 구성 하는 함수는 `[Sales Territory].[Northwest]` 멤버 및 ROWS 축에 대 한 상위 항목입니다.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
