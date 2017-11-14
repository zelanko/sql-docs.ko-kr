---
title: "측정값 | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27ec8f99-e9ef-44c9-a83f-f7c88e128ad3
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38b7467cd4ad765d651ea0ebe4ad57c278c987a1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="measures"></a>측정값 그룹
  테이블 형식 모델에서 측정값은 보고 클라이언트용 DAX 수식을 사용하여 만든 계산입니다. 측정값은 보고 클라이언트 응용 프로그램에서 사용자가 선택하는 필드, 필터 및 슬라이서에 따라 평가됩니다.  
  
##  <a name="bkmk_understanding"></a> 이점  
 AVERAGE, COUNT 또는 SUM과 같은 표준 집계 함수를 기반으로 측정값을 만들거나 DAX를 사용하여 고유한 수식을 정의할 수 있습니다. 각 측정값에는 수식 외에 이름, 테이블 세부 정보, 형식, 소수 자릿수와 같은 측정값 데이터 형식으로 정의된 속성이 있습니다.  
  
 측정값이 모델에서 정의되면 사용자가 이를 보고서나 피벗 테이블에 추가할 수 있습니다. 큐브 뷰 및 역할에 따라 측정값은 필드 목록에 테이블과 연결되어 표시되며 모델의 모든 사용자가 사용할 수 있습니다. 일반적으로 측정값은 팩트 테이블에서 생성되지만 연결된 테이블에 대해 독립적일 수 있습니다.  
  
 계산 열과 측정값 간의 근본적인 차이점을 이해하는 것이 중요합니다. 계산 열에서는 수식이 열에 있는 각 행의 값으로 계산됩니다. 예를 들어 FactSales 테이블에서는 다음 수식을 포함하는 TotalProfit이라는 계산 열이 FactSales 테이블에 있는 각 행(판매당 한 행)의 총 수익 값을 계산합니다.  
  
```  
=[SalesAmount] - [TotalCost] - [ReturnAmount]  
```  
  
 그런 다음 보고 클라이언트에 다른 열과 마찬가지로 TotalProfit 계산 열을 사용할 수 있습니다.  
  
 한편 측정값은 사용자가 선택한 값으로 계산됩니다. 필터 컨텍스트는 피벗 테이블 또는 보고서에서 설정합니다. 예를 들어 FactSales 테이블의 측정값은 다음 수식을 사용하여 만듭니다.  
  
```  
Sum of TotalProfit: =SUM([TotalProfit])  
```  
  
 판매 분석가가 Excel을 사용해 제품 범주의 총 수익을 파악하고자 합니다. 각 제품 범주는 여러 제품으로 구성됩니다. 판매 분석가가 ProductCategoryName 열을 선택하여 피벗 테이블의 행 레이블 필터 창에 추가합니다. 그러면 각 제품 범주의 행이 피벗 테이블에 표시됩니다. 그런 다음 사용자는 TotalProfit 측정값의 합계를 선택합니다. 측정값이 기본적으로 값 필터 창에 추가됩니다. 측정값에서 총 수익의 합계를 계산하고 각 제품 범주의 결과를 표시합니다. 따라서 판매 분석가가 CalendarYear를 슬라이서로 추가하여 각 제품 범주의 연도별 총 수익을 확인하는 등 슬라이서를 사용하여 각 제품 범주의 총 수익 합계를 자세히 필터링할 수 있습니다.  
  
|ProductCategoryName|Totalprofit의 합계|  
|-------------------------|------------------------|  
|오디오|$2,731,061,308.69|  
|카메라 및 캠코더|$620,623,675.75|  
|컴퓨터|$392,999,044.59|  
|Tv와 비디오|$946,989,702.51|  
|**총합계**|**$4,691,673,731.53**|  
  
##  <a name="bkmk_def_mg"></a> Defining measures by using the measure grid  
 측정값은 모델 디자이너에서 측정값 표를 사용하여 디자인 타임에 생성됩니다. 각 테이블에 측정값 표가 포함됩니다. 기본적으로 측정값 표는 모델 디자이너에서 각 테이블 아래에 표시됩니다. 또한 특정 테이블에 대해 측정값 표를 표시하지 않도록 선택할 수 있습니다. 테이블의 측정값 표 표시를 전환하려면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
 측정값 표에서 다음과 같은 방법으로 측정값을 만들 수 있습니다.  
  
-   측정값 표에서 빈 셀을 클릭하고 수식 입력줄에서 DAX 수식을 입력합니다. ENTER를 클릭하여 수식을 완성하면 측정값이 측정값 표의 셀에 나타납니다.  
  
