---
title: Reporting Services SharePoint 2010 용 SharePoint 모드 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 47efa72e-1735-4387-8485-f8994fb08c8c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cc0fe3bef02ebd50558c298ef8d9b3d8565744ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298677"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2010"></a>SharePoint 2010용 Reporting Services SharePoint 모드 설치
  이 항목의 절차에서는 SharePoint 모드에서 Reporting Services 보고서 서버의 단일 서버 설치하는 단계를 안내합니다. 이 단계에는 SharePoint 2010 중앙 관리를 사용하는 SQL Server 설치 마법사 및 추가 구성 태스크가 포합됩니다. 이 항목은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 만드는 등 기존 설치에 대한 개별 절차를 위해 사용할 수도 있습니다. 추가 하는 방법은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 하 여 기존 팜에 서버를 볼 [팜에 추가 보고서 서버를 추가 &#40;SSRS 확장&#41; ](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) 하 고 [추가 Reporting Services 웹 추가 팜에 프런트 엔드](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 단일 서버 설치는 배포 및 테스트 시나리오에서 유용하지만 프로덕션 환경에서는 권장하지 않습니다.  
  
> [!NOTE]  
>  업그레이드 및 종료에 대 한 내용은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 설치 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 참조 하십시오 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)합니다.  
  

  
##  <a name="bkmk_prereq"></a> 필수 구성 요소  
  
-   > [!IMPORTANT]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 구성 및 관리하는 데 더 이상 필요하지 않으며 지원되지 않습니다. SharePoint 중앙 관리를 사용하여 SharePoint 모드에서 보고서 서버를 구성합니다. 자세한 내용은 [Reporting Services SharePoint 서비스 응용 프로그램을 관리](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)합니다.  
  
