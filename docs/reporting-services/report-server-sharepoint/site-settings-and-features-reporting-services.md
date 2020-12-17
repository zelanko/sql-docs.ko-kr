---
title: Reporting Services 사이트 설정 및 사이트 기능(SharePoint 모드) | Microsoft Docs
description: Reporting Services SharePoint 모드의 SharePoint 사이트 설정 페이지에는 사용자가 관리할 수 있는 사이트 수준 사용자 지정 기능 및 사이트 기능이 있습니다.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: feabf5c1a0847983af4a10dea5d4c15a5f51199d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461434"
---
# <a name="reporting-services-site-settings-and-site-features-sharepoint-mode"></a>Reporting Services 사이트 설정 및 사이트 기능(SharePoint 모드)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services SharePoint 모드에는 SharePoint 사이트 설정 페이지에서 관리할 수 있는 몇 가지 사이트 수준 사용자 지정 기능과 사이트 기능이 있습니다. 설정은 사이트 전체에 해당하며 모든 Reporting Services 서비스 애플리케이션에 영향을 줍니다. 이 페이지를 보려면 내용 관리자 및 시스템 관리자 권한이 있어야 합니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

|사이트 설정|Description|  
|------------------|-----------------|  
|Reporting Services 사이트 설정|이 항목에 설명된 사이트 전체 설정입니다.|  
|데이터 경고 관리|데이터 경고 기능의 관리입니다.|  
|보고서 서버 파일 동기화|기본적으로 비활성화되어 있는 사이트 수준 기능입니다.<br /><br /> 문서 라이브러리 안에서 직접 파일이 추가되거나 업데이트되면 보고서 서버 파일(.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx)을 SharePoint 문서 라이브러리에서 보고서 서버로 동기화합니다.<br /><br /> 자세한 내용은 [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)(SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능을 활성화)을 참조하세요.|  
  
## <a name="open-the-reporting-services-site-settings-page"></a>Reporting Services 사이트 설정 페이지 열기
  
1.  SharePoint 사이트의 **사이트 동작** 메뉴에서 **사이트 설정** 을 선택합니다.  
  
2.  **Reporting Services** 섹션에서 **Reporting Services 사이트 설정** 을 선택합니다.  
  
## <a name="options-for-reporting-services-site-settings"></a>Reporting Services 사이트 설정을 위한 옵션
  
|옵션|설명|  
|------------|-----------------|  
|**RSClientPrint ActiveX 컨트롤 다운로드 설정**|이 컨트롤은 특정 페이지와 범위, 페이지 여백 및 방향을 지정하는 페이지 선택 기능, 인쇄 미리 보기 기능을 비롯하여 다른 인쇄 대화 상자에 공통적인 기능을 지원하는 사용자 지정 인쇄 대화 상자를 표시합니다. 컨트롤에 대한 자세한 내용은 [Using the RSClientPrint Control in Custom Applications](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)을 참조하십시오.|  
|**로컬 모드에서 원격 오류를 사용하도록 설정합니다.**|로컬 모드에서 실행 중일 때 원격 컴퓨터에서 자세한 오류 메시지를 표시하거나 숨깁니다. 다음과 유사한 오류 메시지가 나타날 경우 원격 오류를 사용하면 도움이 될 수 있습니다.<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**보고서에 내게 필요한 옵션 메타데이터 사용**|보고서의 HTML 출력에 내게 필요한 옵션 메타데이터 설정|  
|**보고서에 정확히 맞춘 데이터 시각화 크기 조정 사용**|데이터 시각화 맞춤 동작이 테이블릭스 안에서 정확히 맞도록 구성합니다. 여기에는 차트, 계기 및 지도가 포함됩니다. 사용하지 않도록 설정한 경우 데이터 시각화가 대략적으로 맞도록 조정되며 이로 인해 공백이 생길 수 있습니다. 이 설정은 보고서 뷰어 웹 파트의 렌더링에만 적용됩니다. 서버 쪽 렌더링에 대해 이 동작을 관리하려면 **rsreportserver.config** 파일을 수정해야 합니다. 자세한 내용은<br /><br /> [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)<br /><br /> [Customize Rendering Extension Parameters in RSReportServer.Config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)입니다.<br /><br /> [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md)입니다.<br /><br /> 정확한 크기를 결정하기 위한 처리가 대략적인 맞춤보다 오래 걸릴 수 있기 때문에 정확한 수치를 설정하면 성능에 영향을 줄 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목

 [Reporting Services SharePoint 서비스 애플리케이션 관리](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
