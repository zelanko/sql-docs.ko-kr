---
title: 데이터 영역 및 지도(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- data regions
ms.assetid: 3afb8874-b36c-4e44-a0d8-80d2f7135fb1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6065e26f36561b446257825f7f953c5eeccc3b25
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290901"
---
# <a name="data-regions-and-maps-report-builder-and-ssrs"></a>데이터 영역 및 지도(보고서 작성기 및 SSRS)
  데이터 영역은 보고서 데이터 세트에 있는 데이터를 표시하는 보고서의 개체입니다. 보고서 데이터는 테이블, 행렬 또는 목록에 숫자 및 텍스트로 표시되거나, 차트 또는 계기에 그래픽으로 표시되거나, 지도에 지리적 배경을 바탕으로 표시될 수 있습니다. 테이블, 행렬 및 목록은 모두 데이터 세트의 모든 데이터를 표시하기 위해 필요에 따라 확장되는 *테이블릭스* 데이터 영역을 기반으로 합니다. 테이블릭스 데이터 영역은 정적 행과 열 및 동적 행과 열이 모두 포함된 여러 행 및 열 그룹을 지원합니다. 차트는 여러 계열 및 범주 그룹을 다양한 차트 형식으로 표시하고, 계기는 데이터 세트의 단일 값 또는 집계 값을 표시합니다. 또한 지도는 공간 데이터를 데이터 세트에서 집계한 데이터를 기반으로 모양이 변하는 지도 요소로 표시합니다.  
  
 데이터 영역 또는 지도를 *보고서 파트*로 저장할 수 있습니다. [보고서 파트](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)에 대해 자세히 알아봅니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="table"></a>Table  
 테이블은 데이터를 행 단위로 표시하는 데이터 영역입니다. 테이블의 열은 고정되어 있습니다. 열의 개수는 보고서를 디자인할 때 결정합니다. 그러나 테이블 행은 고정되지 않고 데이터에 맞게 아래쪽으로 확장됩니다. 테이블에 그룹을 추가하여 선택한 필드나 식으로 데이터를 구성할 수 있습니다. 보고서에 테이블을 추가하는 방법에 대한 자세한 내용은 [테이블&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="matrix"></a>행렬  
 행렬은 크로스탭이라고도 합니다. 행렬 데이터 영역에는 동적 열과 행이 모두 포함되며 데이터에 맞게 확장됩니다. 또한 행렬에는 동적 열과 행 및 정적 열과 행이 있을 수 있습니다. 열이나 행에 다른 열이나 행을 넣을 수 있으며 데이터를 그룹화하는 데 열이나 행을 사용할 수 있습니다. 자세한 내용은 [보고서에 행렬 추가](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="list"></a>목록  
 목록은 자유로운 형태로 정렬된 데이터를 표시하는 데이터 영역입니다. 보고서 항목을 정렬하여 목록 내의 어느 위치에나 입력란, 이미지 및 기타 데이터 영역을 포함하는 양식을 만들 수 있습니다. 자세한 내용은 [보고서에 목록 추가](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="chart"></a>차트  
 차트는 데이터를 그래픽으로 표시합니다. 차트에는 가로 막대형, 원형 및 꺾은선형 차트가 있으며 이외에도 많은 스타일이 지원됩니다. 자세한 내용은 [보고서에 차트 추가](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="gauge"></a>계기  
 계기는 범위 내의 특정 값을 가리키는 표시기가 있는 범위로 데이터를 나타냅니다. 계기는 KPI(핵심 성과 지표)와 기타 메트릭을 표시하는 데 사용됩니다. 계기의 예로는 선형 계기와 원형 계기가 있습니다. 자세한 내용은 [보고서에 계기 추가](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="map"></a>지도  
 지도를 사용하면 지리적 배경을 바탕으로 데이터를 제공할 수 있습니다. 지도 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리의 공간 데이터, ESRI 셰이프 파일 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing 지도 타일일 수 있습니다. 공간 데이터는 모양이나 영역을 나타내는 다각형, 경로나 길을 나타내는 선, 표식으로 나타내는 점 등을 정의하는 좌표 집합으로 구성됩니다. 집계 데이터와 지도 요소를 연결하면 지도 요소의 색과 크기를 자동으로 변경할 수 있습니다. 예를 들어 판매액을 기준으로 상점의 표식 유형을 변경하거나 속도 제한을 기준으로 길의 색을 변경할 수 있습니다. 자세한 내용은 [지도&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="data-regions-in-the-report-layout"></a>보고서 레이아웃의 데이터 영역  
 보고서에는 여러 데이터 영역을 추가할 수 있으며, 데이터 영역은 연결된 보고서 데이터 세트의 데이터에 맞게 확장됩니다. 예를 들어 연도별 각 제품의 판매량을 표시하는 행렬에는 제품 이름을 기반으로 하는 행 그룹과 연도를 기반으로 하는 열 그룹이 있습니다. 보고서를 실행하면 행렬은 각 제품에 대해 페이지 아래쪽으로 확장되고, 각 연도에 대해 페이지 가로 방향으로 확장됩니다. 보고서 디자인 화면의 행렬 옆에 있는 차트는 렌더링된 보고서의 확장된 행렬 옆에 표시됩니다. 페이지에서 데이터 영역이 렌더링되는 방식은 보고서 출력 형식을 기반으로 하는 규칙 집합을 따릅니다. 예를 들어 차트 및 행렬이 페이지에서 렌더링되는 방식을 제어하려는 경우 사각형을 컨테이너로 사용하거나 목록에 있는 두 데이터 영역을 중첩할 수 있습니다. 자세한 내용은 [페이지 레이아웃 및 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)로 저장할 수 있습니다.  
  
## <a name="nested-data-regions"></a>중첩된 데이터 영역  
 다른 데이터 영역에 데이터 영역을 중첩할 수 있습니다. 예를 들어 각 영업 사원의 영업 실적을 데이터베이스로 만들려는 경우 입력란과 이미지를 포함하는 목록을 만들어 직원에 대한 정보를 표시하고 테이블과 차트 데이터 영역을 목록에 추가하여 영업 사원의 영업 실적을 표시할 수 있습니다. 자세한 내용은 [중첩된 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="multiple-data-regions-linked-to-the-same-dataset"></a>동일한 데이터 세트에 연결된 여러 데이터 영역  
 동일한 데이터 세트에 둘 이상의 데이터 영역을 연결하여 동일한 데이터에 대한 다양한 뷰를 제공할 수 있습니다. 예를 들어 테이블과 차트에 동일한 데이터를 표시할 수 있습니다. 테이블을 정렬하면 차트도 자동으로 정렬되도록 하기 위해 테이블에 대화형 정렬 단추를 제공하는 보고서를 작성할 수 있습니다. 자세한 내용은 [동일한 데이터 세트에 여러 데이터 영역 연결&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="data-for-a-data-region"></a>데이터 영역의 데이터  
 각 테이블릭스, 차트 및 계기는 단일 데이터 세트의 데이터를 표시하도록 디자인되었습니다. 지도는 같은 데이터 세트 또는 여러 데이터 세트의 공간 데이터와 분석 데이터를 표시합니다. 그 밖에 다음과 같은 방법으로 데이터 영역에 연결되지 않은 데이터 세트의 값을 포함할 수 있습니다.  
  
-   다른 데이터 세트로 한정된 정렬 순서나 그룹화에 종속되지 않은 값을 집계합니다.  
  
-   다른 데이터 세트의 이름/값 쌍에서 값을 조회합니다.  
  
 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 제작 개념&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [보고서, 보고서 파트 및 보고서 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [페이지 레이아웃 및 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)   
 [보고서 작성기 자습서](../../reporting-services/report-builder-tutorials.md)   
 [Reporting Services&#40;SSRS&#41; 자습서](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
