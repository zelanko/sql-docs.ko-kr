---
title: Kpi | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a0524602-5239-45a7-8c44-2477302a3637
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bb035968cc7c9b5bc40bf176907221becf29076d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="kpis"></a>KPI
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 형식 모델에서 *KPI* (핵심 성과 지표)는 측정값 또는 절대값으로 정의된 *대상* 값에 대해 *기본* 측정값으로 정의된 값의 성능을 측정하는 데 사용됩니다. 이 문서에서는 테이블 형식 모델 작성자 테이블 형식 모델의 Kpi에 대 한 기본적인 이해를 제공 합니다.  
  
##  <a name="bkmk_benefits"></a> 이점  
 비즈니스 용어에서 KPI(핵심 성과 지표)는 비즈니스 목표를 평가하기 위한 정량 측정값입니다. KPI는 주로 시간에 따라 평가됩니다. 예를 들어 조직의 영업부에서는 KPI를 사용하여 월별 예상 매출 총 이익 대비 매출 총 이익을 계산할 수 있습니다. 회계부에서는 월별 수익 대비 지출을 계산하여 비용을 평가하고, 인사부에서는 분기별 직원 전직률을 계산할 수 있습니다. 각각은 KPI의 예에 해당합니다. 경영진은 비즈니스 성과표에 그룹화된 KPI를 사용하여 비즈니스 성취도에 대한 빠르고 정확한 요약 정보를 얻거나 추세를 확인합니다.  
  
 테이블 형식 모델의 KPI에는 다음이 포함됩니다.  
  
 **기본 값**  
 기본 값은 값으로 확인되는 측정값으로 정의됩니다. 이 값은 예를 들어 실제 매출의 집계 또는 특정 기간 동안의 수익과 같은 계산된 측정값일 수 있습니다.  
  
 **대상 값**  
 대상 값은 값으로 확인되는 측정값이나 절대값으로 정의됩니다. 예를 들어, 대상 값은 조직의 비즈니스 관리자가 매출 또는 수익을 증가시키려는 금액일 수 있습니다.  
  
 **상태 임계값**  
 상태 임계값은 낮은 임계값과 높은 임계값 간의 범위 또는 고정 값으로 정의됩니다. 상태 임계값은 그래픽과 함께 표시되므로 대상 값과 비교한 기본 값의 상태를 손쉽게 확인할 수 있습니다.  
  
##  <a name="bkmk_example"></a> 예제  
 Adventure Works의 영업 관리자는 영업 직원이 특정 기간(년) 동안 자신의 판매 할당량을 달성하고 있는지 여부를 빠르게 표시하는 데 사용할 수 있는 피벗 테이블을 만들려고 합니다. 각 영업 직원에 대해 실제 판매액(달러)과 판매 할당액(달러)이 표시되고 각 영업 직원이 현재 자신의 판매 할당액을 달성했는지 그 이하 또는 이상인지를 보여 주는 간단한 그래픽이 표시되는 피벗 테이블을 만들려고 합니다. 또한 데이터를 연도별로 분류할 수 있도록 하려고 합니다.  
  
 이렇게 하기 위해 영업 관리자는 조직의 BI 솔루션 개발자의 도움을 받아 AdventureWorks 테이블 형식 모델에 Sales KPI를 추가합니다. 영업 관리자는은 데이터 원본으로 Adventure Works 테이블 형식 모델에 연결 하 고 필드 (측정값 및 KPI) 및 영업 사원이 자신의 할당액을 달성 하는지 여부를 분석 하는 슬라이서를 피벗 테이블을 만들 Excel을 사용 합니다.  
  
 모델에서 FactResellerSales 테이블의 SalesAmount 열에는 각 영업 직원의 실제 판매액(달러)을 보여 주는 측정값이 만들어집니다. 이 측정값은 KPI의 기본 값을 정의합니다.  
  
 Sales 측정값은 다음 수식을 사용하여 만듭니다.  
  
```  
Sales:=Sum(FactResellerSales[SalesAmount])  
```  
  
 FactSalesQuota 테이블의 SalesAmountQuota 열에는 각 직원에 대해 정의된 판매 할당액이 있습니다. 이 열의 값은 KPI의 대상 측정값(값)으로 사용됩니다.  
  
 SalesAmountQuota 측정값은 다음 수식을 사용하여 만듭니다.  
  
```  
Target SalesAmountQuota:=Sum(FactSalesQuota[SalesAmountQuota])  
```  
  
> [!NOTE]  
>  FactSalesQuota 테이블의 EmployeeKey 열과 DimEmployees 테이블의 EmployeeKey 간에는 관계가 있습니다. 이 관계는 DimEmployee 테이블의 각 영업 직원이 FactSalesQuota 테이블에 표시되도록 하는 데 필요합니다.  
  
 KPI의 기본 값과 대상 값으로 사용할 측정값을 만든 후에는 Sales 측정값을 새 Sales KPI로 확장합니다. Sales KPI에서 Target SalesAmountQuota 측정값은 대상 값으로 정의됩니다. 상태 임계값은 백분율 단위의 범위로 정의되며, 목표 백분율인 100%는 Sales 측정값으로 정의된 실제 판매액이 Target SalesAmoutnQuota 측정값에 정의된 할당액에 도달했음을 의미합니다. 낮은 백분율과 높은 백분율은 상태 표시줄에 정의되고 그래픽 종류가 선택됩니다.  
  
 이제 영업 관리자는 값 필드에 KPI의 기본 값, 대상 값 및 상태를 추가하여 피벗 테이블을 만들 수 있습니다. Employees 열이 RowLabel 필드에 추가되고 CalendarYear 열이 슬라이서로 추가됩니다.  
  
 이제 영업 관리자는 각 영업 직원의 실제 판매액, 판매 할당액 및 상태를 연도별로 분류할 수 있습니다. 또한 몇 년 동안의 판매 추세를 분석하여 영업 직원의 판매 할당액을 조정해야 하는지 여부를 결정할 수 있습니다.  
  
##  <a name="bkmk_create"></a> Create and edit KPIs  
 KPI를 만들려면 모델 디자이너에서 핵심 성과 지표 대화 상자를 사용합니다. KPI는 측정값과 관련되어야 하므로 기준 값으로 평가되는 측정값을 확장한 다음 대상 값으로 평가되는 측정값을 만들거나 절대값을 입력하여 KPI를 만듭니다. 기본 측정값(값과 대상 값을 정의한 후 기준 값과 대상 값 사이에서 상태 임계값 매개 변수를 정의할 수 있습니다. 상태는 선택 가능한 아이콘, 막대, 그래프 또는 색상을 사용하여 그래픽 형식으로 표시됩니다. 그런 다음 기준 값 및 대상 값과 상태를 다른 데이터 필드에 대해 분할할 수 있는 값으로 보고서 또는 피벗 테이블에 추가할 수 있습니다.  
  
 핵심 성과 지표 대화 상자를 보려면 테이블에 대한 측정값 표에서 기준 값으로 사용되는 측정값을 마우스 오른쪽 단추로 클릭한 다음 **KPI 만들기**를 클릭합니다. 측정값이 기준 값으로 KPI에 확장된 후에는 KPI와 관련된 측정값을 식별하는 아이콘이 측정값 표의 측정값 이름 옆에 나타납니다.  
  
##  <a name="bkmk_related_tasks"></a> 관련 작업  
  
|항목|Description|  
|-----------|-----------------|  
|[KPI 만들기 및 관리](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)|기본 측정값, 대상 측정값 및 상태 임계값을 사용하여 KPI를 만드는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [측정값](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  
