---
title: DRILLTHROUGH 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 82dd8a9527b85350cae31396ad4d238ef1c8c850
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742282"
---
# <a name="mdx-data-manipulation---drillthrough"></a>MDX 데이터 조작 드릴스루


  큐브에서 지정된 셀을 만드는 데 사용된 기본 테이블 행을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DRILLTHROUGH[MAXROWSUnsigned_Integer]   
      <MDX SELECT statement>   
      [RETURNSet_of_Attributes_and_Measures   
            [,Set_of_Attributes_and_Measures ...]  
      ]  
```  
  
## <a name="arguments"></a>인수  
 *Unsigned_Integer*  
 양의 정수 값입니다.  
  
 *MDX SELECT 문*  
 유효한 MDX 식의 SELECT 문입니다.  
  
 *Set_of_Attributes_and_Measures*  
 쉼표로 구분된 차원 특성 및 측정값 목록입니다.  
  
## <a name="remarks"></a>Remarks  
 드릴스루는 최종 사용자가 세부 정보를 가져오기 위해 큐브에서 단일 셀을 선택하고 해당 셀의 원본 데이터에서 결과 집합을 검색하는 작업입니다. 기본적으로 드릴스루 결과 집합은 선택한 큐브 셀 값을 계산하기 위해 평가된 테이블 행에서 파생됩니다. 최종 사용자가 드릴스루하려면 해당 클라이언트 응용 프로그램에서 이 기능을 지원해야 합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 결과 ROLAP 파티션 또는 차원을 쿼리하지 않는 한 MOLAP 저장소에서 직접 검색 됩니다.  
  
> [!IMPORTANT]  
>  드릴스루 보안은 큐브에 정의된 일반 보안 옵션을 기반으로 합니다. 사용자가 MDX를 사용하여 일부 데이터를 가져올 수 없는 경우 드릴스루도 동일한 방식으로 사용자를 제한합니다.  
  
 MDX 문은 제목 셀을 지정합니다. 에 지정 된 값은 **MAXROWS** 인수는 결과 행 집합에서 반환 해야 하는 행의 최대 수를 나타냅니다.  
  
 기본적으로 반환되는 최대 행 수는 10,000개입니다. 즉, 두면 **MAXROWS** 지정 하지 않으면 받아볼 수 10, 000 행이 있습니다. 이 값이 너무 작으면 시나리오에 대해 설정할 수 있습니다 **MAXROWS** 을 더 높은 숫자와 같은 `MAXROWS 20000`합니다. 변경 하 여 기본값을 늘릴 수 인 경우 너무 낮은 overall는 **OLAP\Query\DefaultDrillthroughMaxRows** 서버 속성입니다. 이 속성을 변경 하는 방법에 대 한 자세한 내용은 참조 [Analysis Services에서 서버 속성](../analysis-services/server-properties/server-properties-in-analysis-services.md)합니다.  
  
 달리 지정되지 않은 경우 반환되는 열에는 다 대 다 차원 이외에 지정된 측정값의 측정값 그룹과 관련된 모든 차원 세분성 특성이 모두 포함됩니다. 차원과 측정값 그룹을 구별할 수 있도록 큐브 차원은 $로 시작됩니다. **반환** 절을 사용 하 여 드릴스루 쿼리에서 반환 된 열을 지정 합니다. 다음 함수는 단일 특성에 적용할 수 있습니다 또는에서 측정값은 **반환** 절.  
  
 Name(attribute_name)  
 지정된 특성 멤버의 이름을 반환합니다.  
  
 UniqueName(attribute_name)  
 지정된 특성 멤버의 고유 이름을 반환합니다.  
  
 Key(attribute_name[, N])  
 지정된 특성 멤버의 키를 반환합니다. 여기에서 N은 복합 키(있는 경우)의 열을 지정합니다. N의 기본값은 1입니다.  
  
 Caption(attribute_name)  
 지정된 특성 멤버의 캡션을 반환합니다.  
  
 MemberValue(attribute_name)  
 지정된 특성 멤버의 멤버 값을 반환합니다.  
  
 CustomRollup(attribute_name)  
 지정된 특성 멤버의 사용자 지정 롤업 식을 반환합니다.  
  
 CustomRollupProperties(attribute_name)  
 지정된 특성 멤버의 사용자 지정 롤업 속성을 반환합니다.  
  
 UnaryOperator(attribute_name)  
 지정된 특성 멤버의 단항 연산자를 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 오스트레일리아의 Reseller Sales Amount 측정값(기본 측정값)에 대한 2007년 7월의 셀을 지정합니다. RETURN 절은 이 셀의 기반이 되는 각 판매 날짜, 제품 모델 이름, 직원 이름, 판매 금액, 세액 및 제품 원가가 반환되도록 지정합니다.  
  
```  
DRILLTHROUGH  
SELECT  
   ([Date].[Calendar].[Month].[July 2007])  
ON 0   
FROM [Adventure Works]  
WHERE [Geography].[Country].[Australia]  
RETURN   
  [$Date].[Date]  
  ,KEY([$Product].[Model Name])  
  ,NAME([$Employee].[Employee])  
  ,[Reseller Sales].[Reseller Sales Amount]  
  ,[Reseller Sales].[Reseller Tax Amount]  
  ,[Reseller Sales].[Reseller Standard Product Cost]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 데이터 조작 문 &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