-   열을 클릭하고 도구 모음에서 자동 합계 단추(∑)를 클릭한 다음 표준 집계 함수를 클릭하여 표준 집계 함수를 이용해 측정값을 만듭니다. 표준 집계로는 Sum, Average, Count, DistinctCount, Max 및 Min이 있습니다. 측정값은 항상 측정값 표의 해당 열 바로 아래에 나타납니다.  
  
 기본적으로 자동 합계를 사용하면 관련 열의 이름, 콜론, 수식이 차례로 연결된 형태로 측정값의 이름이 정의됩니다. 이 이름은 수식 입력줄 또는 속성 창의 **측정값 이름** 속성 설정에서 변경할 수 있습니다. 사용자 지정 수식을 사용하여 측정값을 만들 경우 수식 입력줄에 이름, 콜론, 수식을 차례로 입력하거나 속성 창의 **측정값 이름** 속성 설정에 이름을 입력할 수 있습니다.  
  
 반드시 측정값의 이름 신중 하 게 합니다. 측정값 이름이 관련 테이블과 함께 보고 클라이언트의 필드 목록에 표시됩니다. KPI도 기본 측정값에 따라 이름이 지정됩니다. 측정값 이름이 모델에 있는 테이블의 이름과 같으면 안 됩니다.  
  
> [!TIP]  
>  빈 테이블을 만들고 이동하여 여러 테이블에서 한 테이블로 측정값을 그룹화하거나 빈 테이블에서 새 측정값을 만들 수 있습니다. 다른 테이블에서 열을 참조할 때 DAX 수식에 테이블 이름을 포함시켜야 할 수 있습니다.  
  
 큐브 뷰가 모델에 대해 정의된 경우 측정값이 해당 큐브 뷰에 자동으로 추가되지 않습니다. 큐브 뷰 대화 상자를 사용하여 측정값을 큐브 뷰에 수동으로 추가해야 합니다. 자세한 내용은 참고 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_properties"></a> 측정값 속성  
 각 측정값에는 측정값을 정의하는 속성이 있습니다. 속성 창에서 측정값 속성을 관련 열 속성과 함께 편집할 수 있습니다. 측정값의 속성은 다음과 같습니다.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**Description**|비어 있음|측정값에 대한 설명입니다. 설명은 측정값과 함께 보고 클라이언트에 표시되지 않습니다.|  
|**형식**|수식 식에서 참조되는 열의 데이터 형식에 따라 자동으로 결정됩니다.|측정값의 형식입니다. 예를 들어 통화 또는 백분율입니다.|  
|**수식**|측정값을 만들 때 수식 입력줄에 입력된 수식입니다.|측정값의 수식입니다.|  
|**측정값 이름**|자동 합계를 사용하면 측정 값 이름이 열 이름 앞에 표시되고 그 뒤에 콜론이 표시됩니다. 사용자 지정 수식을 입력할 경우 이름, 콜론, 수식을 차례로 입력합니다.|보고 클라이언트 필드 목록에 표시된 측정값의 이름입니다.|  
  
##  <a name="bkmk_KPI"></a> KPI의 측정값 사용  
 KPI(핵심 성과 지표)는 측정값으로 정의된 *기본* 값을 측정값이나 절대값으로 정의된 *대상* 값과 비교하여 정의됩니다. 또한 KPI는 그래픽 형식으로 표시되며 기본 값이 임계값 사이의 대상 값에 대해서만 평가를 수행하는 계산인 *상태*를 포함합니다. KPI는 경영진이 중요한 비즈니스 메트릭 동향을 식별하는 데 자주 사용됩니다.  
  
 모든 측정값을 KPI의 기본 측정값으로 사용할 수 있습니다. KPI를 만들려면 측정값 표에서 측정값을 마우스 오른쪽 단추로 클릭한 다음 **KPI 만들기**를 클릭합니다. KPI 대화 상자에서 측정값 또는 절대값으로 정의된 대상 값을 지정하고 상태 임계값과 그래픽 종류를 정의할 수 있습니다. 자세한 내용은 참고 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_rel_tasks"></a> Related tasks  
  
|항목|Description|  
|-----------|-----------------|  
|[측정값 만들기 및 관리](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)|모델 디자이너의 측정값 표를 사용하여 측정값을 만들고 관리하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Kpi 만들기 및 관리](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)   
 [계산 된 열](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  

