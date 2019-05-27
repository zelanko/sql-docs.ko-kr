---
title: 합계, 집계 및 기본 제공 컬렉션 (보고서 작성기 및 SSRS)의 식 범위 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a8d24287-8557-4b03-bea7-ca087f449b62
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b8d9838306090cf219fed799c5982481ac3365a9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105915"
---
# <a name="expression-scope-for-totals-aggregates-and-built-in-collections-report-builder-and-ssrs"></a>합계, 집계 및 기본 제공 컬렉션의 식 범위(보고서 작성기 및 SSRS)
  식을 작성할 때 여러 컨텍스트에서 *범위* 라는 용어를 자주 볼 수 있습니다. 범위는 식 계산에 사용하는 데이터, 렌더링된 페이지의 입력란 집합, 그리고 토글을 기반으로 표시하거나 숨길 수 있는 보고서 항목 집합을 지정할 수 있습니다. *범위* 라는 용어는 식 계산, 집계 함수 구문, 조건부 표시 유형 및 이러한 영역과 관련된 오류 메시지에서 볼 수 있습니다. 다음 설명을 참조하면 적용되는 *범위* 의 각 의미를 구분할 수 있습니다.  
  
-   **데이터 범위** 보고서 프로세서가 보고서 데이터와 보고서 레이아웃을 결합하고 데이터를 표시할 테이블, 차트 등의 데이터 영역을 작성할 때 사용하는 범위의 계층 구조입니다. 데이터 범위에 대해 이해하면 다음 작업을 수행할 때 원하는 결과를 얻을 수 있습니다.  
  
    -   **집계 함수를 사용하는 식 작성** 집계할 데이터를 지정합니다. 보고서의 식 위치는 집계 계산의 범위에 속하는 데이터에 영향을 줍니다.  
  
    -   **테이블 또는 행렬에 스파크라인 추가** 테이블 또는 행렬에서 중첩된 인스턴스를 맞추는 차트 축의 최소 및 최대 범위를 지정합니다.  
  
    -   **테이블 또는 행렬에 표시기 추가** 테이블 또는 행렬에서 중첩된 인스턴스를 맞추는 계기의 최소 및 최대 눈금을 지정합니다.  
  
    -   **정렬 식 작성** 여러 관련 보고서 항목의 정렬 순서를 동기화하는 데 사용할 수 있는 포함 범위를 지정합니다.  
  
-   **셀 범위** 테이블릭스 데이터 영역에서 셀이 속하는 행 및 열 그룹 집합입니다. 기본적으로 각 테이블릭스 셀은 입력란을 포함합니다. 이 입력란의 결과가 식입니다. 셀의 위치는 식의 집계 계산에 대해 지정할 수 있는 데이터 범위를 결정하는 데 간접적으로 영향을 줍니다.  
  
-   **보고서 항목 범위** 렌더링된 보고서 페이지의 항목 컬렉션을 의미합니다. 보고서 프로세서는 데이터 및 보고서 레이아웃을 결합하여 컴파일된 보고서 정의를 생성합니다. 이 프로세스 중에 테이블, 행렬 등의 데이터 영역은 필요에 따라 확장되어 모든 보고서 데이터를 표시합니다. 그런 다음 컴파일된 보고서는 보고서 렌더러에서 처리됩니다. 보고서 렌더러는 각 페이지에 표시되는 보고서 항목을 결정합니다. 보고서 서버에서 각 페이지는 표시할 때 렌더링됩니다. 보고서를 내보내면 모든 페이지가 렌더링됩니다. 보고서 항목 범위에 대해 이해하면 다음 작업을 수행할 때 원하는 결과를 얻을 수 있습니다.  
  
    -   **토글 항목 추가** 보고서 항목 표시 유형을 제어하는 토글을 추가할 입력란을 지정합니다. 토글할 보고서 항목의 범위에 있는 입력란에만 토글을 추가할 수 있습니다.  
  
    -   **페이지 머리글 및 바닥글에 식 작성** 렌더링된 페이지에 나타나는 입력란이나 기타 보고서 항목에 있는 식의 값을 지정합니다.  
  
 범위에 대해 이해하면 원하는 결과를 얻을 수 있게 하는 식을 올바르게 작성할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DataScope"></a> 데이터 범위 및 데이터 계층 이해  
 데이터 범위는 보고서 데이터 집합을 지정하며 기본 제약 관계가 지정된 자연 계층을 포함합니다. 계층에서 순위가 높은 범위가 낮은 범위를 포함합니다. 다음 데이터 범위 목록에서는 계층을 데이터가 많은 순서대로 설명합니다.  
  
