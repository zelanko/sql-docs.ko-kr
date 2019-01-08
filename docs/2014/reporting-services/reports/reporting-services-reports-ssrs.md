---
title: Reporting Services 보고서(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, report creation
ms.assetid: 52ed9e74-f2c8-488b-a2c2-6dfbc2a2c8cc
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7372f5457e047772febf4cf040da3f897ae033a2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362905"
---
# <a name="reporting-services-reports-ssrs"></a>Reporting Services 보고서(SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서는 보고서 데이터 및 보고서 레이아웃 요소가 포함된 XML 기반 보고서 정의입니다. 보고서 정의는 .rdl 확장자로 클라이언트 파일 시스템에 저장됩니다. 보고서가 게시된 후에는 보고서 서버 또는 SharePoint 사이트에 저장된 보고서 항목이 됩니다. 보고서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 제공하는 서버 기반 보고 플랫폼의 일부입니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]를 처음 사용하는 경우 [Reporting Services 개념&#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)에 설명된 정보를 검토해야 합니다.  
  
## <a name="benefits-of-reporting-services-reports"></a>Reporting Services 보고서의 이점  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서 솔루션을 사용하면 다음과 같은 이점이 있습니다.  
  
-   단일 버전의 팩트를 제공하는 하나의 데이터 원본 집합을 사용할 수 있습니다. 이러한 데이터 원본의 보고서를 기반으로 비즈니스 의사 결정을 도와주는 통합 데이터 보기를 제공할 수 있습니다.  
  
-   데이터 영역을 사용하여 여러 가지 상호 연결된 방식으로 데이터를 시각화할 수 있습니다. 테이블에 차트를 중첩하는 기능을 사용하여 테이블, 행렬 또는 크로스탭, 확장/축소 그룹, 차트, 계기, 표시기 또는 KPI 및 지도로 구성된 데이터를 표시할 수 있습니다.  
  
-   사용자 자신만 사용하기 위해 보고서를 보거나, 보고서 서버 또는 SharePoint 사이트에 보고서를 게시하여 팀이나 조직과 공유할 수 있습니다.  
  
-   보고서를 한 번 정의하여 다양한 방식으로 표시할 수 있습니다. 보고서를 여러 파일 형식으로 내보내거나, 구독자에게 전자 메일 배달하거나, 공유 파일로 전달할 수 있습니다. 동일한 보고서 정의에 별도의 매개 변수 집합을 적용하는 여러 개의 연결된 보고서를 만들 수 있습니다.  
  
-   보고서 파트, 공유 데이터 원본, 공유 쿼리 및 하위 보고서를 사용하여 다시 사용하도록 데이터 시각화를 정의할 수 있습니다.  
  
-   보고서 데이터 원본을 보고서 정의와 별도로 관리할 수 있습니다. 예를 들어 보고서를 변경하지 않고 테스트 데이터 원본을 프로덕션 데이터 원본으로 변경할 수 있습니다.  
  
-   자유 형식 레이아웃의 보고서를 디자인할 수 있습니다. 이 보고서 레이아웃은 정보 밴드에 제한되지 않습니다. 이해력과 통찰력을 높이고 동작을 향상시키는 방식으로 페이지에 표시되는 데이터를 구성할 수 있습니다.  
  
-   드릴스루 동작, 토글 확장/축소, 단추 정렬, 도구 모음 및 보고서 매개 변수를 사용하여 보고서 구독자가 보고서와 상호 작용하도록 할 수 있습니다. 또한 사용자가 작성한 식과 통합된 보고서 매개 변수를 사용하여 보고서 구독자가 데이터 필터링, 그룹화 및 정렬 방식을 제어하도록 할 수 있습니다.  
  
-   보고서 데이터 필터링, 그룹화 및 정렬 방식을 사용자 지정하는 기능을 제공하는 식을 정의할 수 있습니다.  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="bkmk_StagesSummary"></a> 보고서 처리 단계  
 보고서를 만들 때 XML 형식의 보고서 정의 파일(.rdl)을 정의합니다. 이 파일에는 보고서 처리기에서 보고서 데이터와 보고서 레이아웃을 통합하는 데 필요한 모든 정보가 포함되어 있습니다. 보고서를 볼 때 보고서는 다음 단계를 통해 처리됩니다.  
  
-   **컴파일.** 보고서 정의에 포함된 식을 평가하여 컴파일된 중간 형식을 보고서 서버에 내부적으로 저장합니다.  
  
-   **프로세스.** 데이터 세트 쿼리를 실행하여 중간 형식을 데이터 및 레이아웃과 결합합니다.  
  
-   **렌더링.** 처리된 보고서를 렌더링 확장 프로그램으로 보내 각 페이지에 적합한 정보의 양을 확인하고 페이지가 지정된 보고서를 만듭니다.  
  
-   **내보내기(선택 사항).** 다른 파일 유형으로 보고서를 내보냅니다.  
  
 자세한 내용은 [Reporting Services 개념&#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)에서 [보고서 개발 단계](../reporting-services-concepts-ssrs.md#bkmk_StagesofReports)를 참조하세요.  
  
## <a name="create-reports"></a>보고서 만들기  
 보고서를 만들려면  
  
-   **보고서의 용도를 확인합니다.** 보고서를 사용할 대상의 보고서 사용 목적을 확인합니다. 잘 디자인된 보고서는 보고서 구독자에게 이해를 넓히고 동작을 수행할 수 있는 정보를 제공합니다. 이 단계 중에 결정된 디자인 의사는 보고서 매개 변수, 보고서 레이아웃 디자인 및 보고서 보기 환경에 대한 선택에 영향을 줍니다. 자세한 내용은 msdn.microsoft.com의 [보고서 작성기 설명서](https://go.microsoft.com/fwlink/?LinkId=154494)에서 [보고서 계획&#40;보고서 작성기&#41;](../report-design/planning-a-report-report-builder.md) 및 [보고서 디자인 팁&#40;보고서 작성기 및 SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md)을 참조하세요.  
  
-   **쿼리 유형을 선택합니다.** 일반화된 공유 데이터 세트 쿼리를 사용할지, 아니면 보고서 집합에 특정한 데이터 세트 쿼리를 사용할지 결정합니다. 일반화된 쿼리가 포함된 공유 데이터 세트는 여러 보고서에서 사용하도록 쉽게 유지 관리할 수 있지만 각 보고서 디자이너가 특정 보고서 세트에 필요한 대로 데이터를 필터링해야 합니다. 자세한 내용은 [보고서 데이터&#40;SSRS&#41;](../report-data/report-data-ssrs.md)를 참조하세요.  
  
-   **관련 데이터 보기를 계획합니다.** 보고서 구독자의 보기 환경을 계획합니다. 세부 데이터를 드릴다운할 수 있는 기능이 포함된 요약 보고서는 많은 양의 데이터를 처리하는 데 유용한 접근 방법입니다. 자세한 내용은 [드릴스루, 드릴다운, 하위 보고서 및 중첩 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)을 참조하세요.  
  
-   **사용 권한을 구성합니다.** 올바른 수준의 사용 권한을 부여할 전략을 계획합니다. 일반적인 전략은 보고서 서버에서 폴더 구조를 만들고 역할 및 폴더 보안을 기반으로 보고서 및 보고서 관련 항목에 대한 액세스 권한을 부여하는 것입니다. 자세한 내용은 [보고서 보안](#bkmk_SecureReportsSummary)을 참조하세요.  
  
-   **제작 환경을 선택합니다.** 제작 도구에 따라 지원하는 기능이 다릅니다. 자세한 내용은 [Reporting Services 도구](../tools/reporting-services-tools.md)를 참조하세요.  
  
-   각 보고서에 대해 다음을 수행합니다.  
  
    -   **데이터 원본을 확인합니다.** 각 데이터 원본에 하나씩 보고서 데이터 원본을 정의합니다. 자세한 내용은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)을 참조하세요.  
  
    -   **각 원본에서 사용할 데이터를 선택합니다.** 각 데이터 원본에 대해 보고서 데이터 세트를 정의합니다. 각 데이터 세트에는 사용할 데이터를 지정하는 쿼리가 포함되어 있습니다. 보고서 매개 변수가 있는 경우 각 매개 변수에 사용 가능한 값 목록을 채울 데이터 세트를 정의합니다. 자세한 내용은 [보고서에 데이터 추가&#40;보고서 작성기 및 SSRS&#41;](../report-data/report-datasets-ssrs.md) 및 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
    -   **데이터 시각화를 선택합니다.** 각 데이터 세트에 대해 데이터를 표시하는 데 사용할 데이터 영역을 선택합니다. 테이블, 차트, 계기 및 지도 목록에서 선택할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
        -   [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
        -   [차트&#40;보고서 작성기 및 SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
        -   [스파크라인 및 데이터 막대&#40;보고서 작성기 및 SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
        -   [표시기&#40;보고서 작성기 및 SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)  
  
        -   [지도&#40;보고서 작성기 및 SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)  
  
        -   [계기&#40;보고서 작성기 및 SSRS&#41;](../report-design/gauges-report-builder-and-ssrs.md)  
  
    -   **데이터 및 레이아웃을 사용자 지정합니다.** 보고서 레이아웃을 디자인합니다. 보고서 정의에는 보고서 원문, 데이터 원본, 데이터 세트, 데이터 영역, 입력란, 선 및 이미지가 있습니다. 사각형은 레이아웃의 컨테이너 및 시각적 요소로 사용됩니다. 데이터에 대해 필터, 그룹, 정렬, 서식 및 표시를 제어할 식을 작성하여 각 데이터 영역을 사용자 지정합니다. 보고서 이름과 위치를 비롯하여 수십 개 또는 수백 개의 보고서를 관리하는 데 유용한 기타 식별 정보를 추가합니다. 시각적 요소 및 컨테이너를 추가하여 페이지의 레이아웃 요소를 구성합니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
        -   [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
        -   [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
        -   [식&#40;보고서 작성기 및 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
        -   [보고서 항목 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../report-design/formatting-report-items-report-builder-and-ssrs.md)  
  
        -   [이미지, 입력란, 사각형 및 선&#40;보고서 작성기 및 SSRS&#41;](../report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
        -   [페이지 레이아웃 및 렌더링&#40;보고서 작성기 및 SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
    -   **대화형 기능을 구성합니다.** 보고서 구독자를 위한 대화형 기능을 추가합니다. 예를 들어 쿼리를 볼 수 있는 정렬 단추나 토글 항목을 추가합니다. 자세한 내용은 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)를 참조하세요.  
  
    -   **디자인을 검토하고 반복합니다.** 보고서를 미리 봅니다. 예비 버전을 게시하여 보고서 구독자의 의견을 수집합니다. 디자인을 반복합니다.  
  
-   **보고 솔루션을 검토합니다.** 보고서 집합이 올바르게 상호 작용하는지 확인합니다.  
  
-   **다시 사용할 수 있는 구성 요소를 검토합니다.**  데이터 원본 또는 데이터 세트 쿼리를 다시 사용하도록 공유할 수 있는지 확인합니다. 다시 사용할 수 있다면 보고서 서버 또는 SharePoint 사이트에서 공유 데이터 원본 및 공유 데이터 세트를 만듭니다. 데이터 영역이 보고서 파트로 다시 사용하는 데 적절한지 확인합니다. 자세한 내용은 [보고서 디자이너의 보고서 파트&#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md)를 참조하세요.  
  
## <a name="preview-reports"></a>보고서 미리 보기  
 각 보고서 제작 도구는 보고서 미리 보기를 지원합니다. 자세한 내용은 msdn.microsoft.com의 [보고서 작성기 설명서](https://go.microsoft.com/fwlink/?LinkId=154494)에서 [미리 보기](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_Preview), [보고서 작성기&#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) 및 [보고서 작성기에서 보고서 미리 보기](../report-builder/previewing-reports-in-report-builder.md)를 참조하세요.  
  
## <a name="save-or-publish-reports"></a>보고서 저장 또는 게시  
 각 제작 도구는 보고서를 로컬로 저장하거나 보고서 서버 또는 SharePoint 사이트에 보고서를 게시하는 기능을 지원합니다. 자세한 내용은 msdn.microsoft.com의 [보고서 작성기 설명서](https://go.microsoft.com/fwlink/?LinkId=154494)에서 [저장 및 배포](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_SaveandDeploy), [보고서 작성기&#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) 및 [보고서 저장&#40;보고서 작성기&#41;](../report-builder/saving-reports-report-builder.md)을 참조하세요.  
  
## <a name="view-reports"></a>보고서 보기  
 로컬로 저장되거나 보고서 서버에 게시된 보고서를 미리 볼 수 있을 뿐만 아니라 보고서 구독자에게 다양한 보기 환경을 제공할 수 있습니다. 보고서를 보는 방법은 다음과 같습니다.  
  
-   **브라우저.**  보고서 서버 웹 서비스 또는 SharePoint 사이트를 사용하여 게시된 보고서를 볼 수 있습니다. SharePoint 사이트에서는 게시된 보고서를 표시할 웹 파트를 구성할 수도 있습니다. 자세한 내용은 [Reporting Services 및 파워 뷰 브라우저 지원 계획&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md), [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md) 및 [URL 액세스&#40;SSRS&#41;](../url-access-ssrs.md)를 참조하세요.  
  
-   **배달.**  공유 파일 폴더로 또는 보고서 구독자에게 전자 메일로 보고서를 배달하도록 구독을 구성할 수 있습니다.  자세한 내용은 [구독 및 배달&#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)을 참조하세요.  
  
-   **내보내기.**  보고서 구독자는 보고서 뷰어 도구 모음에서 보고서를 다른 파일 형식으로 내보낼 수 있습니다. 내보내기 파일 형식은 보고서 서버 관리자가 구성할 수 있습니다. 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **인쇄.**  보고서 구독자는 보고서가 표시된 방식에 따라 보고서 또는 보고서 페이지를 인쇄할 수 있습니다. 자세한 내용은 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **웹 또는 Windows Form 응용 프로그램.**  Visual Studio를 사용하여 보고서 뷰어 컨트롤을 호스팅하는 ASP.NET AJAX 애플리케이션 또는 Windows Form 애플리케이션을 개발할 수 있습니다. 이 컨트롤은 보고서 서버에 게시된 보고서를 가리킬 수 있습니다. 자세한 내용은 [Microsoft 보고서](https://go.microsoft.com/fwlink/?LinkID=205399)를 참조하세요.  
  
## <a name="manage-reports"></a>보고서 관리  
 게시된 보고서를 관리하는 방법은 다음과 같습니다.  
  
-   **데이터 원본** .  공유 및 포함된 데이터 원본은 보고서 정의와 독립적으로 관리됩니다.  
  
-   **데이터 집합.**  공유 데이터 세트는 보고서 정의와 독립적으로 관리됩니다.  
  
-   **매개 변수.**  매개 변수는 보고서 정의와 독립적으로 관리됩니다. 보고서 서버에서 매개 변수를 변경한 후에는 보고서 제작 클라이언트에서 서버에 적용된 변경 내용 위에 게시할 수 없습니다.  
  
-   **리소스.**  ESRI 셰이프 파일의 이미지 및 공간 데이터는 보고서 정의와 독립적으로 게시하고 관리할 수 있는 리소스입니다.  
  
-   **보고서 캐시.**  대형 보고서가 사용률이 낮은 시간에 실행되도록 예약하여 중요한 업무 시간 동안 보고서 서버 처리로 인한 영향을 줄일 수 있습니다.  
  
-   **스냅숏**  동일한 데이터 집합으로 작업해야 하는 여러 사용자에게 일관된 결과를 제공하려는 경우 보고서 스냅숏을 사용합니다. 일시적인 데이터로 요청 시 실행 보고서를 사용하면 매 시간마다 다른 결과를 생성할 수 있습니다. 하지만 보고서 스냅숏을 사용하면 같은 시점의 데이터가 들어 있는 다른 보고서나 분석 도구와 비교하여 유효한 결과를 생성할 수 있습니다.  
  
-   **보고서 기록.** 일련의 보고서 스냅숏을 만들어서 시간에 따른 데이터 변경 내역을 보여 주는 보고서 기록을 작성할 수 있습니다.  
  
 성능에 대한 자세한 내용은 [성능, 스냅숏, 캐시&#40;Reporting Services&#41;](../report-server/performance-snapshots-caching-reporting-services.md)을 참조하세요.  
  
##  <a name="bkmk_SecureReportsSummary"></a> 보고서 보안  
 보고서 보안을 유지하려면  
  
-   보고서 서버 관리자로부터 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 설치에 사용된 권한 부여 및 인증 시스템을 확인합니다. 기본적으로 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 에서는 Windows 인증, 통합 보안 및 역할 할당을 사용하여 게시된 보고서에 대한 액세스를 제어하도록 도와줍니다. 자세한 내용은 [역할 및 권한&#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md) 및 [Reporting Services 보안 및 보호](../security/reporting-services-security-and-protection.md)를 참조하세요.  
  
## <a name="create-notifications-based-on-report-data"></a>보고서 데이터 기반 알림 만들기  
 SharePoint 사이트에 게시된 보고서에 대한 데이터 경고를 만들 수 있습니다. 데이터 경고는 보고서 내 데이터 영역의 데이터 피드를 기반으로 합니다. 기본적으로 데이터 영역의 이름은 자동으로 지정됩니다. 보고서 작성자는 비즈니스 용도에 따라 데이터 영역의 이름을 지정하여 보고서에 데이터 경고를 보다 쉽게 만들 수 있습니다. 데이터 경고를 만들면 데이터가 지정한 조건을 충족하는 경우 전자 메일 알림이 제공됩니다. 자세한 내용은 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](../report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md), [데이터 경고 디자이너에서 데이터 경고 만들기](../create-a-data-alert-in-data-alert-designer.md) 및 [Reporting Services 데이터 경고](../reporting-services-data-alerts.md)를 참조하세요.  
  
## <a name="upgrade-reports"></a>Upgrade Reports  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서는 여러 버전의 보고서 정의, 보고서 서버 및 SharePoint 사이트를 지원합니다. 보고서를 업그레이드합니다.  
  
-   보고서 서버 설치를 업그레이드합니다. 보고서 서버에 저장된 컴파일된 보고서는 처음 사용할 때 자동으로 업그레이드됩니다. 그러나 보고서 정의(.rdl)는 변경되지 않습니다. 자세한 내용은 [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.  
  
-   보고서 제작 환경에서 보고서를 엽니다. 이 경우에는 대부분 보고서 정의가 업그레이드됩니다. 자세한 내용은 [보고서 업그레이드](../install-windows/upgrade-reports.md) 및 [SQL Server Data Tools의 배포 및 버전 지원&#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)를 참조하세요.  
  
## <a name="troubleshoot-reports"></a>보고서 문제 해결  
 보고서 문제를 해결하려면  
  
-   **문제가 발생한 위치를 확인합니다.** [보고서 단계](#bkmk_StagesSummary)의 정보를 검토합니다.  
  
-   **추가 정보를 찾을 수 있는 위치를 확인합니다.** 예를 들어 식이 포함된 보고서 디자인의 경우 보고서 디자이너 도구가 보고서 작성기 도구보다 식 평가 문제에 대한 보다 자세한 정보를 제공합니다. 보고서 처리 오류의 경우 로그 파일에 자세한 정보가 포함됩니다.  
  
## <a name="tasks"></a>태스크  
 단계별 항목에 대한 링크는 이 항목의 이전 섹션에 언급된 기능 관련 문서의 태스크 섹션을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 도구](../tools/reporting-services-tools.md)   
 [확장 프로그램&#40;SSRS&#41;](../extensions-ssrs.md)   
 [Reporting Services 보고서 서버](../reporting-services-report-server.md)  
  
  
