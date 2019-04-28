---
title: PowerPivot을 SharePoint 2013으로 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: f698ceb1-d53e-4717-a3a0-225b346760d0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 64f3d3474ac812f07645cd3064c270ba10ad76c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729925"
---
# <a name="migrate-powerpivot-to-sharepoint-2013"></a>Migrate PowerPivot to SharePoint 2013
  
  
 SharePoint 2013에서는 전체 업그레이드를 지원하지 않습니다. 그러나 **데이터베이스 연결 업그레이드 절차는 지원**됩니다. 동작은 전체 업그레이드 및 데이터베이스 연결 업그레이드의 두 가지 기본 업그레이드 방법 중 고객이 선택할 수 있는 SharePoint 2010으로 업그레이드와 다릅니다.  
  
 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 설치가 SharePoint 2010에 통합되어 있는 경우에는 SharePoint 서버를 전체 업그레이드할 수 없습니다. 그러나 SharePoint 2010 팜에서 콘텐츠 데이터베이스 및 서비스 애플리케이션 데이터베이스를 SharePoint 2013 팜으로 마이그레이션할 수 있습니다. 이 항목은 데이터베이스 연결 업그레이드를 완료하고 PowerPivot 관련 마이그레이션을 완료하는 데 필요한 단계에 대한 개요입니다.  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013  
  
### <a name="migration-overview"></a>마이그레이션 개요  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|SharePoint 2013 팜 준비|데이터베이스 백업, 복사 및 복원|콘텐츠 데이터베이스 탑재|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 일정 마이그레이션|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|SharePoint 중앙 관리<br /><br /> Windows PowerShell|SharePoint 애플리케이션 페이지<br /><br /> Windows PowerShell|  
  
 **항목 내용**  
  
