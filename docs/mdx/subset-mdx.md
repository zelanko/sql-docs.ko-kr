---
title: Subset (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: subset
dev_langs: kbMDX
helpviewer_keywords: Subset function
ms.assetid: 49a7cd28-cd6f-4ae7-8c91-94a8652a97a5
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 820ab5f42f8956ccf454fbed6c60600516c36a67
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="subset-mdx"></a>Subset(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 집합에서 튜플의 하위 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *시작*  
 반환할 첫 번째 튜플의 위치를 지정하는 유효한 숫자 식입니다.  
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 지정된 된 집합에서의 **하위 집합** 함수는 지정 된 수 만큼의 튜플이 지정 된 시작 위치에서 시작을 포함 하는 하위 집합을 반환 합니다. 시작 위치는 인덱스(0부터 시작)를 기반으로 합니다. 즉, 0은 지정된 집합의 첫 번째 튜플에 해당하고 1은 두 번째 튜플에 해당합니다.  
  
 경우 *Count* 를 지정 하지 않으면 함수까지 모든 튜플을 반환 *시작* 집합의 끝에 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. **하위 집합** 함수는 사용 하 여 결과 정렬 한 후 결과에서 처음 다섯 개의 집합만 반환 하는 데 사용 되는 **순서** 함수입니다.  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
