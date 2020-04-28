---
title: TopPercent (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8c92a4b6a76cb9d15048d6f058038363970cb8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036588"
---
# <a name="toppercent-mdx"></a>TopPercent(MDX)


  집합을 내림차순으로 정렬하고 누적 합계가 지정된 백분율 이상인 상위 값 튜플 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TopPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *백분율*  
 반환할 튜플의 백분율을 지정하는 유효한 숫자 식입니다.  
  
> [!IMPORTANT]  
>  *백분율* 은 양수 여야 합니다. 음수 값은 오류를 생성 합니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **TopPercent** 함수는 지정 된 집합에 대해 계산 된 지정 된 숫자 식의 합계를 계산 하 여 집합을 내림차순으로 정렬 합니다. 그런 다음 총 합계 값에 대한 누적 백분율이 지정된 백분율 이상이 되는 상위 값 요소를 반환합니다. 이 함수는 누적 합계가 지정된 백분율 이상이 되는 집합의 가장 작은 하위 집합을 반환합니다. 반환되는 요소는 가장 큰 값에서 가장 작은 값 순서로 정렬됩니다.  
  
> [!WARNING]  
>  *Numeric_Expression* 음수 값을 반환 하는 경우 **TopPercent** 는 1 개의 행만 반환 합니다.  
>   
>  이 동작의 세부적인 내용은 두 번째 예제를 참조하십시오.  
  
> [!IMPORTANT]  
>  [BottomPercent](../mdx/bottompercent-mdx.md) 함수와 마찬가지로 **TopPercent** 함수는 항상 계층 구조를 중단 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Bike 범주에 대해 대리점의 상위 10% 매출에 기여하는 최고의 도시를 반환합니다. 결과는 매출액이 가장 높은 도시부터 내림차순으로 정렬됩니다.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopPercent  
   ({[Geography].[Geography].[City].Members}  
   , 10  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
```  
  
 위의 식은 다음 결과를 생성합니다.  
  
||Reseller Sales Amount|  
|-|---------------------------|  
|Toronto|$3508904.84|  
|London|$1521530.09|  
|Seattle|$1209418.16|  
|파리|$1170425.18|  
  
 원래 데이터 집합은 다음 쿼리로 얻을 수 있으며 588개의 행을 반환합니다.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
Order  
   ({[Geography].[Geography].[City].Members}  
   , [Measures].[Reseller Sales Amount]  
   , BDESC  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
  
```  
  
## <a name="example"></a>예제  
 다음 연습은 *Numeric_Expression*음수 값의 효과를 이해 하는 데 도움이 됩니다. 우선 동작을 나타낼 수 있는 컨텍스트를 만들어 보겠습니다.  
  
 다음 쿼리는 수익의 내림차순으로 정렬된 Resellers 'Sales Amount', 'Total Product Cost' 및 'Gross Profit'의 테이블을 반환합니다. 수익이 음수 값만 있으므로 가장 적은 손해가 위쪽에 나타납니다.  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  ORDER( [Product].[Product Categories].[Bikes].[Touring Bikes].children, [Measures].[Reseller Gross Profit], BDESC )   ON rows  
FROM [Adventure Works]  
  
```  
  
 위의 쿼리는 다음 결과를 반환합니다. 가운데 섹션의 행은 가독성을 위해 제거되었습니다.  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157444.56|$163112.57|($5668.01)|  
|여행용-2000 파랑, 46|$321027.03|$333021.50|($11994.47)|  
|Touring-3000 Blue, 62|$87773.61|$100133.52|($12359.91)|  
|...|...|...|...|  
|여행용-1000 노랑, 46|$1016312.83|$1234454.27|($218141.44)|  
|Touring-1000 Yellow, 60|$1184363.30|$1443407.51|($259044.21)|  
  
 수익별로 상위 100% 자전거를 프레젠테이션해야 할 경우에는 다음과 같은 쿼리를 작성합니다.  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  TOPPERCENT( [Product].[Product Categories].[Bikes].[Touring Bikes].children, 100,[Measures].[Reseller Gross Profit] )   ON rows  
FROM [Adventure Works]  
  
```  
  
 100%를 요청하는 쿼리란 모든 행을 반환해야 함을 의미합니다. 그러나 *Numeric_Expression* 에는 음수 값이 있으므로 한 행만 반환 됩니다.  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157444.56|$163112.57|($5668.01)|  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
