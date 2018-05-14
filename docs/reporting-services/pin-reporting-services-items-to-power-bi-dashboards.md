---
title: Power BI 대시보드에 Reporting Services 항목 고정 | Microsoft Docs
ms.custom: ''
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- pbi
- dashboard
- pin
- powerbi
- power bi integration
ms.assetid: 1d96c3f7-2fd4-40f7-8d1c-14a7f54cdb15
caps.latest.revision: 23
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7e3e738ef82486f80b9f81ae8e1d1218397980d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="pin-reporting-services-items-to-power-bi-dashboards"></a>Power BI 대시보드에 Reporting Services 항목 고정
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 을 통해 사용자는 보고서 뷰어 도구 모음의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 항목을 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드에 새 타일로 고정합니다.   고정하려면 먼저 관리자가 보고서 서버를 Azure Active Directory 및 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]과 통합해야 합니다.  
  
 ![rs_powerbi_icon](../reporting-services/media/ssrs-powerbi-icon.png "rs_powerbi_icon")  
  
 [!INCLUDE[applies](../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기본 모드
  
##  <a name="bkmk_requirements_to_pin"></a> 고정하기 위한 요구 사항  
  
-   보고서 서버는 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 통합에 대해 구성됩니다. 자세한 내용은 [Power BI 보고서 서버 통합&#40;구성 관리자&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)과 통합해야 합니다. 보고서 서버가 구성되지 않은 경우 도구 모음에 **Power BI 대시보드에 고정** 단추가 표시되지 않습니다.  
  
     ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 뷰어에서 고정합니다(예: `http://myserver/Reports`).  [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)], [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 보고서 디자이너 또는 보고서 서버 url에서는 고정할 수 없습니다.  예를 들면 `http://myserver/ReportServer`과 같습니다.  
  
-   브라우저에서 보고서 서버 사이트의 팝업을 허용하도록 구성해야 합니다.  
  
-   고정된 항목을 새로 고치도록 하려면 저장된 자격 증명에 대해 보고서를 구성해야 합니다.  항목을 고정하면 대시보드에 대한 항목의 데이터 새로 고침을 관리하기 위해 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구독이 자동으로 생성됩니다.  보고서가 저장된 자격 증명을 사용하지 않는 경우 구독이 실행될 때 **내 구독** 페이지에 다음과 같은 오류 메시지가 표시됩니다.  
  
        PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credential.
 
    [Reporting Services 데이터 원본에 자격 증명 저장](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)에서 "보고서별 데이터 원본에 대한 저장된 자격 증명 구성(기본 모드)" 섹션을 참조하세요.  
  
##  <a name="bkmk_supported_items"></a> 고정할 수 있는 항목  
 다음과 같은 보고서 항목을 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드에 고정할 수 있습니다.  데이터 영역 내에 중첩된 항목을 고정할 수 없습니다. 예를 들어 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 테이블 또는 목록 내에 중첩된 항목을 고정할 수 없습니다.  
  
-   차트  
  
-   계기 패널(gauge panel)  
  
-   맵  
  
-   이미지  
  
-   항목이 보고서 본문에 있어야 합니다.  페이지 머리글 또는 페이지 바닥글에 있는 항목을 고정할 수 없습니다.  
  
-   최상위 수준 사각형 내에 있는 개별 항목을 고정할 수 있지만 해당 항목을 모두 단일 그룹으로 고정할 수 없습니다.  
  
##  <a name="bkmk_to_pin"></a> 보고서 항목을 고정하려면  
  
1. [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)](으)로 로그인되었는지 확인합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]에서 **내 설정** 메뉴 항목을 선택하고 로그인합니다. 자세한 내용은  [Power BI 통합을 위한 내 설정&#40;웹 포털&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5) 을 참조하세요.

    ![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
2. 보고서가 포함된 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 폴더로 이동한 다음 보고서를 봅니다.  
  
3. 보고서가 표시된 상태로 도구 모음에서 **Power BI에 고정** 단추를 선택합니다.  아직 로그인하지 않은 경우 로그인하라는 메시지가 표시됩니다.  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 단추가 표시되지 않는 경우 보고서 서버가 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]에 통합되지 않은 것입니다. 자세한 내용은 [Power BI 보고서 서버 통합&#40;구성 관리자&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)과 통합해야 합니다.  
  
    ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
4. [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]에 고정할 보고서 항목을 선택합니다. 한 번에 한 항목만 고정할 수 있습니다.  보고서 뷰어가 보고서의 음영 처리된 뷰를 표시하며 고정할 수 있는 보고서 항목은 강조 표시되는 반면에 고정할 수 없는 항목은 어둡게 음영 처리되어 표시됩니다.  
  
    **(1)** 고정할 대시보드가 있는 그룹을 선택하고, **(2)** 항목을 고정할 대시보드를 선택하고 **(3)** 대시보드에서 타일을 업데이트할 빈도를 선택합니다.   ![참고](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "참고") 새로 고침은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구독에 의해 관리되며 항목이 고정된 후 구독을 편집하고 다른 새로 고침 일정을 구성할 수 있습니다.  
  
    ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png)  
  
5. **고정**을 선택합니다.  
  
    **고정 성공** 대화 상자에서 **Power BI에서 확인** 링크를 선택하여 대시보드로 이동하고 방금 고정한 항목을 확인할 수 있습니다.  
  
6. 보고서를 기본 보기로 되돌리려면 **닫기** 를 선택합니다.  
  
##  <a name="bkmk_in_the_dashboard"></a> 대시보드에서

보고서 항목이 대시보드에 고정된 후 타일은 다른 대시보드 타일과 같으며 타일이 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 나왔다는 시각적인 표시는 없습니다. 다음 목록은 보고서 항목에서 타일 속성이 채워지는 방법을 요약합니다.  
  
[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드에서 고정된 보고서 항목은 다른 타일처럼 동작합니다.

**(1)** 타일을 다른 대시보드에 고정할 수 있습니다.

**(2)** **타일 세부 정보** 에서 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 타일이 타일의 기본 제목에 사용되는지 확인할 수 있습니다.

**(3)** 타일 부제목은 타일이 고정된 날짜 및 시간 또는 데이터가 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 새로 고쳐진 날짜를 기반으로 지정됩니다. 새로 고침 일정은 보고서 항목을 고정할 때 자동으로 생성된 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구독에 의해 관리됩니다.

**(4)** 타일 자체를 선택하면 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 은 **(3) 사용자 지정 링크** 를 사용하여 등록된 보고서 서버의 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 페이지로 이동합니다. 링크는 항목이 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 고정될 때 설정되었습니다. 보고서 서버에 인터넷 연결이 없는 경우 브라우저에 오류가 표시됩니다.  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="bkmk-troubleshoot"></a> 문제 해결  
  
-   **보고서 뷰어 도구 모음에 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 단추 없음:** 보고서 서버가 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]에 통합되지 않았음을 나타냅니다. 자세한 내용은 [Power BI 보고서 서버 통합&#40;구성 관리자&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)과 통합해야 합니다.  
  
- **고정할 수 없음**: 항목의 고정을 시도할 때 다음과 같은 오류 메시지가 표시됩니다. [고정할 수 있는 항목](#bkmk_supported_items)섹션을 참조하세요.  
  
      Cannot Pin: There are no report items on this page that you can pin to [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
-   **고정된 항목이 부실 데이터** 를 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드에 표시하며 일정 기간 동안 업데이트되었습니다.  사용자 자격 증명 토큰이 만료되었으며 다시 로그인해야 합니다.  Azure 및 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 에 대한 사용자 자격 증명 등록은 90일 동안 유효합니다. [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]에서 **내 설정**을 클릭합니다. 자세한 내용은 [Power BI 통합을 위한 내 설정&#40;웹 포털&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5)과 통합해야 합니다.  
  
-   **고정된 항목이 부실 데이터** 를 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드에 표시하며 한 번도 새로 고쳐지지 않았습니다.  문제는 보고서가 저장된 자격 증명을 사용하도록 구성되지 않은 것입니다. 보고서 항목 고정 작업은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구독을 만들어 타일의 새로 고침 일정을 관리하므로 보고서가 저장된 자격 증명을 사용했어야 합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구독에는 저장된 자격 증명이 필요합니다. **내 구독** 페이지를 검토하면 다음과 유사한 오류 메시지를 확인할 수 있습니다.  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified. (rsInvalidDataSourceCredentialSetting)
  
-   **만료된 Power BI 자격 증명:**  항목의 고정을 시도하는데 다음과 같은 오류 메시지가 표시됩니다. [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]에서 **내 설정** 을 클릭하고 내 설정 페이지에서 **로그인**을 클릭합니다. 자세한 내용은  [Power BI 통합을 위한 내 설정&#40;웹 포털&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5) 을 참조하세요.  
  
        Cannot Pin : Unexpected Server Error: Missing, invalid or expired Power BI credentials.  
  
-   **고정할 수 없음**: 읽기 전용 상태에 있는 대시보드에 항목의 고정을 시도하면 다음과 유사한 오류 메시지가 표시됩니다.  
  
        Server Error : The item 'Dashboard deleted 015cf022-8e2f-462e-88e5-75ab0a04c4d0' cannot be found. (rsItemNotFound)  
  
##  <a name="bkmk_subscription_management"></a> 구독 관리  
 문제 해결 섹션에서 설명한 구독 관련 문제 외에도 다음 정보는 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 관련 구독을 유지 관리하는 데 도움이 됩니다.
  
-   **항목 이름이 변경됨:** 고정된 보고서 항목이 이름 변경되거나 삭제된 경우 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 타일이 더 이상 업데이트되지 않으며 다음과 유사한 오류 메시지가 표시됩니다.  항목 이름을 원래 이름으로 다시 바꾸면 구독이 다시 작동하기 시작하며 구독 일정에서 타일이 새로 고쳐집니다.  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image1, error: Error: Report item 'Image1' cannot be found.  
  
     또한 구독 속성을 편집하고 **보고서 시각적 이름** 을 적절한 보고서 항목 이름으로 변경할 수 있습니다. ![power bi 새로 고침에 사용되는 시각적 개체 변경](../reporting-services/media/ssrs-powerbi-subscription-visual.png "power bi 새로 고침에 사용되는 시각적 개체 변경")  
  
-   **타일을 삭제**합니다. [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]에서 타일을 삭제했는데 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 및 **내 구독**페이지에서 연결된 구독이 삭제되지 않은 경우 다음과 유사한 오류가 표시됩니다. 구독만 삭제할 수 있습니다.  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The item 'Tile deleted af7131d9-5eaf-480f-ba45-943a07d19c9f' cannot be found.  

## <a name="video"></a>비디오

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>참고 항목  
 [Power BI 보고서 서버 통합&#40;구성 관리자&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Power BI 통합을 위한 내 설정&#40;웹 포털&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5)  
 [Power BI의 대시보드](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