-   **데이터 집합 필터를 적용한 후의 데이터 집합** 보고서 본문의 보고서 항목 또는 데이터 영역에 연결된 보고서 데이터 집합을 지정합니다. 집계에 사용되는 데이터는 데이터 세트 필터 식을 적용한 후 보고서 데이터 세트에서 가져옵니다. 공유 데이터 세트의 경우에는 공유 데이터 세트 정의의 필터와 보고서의 공유 데이터 세트 인스턴스 필터가 모두 해당됩니다.  
  
-   **데이터 영역** 데이터 영역 필터와 정렬 식을 적용한 후의 데이터 영역에 있는 데이터를 지정합니다. 그룹 필터는 데이터 영역의 집계를 계산할 때 사용되지 않습니다.  
  
-   **그룹 필터를 적용한 후의 데이터 영역 그룹** 부모 그룹과 자식 그룹에 그룹 식과 그룹 필터를 적용한 후의 데이터를 지정합니다. 테이블의 경우에는 행 및 열 그룹이고 차트의 경우에는 계열 및 범주 그룹입니다. 범위 제약을 식별하기 위해 모든 부모 그룹은 해당 자식 그룹을 포함합니다.  
  
-   **중첩된 데이터 영역** 추가된 셀의 컨텍스트에서 중첩된 데이터 영역 필터와 정렬 식을 적용한 후의 중첩된 데이터 영역에 대한 데이터를 지정합니다.  
  
-   **중첩된 데이터 영역에 대한 행 및 열 그룹** 중첩된 데이터 영역의 그룹 식과 그룹 필터를 적용한 후의 데이터를 지정합니다.  
  
 집계 함수를 포함하는 식을 작성할 때는 포함하는 범위와 포함되는 범위를 이해해야 합니다.  
  
##  <a name="Aggregates"></a> 셀 범위 및 식  
 범위를 지정할 때는 집계 계산에 사용할 데이터를 보고서 프로세서가 알 수 있도록 지정합니다. 식 및 식 위치에 따라 유효한 범위는 *포함하는 범위*(부모 범위라고도 함)일 수도 있고 *포함되는 범위*(자식 또는 중첩된 범위라고도 함)일 수도 있습니다. 일반적으로는 집계 계산에서 개별 그룹 인스턴스를 지정할 수 없으며 모든 그룹 인스턴스에 대해 집계를 지정할 수 있습니다.  
  
 보고서 프로세서는 보고서 데이터 세트의 데이터를 테이블릭스 데이터 영역에 결합할 때 그룹 식을 계산하여 그룹 인스턴스를 표시하는 데 필요한 행 및 열을 만듭니다. 각 테이블릭스 셀에 있는 입력란의 식 값은 셀 범위의 컨텍스트에서 계산됩니다. 테이블릭스 구조에 따라 한 셀이 여러 행 그룹 및 열 그룹에 속할 수 있습니다. 집계 함수의 경우에는 사용할 범위를 지정할 때 다음 범위 중 하나를 사용할 수 있습니다.  
  
-   **기본 범위** 보고서 프로세서가 식을 계산할 때 계산 범위에 있는 데이터입니다. 기본 범위는 셀이나 데이터 요소가 속하는 가장 안쪽 그룹 집합입니다. 테이블릭스 데이터 영역의 경우 이 집합에는 행 및 열 그룹이 포함될 수 있으며 차트 데이터 영역의 경우에는 범주 및 계열 그룹이 포함될 수 있습니다.  
  
