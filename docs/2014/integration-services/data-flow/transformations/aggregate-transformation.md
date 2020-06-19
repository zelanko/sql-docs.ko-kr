---
title: 집계 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregatetrans.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8f97259e9388575c8a300ad6e4d1284e55443a60
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84913950"
---
# <a name="aggregate-transformation"></a>집계 변환
  집계 변환은 Average와 같은 집계 함수를 열 값에 적용하고 결과를 변환 출력에 복사합니다. 집계 함수 외에도 변환은 집계할 그룹을 지정하는 데 사용할 수 있는 GROUP BY 절을 제공합니다.  
  
## <a name="operations"></a>작업  
 집계 변환은 다음과 같은 연산을 지원합니다.  
  
|작업(Operation)|Description|  
|---------------|-----------------|  
|Group By|데이터 세트를 그룹으로 나눕니다. 그룹화에는 모든 종류의 데이터 형식의 열을 사용할 수 있습니다. 자세한 내용은 [GROUP BY&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-group-by-transact-sql)를 참조하세요.|  
|합계|열에 있는 값의 합계를 계산합니다. 숫자 데이터 형식의 열만 합계를 계산할 수 있습니다. 자세한 내용은 [SUM&#40;Transact-SQL&#41;](/sql/t-sql/functions/sum-transact-sql)을 참조하세요.|  
|평균|열에 있는 열 값의 평균을 반환합니다. 숫자 데이터 형식의 열만 평균을 계산할 수 있습니다. 자세한 내용은 [AVG&#40;Transact-SQL&#41;](/sql/t-sql/functions/avg-transact-sql)를 참조하세요.|  
|개수|그룹의 항목 개수를 반환합니다. 자세한 내용은 [COUNT&#40;Transact-SQL&#41;](/sql/t-sql/functions/count-transact-sql)를 참조하세요.|  
|Count distinct|그룹에서 Null이 아닌 고유한 값의 개수를 반환합니다.|  
|최소|그룹의 최소값을 반환합니다. 자세한 내용은 [MIN&#40;Transact-SQL&#41;](/sql/t-sql/functions/min-transact-sql)을 참조하세요. Transact-SQL MIN 함수와는 반대로 이 연산은 숫자, 날짜 및 시간 데이터 형식에서만 사용할 수 있습니다.|  
|최대|그룹의 최대값을 반환합니다. 자세한 내용은 [MAX&#40;Transact-SQL&#41;](/sql/t-sql/functions/max-transact-sql)를 참조하세요. Transact-SQL MAX 함수와는 반대로 이 연산은 숫자, 날짜 및 시간 데이터 형식에서만 사용할 수 있습니다.|  
  
 집계 변환은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관계형 데이터베이스 엔진과 동일한 방식으로 Null 값을 처리합니다. 이러한 동작은 SQL-92 표준에서 정의됩니다. 다음 규칙이 적용됩니다.  
  
-   GROUP BY 절에서 Null은 다른 열 값과 같이 취급됩니다. 그룹화 열에 둘 이상의 Null 값이 있다면 단일 그룹에 이 Null 값을 둡니다.  
  
-   COUNT(column name) 및 COUNT (DISTINCT column name) 함수에서는 Null이 무시되고 결과에는 명명된 열에 Null 값이 포함된 행이 제외됩니다.  
  
-   COUNT (*) 함수에서는 Null 값이 포함된 행을 비롯한 모든 행의 개수가 계산됩니다.  
  
## <a name="big-numbers-in-aggregates"></a>집계의 큰 숫자  
 열에는 필요한 값이나 전체 자릿수가 크기 때문에 특별한 고려가 필요한 숫자 값이 포함될 수 있습니다. 집계 변환에는 숫자가 크거나 전체 자릿수가 많은 경우를 특별하게 처리하기 위해 출력 열에 설정할 수 있는 IsBig 속성이 포함됩니다. 열 값이 40억을 넘거나 부동 소수점 데이터 형식보다 큰 전체 자릿수가 필요한 경우에는 IsBig을 1로 설정해야 합니다.  
  
 IsBig 속성을 1로 설정하면 집계 변환의 출력이 다음과 같이 됩니다.  
  
-   DT_R4 데이터 형식 대신 DT_R8 데이터 형식이 사용됩니다.  
  
-   카운트 결과가 DT_UI8 데이터 형식으로 저장됩니다.  
  
-   고유 카운트 결과가 DT_UI4 데이터 형식으로 저장됩니다.  
  
> [!NOTE]  
>  GROUP BY, Maximum 또는 Minimum 연산에서 사용되는 열에는 IsBig을 1로 설정할 수 없습니다.  
  
## <a name="performance-considerations"></a>성능 고려 사항  
 집계 변환에는 변환 성능을 향상시키기 위해 설정할 수 있는 일련의 속성이 포함됩니다.  
  
-   **Group by** 연산을 수행할 때 구성 요소 및 구성 요소 출력의 Keys 또는 KeysScale 속성을 설정합니다. Keys를 사용하면 변환에서 처리할 정확한 개수의 키를 지정할 수 있습니다. 여기서 말하는 Keys는 **Group by** 연산의 결과로 반환될 그룹 수를 나타냅니다. KeysScale을 사용하면 대략적인 개수의 키를 지정할 수 있습니다. Keys 또는 KeyScale에 대한 적절한 값을 지정하는 경우 변환이 캐시하는 데이터에 대해 적합한 메모리를 할당할 수 있으므로 성능이 향상됩니다.  
  
-   **고유 카운트** 연산을 수행할 때 구성 요소의 CountDistinctKeys 또는 CountDistinctScale 속성을 설정합니다. CountDistinctKeys를 사용하면 변환에서 Count distinct 연산에 대해 처리할 정확한 개수의 키를 지정할 수 있습니다. 여기서 말하는 CountDistinctKeys는 **고유 카운트** 연산의 결과로 반환될 고유 값 수를 나타냅니다. CountDistinctScale을 사용하면 Count distinct 연산에 대한 대략적인 개수의 키를 지정할 수 있습니다. CountDistinctKeys 또는 CountDistinctScale에 대한 적절한 값을 지정하는 경우 변환이 해당 변환이 캐시하는 데이터에 대해 적합한 메모리를 할당할 수 있으므로 성능이 향상됩니다.  
  
## <a name="aggregate-transformation-configuration"></a>집계 변환 구성  
 집계 변환은 변환, 출력 및 열 수준에서 구성됩니다.  
  
-   변환 수준에서는 다음 값을 지정하여 집계 변환을 성능에 맞게 구성합니다.  
  
    -   **Group by** 연산의 결과로 반환될 그룹 수  
  
    -   **Count distinct** 연산의 결과로 반환될 고유 값 수  
  
    -   집계 중에 메모리를 확장할 수 있는 비율  
  
     또한 제수 값이 0일 때 오류가 발생하는 대신 경고를 생성하도록 집계 변환을 구성할 수 있습니다.  
  
-   출력 수준에서는 **Group by** 연산의 결과로 반환될 그룹 수를 지정하여 집계 변환을 성능에 맞게 구성합니다. 집계 변환에는 여러 출력이 지원되며 각 출력은 서로 다르게 구성될 수 있습니다.  
  
-   열 수준에서는 다음 값을 지정합니다.  
  
    -   열에서 수행하는 집계  
  
    -   집계의 비교 옵션  
  
 또한 다음 값을 지정하여 집계 변환을 성능에 맞게 구성할 수 있습니다.  
  
-   열에서 **Group by** 연산의 결과로 반환될 그룹 수  
  
-   열에서 **Count distinct** 연산의 결과로 반환될 고유 값 수  
  
 또한 열에 큰 숫자 값이나 전체 자릿수가 높은 숫자 값이 있는 경우 열을 IsBig으로 식별할 수 있습니다.  
  
 집계 변환은 비동기적이며 따라서 행별로 데이터를 사용하고 게시하지 않습니다. 대신 전체 행 집합을 사용하고 그룹화 및 집계를 수행한 다음 결과를 게시합니다.  
  
 이 변환은 어떤 열을 통해서도 전달되지 않지만 게시하는 데이터에 대한 데이터 흐름에 새 열을 만듭니다. 집계 함수가 적용하는 입력 열이나 변환에서 그룹화를 위해 사용되는 입력 열만 변환 출력으로 복사됩니다. 예를 들어 집계 변환 입력에는 **CountryRegion**, **City**및 **Population**과 같은 3개의 열만 포함될 수 있습니다. 변환은 **CountryRegion** 열에 따라 그룹화되며 Sum 함수를 **Population** 열에 적용합니다. 따라서 출력에는 **City** 열이 포함되지 않습니다.  
  
 또한 집계 변환에 여러 출력을 추가하고 각 집계를 서로 다른 출력으로 지정할 수 있습니다. 예를 들어 집계 변환이 Sum 및 the Average 함수를 적용하는 경우 각 집계는 서로 다른 출력으로 지정될 수 있습니다.  
  
 단일 입력 열에 여러 집계를 적용할 수 있습니다. 예를 들어 **Sales**라는 입력 열에 대한 합계 및 평균 값이 필요하면 Sum 및 Average 함수를 모두 **Sales** 열에 적용하도록 변환을 구성할 수 있습니다.  
  
 집계 변환에는 하나의 입력과 하나 이상의 출력이 포함됩니다. 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **집계 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [집계 변환 편집기&#40;집계 탭&#41;](../../aggregate-transformation-editor-aggregations-tab.md)  
  
-   [집계 변환 편집기&#40;고급 탭&#41;](../../aggregate-transformation-editor-advanced-tab.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [집계 변환을 사용하여 데이터 세트의 값 집계](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [집계 변환을 사용하여 데이터 세트의 값 집계](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../data-flow.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