-   SharePoint 2010 제품을 포함한 요구 사항은 다음 항목을 검토하십시오.  
  
    -   [온라인 릴리스 정보](https://msdn.microsoft.com/library/dn169381.aspx)
  
    -   [SharePoint 2010 팜에서 SQL Server BI 기능을 사용하기 위한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
-   이 항목에서 SharePoint 2010 제품 설치에 대해서는 다루지 않습니다. 자세한 내용은 [SharePoint 2010 팜에서 SQL Server BI 기능 사용에 대 한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)합니다.  
  
-   이러한 절차는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버를 구성하기 위한 것이며 이전 버전의 보고서 서버에는 적용되지 않습니다. 이전 버전의 보고서 서버에서는 SharePoint Shared Service 아키텍처를 사용하지 않습니다. 예를 들어 SQL Server 2008 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 및 SQL Server 2008 R2 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버입니다.  
  
-   **SharePoint 2010 관리** 서비스를 Windows Server Manager에서 시작했는지 확인합니다.  
  
 ![서버 한 대 설치의 SSRS 구성 요소](../../../2014/sql-server/install/media/rs-deployment-1-server.gif "서버 한 대 설치의 SSRS 구성 요소")  
  
### <a name="database-considerations-for-a-single-server-configuration"></a>단일 서버 구성을 위한 데이터베이스 고려 사항  
  
-   Reporting Services와 SharePoint 제품 및 기술은 모두 SQL Server 관계형 데이터베이스를 사용하여 애플리케이션 데이터를 저장합니다.  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]에는 SQL Engine의 호환되는 SQL Server 평가 버전 인스턴스가 필요합니다.  
  
-   SharePoint 제품에서는 기존 데이터베이스 인스턴스를 사용할 수 있습니다. 데이터베이스 엔진의 인스턴스가 설치되지 않은 경우 SharePoint 제품 설치 프로그램은 SharePoint 애플리케이션 데이터베이스에 대해 SQL Server Express Edition을 설치합니다.  
  
-   보고서 서버 인스턴스는 SQL Server Express Edition을 데이터베이스로 사용할 수 없습니다. 그러나 SharePoint 제품에 의해 설치된 SQL Server Express Edition 인스턴스는 다른 데이터베이스 엔진 버전과 함께 있을 수 있습니다.  
  

  
##  <a name="bkmk_install_SSRS"></a> SharePoint 모드의 Reporting Services 보고서 서버 설치  
  
1.  SQL Server 설치 마법사를 실행합니다.  
  
2.  마법사의 왼쪽에서 **설치** 를 클릭하고 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
3.  모든 규칙이 통과되었다고 가정하고 **설치 지원 규칙** 페이지에서 **확인** 을 클릭합니다.  
  
4.  **설치 지원 파일** 페이지에서 **설치** 를 클릭합니다.  
  
5.  지원 파일이 설치를 끝내고 지원 규칙이 **통과** 상태를 나타내면 **다음**을 클릭합니다. 경고 또는 차단 문제를 검토합니다.  
  
6.  에 **제품 키** 페이지에서 키를 입력 하거나 ' Enterprise Evaluation' 버전의 기본값을 적용 합니다.  
  
     **다음**을 클릭합니다.  
  
7.  라이선스 조건을 검토하고 동의합니다. 제품 기능 및 지원 향상에 도움이 되는 기능 사용 데이터 전송에 동의한 것에 감사한다는 메시지가 표시됩니다.  
  
     **다음**을 클릭합니다.  
  
8.  **설치 역할** 페이지에서 **SQL Server 기능 설치** 를 클릭합니다.  
  
      **다음**을 클릭합니다.  
  
     ![설치 역할을 위한 SQL Server 기능 설치](../../../2014/sql-server/install/media/rs-setuprole.gif "설치 역할을 위한 SQL Server 기능 설치")  
  
9. **기능 선택** 페이지에서 다음을 선택합니다.  
  
    -   **Reporting Services – SharePoint**  
  
    -   **SharePoint 2010 제품용 Reporting Services 추가 기능**. ![참고](../../../2014/reporting-services/media/rs-fyinote.png "참고")추가 기능을 설치 하는 것에 대 한 설치 마법사 옵션을 사용 하 여 새로운는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 릴리스 합니다.  
  
    -   아직 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스가 없는 경우 전체 환경에 대해 **데이터베이스 엔진 서비스** 및 **관리 도구 전체** 를 선택할 수 있습니다.  
  
     **다음**을 클릭합니다.  
  
     ![SharePoint 모드로 SSRS 기능 선택](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "SharePoint 모드로 SSRS 기능 선택")  
  
10. **설치 규칙** 페이지에서 **다음** 을 클릭합니다. 경고 또는 차단 문제를 검토합니다.  
  
11. 데이터베이스 엔진 서비스를 선택한 경우 **인스턴스 구성** 페이지에서 **MSSQLSERVER** 의 기본 인스턴스를 적용하고 **다음**을 클릭합니다. Reporting Services 공유 서비스 아키텍처는 이전 Reporting Services 아키텍처처럼 SQL Server "인스턴스"를 기반으로 하지 않습니다.  
  
12. **디스크 공간 요구 사항** 페이지를 검토하고 **다음**을 클릭합니다.  
  
13. **서버 구성** 페이지에서 적합한 자격 증명을 입력합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 또는 가입 기능을 사용하려면 SQL Server 에이전트의 **시작 유형** 을 **자동**으로 변경해야 합니다.  
  
     **다음**을 클릭합니다.  
  
14. 데이터베이스 엔진 서비스를 선택한 경우 **데이터베이스 엔진 구성** 페이지가 표시되면 해당 계정을 SQL 관리자 목록에 추가하고 **다음**을 클릭합니다.  
  
15. **Reporting Services 구성** 페이지에서 **설치만** 옵션이 선택된 상태로 표시되어야 합니다. 이 옵션은 보고서 서버 파일을 설치하고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대한 SharePoint 환경을 구성하지 않습니다. SQL Server 설치가 완료되면 이 항목의 다른 섹션에 따라 SharePoint 환경을 구성합니다. 이 절차에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스 설치 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 생성이 포함됩니다.  
  
     ![rs_SQL11_SETUP_SSRS_configpage_withcircles](../../../2014/sql-server/install/media/rs-kj-setup-ssrs-configpage-withcircles.gif "rs_SQL11_SETUP_SSRS_configpage_withcircles")  
  
16. **오류 보고** 페이지에서 오류 보고서를 보내기 위한 확인란을 클릭하면 Microsoft가 SQL Server 기능 및 서비스를 개선하는 데 도움이 됩니다.  
  
     **다음**을 클릭합니다.  
  
17. 경고를 검토한 후 **설치 구성 규칙** 페이지에서 **다음** 을 클릭합니다.  
  
18. **설치 준비** 페이지에서 설치 요약을 검토한 후 **다음**을 클릭합니다. 요약에는 계정 정보와 **SharePointFilesOnlyMode** 설치 모드 값을 포함하는 **Reporting Services** 노드가 포함됩니다.  
  

  
##  <a name="bkmk_install_SSRS_sharedservice"></a> 설치 하 고 Reporting Services SharePoint 서비스를 시작 합니다.  
 ![PowerShell 관련 콘텐츠](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")  
  
> [!NOTE]  
>  기존 SharePoint 팜에 설치하는 경우에는 이 섹션의 단계를 완료할 **필요가 없습니다** . 이전 섹션에서 SQL Server 설치 마법사를 실행한 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 서비스가 이미 설치되어 시작되었습니다.  
  
 필요한 파일이 SQL Server 설치 마법사의 일부로 설치되었지만 서비스를 SharePoint 팜에 등록해야 합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 릴리스에는 SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 대한 PowerShell 지원이 도입되었습니다. 다음 단계에서는 SharePoint 관리 셸을 열고 cmdlet을 실행하는 절차를 안내합니다.  
  
1.  **시작** 단추를 클릭합니다.  
  
2.  **Microsoft SharePoint 2010 제품** 그룹을 클릭합니다.  
  
3.  **SharePoint 2010 관리 셸** 을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
4.  다음 PowerShell 명령을 실행하여 SharePoint 서비스를 설치합니다. 명령을 성공적으로 완료하면 관리 셸에 새 줄이 표시됩니다. 명령을 성공적으로 완료하면 메시지가 관리 셸로 반환되지 않습니다.  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  다음 PowerShell 명령을 실행하여 서비스 프록시를 설치합니다.  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  다음 PowerShell 명령을 실행하여 서비스를 시작하거나 다음 지침 참고 사항을 참조하여 SharePoint 중앙 관리에서 서비스를 시작합니다.  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 또한 세 번째 PowerShell 명령을 실행하는 대신 SharePoint 중앙 관리에서 서비스를 시작할 수도 있습니다. 또한 다음 단계는 서비스가 실행 중인지 확인하는 데 유용합니다.  
  
1.  SharePoint 중앙 관리의 **시스템 설정** 그룹에서 **서버의 서비스 관리** 를 클릭합니다.  
  
2.  **SQL Server Reporting Services 서비스** 를 찾고 동작 열의 **시작** 을 클릭합니다.  
  
3.  Reporting Services 서비스 상태가 **중지됨** 에서 **시작됨**으로 변경됩니다. Reporting Services 서비스가 목록에 없으면 PowerShell을 사용하여 서비스를 설치합니다.  
  
    > [!NOTE]  
    >  Reporting Services 서비스에서 유지 되는 경우는 **시작** 상태에 변경 되지 않습니다 **시작**, ' SharePoint 2010 관리 ' 서비스가 Windows Server Manager에서 시작 되었는지 확인 합니다.  
  

  
##  <a name="bkmk_create_serrviceapplication"></a> Reporting Services 서비스 응용 프로그램 만들기  
 이 섹션에서는 서비스 애플리케이션을 만드는 단계와 속성에 대한 설명(기존 서비스 애플리케이션을 검토하려는 경우)을 제공합니다.  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  SharePoint 리본에서 **새로 만들기** 단추를 클릭합니다.  
  
3.  새로 만들기 메뉴에서 **SQL Server Reporting Services 서비스 애플리케이션**을 클릭합니다.  
  
    > [!WARNING]  
    >  경우는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 옵션이 표시 되지 않습니다 목록의 것을 **표시는를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스가 설치 되어 있지**. PowerShell cmdlt을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 설치하는 방법에 대한 이전 섹션을 검토합니다.  
  
4.  **SQL Server Reporting Services 서비스 응용 프로그램 만들기** 페이지에서 응용 프로그램의 이름을 입력합니다. 여러 개의 Reporting Services 서비스 애플리케이션을 만들 경우 자세한 이름을 지정하거나 또는 명명 규칙을 사용하면 관리 및 운영을 개선하는 데 도움이 됩니다.  
  
5.  **응용 프로그램 풀** 섹션에서 응용 프로그램에 대한 새 응용 프로그램 풀을 만듭니다(권장). 새 애플리케이션 풀의 이름을 서비스 애플리케이션의 이름과 동일하게 사용할 경우 진행 중인 관리를 쉽게 수행할 수 있습니다.  
  
     애플리케이션 풀에 대한 관리 계정을 선택하거나 만듭니다. 도메인 사용자 계정을 지정하세요. 도메인 사용자 계정을 사용하면 SharePoint의 관리되는 계정 기능을 사용할 수 있으므로 암호 및 계정 정보를 한 곳에서 업데이트할 수 있습니다. 같은 ID로 실행할 추가 서비스 인스턴스를 포함하도록 배포를 확장하려는 경우에도 도메인 계정이 필요합니다.  
  
6.  **데이터베이스 서버**에서 현재 서버를 사용하거나 다른 SQL Server를 선택할 수 있습니다.  
  
7.  **데이터베이스 이름** 에서 기본값은 `ReportingService_<guid>`이고 고유한 데이터베이스 이름입니다. 새 값을 입력하는 경우 고유한 값을 입력합니다.  
  
8.  **데이터베이스 인증**에서 기본값은 Windows 인증입니다. **SQL 인증**을 선택하는 경우 SharePoint 배포에서 이 인증 유형을 사용하는 최선의 구현 방법을 SharePoint 관리자 설명서에서 참조하십시오.  
  
9. **웹 응용 프로그램 연결** 섹션에서 현재 Reporting Services 서비스 응용 프로그램에 의해 액세스하기 위해 프로비전 대상 웹 응용 프로그램을 선택합니다. 하나의 Reporting Services 서비스 애플리케이션을 하나의 웹 애플리케이션에 연결할 수 있습니다. 모든 현재 웹 애플리케이션이 이미 Reporting Services 서비스 애플리케이션에 연결된 경우 경고 메시지가 표시됩니다.  
  
10. **확인**을 클릭합니다.  
  
11. 서비스 애플리케이션 만들기를 완료하는 데 몇 분이 걸릴 수 있습니다. 완료되면 확인 메시지와 **구독 및 경고 프로비전** 페이지로 이동하는 링크가 표시됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 및 경고 기능을 사용하려면 프로비전 단계를 완료합니다. 자세한 내용은 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)을 참조하세요.  
  
 ![PowerShell 관련 콘텐츠](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") 만들려면 PowerShell을 사용 하는 방법은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램, 참조 [Reporting Services 서비스 응용 프로그램을 만들려면 PowerShell을 사용 하 여](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp)입니다.  
  

  
##  <a name="bkmk_powerview"></a> Power View 사이트 모음 기능을 활성화 합니다.  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]의 기능 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 추가 기능 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition,이 사이트 모음 기능입니다. 이 기능은 루트 사이트 모음과 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 설치된 후에 생성된 사이트 모음에 대해 자동으로 활성화됩니다. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]를 사용하려면 기능이 활성화되어 있는지 확인합니다.  
  
 SharePoint 2010 제품의 설치 이후에 SharePoint 2010 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치하면 보고서 서버 통합 기능 및 Power View 통합 기능이 루트 사이트 모음에 대해서만 활성화됩니다. 기타 사이트 모음의 경우 기능을 수동으로 활성화합니다.  
  
#### <a name="to-activate-the-power-view-feature"></a>Power View 기능을 활성하려면  
  
1.  원하는 SharePoint 사이트로 브라우저를 엽니다.  
  
2.  **사이트 작업**을 클릭합니다.  
  
3.  **사이트 설정**을 클릭합니다.  
  
4.  사이트 모음 관리 그룹에서 **사이트 모음 기능** 을 클릭합니다.  
  
5.  목록에서 **Power View 통합 기능** 을 찾습니다.  
  
6.  **활성화**를 클릭합니다.  
  
 이 절차는 사이트 모음별로 완료됩니다. 자세한 내용은 [보고서 서버 및 SharePoint에서 Power View 통합 기능을 활성화](../../reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md) 합니다.  
  
##  <a name="bkmk_additional_config"></a> 기타 고려 사항  
 이 섹션에서는 대부분의 SharePoint 배포에서 중요한 추가 구성 단계에 대해 설명합니다.  
  
###  <a name="bkmk_provision_agent"></a> 구독 및 경고 프로비전  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 및 데이터 경고 기능을 사용하려면 SQL Server 에이전트 권한 구성이 필요할 수 있습니다. SQL Server 에이전트가 필요하고 SQL Server 에이전트 실행 확인을 나타내는 오류 메시지가 표시되는 경우 사용 권한을 업데이트합니다. 서비스 애플리케이션 만들기 성공 페이지에서 **구독 및 경고 프로비전** 링크를 클릭하여 SQL Server 에이전트를 프로비전할 다른 페이지로 이동할 수 있습니다. 예를 들어 SQL Server 데이터베이스 인스턴스가 다른 시스템에 있는 경우와 같이 여러 시스템 경계를 이동하며 배포하는 경우 프로비전 단계가 필요합니다. 자세한 내용은 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)을 참조하세요.  
  

  
### <a name="configure-e-mail-for-a-service-application"></a>서비스 애플리케이션에 대한 전자 메일 구성  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 기능은 전자 메일 메시지로 경고를 보냅니다. 전자 메일을 보내기 위해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 구성하고 서비스 애플리케이션을 위한 전자 메일 배달 확장 프로그램을 수정해야 할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가입 기능을 위해 전자 메일 배달 확장 프로그램을 사용하려면 전자 메일 설정이 필요합니다. 자세한 내용은 [Reporting Services 서비스 응용 프로그램에 대한 메일 구성&#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)을 참조하세요.  
  

  
### <a name="add-reporting-services-content-types"></a>Reporting Services의 콘텐츠 형식 추가  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 공유 데이터 원본 파일(.rsds), 보고서 모델 파일(.smdl) 및 보고서 작성기 보고서 정의 파일(.rdl)을 관리하는 데 사용하는 미리 정의된 콘텐츠 형식을 제공합니다. **보고서 작성기 보고서**, **보고서 모델**및 **보고서 데이터 원본** 콘텐츠 형식을 라이브러리에 추가하면 해당 유형의 새 문서를 만들 수 있도록 **새로 만들기** 명령이 활성화됩니다. 자세한 내용은 [라이브러리에 보고서 서버 콘텐츠 형식을 추가 &#40;Reporting Services SharePoint 통합 모드의&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)합니다.  
  

  
### <a name="activate-the-file-sync-feature"></a>파일 동기화 기능 활성화  
 사용자가 게시된 보고서 항목을 SharePoint 문서 라이브러리에 직접 자주 업로드하는 경우 보고서 서버 파일 동기화 기능이 유용합니다. 파일 동기화 기능은 보고서 서버 카탈로그를 문서 라이브러리의 항목과 자주 동기화합니다. 자세한 내용은 [SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능 활성화](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Reporting Services SharePoint Service 및 서비스 애플리케이션](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
  
  