-   **명명된 범위** 식의 범위에 있는 데이터 집합, 데이터 영역 또는 데이터 영역 그룹의 이름입니다. 집계 계산의 경우 포함하는 범위를 지정할 수 있습니다. 단일 식에서 행 그룹과 열 그룹 모두에 대해 명명된 범위를 지정할 수는 없습니다. 또한 집계의 집계를 위한 식이 아니면 포함되는 범위는 지정할 수 없습니다.  
  
     다음 식은 SellStartDate와 LastReceiptDate 사이의 간격 연도를 생성합니다. 이러한 필드는 두 가지 다른 데이터 세트 즉, DataSet1 및 DataSet2에 있습니다. 집계 함수인 [첫 번째 함수&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-first-function.md)는 DataSet1에 있는 SellStartDate의 첫 번째 값과 DataSet2에 있는 LastReceiptDate의 첫 번째 값을 반환합니다.  
  
    ```  
    =DATEDIFF("yyyy", First(Fields!SellStartDate.Value, "DataSet1"), First(Fields!LastReceiptDate.Value, "DataSet2"))  
    ```  
  
-   **도메인 범위** 동기화 범위라고도 하며, 중첩된 데이터 영역의 식 계산에 적용되는 데이터 범위 유형입니다. 도메인 범위는 중첩된 인스턴스를 맞추고 쉽게 비교할 수 있도록 모든 그룹 인스턴스에 걸쳐 집계를 지정하는 데 사용됩니다. 예를 들어 값이 정렬되도록 테이블에 포함된 스파크라인에 대해 범위와 높이를 맞출 수 있습니다.  
  
 일부 보고서 위치에서는 범위를 반드시 지정해야 합니다. 예를 들어 디자인 화면의 입력란에는 사용할 데이터 세트의 이름(`=Max(Fields!Sales.Value,"Dataset1")`)을 지정해야 합니다. 즉, 암시적인 기본 범위가 있습니다. 예를 들어 그룹 범위의 입력란에 대해 집계를 지정하지 않으면 기본 집계인 First가 사용됩니다.  
  
 각 집계 함수 항목에는 해당 함수가 사용할 수 있는 범위가 나와 있습니다. 자세한 내용은 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
##  <a name="Examples"></a> 테이블 데이터 영역의 예제 집계 식  
 기본값이 아닌 범위를 지정하는 식을 작성할 때는 특정 방식을 사용합니다. 다음 그림과 표를 참조하면 서로 다른 각 범위를 이해하는 데 도움이 됩니다. 그림에는 상품 판매량을 연도/분기별 및 판매 지역별로 표시하는 판매 정보 테이블의 각 셀이 나와 있습니다. 행 및 열 그룹 구조를 표시하는 행 핸들 및 열 핸들에는 중첩된 그룹을 나타내는 시각 신호가 있습니다. 이 테이블의 구조는 다음과 같습니다.  
  
-   모퉁이 셀 및 행 3개(열 그룹 머리글 포함)가 있는 테이블 머리글  
  
-   범주(Cat) 및 하위 범주(SubCat)를 기준으로 하는 두 중첩된 행 그룹  
  
-   연도(Year) 및 분기(Qtr)를 기준으로 하는 두 중첩된 열 그룹  
  
-   레이블이 Totals인 정적 합계 열 하나  
  
-   판매 지역을 기준으로 하는 인접 열 그룹 하나(Territory)  
  
 Territory 그룹의 열 머리글은 표시를 위해 두 셀로 분할되어 있습니다. 첫 번째 셀에는 지역 이름과 합계가 표시되고 두 번째 셀에는 모든 판매에 대해 각 지역이 차지하는 비율을 계산한 자리 표시자 텍스트가 있습니다.  
  
 ![rs_BasicTableSumCellScope](../media/rs-basictablesumcellscope.gif "rs_BasicTableSumCellScope")  
  
 데이터 세트 이름이 DataSet1이고 테이블 이름이 Tablix1이라고 가정하겠습니다. 다음 표에는 셀 레이블, 기본 범위 및 예제가 나와 있습니다. 자리 표시자 텍스트의 값은 식 구문에서 표시됩니다.  
  
