---
title: Predict (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca47db953df9889cb1d72d0add45f2b0ed681980
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742612"
---
# <a name="predict-mdx"></a>Predict(MDX)


    
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
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
