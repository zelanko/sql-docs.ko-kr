---
title: Predict (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PREDICT
dev_langs: kbMDX
helpviewer_keywords: Predict function
ms.assetid: a82f3edd-249b-4559-98d3-6e10d81a095d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c06caa21c9bfcd041cfd25df17d134a317d518fb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="predict-mdx"></a>Predict(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!CAUTION]  
>  이 함수는 내부 불일치로 인해 제거 중에 있습니다.  
>   
>  DMX 식을 사용한 해결 방법을 보려면 "예" 섹션을 검토하십시오.  
  
 데이터 마이닝 모델에 대해 계산되는 숫자 식의 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Predict(Mining_Model_Name,String_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Mining_Model_Name*  
 마이닝 모델의 이름을 나타내는 유효한 문자열 식입니다.  
  
 *String_Expression*  
 지정한 마이닝 모델에 대해 유효한 DMX 식으로 계산되는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 **Predict** 함수 지정된 된 마이닝 모델의 컨텍스트 내에서 지정 된 문자열 식을 계산 합니다.  
  
 데이터 마이닝 구문과 함수는 DMX(Data Mining Expression) 참조에 설명되어 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Customer Clusters 마이닝 모델을 사용하여 클러스터의 이름 및 특정 고객 클러스터와의 거리를 예측합니다.  
  
```  
WITH MEMBER MEASURES.CLNAME AS   
PREDICT("Customer Clusters", "Cluster()")  
MEMBER MEASURES.CLDISTANCE AS   
PREDICT("Customer Clusters", "ClusterDistance(Cluster())")  
SELECT {MEASURES.CLNAME, MEASURES.CLDISTANCE} ON 0   
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Customer].&[12012])  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
