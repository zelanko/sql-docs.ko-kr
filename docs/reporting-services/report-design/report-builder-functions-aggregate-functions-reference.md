---
title: "집계 함수 참조(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: db6542ee-02d0-4073-90e6-cba8f9510fbb
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 8e5fec757d51ced0226c57a76c9117ba752177e3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="report-builder-functions---aggregate-functions-reference"></a>보고서 작성기 함수 - 집계 함수 참조
  보고서에 집계 값을 포함하려면 식에서 기본 제공 집계 함수를 사용할 수 있습니다. 숫자 필드에 대한 기본 집계 함수는 SUM입니다. 식을 편집하고 다른 기본 제공 집계 함수를 사용하거나 다른 범위를 지정할 수 있습니다. 범위는 계산에 사용할 데이터 집합을 식별합니다.  
  
 보고서 처리기가 보고서 데이터와 보고서 레이아웃을 결합할 때 각 보고서 항목에 대한 식이 계산됩니다. 보고서의 각 페이지를 볼 때 렌더링된 보고서 항목에 각 식의 결과가 표시됩니다.  
  
 다음 표에서는 식에 포함할 수 있는 기본 제공 함수의 범주를 나열합니다.  
  
-   [기본 제공 집계 함수](#CalculatingAggregates)  
  
-   [기본 제공 필드, 컬렉션 및 집계 함수의 제한 사항](#Restrictions)  
  
-   [중첩 집계의 제한 사항](#NestedRestrictions)  
  
-   [실행 값 계산](#CalculatingRunningValues)  
  
-   [행 개수 검색](#RetrievingRowCounts)  
  
-   [다른 데이터 집합에서 값 조회](#LookupFunctions)  
  
-   [정렬 종속 값 검색](#RetrievingPostsortValues)  
  
-   [서버 집계 검색](#RetrievingServerAggregates)  
  
-   [재귀 수준 검색](#RetrievingRecursiveLevel)  
  
-   [범위 테스트](#TestingforScope)  
  
 각 함수에 대한 유효한 범위를 확인하려면 개별 함수 참조 항목을 확인하십시오. 예제는 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CalculatingAggregates"></a> 기본 제공 집계 함수  
 다음 기본 제공 함수는 기본 범위 또는 명명된 범위에서 Null이 아닌 숫자 데이터의 집합에 대한 요약 값을 계산합니다.  
  
|**함수**|**Description**|  
|------------------|---------------------|  
|[Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md)|식으로 지정되어 정해진 범위에서 계산되는 Null이 아닌 모든 숫자 값의 평균을 반환합니다.|  
|[Count](../../reporting-services/report-design/report-builder-functions-count-function.md)|식으로 지정되어 정해진 범위의 컨텍스트에서 계산되는 Null이 아닌 값의 개수를 반환합니다.|  
|[CountDistinct](../../reporting-services/report-design/report-builder-functions-countdistinct-function.md)|식으로 지정되어 정해진 범위의 컨텍스트에서 계산되는 Null이 아닌 모든 고유 값의 개수를 반환합니다.|  
|[Max](../../reporting-services/report-design/report-builder-functions-max-function.md)|특정 범위의 컨텍스트에서 식에 의해 지정된 Null이 아닌 모든 숫자 값의 최대값을 반환합니다. 이 함수로 차트 축의 최대값을 지정하여 눈금을 제어할 수 있습니다.|  
|[Min](../../reporting-services/report-design/report-builder-functions-min-function.md)|지정된 범위의 컨텍스트에서 식으로 지정되는 Null이 아닌 모든 숫자 값의 최소값을 반환합니다. 이 함수로 차트 축의 최소값을 지정하여 눈금을 제어할 수 있습니다.|  
|[StDev](../../reporting-services/report-design/report-builder-functions-stdev-function.md)|식으로 지정되어 정해진 범위에서 계산되는 Null이 아닌 모든 숫자 값의 표준 편차를 반환합니다.|  
|[StDevP](../../reporting-services/report-design/report-builder-functions-stdevp-function.md)|식으로 지정되어 정해진 범위의 컨텍스트에서 계산되는 Null이 아닌 모든 숫자 값의 모집단 표준 편차를 반환합니다.|  
|[Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md)|식으로 지정되어 정해진 범위에서 계산되는 Null이 아닌 모든 숫자 값의 합계를 반환합니다.|  
|[Union](../../reporting-services/report-design/report-builder-functions-union-function.md)|식으로 지정되어 정해진 범위에서 계산되는 **SqlGeometry** 또는 **SqlGeography** 형식의 Null이 아닌 모든 공간 데이터 값의 합집합을 반환합니다.|  
|[Var](../../reporting-services/report-design/report-builder-functions-var-function.md)|식으로 지정되어 정해진 범위에서 계산되는 Null이 아닌 모든 숫자 값의 분산을 반환합니다.|  
|[VarP](../../reporting-services/report-design/report-builder-functions-varp-function.md)|식으로 지정되어 정해진 범위의 컨텍스트에서 계산되는 Null이 아닌 모든 숫자 값의 모집단 분산을 반환합니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="Restrictions"></a> 기본 제공 필드, 컬렉션 및 집계 함수의 제한 사항  
 다음 표에는 전역 기본 제공 컬렉션에 대한 참조가 포함된 식을 추가할 수 있는 보고서 위치에서의 제한 사항이 요약되어 있습니다.  
  
|보고서의 위치|필드|매개 변수|ReportItems|PageNumber<br /><br /> TotalPages|DataSource<br /><br /> DataSet|변수|RenderFormat|  
|------------------------|------------|----------------|-----------------|-------------------------------|----------------------------|---------------|------------------|  
|페이지 머리글<br /><br /> 페이지 바닥글|예|예|최대 하나<br /><br /> 참고 1|예|예|예|예|  
|본문|예<br /><br /> 참고 2|예|현재 범위 또는 포함하는 범위의 항목만<br /><br /> 참고 3|아니오|예|예|예|  
|보고서 매개 변수|아니오|목록 앞부분의 매개 변수만<br /><br /> 참고 4|아니오|아니오|아니오|아니오|아니오|  
|필드|예|예|아니오|아니오|아니오|아니오|아니오|  
|쿼리 매개 변수|아니오|예|아니오|아니오|아니오|아니오|아니오|  
|그룹 식|예|예|아니오|아니요|예|아니오|아니오|  
|정렬 식|예|예|아니오|아니요|예|예<br /><br /> 참고 5|아니오|  
|필터 식|예|예|아니오|아니요|예|예<br /><br /> 참고 6|아니오|  
|코드|아니오|예<br /><br /> 참고 7|아니오|아니오|아니오|아니오|아니오|  
|보고서 언어|아니오|예|아니오|아니오|아니오|아니오|아니오|  
|변수|예|예|아니오|아니요|예|현재 범위 또는 포함하는 범위|아니오|  
|집계|예|예|페이지 머리글/페이지 바닥글에서만|보고서 항목 집계에서만|예|아니오|아니오|  
|조회 함수|예|예|예|아니오|예|아니오|아니오|  
  
-   **참고 1.** ReportItems는 렌더링된 보고서 페이지에 있어야 하며, 그렇지 않은 경우 값이 null입니다. 보고서 항목의 표시 유형이 False로 계산되는 식에 따라 달라지는 경우 해당 보고서 항목이 페이지에 없습니다.  
  
-   **참고 2.** 필드 참조가 그룹 범위에서 사용되고 필드 참조가 그룹 식에 포함되어 있지 않은 경우 범위에 값이 하나만 있지 않으면 필드의 값이 정의되지 않습니다. 값을 지정하려면 First 또는 Last와 그룹 범위를 사용합니다.  
  
-   **참고 3.** ReportItems에 대한 참조를 포함하는 식은 동일한 그룹 범위나 포함하는 그룹 범위에서 다른 ReportItems의 값을 지정할 수 있습니다.  
  
-   **참고 4.** 이전 매개 변수의 속성 값이 null일 수 있습니다.  
  
-   **참고 5.** 멤버 정렬에서만. 데이터 영역 정렬 식에서는 사용할 수 없습니다.  
  
-   **고 6.** 멤버 필터에서만. 데이터 영역 또는 데이터 집합 필터 식에서는 사용할 수 없습니다.  
  
-   **참고 7.** 매개 변수 컬렉션은 코드 블록이 처리된 후까지 초기화되지 않으므로 메서드를 사용하여 초기화 시 매개 변수를 제어할 수 없습니다.  
  
-   **참고 8.** Count 및 CountDistinct를 제외한 모든 집계의 데이터 형식은 모든 값에 대해 동일한 데이터 형식이거나 Null이어야 합니다.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="NestedRestrictions"></a> 중첩 집계의 제한 사항  
 다음 표에는 다른 집계 함수를 중첩 집계로 지정할 수 있는 집계 함수의 제한 사항이 요약되어 있습니다.  
  
|컨텍스트|RunningValue|RowNumber|첫째<br /><br /> 마지막|Previous|Sum 및 기타 미리 정렬 함수|ReportItem 집계|조회 함수|Aggregate 함수|  
|-------------|------------------|---------------|--------------------|--------------|-------------------------------------|---------------------------|----------------------|------------------------|  
|Running Value|아니오|아니오|아니오|아니요|예|아니오|예|아니오|  
|첫째<br /><br /> 마지막|아니오|아니오|아니오|아니요|예|아니오|아니오|아니오|  
|Previous|예|예|예|아니오|예|아니오|예|아니오|  
|Sum 및 기타 미리 정렬 함수|아니오|아니오|아니오|아니요|예|아니오|예|아니오|  
|ReportItem 집계|아니오|아니오|아니오|아니오|아니오|아니오|아니오|아니오|  
|조회 함수|예|예<br /><br /> 참고 1|예<br /><br /> 참고 1|예<br /><br /> 참고 1|예<br /><br /> 참고 1|예<br /><br /> 참고 1|아니오|아니오|  
|Aggregate 함수|아니오|아니오|아니오|아니오|아니오|아니오|아니오|아니오|  
  
-   **참고 1.** 집계 함수는 Lookup 함수가 집계에 포함되지 않은 경우 Lookup 함수의 *Source* 식 안에서만 허용됩니다. 집계 함수는 Lookup 함수의 *Destination* 또는 *Result* 식 안에서 허용되지 않습니다.  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="CalculatingRunningValues"></a> 실행 값 계산  
 다음 기본 제공 함수는 데이터의 집합에 대한 실행 값을 계산합니다. **RowNumber** 는 포함하는 범위 내의 각 행에 대해 증가하는 개수의 실행 값을 반환한다는 점에서 **RunningValue** 와 비슷합니다. 이러한 함수의 범위 매개 변수는 개수 계산을 다시 시작하는 시점을 제어하는 포함하는 범위를 지정해야 합니다.  
  
|**함수**|**Description**|  
|------------------|---------------------|  
|[RowNumber](../../reporting-services/report-design/report-builder-functions-rownumber-function.md)|지정한 범위에서 행 개수의 실행 개수를 반환합니다. **RowNumber** 는 0이 아닌 1부터 계산을 다시 시작합니다.|  
|[RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md)|식으로 지정되어 정해진 범위에서 계산되는 Null이 아닌 모든 숫자 값의 실행 집계를 반환합니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="RetrievingRowCounts"></a> 행 개수 검색  
 다음 기본 제공 함수는 지정된 범위에서 행 개수를 계산합니다. 이 함수를 사용하여 Null 값을 가진 행을 포함한 모든 행의 개수를 계산할 수 있습니다.  
  
|**함수**|**Description**|  
|------------------|---------------------|  
|[CountRows](../../reporting-services/report-design/report-builder-functions-countrows-function.md)|Null 값을 가진 행을 포함하여 지정된 범위의 행 수를 반환합니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="LookupFunctions"></a> 다른 데이터 집합에서 값 조회  
 다음 조회 함수는 지정된 데이터 집합에서 값을 검색합니다.  
  
|**함수**|**Description**|  
|------------------|---------------------|  
|[Lookup 함수](../../reporting-services/report-design/report-builder-functions-lookup-function.md)|데이터 집합에서 지정된 식에 대한 값을 반환합니다.|  
|[LookupSet 함수](../../reporting-services/report-design/report-builder-functions-lookupset-function.md)|데이터 집합에서 지정된 식에 대한 값 집합을 반환합니다.|  
|[Multilookup 함수](../../reporting-services/report-design/report-builder-functions-multilookup-function.md)|이름/값 쌍을 포함하는 데이터 집합에서 이름 집합과 처음 일치하는 값 집합을 반환합니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="RetrievingPostsortValues"></a> 정렬 종속 값 검색  
 다음 기본 제공 함수는 지정된 범위 내의 첫 번째, 마지막 또는 이전 값을 반환합니다. 이러한 함수는 데이터 값의 정렬 순서에 따라 달라집니다. 예를 들어 이러한 함수를 사용하여 페이지의 첫 번째와 마지막 값을 찾아 사전 스타일의 페이지 머리글을 만들 수 있습니다. 예를 들어 **Previous** 를 사용하여 특정 범위 내에서 한 행에 있는 값을 이전 행의 값과 비교하여 테이블에서 전년동기대비 백분율 값을 찾을 수 있습니다.  
  
|**함수**|**Description**|  
|------------------|---------------------|  
|[첫째](../../reporting-services/report-design/report-builder-functions-first-function.md)|지정된 식의 지정된 범위에서 첫 번째 값을 반환합니다.|  
|[마지막](../../reporting-services/report-design/report-builder-functions-last-function.md)|지정된 식의 지정된 범위에서 마지막 값을 반환합니다.|  
|[Previous](../../reporting-services/report-design/report-builder-functions-previous-function.md)|지정된 범위 내에서 항목의 이전 인스턴스에 대한 지정된 집계 값 또는 값을 반환합니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="RetrievingServerAggregates"></a> 서버 집계 검색  
 다음 기본 제공 함수는 데이터 공급자에서 사용자 지정 집계를 검색합니다. 예를 들어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본 유형을 사용하면 데이터 원본 서버에서 계산된 집계를 검색하여 그룹 머리글에 사용할 수 있습니다.  
  
|**함수**|**Description**|  
|------------------|---------------------|  
|[집계](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)|데이터 공급자가 정의한 대로 지정한 식의 사용자 지정 집계를 반환합니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="TestingforScope"></a> 범위 테스트  
 다음 기본 제공 함수는 보고서 항목의 현재 컨텍스트를 테스트하여 특정 범위에 속하는지 확인합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|[InScope](../../reporting-services/report-design/report-builder-functions-inscope-function.md)|항목의 현재 인스턴스가 지정한 범위 내에 있는지 여부를 나타냅니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
##  <a name="RetrievingRecursiveLevel"></a> 재귀 수준 검색  
 다음 기본 제공 함수는 재귀 계층이 처리될 때 현재 수준을 검색합니다. 이 함수의 결과를 입력란의 **Padding** 속성에 사용하여 재귀 그룹에 대한 시각적 계층의 들여쓰기 수준을 제어할 수 있습니다. 자세한 내용은 [재귀 계층 구조 그룹 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)을 참조하세요.  
  
|함수|Description|  
|--------------|-----------------|  
|[Level](../../reporting-services/report-design/report-builder-functions-level-function.md)|재귀 계층의 현재 수준을 반환합니다.|  
  
 ![맨 위 링크와 함께 사용되는 화살표 아이콘](../../analysis-services/instances/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")맨 위로 이동  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