-   [1) SharePoint 2013 팜 준비](#bkmk_prepare_sharepoint2013)  
  
-   [2) 데이터베이스 백업, 복사 및 복원](#bkmk_backup_restore)  
  
-   [3) 웹 응용 프로그램 준비 및 콘텐츠 데이터베이스 탑재](#bkmk_prepare_mount_databases)  
  
-   [4) PowerPivot 일정 업그레이드](#bkmk_upgrade_powerpivot_schedules)  
  
-   [추가 리소스](#bkmk_additional_resources)  
  
##  <a name="bkmk_prepare_sharepoint2013"></a> 1) SharePoint 2013 팜 준비  
  
1.  > [!TIP]  
    >  기존 웹 애플리케이션을 구성한 인증 방법을 검토하세요. SharePoint 2013 웹 애플리케이션은 클레임 기반 인증을 기본적으로 사용합니다. 클래식 모드 인증에 대해 구성된 SharePoint 2010 웹 애플리케이션을 사용하려면 SharePoint 2010에서 SharePoint 2013으로 데이터베이스를 마이그레이션하는 추가 단계가 필요합니다. 클래식 모드 인증에 대해 웹 애플리케이션이 구성된 경우 SharePoint 2013 설명서를 검토합니다.  
  
2.  새로 SharePoint Server 2013 팜을 설치합니다.  
  
3.  SharePoint 모드에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버 인스턴스를 설치합니다. 자세한 내용은 [PowerPivot for SharePoint 2013 Installation](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)을 참조하세요.  
  
4.  SharePoint 팜의 각 서버에서 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 설치 패키지 **spPowerPivot.msi** 를 실행합니다. 자세한 내용은 [를 설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot 제거 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)합니다.  
  
5.  SharePoint 2013 중앙 관리에서 이전 단계에서 만든 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 모드 서버를 사용하도록 Excel Services 서비스 애플리케이션을 구성합니다. 자세한 내용은의 "Basic Analysis Services SharePoint 통합 구성" 섹션을 참조 하세요 [SharePoint 용 PowerPivot 2013 설치](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)합니다.  
  
##  <a name="bkmk_backup_restore"></a> 2) 데이터베이스 백업, 복사 및 복원  
 "SharePoint 데이터베이스 연결 업그레이드" 프로세스는 백업 하는 단계 시퀀스로, 복사 및 복원을 PowerPivot 관련 콘텐츠 및 서비스 응용 프로그램 데이터베이스를 SharePoint 2013 팜  
  
1.  **데이터베이스를 읽기 전용으로 설정 합니다.** [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다. **옵션** 페이지에서 **데이터베이스 읽기 전용** 속성을 **True**로 설정합니다.  
  
2.  **뒷받침하다:** 각 콘텐츠 데이터베이스 및 SharePoint 2013 팜에 마이그레이션할 하려는 서비스 응용 프로그램 데이터베이스를 백업 합니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 클릭한 다음 **백업**을 클릭합니다.  
  
3.  원하는 대상 서버에 데이터베이스 백업 파일(.bak)을 복사합니다.  
  
4.  **복원:** 대상 데이터베이스를 복원 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]합니다. 이 단계는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용하여 수행할 수 있습니다.  
  
5.  **데이터베이스를 읽기 / 쓰기로 설정:** 설정 합니다 **데이터베이스가 읽기 전용** 하 **False**합니다.  
  
##  <a name="bkmk_prepare_mount_databases"></a> 3) 웹 응용 프로그램 준비 및 콘텐츠 데이터베이스 탑재  
 에 대 한 자세한 설명은 다음 절차를 참조 하세요 [SharePoint 2010에서 SharePoint 2013으로 데이터베이스 업그레이드](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690)합니다.  
  
1.  **데이터베이스를 오프라인 상태로 만들기:**  
  
     각 SharePoint 2013 콘텐츠 데이터베이스를 오프라인 상태로 만들려면 SharePoint 중앙 관리를 사용합니다. 콘텐츠 데이터베이스는 복사한 데이터베이스로 대체됩니다. 환경에 가장 적합한 순서를 고려하세요. 각 데이터베이스를 오프라인 상태로 만들고 다음 콘텐츠 데이터베이스를 오프라인 상태로 만들기 전에 관련 교체 데이터베이스를 탑재합니다. 다른 옵션은 모든 콘텐츠 데이터베이스를 그룹으로 오프라인 상태로 만드는 것입니다.  
  
    1.  SharePoint 중앙 관리에서 **애플리케이션 관리**를 클릭합니다.  
  
    2.  **콘텐츠 데이터베이스 관리**를 클릭합니다.  
  
    3.  데이터베이스 이름을 클릭합니다.  
  
    4.  **콘텐츠 데이터베이스 설정 관리**에서 **데이터베이스 상태** 를 **오프라인**으로 설정합니다.  
  
    5.  **콘텐츠 데이터베이스 제거**를 선택합니다. 콘텐츠 데이터베이스에 저장된 사이트에 더 이상 액세스할 수 없다는 경고가 표시됩니다.  
  
-   **콘텐츠 데이터베이스 탑재:**  
  
     SharePoint 2013 관리 셸에서 PowerShell cmdlet을 사용하여 마이그레이션된 콘텐츠 데이터베이스를 탑재합니다. 서비스 애플리케이션 데이터베이스는 탑재하지 않아도 되며, 콘텐츠 데이터베이스만 탑재 ![PowerShell 관련 콘텐츠](../../../reporting-services/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     자세한 내용은 [연결 또는 콘텐츠 데이터베이스 (SharePoint Server 2010)을 분리](https://technet.microsoft.com/library/ff628582.aspx) (https://technet.microsoft.com/library/ff628582.aspx)합니다.  
  
     **단계가 완료 된 상태:**  탑재 작업이 완료 되 면 사용자가 이전 콘텐츠 데이터베이스에 있는 파일을 볼 수 있습니다. 따라서 사용자는 문서 라이브러리에서 통합 문서를 보고 열 수 있습니다.  
  
    > [!TIP]  
    >  마이그레이션 프로세스의 이 시점에서 마이그레이션된 통합 문서에 대한 새 일정을 만들 수 있습니다. 하지만 일정은 새 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 서비스 애플리케이션 데이터베이스에서 만들어지고 기존 SharePoint 팜에서 복사한 데이터베이스에는 만들어지지 않습니다. 따라서 새 일정에는 기존 일정이 포함되지 않습니다. 다음 단계를 완료하여 기존 데이터베이스를 사용하고 기존 일정을 마이그레이션한 후에는 새 일정을 사용할 수 있습니다.  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>데이터베이스 탑재 시 발생하는 문제 해결  
 이 섹션에서는 데이터베이스를 탑재할 때 발생할 수 있는 문제를 요약합니다.  
  
1.  **인증 오류:** 인증에 관련 된 오류를 표시 되 면 소스 웹 응용 프로그램을 사용 하는 인증 모드를 검토 합니다. 이 오류는 SharePoint 2013 웹 애플리케이션과 SharePoint 2010 웹 애플리케이션 간의 인증 불일치로 인해 발생할 수 있습니다. 자세한 내용은 [1) SharePoint 2013 팜 준비](#bkmk_prepare_sharepoint2013) 을(를) 참조하십시오.  
  
2.  **PowerPivot.Files 누락:** PowerPivot.dll 누락 관련 오류가 표시 되는 **spPowerPivot.msi** 설치 되지 않은 또는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] PowerPivot을 구성 하려면 구성 도구 사용 되지 않았습니다.  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a> 4) PowerPivot 일정 업그레이드  
 이 섹션에서는 PowerPivot 일정 마이그레이션에 대한 세부 정보와 옵션을 설명합니다. 일정 마이그레이션 프로세스는 두 단계로 구성됩니다. 먼저 마이그레이션된 서비스 애플리케이션 데이터베이스를 사용하도록 PowerPivot 서비스 애플리케이션을 구성합니다. 그런 다음, 일정 마이그레이션에 대한 두 가지 옵션 중 하나를 선택합니다.  
  
 **마이그레이션된 서비스 응용 프로그램 데이터베이스를 사용하도록 서비스 응용 프로그램을 구성합니다.**  
  
 SharePoint 중앙 관리에서 복사한 기존 서비스 애플리케이션 데이터베이스를 사용하도록 PowerPivot 서비스 애플리케이션을 구성합니다. PowerPivot 서비스는 서비스 애플리케이션 데이터베이스를 새 스키마로 업그레이드합니다.  
  
1.  SharePoint 중앙 관리에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  PowerPivot 서비스 응용 프로그램, 예를 들어 "기본 PowerPivot 서비스 응용 프로그램"을 클릭 서비스 응용 프로그램의 이름을 찾아서 클릭 **속성** SharePoint 리본에서.  
  
3.  데이터베이스 서버 이름-인스턴스 및 데이터베이스 이름을 업데이트합니다. 백업, 복사 및 복원한 데이터베이스에 대한 올바른 이름입니다. **확인**을 클릭하면 서비스 응용 프로그램 데이터베이스가 업그레이드됩니다. 오류는 ULS 로그에 있습니다.  
  
 **PowerPivot 일정 업그레이드**  
  
 새로 고침 일정을 마이그레이션하도록 PowerPivot 서비스 애플리케이션을 구성합니다.  
  
-   **일정 옵션 1 마이그레이션: SharePoint 팜 관리자**  
  
    1.  SharePoint 2013 관리 실행에서 합니다 `Set-PowerPivotServiceApplication` cmdlet을 사용 합니다 `-StartMigratingRefreshSchedules` 스위치를 필요 시 일정 마이그레이션에 대 한 자동 ![PowerShell 관련 콘텐츠](../../../reporting-services/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠"). 다음 Windows PowerShell 스크립트는 PowerPivot 서비스 애플리케이션이 한 개만 있다고 가정합니다.  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         Windows PowerShell 스크립트를 실행하면 일정이 활성화되고 일정이 적절한 다음 시간에 실행됩니다. 하지만 일정 새로 고침 페이지 상태 1이 사용되지 않습니다. 일정이 처음 실행되면 일정이 마이그레이션되며 일정 새로 고침 페이지에서 **사용**  이 true가 됩니다.  
  
    2.  StartMigratingRefreshSchedules 속성의 현재 값을 확인하려면 다음 PowerShell 스크립트를 실행합니다. 스크립트는 모든 PowerPivot 서비스 애플리케이션 개체를 반복하며 이름 및 속성 값을 표시합니다.  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **일정 옵션 2 마이그레이션: 사용자가 각 통합 문서 업데이트**  
  
    1.  일정을 마이그레이션하는 다른 옵션은 각 통합 문서에 대한 일정 새로 고침을 사용하는 것입니다. 통합 문서가 있는 문서 라이브러리로 이동합니다.  
  
    2.  상황에 맞는 메뉴를 열고 **PowerPivot 데이터 새로 고침 관리**를 클릭합니다.  
  
    3.  **새로 고침 일정** 섹션에서 **사용**을 클릭합니다.  
  
    4.  **가능한 빨리 새로 고치세요.** 를 선택할 수 있습니다. 이 옵션은 확인을 클릭하면 바로 새로 고침 인스턴스 한 개를 큐에 추가합니다. 정기적인 새로 고침 일정도 적절한 시간에 트리거됩니다.  
  
    5.  **확인**을 클릭합니다. 새로 고침 기록은 이제 새로 고침 페이지에서 볼 수 있고 일정이 정상 시간에 실행됩니다.  
  
 **SQL Server 2008 R2 PowerPivot 통합 문서**  
  
-   SQL Server 2008 R2 PowerPivot 통합 문서는 SQL Server 2012 SP1 SharePoint 2013용 PowerPivot에서 사용할 경우 자동으로 업그레이드되지 않습니다. 2008 R2 통합 문서가 포함된 콘텐츠 데이터베이스를 마이그레이션한 후 통합 문서를 사용할 수 있지만 일정이 업그레이드되지 않습니다.  
  
-   자세한 내용은 [통합 문서 업그레이드 및 예약된 데이터 새로 고침&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)을 검토하세요.  
  
##  <a name="bkmk_additional_resources"></a> 추가 리소스  
  
> [!NOTE]  
>  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 및 SharePoint 데이터베이스 연결 업그레이드에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [통합 문서 업그레이드 및 예약된 데이터 새로 고침&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
-   [SharePoint 2013으로 업그레이드 프로세스 개요](https://go.microsoft.com/fwlink/p/?LinkId=256688) (https://go.microsoft.com/fwlink/p/?LinkId=256688)합니다.  
  
-   [SharePoint 2013으로 업그레이드 하기 전에 정리 준비](https://go.microsoft.com/fwlink/p/?LinkId=256689) (https://go.microsoft.com/fwlink/p/?LinkId=256689)합니다.  
  
-   [SharePoint 2010에서 SharePoint 2013으로 데이터베이스 업그레이드](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690)합니다.  
  
  
