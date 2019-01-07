---
title: 보고서 디자인 뷰 (보고서 작성기) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10440"
- "10426"
- "10439"
- "10434"
- "10438"
- "10436"
helpviewer_keywords:
- reports, creating
- user interface
- overview of Report Builder
ms.assetid: 1544472c-2803-448d-af52-e901cb457a00
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 42fdd43e7e535452d01701fd7d230484ae30fcae
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52712164"
---
# <a name="report-design-view-report-builder"></a>보고서 디자인 뷰(보고서 작성기)
  보고서 작성기 창은 보고서 리소스를 쉽게 구성하고 필요한 페이지가 매겨진 보고서를 신속하게 작성할 수 있도록 디자인되어 있습니다. 디자인 화면은 창의 가운데에 있고 그 주위에 리본과 창이 있습니다. 디자인 화면에서 보고서 항목을 추가하고 구성합니다. 이 문서에서는 보고서 리소스를 추가, 선택 및 구성하고 보고서 항목 속성을 변경하는 데 사용하는 창에 대해 설명합니다.  
  
 ![보고서 작성기 디자인 뷰](../../reporting-services/report-builder/media/ssrb-designview.png "보고서 작성기 디자인 뷰")  
  
1.  리본  
  
2.  [매개 변수 창](#Ribbon)  
  
3.  [보고서 파트 갤러리](#ReptPartGallery)  
  
4.  [속성 창](#PropertiesPane)  
  
5.  [보고서 디자인 화면](#RptDesignSurface)  
  
6.  [보고서 데이터 창](#ReptDataPane)  
  
7.  [그룹화 창](#GroupPane)  
  
8.  현재 보고서 상태 표시줄  
  
##  <a name="Ribbon"></a> 매개 변수 창  
 보고서 매개 변수를 사용하면 보고서 데이터를 제어하고, 관련된 보고서를 서로 연결하고, 다양하게 보고서를 표현할 수 있습니다. 매개 변수 창에서는 보고서 매개 변수에 대한 유연한 레이아웃을 제공합니다.  
  
 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
  
##  <a name="RptDesignSurface"></a> 보고서 디자인 화면  
 보고서 작성기 보고서 디자인 화면은 보고서를 디자인할 때 주로 사용되는 작업 영역입니다. 데이터 영역, 하위 보고서, 입력란, 이미지, 사각형 및 선과 같은 보고서 항목을 보고서에 배치하려면 원하는 보고서 항목을 리본 또는 보고서 파트 갤러리에서 디자인 화면에 추가합니다. 디자인 화면에서 보고서 항목에 그룹, 식, 매개 변수, 필터, 동작, 표시 유형 및 서식을 추가할 수 있습니다.  
  
 다음을 변경할 수도 있습니다.  
  
-   디자인 화면에서 보고서 항목 바깥쪽의 흰색 영역을 마우스 오른쪽 단추로 클릭하고 **본문 속성**을 클릭하여 보고서 본문 속성(예: 테두리 및 채우기 색)을 변경할 수 있습니다.  
  
-   디자인 화면의 머리글 또는 바닥글 영역에서 보고서 항목 바깥쪽의 흰색 영역을 마우스 오른쪽 단추로 클릭하고 **머리글 속성** 또는 **바닥글 속성**을 클릭하여 머리글 및 바닥글 속성(예: 테두리 및 채우기 색)을 변경할 수 있습니다.  
  
-   디자인 화면 주변의 회색 영역을 마우스 오른쪽 단추로 클릭하고 **보고서 속성**을 클릭하여 페이지 설정과 같은 보고서 자체의 속성을 변경할 수 있습니다.  
  
-   보고서 항목을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하여 보고서 항목의 속성을 변경할 수 있습니다.  
  
 키보드를 사용하여 디자인 화면의 항목을 조작하는 방법에 대한 자세한 내용은 [바로 가기 키&#40;보고서 작성기&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)를 참조하세요.  
  
### <a name="design-surface-size-and-print-area"></a>디자인 화면 크기 및 인쇄 영역  
 디자인 화면의 크기가 보고서 인쇄를 위해 지정한 인쇄 영역의 페이지 크기와 다를 수도 있습니다. 디자인 화면의 크기를 변경해도 보고서의 인쇄 영역은 변경되지 않습니다. 보고서 인쇄 영역으로 설정한 크기에 관계없이 전체 디자인 화면 크기는 변경되지 않습니다. 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!TIP]  
>  눈금자를 표시하려면 **보기** 탭에서 **눈금자** 확인란을 선택합니다.  
  
  
##  <a name="ReptDataPane"></a> The Report Data Pane  
 보고서 데이터 창에서는 보고서 레이아웃을 디자인하기 전에 보고서에 필요한 보고서 데이터와 보고서 리소스를 정의합니다. 예를 들어 데이터 원본, 데이터 세트, 계산 필드, 보고서 매개 변수 및 이미지를 보고서 데이터 창에 추가할 수 있습니다.  
  
 보고서 데이터 창에 항목을 추가한 후 필드를 디자인 화면의 보고서 항목으로 끌어 보고서에서 데이터가 나타나는 위치를 제어할 수 있습니다.  
  
> [!TIP]  
>  보고서 데이터 창의 필드를 테이블 또는 차트와 같은 데이터 영역에 배치하는 대신에 보고서 디자인 화면으로 직접 끌어서 놓으면 보고서를 실행할 때 해당 필드의 데이터에 있는 첫 번째 값만 표시됩니다.  
  
 또한 보고서 데이터 창에서 기본 제공 필드를 보고서 디자인 화면으로 끌 수 있습니다. 이러한 필드는 렌더링될 때 보고서 이름, 보고서의 총 페이지 수, 현재 페이지 번호 등 보고서에 대한 정보를 제공합니다.  
  
 보고서 디자인 화면에 추가할 때 일부 항목은 보고서 데이터 창에 자동으로 추가됩니다. 예를 들어 보고서 파트 갤러리에서 보고서 파트를 추가할 때 보고서 파트가 데이터 영역인 경우 데이터 세트가 보고서 데이터 창에 자동으로 추가됩니다. 자세한 내용은 [보고서 작성기의 보고서 파트 및 데이터 세트](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)를 참조하세요. 또한 보고서에 이미지를 포함한 경우 보고서 데이터 창의 이미지 폴더에 이미지가 추가됩니다.  
  
> [!NOTE]  
>  **새로 만들기** 단추를 사용하여 보고서 데이터 창에 새 항목을 추가할 수 있습니다. 동일한 데이터 원본 또는 다른 데이터 원본의 여러 데이터 세트를 보고서에 추가할 수 있습니다. 또한 보고서 서버에 있는 공유 데이터 세트를 추가할 수 있습니다. 같은 데이터 원본의 새 데이터 세트를 추가하려면 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음, **데이터 세트 추가**를 클릭합니다.  
  
 보고서 데이터 창의 항목에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
-   [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)  
  
-   [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [이미지&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)  
  
-   [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
-   [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
-   [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
##  <a name="ReptPartGallery"></a> 보고서 파트 갤러리  
 보고서를 만드는 가장 쉬운 방법은 보고서 서버나 SharePoint 사이트에 통합된 보고서 서버에서 테이블, 차트 등의 기존 보고서 파트를 찾는 것입니다.  
  
 삽입 탭에서 **보고서 파트** 를 클릭하여 보고서 파트 갤러리를 엽니다. 여기서 보고서에 추가할 보고서 파트를 검색할 수 있습니다. 보고서 파트 이름(전체 또는 일부분), 파트를 만든 사람, 마지막으로 수정한 사람, 마지막으로 수정한 시간, 저장 위치 또는 파트 유형으로 파트를 필터링할 수 있습니다. 예를 들어 지난 주에 동료 중 한 사람이 만든 모든 차트를 검색할 수 있습니다.  
  
> [!NOTE]  
>  보고서 파트 갤러리를 보려면 서버에 연결되어 있어야 합니다.  
  
 검색 결과는 축소판 그림이나 목록으로 볼 수 있으며 이름, 만든 날짜/수정한 날짜 및 작성자로 정렬할 수 있습니다. 자세한 내용은 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)를 참조하세요.  
  
  
##  <a name="PropertiesPane"></a> 속성 창(보고서 작성기)  
 데이터 영역, 이미지, 입력란 및 보고서 본문 자체를 비롯한 보고서의 모든 항목은 연관된 속성을 가지고 있습니다. 예를 들어 입력란의 BorderColor 속성은 입력란 테두리의 색 값을 표시하고 보고서의 PageSize 속성은 보고서의 페이지 크기를 표시합니다.  
  
 이러한 속성은 속성 창에 표시됩니다. 선택한 보고서 항목에 따라 속성 창에 표시되는 속성이 달라집니다.  
  
 속성 창을 보려면 보기 탭의 표시/숨기기 그룹에서 속성을 클릭합니다.  
  
### <a name="changing-property-values"></a>속성 값 변경  
 보고서 작성기에서는 다음과 같은 몇 가지 방법으로 보고서 항목의 속성을 변경할 수 있습니다.  
  
-   리본의 단추 및 목록을 클릭합니다.  
  
-   대화 상자 내에서 설정을 변경합니다.  
  
-   속성 창에서 속성 값을 변경합니다.  
  
 자주 사용하는 속성은 대화 상자와 리본에 표시됩니다.  
  
 속성에 따라 드룹다운 목록에서 속성 값을 선택하여 속성을 설정하거나, 속성 값을 직접 입력하거나, `<Expression>` 을 클릭하여 식을 만들 수 있습니다.  
  
### <a name="changing-the-properties-pane-view"></a>속성 창 보기 변경  
 속성 창에 표시되는 속성은 기본적으로 Action, Border, Fill, Font 및 General이라는 큰 범주로 나뉘어 표시됩니다. 범주마다 연관된 속성 집합이 있습니다. 예를 들어 Color, FontFamily, FontSize, FontStyle, FontWeight, LineHeight 및 TextDecoration 속성은 Font 범주에 나타납니다. 원하는 경우 속성 창에서 모든 속성을 사전순으로 표시할 수 있습니다. 이 경우 범주가 없어지고 모든 속성이 범주에 관계없이 사전순으로 표시됩니다.  
  
 속성 창의 아래쪽에는 범주, 사전순, 속성 페이지라는 세 개의 단추가 있습니다. 범주 및 사전순 단추를 클릭하면 속성 창 보기를 전환할 수 있고 **속성 페이지** 단추를 클릭하면 선택한 보고서 항목의 속성 대화 상자를 열 수 있습니다.  
  
  
##  <a name="GroupPane"></a> 그룹화 창(보고서 작성기)  
 그룹은 보고서 데이터를 시각적 계층으로 구성하고 합계를 계산하는 데 사용됩니다. 디자인 화면은 물론 그룹화 창에서도 데이터 영역 내의 행 및 열 그룹을 볼 수 있습니다. 그룹화 창에는 행 그룹과 열 그룹의 두 창이 있습니다. 데이터 영역을 선택하면 해당 데이터 영역 내의 모든 그룹이 계층적 목록으로 그룹화 창에 표시되며, 자식 그룹은 해당 부모 그룹보다 한 수준 아래에 표시됩니다.  
  
 ![보고서 작성기 행 그룹](../../reporting-services/report-builder/media/ssrb-rowgroups.png "보고서 작성기 행 그룹")  
  
 보고서 데이터 창에서 필드를 끌어 디자인 화면이나 그룹화 창에 놓아서 그룹을 만들 수 있습니다. 그룹화 창에서는 부모 그룹, 인접 그룹 및 자식 그룹을 추가하거나 그룹 속성을 변경하거나 그룹을 삭제하는 등의 작업을 수행할 수 있습니다.  
  
 그룹화 창은 기본적으로 표시되지만 보기 탭에서 그룹화 창 확인란의 선택을 취소하여 닫을 수 있습니다. 차트 및 계기 데이터 영역은 그룹화 창에서 사용할 수 없습니다.  
  
 자세한 내용은 [그룹화 창&#40;보고서 작성기&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md) 및 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
  
##  <a name="RunMode"></a> 실행 모드에서 보고서 미리 보기  
 보고서 디자인 뷰에서는 실제 데이터로 작업하는 것이 아니라 필드 이름이나 식으로 나타나는 데이터 표현으로 작업합니다. 디자인한 보고서의 문맥에 표시되는 실제 데이터를 확인하려는 경우에는 보고서를 실행하여 보고서 레이아웃에 표시되는 기본 데이터베이스의 데이터를 미리 볼 수 있습니다. 보고서 디자인과 실행 작업 간을 전환하면서 보고서의 디자인을 조정하고 결과를 즉시 볼 수 있습니다. 보고서를 미리 보려면 리본의 **뷰** 그룹에서 **실행** group on the ribbon.  
  
 **실행**을 클릭하면 보고서 작성기가 보고서 데이터 원본에 연결하고, 컴퓨터에 데이터를 캐시하고, 데이터와 레이아웃을 결합한 다음 HTML 뷰어에서 보고서를 렌더링합니다. 보고서를 계속 디자인하면서 필요에 따라 보고서를 실행해 볼 수 있습니다. 보고서가 만족스럽게 작성되면 보고서 서버에 보고서를 저장할 수 있으며 보고서 서버에 저장된 보고서는 적절한 권한이 있는 다른 사용자가 볼 수 있습니다.  
   
 자세한 내용은 [보고서 작성기에서 보고서 미리 보기](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)를 참조하세요.  
  
### <a name="running-a-report-with-parameters"></a>매개 변수가 있는 보고서 실행  
 보고서를 실행하면 보고서가 자동으로 처리됩니다. 보고서에 매개 변수가 있는 경우 모든 매개 변수에 기본값이 있어야 보고서를 자동으로 실행할 수 있습니다. 매개 변수에 기본값이 없는 경우 보고서를 실행할 때에는 매개 변수 값을 선택한 후 실행 탭에서 **보고서 보기** 를 클릭해야 합니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
### <a name="print-preview"></a>인쇄 미리 보기  
 보고서를 실행 모드에서 미리 보면 HTML로 생성된 보고서와 유사하게 표시됩니다. 미리 보기는 HTML 형식은 아니지만 보고서의 레이아웃 및 페이지 매기기는 HTML 출력과 유사합니다. 인쇄 미리 보기 모드로 전환하여 인쇄될 보고서를 표시할 수 있습니다. **실행** 탭에서 **인쇄 미리 보기** 단추를 클릭합니다. 보고서는 실제 인쇄된 페이지처럼 표시되며 이미지 및 PDF 렌더링 확장 프로그램에서 생성된 출력과도 유사합니다. 인쇄 미리 보기는 이미지나 PDF 파일 형식은 아니지만 보고서의 레이아웃 및 페이지 매기기는 해당 형식의 출력과 유사합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [SQL Server의 보고서 작성기](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  
  