|셀|기본 범위|자리 표시자 레이블|텍스트 또는 자리 표시자 값|  
|----------|-------------------|------------------------|--------------------------------|  
|C01|Tablix1|[Sum(Qty)]|집계 및 범위<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C02|바깥쪽 열 그룹 "Year"|[Year]<br /><br /> ([YearQty])|`=Fields!Year.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C03|Tablix1|[Sum(Qty)]|합계<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C04|피어 열 그룹 "Territory"|([Total])|Territory<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C05|내부 그룹 "Qtr"|[Qtr]<br /><br /> ([QtrQty])|Q<br /><br /> `=Fields!Qtr.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C06|피어 열 그룹 "Territory"|[Territory]<br /><br /> ([Tty])<br /><br /> [Pct]|`=Fields!Territory.Value`<br /><br /> `=Sum(Fields!Qty.Value)`<br /><br /> `=FormatPercent(Sum(Fields!Qty.Value,"Territory")/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C07|바깥쪽 행 그룹 "Cat"|[Cat]<br /><br /> [Sum(Qty)]|`=Fields!Cat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C08|C07과 같음|||  
|C09|바깥쪽 행 그룹 "Cat" 및 안쪽 열 그룹 "Qtr"|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C10|C07과 같음|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C11|바깥쪽 행 그룹 "Cat" 및 열 그룹 "Territory"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Territory"),0) & " of " & Sum(Fields!Qty.Value,"Territory")`|  
|C12|안쪽 행 그룹 "Subcat"|[Subcat]<br /><br /> [Sum(Qty)]|`=Fields!SubCat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C13|안쪽 행 그룹 "Subcat" 및 안쪽 열 그룹 "Qtr"|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C14|안쪽 행 그룹 "Subcat"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Cat"),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
|C15|안쪽 행 그룹 "Subcat" 및 열 그룹 "Territory"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Code.CalcPercentage(Sum(Fields!Qty.Value),Sum(Fields!Qty.Value,"Cat")),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
  
 테이블릭스 데이터 영역의 시각 신호 해석에 대한 자세한 내용은 [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기&#41; 및 SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)를 참조하세요. 테이블릭스 데이터 영역에 대한 자세한 내용은 [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기&#41; 및 SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)를 참조하세요. 식 및 집계에 대한 자세한 내용은 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) 및 [집계 함수 참조&#40;보고서 작성기 및 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)를 참조하세요.  
  
  
  
##  <a name="Sparklines"></a> 스파크라인의 눈금 동기화  
 테이블 또는 행렬에 중첩된 스파크라인 차트에 대해 전체 시간에서 가로 축의 값을 비교하려면 범주 그룹 값을 동기화하면 됩니다. 이를 축 맞추기라고 합니다. 축 맞추기 옵션을 선택하면 보고서가 축의 최소값 및 최대값을 자동으로 설정하며 모든 범주에 없는 집계 값에 대한 자리 표시자를 제공합니다. 그러면 모든 범주에 걸쳐 스파크라인의 값이 정렬되므로 집계된 데이터의 각 행에 대해 값을 비교할 수 있습니다. 이 옵션을 선택하면 식 계산 범위가 *도메인 범위*로 변경됩니다. 중첩된 차트에 대해 도메인 범위를 설정하면 범례에 있는 각 범주에 대한 색 지정도 간접적으로 제어됩니다.  
  
 예를 들어 주별 추세를 표시하는 스파크라인에서 특정 도시의 판매 데이터는 3개월치인데 다른 도시의 판매 데이터는 12개월치라고 가정해 보겠습니다. 동기화된 눈금이 없으면 첫 번째 도시의 스파크라인에는 막대가 3개뿐이므로 12개월에 해당하는 막대 집합이 포함된 두 번째 도시의 스파크라인과 차지하는 공간은 같지만 막대의 폭이 훨씬 넓습니다.  
  
 자세한 내용은 [테이블 또는 행렬에서 차트의 데이터 정렬&#40;보고서 작성기 및 SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)을 참조하세요.  
  
  
  
##  <a name="Indicators"></a> 표시기의 범위 동기화  
 표시기 집합에 사용할 데이터 값을 지정하려면 범위를 지정해야 합니다. 표시기가 포함된 데이터 영역의 레이아웃에 따라 범위 또는 포함하는 범위를 지정합니다. 예를 들어 판매 범주와 연결된 그룹 머리글 행에서는 화살표 집합(위쪽, 아래쪽, 옆쪽)이 임계값을 기준으로 하는 판매 값을 나타낼 수 있습니다. 포함하는 범위는 표시기가 포함된 테이블 또는 행렬의 이름입니다.  
  
 자세한 내용은 [동기화 범위 설정&#40;보고서 작성기 및 SSRS&#41;](set-synchronization-scope-report-builder-and-ssrs.md)을 참조하세요.  
  
  
  
##  <a name="Page"></a> 페이지 머리글 또는 페이지 바닥글에서 범위 지정  
 보고서의 각 페이지마다 달라지는 데이터를 표시하려면 렌더링된 페이지에 있어야 하는 보고서 항목에 식을 추가합니다. 보고서는 렌더링될 때 페이지로 분할되므로 렌더링 중에만 페이지에 있는 항목을 확인할 수 있습니다. 예를 들어 정보 행의 셀에는 페이지의 여러 인스턴스가 포함된 입력란이 있습니다.  
  
 ReportItem이라는 전역 컬렉션을 이 작업에 사용할 수 있습니다. 이 컬렉션은 현재 페이지의 입력란 집합입니다.  
  
 자세한 내용은 [페이지 머리글 및 바닥글&#40;보고서 작성기 및 SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md) 및 [ReportItems 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-reportitems-collection-references-report-builder.md)를 참조하세요.  
  
  
  
##  <a name="Toggles"></a> 드릴다운 및 조건부 표시 유형에 대해 토글 항목 지정  
 토글은 사용자가 클릭하여 다른 보고서 항목을 숨기거나 표시할 수 있는 더하기 또는 빼기 기호 이미지로, 입력란에 추가됩니다. 대다수 보고서 항목 속성의 **표시 유형** 페이지에서 토글을 추가할 보고서 항목을 지정할 수 있습니다. 토글 항목은 표시하거나 숨길 항목보다 상위의 제약 범위에 있어야 합니다.  
  
 테이블릭스 데이터 영역에서 입력란을 클릭해 테이블을 확장하여 더 많은 데이터를 표시할 수 있는 드릴다운 효과를 만들려면 그룹에 대해 **표시 유형** 속성을 설정하고 포함하는 그룹과 연결된 그룹 머리글의 입력란을 토글로 선택해야 합니다.  
  
 자세한 내용은 [항목에 확장 또는 축소 동작 추가&#40;보고서 작성기 및 SSRS&#41;](add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)를 참조하세요.  
  
  
  
##  <a name="Sort"></a> 정렬 순서를 동기화할 정렬 식 지정.  
 대화형 정렬 단추를 테이블 열에 추가할 때 공통의 포함하는 범위를 가진 여러 항목에 대한 정렬을 동기화할 수 있습니다. 예를 들어 행렬의 열 머리글에 정렬 단추를 추가하고 포함하는 범위를 행렬에 바인딩되는 데이터 세트의 이름으로 지정할 수 있습니다. 사용자가 정렬 단추를 클릭하면 행렬 행도 정렬되고 동일 데이터 집합에 바인딩되는 차트의 차트 계열 그룹도 정렬됩니다. 이러한 방식으로 해당 데이터 세트를 사용하는 모든 데이터 영역을 동기화해 같은 정렬 순서를 표시할 수 있습니다.  
  
 자세한 내용은 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)을 참조하세요.  
  
  
  
##  <a name="Nulls"></a> 셀에 Null 또는 0 값 표시하지 않기  
 많은 보고서의 범위가 그룹인 계산에서 0 또는 Null 값이 있는 셀이 여러 개 생성됩니다. 이러한 경우 보고서를 좀 더 단순하게 하려면 집계 값이 0인 경우 공백을 반환하는 식을 추가할 수 있습니다. 자세한 내용은 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md))을 지정해야 합니다.  
  
  
  
## <a name="see-also"></a>관련 항목  
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [그룹 식 예&#40;보고서 작성기 및 SSRS&#41;](group-expression-examples-report-builder-and-ssrs.md)   
 [재귀 계층 구조 그룹 생성&#40;보고서 작성기 및 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
