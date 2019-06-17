---
title: Reporting Services SharePoint 2013 용 SharePoint 모드 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9f50e2d4a1cee7bfb36d03f69a8ee4a41772939b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094607"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2013"></a>Install Reporting Services SharePoint Mode for SharePoint 2013
  이 항목의 절차에서는 SharePoint 배포 모드에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 단일 서버 설치 과정을 안내합니다. 이 단계에는 SharePoint 중앙 관리를 사용하는 구성 태스크 및 SQL Server 설치 마법사의 실행이 포합됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 만드는 등 기존 설치를 업데이트하는 개별 절차에 이 항목을 사용할 수도 있습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; **참고:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에서는 **되지** SharePoint 서버 다중 테 넌 트를 지원 합니다.|  
  
 기존 팜에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버를 추가하는 방법은 다음을 참조하세요.  
  
-   [팜에 추가 보고서 서버 추가&#40;SSRS 확장&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [팜에 추가 Reporting Services 웹 프런트 엔드 추가](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 단일 서버 설치는 개발 및 테스트 시나리오에 유용하지만 프로덕션 환경에서는 권장되지 않습니다.  
  
 **항목 내용**  
  
-   [단일 서버 배포 예](#bkmk_singleserver)  
  
-   [설치 계정](#bkmk_setupaccounts)  
  
-   [1단계: SharePoint 모드의 Reporting Services 보고서 서버 설치](#bkmk_install_SSRS)  
  
-   [2단계: 등록 및 Reporting Services SharePoint 서비스를 시작 합니다.](#bkmk_install_SSRS_sharedservice)  
  
-   [3단계: Reporting Services 서비스 응용 프로그램 만들기](#bkmk_create_serrviceapplication)  
  
-   [4단계: Power View 사이트 모음 기능을 활성화 합니다.](#bkmk_powerview)  
  
-   [1 ~ 4 단계에 대 한 Windows PowerShell 스크립트](#bkmk_full_script)  
  
-   [Additional Configuration](#bkmk_additional_config) 에는 구독과 경고에 대한 프로비전, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 콘텐츠 형식 및 Analysis Services 서버 사용을 위한 Excel Services 구성이 포함됩니다.  
  
-   [설치 확인](#bkmk_verify_installation)  
  
##  <a name="bkmk_singleserver"></a> 단일 서버 배포 예  
 단일 서버 설치는 개발 및 테스트 시나리오에 유용하지만 프로덕션 환경에서 단일 서버는 권장되지 않습니다. 단일 서버 환경은 같은 컴퓨터에 SharePoint 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 설치된 단일 컴퓨터를 의미합니다. 이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버가 여러 대인 확장을 다루지 않습니다.  
  
 다음 다이어그램에서는 단일 서버 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포의 일부인 구성 요소를 보여 줍니다.  
  
|||  
|-|-|  
|**(1)**|SQL Server와 함께 설치되는 SharePoint 서비스입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 하나 이상 만들 수 있습니다.|  
|**(2)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(SharePoint 제품용)은 SharePoint Server에 사용자 인터페이스 구성 요소를 제공합니다.|  
|**(3)**|Excel Services 애플리케이션은 Power View 및 PowerPivot에서 사용됩니다.|  
|**(4)**|PowerPivot 서비스 애플리케이션입니다.|  
  
 ![SSRS SharePoint 모드 단일 서버 배포](../../../2014/sql-server/install/media/rs-sharepoint-1server-deployment.gif "SSRS SharePoint 모드 단일 서버 배포")  
  
> [!TIP]  
>  더 복잡한 배포 예제는 [SharePoint의 SQL Server BI 기능에 대한 배포 토폴로지](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)를 참조하세요.  
  
##  <a name="bkmk_setupaccounts"></a> 설치 계정  
 이 세션에서는 SharePoint 모드에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 기본 배포 단계에 사용된 계정 및 권한에 대해 설명합니다.  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스의 설치 및 등록:**  
  
-   설치 ('설치' 계정이 라고도 함) 하는 동안 현재 계정 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드는 로컬 컴퓨터에 대 한 관리 권한이 필요 합니다. 설치 하는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint가 설치 된 후 '설치' 계정이 또한 SharePoint 팜 관리자 그룹의 멤버를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치는 등록을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 합니다. 설치 하는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 수동으로 서비스를 등록에 SharePoint가 설치 하거나 '설치' 계정이 팜 관리자 그룹의 멤버인 되지 전에 합니다. 섹션을 참조 [2 단계: 등록 및 Reporting Services SharePoint 서비스를 시작](#bkmk_install_SSRS_sharedservice)합니다.  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램 만들기**  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 설치하고 등록하여 하나 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 만드세요. "SharePoint 팜 서비스 계정"이 일시적으로 로컬 관리자 그룹의 멤버여야 Reporting Services 서비스 애플리케이션을 만들 수 있습니다. SharePoint 2013 계정 권한에 대 한 자세한 내용은 참조 하세요. [계정 권한 및 SharePoint 2013에서 보안 설정](https://technet.microsoft.com/library/cc678863.aspx) (https://technet.microsoft.com/library/cc678863.aspx) 합니다.  
  
     SharePoint 팜 관리자 계정이 또한 로컬 운영 체제 관리자 계정이 아닌 것이 가장 좋은 보안 방법입니다. 설치 프로세스의 일부로 로컬 관리자 그룹에 팜 관리자 계정을 추가하는 경우 설치가 완료된 후 로컬 관리자 그룹에서 계정을 제거하는 것이 좋습니다.  
  
##  <a name="bkmk_install_SSRS"></a> 1단계: SharePoint 모드에서 Reporting Services 보고서 서버 설치  
 이 단계는 SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치합니다. 컴퓨터에 이미 설치된 기능에 따라 다음 단계에 설명된 설치 페이지 중 일부가 표시되지 않을 수 있습니다.  
  
1.  SQL Server 설치 마법사(Setup.exe)를 실행합니다.  
  
2.  마법사의 왼쪽에서 **설치** 를 클릭하고 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
3.  모든 규칙이 통과되었다고 가정하고 **설치 지원 규칙** 페이지에서 **확인** 을 클릭합니다.  
  
4.  **설치 지원 파일** 페이지에서 **설치** 를 클릭합니다. 컴퓨터에 이미 설치된 기능에 따라 다음과 같은 메시지가 표시될 수 있습니다.  
  
    -   "영향을 받는 하나 이상의 파일에 보류 중인 작업이 있습니다. 설치 프로세스가 완료된 후 컴퓨터를 다시 시작해야 합니다."  
  
    -   **확인**을 클릭합니다.  
  
5.  지원 파일 설치가 끝내고 **지원 규칙** 페이지에 **통과** 상태가 표시되면 **다음**을 클릭합니다. 경고 또는 차단 문제를 검토합니다.  
  
6.  **설치 유형** 페이지에서 **SQL Server 2014의 기존 인스턴스에 기능 추가**를 클릭합니다. 드롭다운 목록에서 올바른 인스턴스를 선택하고 **다음**을 클릭합니다.  
  
7.  **제품 키** 페이지가 표시되면 키를 입력하거나 기본값인 '평가판' 버전을 적용합니다.  
  
     **다음**을 클릭합니다.  
  
8.  사용 조건 페이지가 표시되면 사용 조건을 검토하고 동의합니다. 제품 기능 및 지원 향상에 도움이 되는 기능 사용 데이터 전송에 동의한 것에 감사한다는 메시지가 표시됩니다.  
  
     **다음**을 클릭합니다.  
  
9. **설치 역할** 페이지가 표시되면 **SQL Server 기능 설치**를 선택합니다.  
  
     **다음**을 클릭합니다.  
  
     ![설치 역할을 위한 SQL Server 기능 설치](../../../2014/sql-server/install/media/rs-setuprole.gif "설치 역할을 위한 SQL Server 기능 설치")  
  
10. **기능 선택** 페이지에서 다음을 선택합니다.  
  
    -   **Reporting Services – SharePoint**  
  
    -   **SharePoint 제품용 Reporting Services 추가 기능**.  
  
         ![참고](../../../2014/reporting-services/media/rs-fyinote.png "참고") 추가 기능을 설치 하는 것에 대 한 설치 마법사 옵션을 사용 하 여 새로운는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 릴리스 합니다.  
  
    -   아직 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스가 없는 경우 전체 환경에 대해 **데이터베이스 엔진 서비스** 및 **관리 도구 전체** 를 선택할 수 있습니다.  
  
     **다음**을 클릭합니다.  
  
     ![SharePoint 모드로 SSRS 기능 선택](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "SharePoint 모드로 SSRS 기능 선택")  
  
11. **설치 규칙** 페이지가 표시되면 다음을 수행합니다. 경고 또는 차단 문제를 검토합니다. 그리고 **다음**을 클릭합니다.  
  
12. 데이터베이스 엔진 서비스를 선택한 경우 **인스턴스 구성** 페이지에서 **MSSQLSERVER** 의 기본 인스턴스를 적용하고 **다음**을 클릭합니다.  
  
     ![참고](../../../2014/reporting-services/media/rs-fyinote.png "참고")Reporting Services SharePoint 서비스 아키텍처는 이전 Reporting Services 아키텍처처럼 SQL Server "인스턴스"를 기반으로 하지 않습니다.  
  
13. **디스크 공간 요구 사항** 페이지를 검토하고 **다음**을 클릭합니다.  
  
14. **서버 구성** 페이지가 표시되면 적합한 자격 증명을 입력합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 또는 가입 기능을 사용하려면 SQL Server 에이전트의 **시작 유형** 을 **자동**으로 변경해야 합니다. 컴퓨터에 이미 설치된 기능에 따라 **서버 구성** 페이지가 표시되지 않을 수 있습니다.  
  
     **다음**을 클릭합니다.  
  
15. 데이터베이스 엔진 서비스를 선택한 경우 **데이터베이스 엔진 구성** 페이지가 표시되면 해당 계정을 SQL 관리자 목록에 추가하고 **다음**을 클릭합니다.  
  
16. **Reporting Services 구성** 페이지에서 **설치만** 옵션이 선택된 상태로 표시되어야 합니다. 이 옵션은 보고서 서버 파일을 설치하고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]용 SharePoint 환경을 구성하지 않습니다.  
  
    > [!NOTE]  
    >  SQL Server 설치가 완료되면 이 항목의 다른 섹션을 따라 SharePoint 환경을 구성합니다. 이 절차에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스 설치 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 생성이 포함됩니다.  
  
     ![SQL Server 설치 마법사-SSRS 구성 페이지](../../../2014/sql-server/install/media/rs-2012sp1-setup-ssrs-configpage-with-circles.gif "SQL Server 설치 마법사-SSRS 구성 페이지")  
  
17. **오류 보고** 페이지에서 오류 보고서를 보내기 위한 확인란을 클릭하면 Microsoft가 SQL Server 기능 및 서비스를 개선하는 데 도움이 됩니다.  
  
     **다음**을 클릭합니다.  
  
18. 경고를 검토한 후 **설치 구성 규칙** 페이지에서 **다음** 을 클릭합니다.  
  
19. **설치 준비** 페이지에서 설치 요약을 검토한 후 **다음**을 클릭합니다. 요약에 **SharePointFilesOnlyMode** 값을 표시하는 **Reporting Services SharePoint 모드**하위 노드가 포함됩니다. **설치**를 클릭합니다.  
  
20. 설치하는 데 몇 분 정도 걸립니다. 기능 목록 및 각 기능의 상태가 표시된 **완료** 페이지가 나타납니다. 컴퓨터를 다시 시작해야 함을 나타내는 정보 대화 상자가 표시될 수 있습니다.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a> 2단계: 등록 및 Reporting Services SharePoint 서비스를 시작 합니다.  
 ![PowerShell 관련 콘텐츠](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")  
  
> [!NOTE]  
>  기존 SharePoint 팜에 설치하는 경우에는 이 섹션의 단계를 완료할 필요가 없습니다. 이 문서의 이전 섹션의 일부로 SQL Server 설치 마법사를 실행한 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 서비스가 설치되어 시작되었습니다.  
  
 다음은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 수동으로 등록해야 하는 일반적인 이유입니다.  
  
-   SharePoint가 설치되기 전에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 설치했습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 설치에 사용된 계정이 SharePoint 팜 관리자 그룹의 멤버가 아닙니다. 자세한 내용은 [Setup accounts](#bkmk_setupaccounts)을 참조하세요.  
  
 필요한 파일이 SQL Server 설치 마법사의 일부로 설치되었지만 서비스를 SharePoint 팜에 등록해야 합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 릴리스에는 SharePoint 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 대한 PowerShell 지원이 도입되었습니다.  
  
 다음 단계에서는 SharePoint 관리 셸을 열고 cmdlet을 실행하는 절차를 안내합니다.  
  
1.  **시작** 단추를 클릭합니다.  
  
2.  **Microsoft SharePoint 2013 제품** 그룹을 클릭합니다.  
  
3.  **SharePoint 2013 관리 셸** 을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다. 참고: SharePoint 명령은 표준 Windows PowerShell 창에서 인식되지 않습니다. **SharePoint 2013 관리 셸**을 사용합니다.  
  
4.  다음 PowerShell 명령을 실행하여 SharePoint 서비스를 설치합니다. 명령을 성공적으로 완료하면 관리 셸에 새 줄이 표시됩니다. 명령을 성공적으로 완료하면**메시지가 관리 셸로 반환되지 않습니다.**  
  
    ```  
    Install-SPRSService  
    ```  
  
    > [!IMPORTANT]  
    >  다음과 유사한 오류 메시지가 표시되는 경우  
    >   
    >  Install-sprsservice: ' Install-sprsservice ' 용어 **인식 되지 않습니다** 으로  
    > cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식되지 않습니다. 이름의 철자, 경로 포함 여부와  
    > 경로가 올바른지 확인한 다음  
    > 다시 시도하세요.  
  
5.  다음 PowerShell 명령을 실행하여 서비스 프록시를 설치합니다. 명령을 성공적으로 완료하면 관리 셸에 새 줄이 표시됩니다. 명령을 성공적으로 완료하면**메시지가 관리 셸로 반환되지 않습니다.**  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  다음 PowerShell 명령을 실행하여 서비스를 시작하거나 SharePoint 중앙 관리에서 서비스를 시작하는 방법에 대한 다음 지침 참고 사항을 참조합니다.  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 SharePoint 관리 셸 대신 Windows PowerShell에 있거나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드가 설치되어 있지 않습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 PowerShell에 대한 자세한 내용은 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)을 참조하세요.  
  
 또한 세 번째 PowerShell 명령을 실행하는 대신 SharePoint 중앙 관리에서 서비스를 시작할 수도 있습니다. 또한 다음 단계는 서비스가 실행 중인지 확인하는 데 유용합니다.  
  
1.  SharePoint 중앙 관리의 **시스템 설정** 그룹에서 **서버의 서비스 관리** 를 클릭합니다.  
  
2.  **SQL Server Reporting Services 서비스** 를 찾고 동작 열의 **시작** 을 클릭합니다.  
  
3.  Reporting Services 서비스 상태가 **중지됨** 에서 **시작됨**으로 변경됩니다. Reporting Services 서비스가 목록에 없으면 PowerShell을 사용하여 서비스를 설치합니다.  
  
    > [!NOTE]  
    >  Reporting Services 서비스가 **시작 중** 상태를 유지하고 **시작됨**으로 변경되지 않을 경우 'SharePoint 2013 관리' 서비스가 Windows Server Manager에서 시작되었는지 확인합니다.  
  
##  <a name="bkmk_create_serrviceapplication"></a> 3단계: Reporting Services 서비스 애플리케이션 만들기  
 이 섹션에서는 서비스 애플리케이션을 만드는 단계와 속성에 대한 설명(기존 서비스 애플리케이션을 검토하려는 경우)을 제공합니다.  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  SharePoint 리본에서 **새로 만들기** 단추를 클릭합니다.  
  
3.  새로 만들기 메뉴에서 **SQL Server Reporting Services 서비스 애플리케이션**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  경우는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 옵션이 표시 되지 않습니다 목록의 것을 **표시는를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 공유 서비스가 설치 되어 있지**. PowerShell cmdlt을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 설치하는 방법에 대한 이전 섹션을 검토합니다.  
  
4.  **SQL Server Reporting Services 서비스 응용 프로그램 만들기** 페이지에서 응용 프로그램의 이름을 입력합니다. 여러 개의 Reporting Services 서비스 애플리케이션을 만들 경우 설명이 포함된 이름이나 명명 규칙을 사용하면 관리 및 운영 작업을 구성하는 데 도움이 됩니다.  
  
5.  **응용 프로그램 풀** 섹션에서 응용 프로그램에 대한 새 응용 프로그램 풀을 만듭니다(권장). 애플리케이션 풀과 서비스 애플리케이션에 동일한 이름을 사용할 경우 진행 중인 관리를 쉽게 수행할 수 있습니다. 이는 만들려는 서비스 애플리케이션 수와 단일 애플리케이션 풀에 여러 서비스 애플리케이션을 사용해야 하는지 여부의 영향을 받을 수도 있습니다. 애플리케이션 풀 관리에 대한 권장 사항 및 모범 사례에 대해서는 SharePoint Server 설명서를 참조하세요.  
  
     애플리케이션 풀에 대한 보안 계정을 선택하거나 만듭니다. 도메인 사용자 계정을 지정하세요. 도메인 사용자 계정을 사용하면 SharePoint의 관리되는 계정 기능을 사용할 수 있으므로 암호 및 계정 정보를 한 곳에서 업데이트할 수 있습니다. 같은 ID로 실행할 추가 서비스 인스턴스를 포함하도록 배포를 확장하려는 경우에도 도메인 계정이 필요합니다.  
  
6.  **데이터베이스 서버**에서 현재 서버를 사용하거나 다른 SQL Server를 선택할 수 있습니다.  
  
7.  **데이터베이스 이름** 에서 기본값은 `ReportingService_<guid>`이고 고유한 데이터베이스 이름입니다. 새 값을 입력하는 경우 고유한 값을 입력합니다. 이 데이터베이스는 서비스 애플리케이션용으로 새로 만든 것입니다.  
  
8.  **데이터베이스 인증**에서 기본값은 Windows  인증입니다. **SQL 인증**을 선택하는 경우 SharePoint 배포에서 이 인증 유형을 사용하는 최선의 구현 방법은 SharePoint 설명서를 참조하세요.  
  
9. **웹 응용 프로그램 연결** 섹션에서 현재 Reporting Services 서비스 응용 프로그램에 의해 액세스하기 위해 프로비전 대상 웹 응용 프로그램을 선택합니다. 하나의 Reporting Services 서비스 애플리케이션을 하나의 웹 애플리케이션에 연결할 수 있습니다. 모든 현재 웹 애플리케이션이 이미 Reporting Services 서비스 애플리케이션에 연결된 경우 경고 메시지가 표시됩니다.  
  
10. **확인**을 클릭합니다.  
  
11. 서비스 애플리케이션 만들기를 완료하는 데 몇 분이 걸릴 수 있습니다. 완료되면 확인 메시지와 **구독 및 경고 프로비전** 페이지로 이동하는 링크가 표시됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 기능 및 데이터 경고 기능을 사용하려면 프로비전 단계를 완료합니다. 자세한 내용은 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)을 참조하세요.  
  
 ![PowerShell 관련 콘텐츠](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") 만들려면 PowerShell을 사용 하는 방법은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 참조 하십시오.  
  
-   다음 섹션인 [1-4단계를 위한 Windows PowerShell 스크립트](#bkmk_full_script)를 참조하세요.  
  
-   항목 [PowerShell을 사용하여 Reporting Services 서비스 애플리케이션을 만들려면](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp)  
  
##  <a name="bkmk_powerview"></a> 4 단계: Power View 사이트 모음 기능 활성화  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 제품용 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능으로, 사이트 모음 기능입니다. 이 기능은 루트 사이트 모음과 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 설치된 후에 생성된 사이트 모음에 대해 자동으로 활성화됩니다. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]를 사용하려면 기능이 활성화되어 있는지 확인합니다.  
  
 SharePoint Server 설치 후에 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치하면 보고서 서버 통합 기능 및 Power View 통합 기능이 루트 사이트 모음에 대해서만 활성화됩니다. 기타 사이트 모음의 경우 기능을 수동으로 활성화합니다.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Power View 사이트 모음 기능을 활성화하거나 확인하려면  
  
1.  다음 단계에서는 SharePoint 사이트가 2013 **환경 버전**에 대해 구성되었다고 가정합니다.  
  
     원하는 SharePoint 사이트로 브라우저를 엽니다. 예를 들어, http://\<서버 이름>/사이트/bi  
  
2.  클릭 **설정을**![SharePoint 설정](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 설정")합니다.  
  
3.  **사이트 설정**을 클릭합니다.  
  
4.  **사이트 모음 관리** 그룹에서 **사이트 모음 기능**을 클릭합니다.  
  
5.  목록에서 **Power View 통합 기능** 을 찾습니다.  
  
6.  **활성화**를 클릭합니다. 기능 상태가 **활성**으로 변경됩니다.  
  
 이 절차는 사이트 모음별로 완료됩니다. 자세한 내용은 [SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화](../../../2014/reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)를 참조하세요.  
  
##  <a name="bkmk_full_script"></a> 1 ~ 4 단계에 대 한 Windows PowerShell 스크립트  
 이 섹션의 PowerShells 스크립트는 이전 섹션의 1~4단계를 완료하는 것과 동일합니다. 이 스크립트는 다음 작업을 완료합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 및 서비스 프록시를 설치하고 서비스를 시작합니다.  
  
-   “Reporting Services”라는 서비스 프록시를 만듭니다.  
  
-   만듭니다는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] "Reporting Services Application" 이라는 응용 프로그램을 서비스 합니다.  
  
-   사이트 모음에 대해 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 기능을 사용하도록 설정합니다.  
  
 매개 변수  
  
-   서비스 프록시에 대해 **-Account** 를 업데이트합니다. 계정은 SharePoint 팜에서 관리되는 서비스 계정이어야 합니다. 자세한 내용은 SharePoint 항목 [SharePoint 2013에서 관리 및 서비스 계정 계획](https://technet.microsoft.com/library/cc263445.aspx)을 참조하세요.  
  
-   서비스 애플리케이션에 대해 **–DatabaseServer** 매개 변수를 업데이트합니다. 이 매개 변수는 데이터베이스 엔진 인스턴스입니다.  
  
-   **기능을 사용하도록 설정하려는 사이트의** –url[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 매개 변수를 업데이트합니다.  
  
 **스크립트를 사용하려면:**  
  
1.  관리 권한으로 Windows PowerShell을 엽니다.  
  
2.  다음 코드를 스크립트 창에 복사합니다.  
  
3.  이전 섹션에서 설명한 세 가지 매개 변수를 업데이트한 후 스크립트를 실행합니다.  
  
```  
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy  
  
```  
  
##  <a name="bkmk_additional_config"></a> 기타 고려 사항  
 이 섹션에서는 대부분의 SharePoint 배포에서 중요한 추가 구성 단계에 대해 설명합니다.  
  
###  <a name="bkmk_configure_ECS"></a> Excel Services 및 PowerPivot 구성  
 SharePoint의 Excel 2013 통합 문서에서 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Power View 보고서를 보려는 경우 팜에서 Excel Services 애플리케이션을 SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버를 사용하도록 구성해야 합니다. 또한, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에서 사용하는 애플리케이션 풀 보안 계정은 Analysis Services 서버에서 관리자여야 합니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   섹션을 Excel Services 구성"Analysis Services의 통합에 대 한"에서 [SharePoint 용 PowerPivot 2013 설치](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)합니다.  
  
-   [Excel Services 데이터 모델 설정(SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx).  
  
###  <a name="bkmk_provision_agent"></a> 구독 및 경고 프로비전  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 및 데이터 경고 기능을 사용하려면 SQL Server 에이전트 권한 구성이 필요할 수 있습니다. SQL Server 에이전트가 필요하고 SQL Server 에이전트 실행 확인을 나타내는 오류 메시지가 표시되는 경우 사용 권한을 업데이트합니다. 서비스 애플리케이션 만들기 성공 페이지에서 **구독 및 경고 프로비전** 링크를 클릭하여 SQL Server 에이전트를 프로비전할 다른 페이지로 이동할 수 있습니다. 예를 들어 SQL Server 데이터베이스 인스턴스가 다른 시스템에 있는 경우와 같이 여러 시스템 경계를 이동하며 배포하는 경우 프로비전 단계가 필요합니다. 자세한 내용은 [SSRS 서비스 애플리케이션에 대한 구독 및 경고 프로비전](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)을 참조하세요.  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>SSRS 서비스 애플리케이션에 대한 전자 메일 구성  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 경고 기능은 전자 메일 메시지로 경고를 보냅니다. 전자 메일을 보내기 위해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 구성하고 서비스 애플리케이션을 위한 전자 메일 배달 확장 프로그램을 수정해야 할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가입 기능을 위해 전자 메일 배달 확장 프로그램을 사용하려면 전자 메일 설정이 필요합니다. 자세한 내용은 [Reporting Services 서비스 응용 프로그램에 대한 메일 구성&#40;SharePoint 2010 및 SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)을 참조하세요.  
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>콘텐츠 라이브러리에 Reporting Services 콘텐츠 형식 추가  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 공유 데이터 원본 파일(.rsds), 보고서 모델 파일(.smdl) 및 보고서 작성기 보고서 정의 파일(.rdl)을 관리하는 데 사용하는 미리 정의된 콘텐츠 형식을 제공합니다. **보고서 작성기 보고서**, **보고서 모델**및 **보고서 데이터 원본** 콘텐츠 형식을 라이브러리에 추가하면 해당 유형의 새 문서를 만들 수 있도록 **새로 만들기** 명령이 활성화됩니다. 자세한 내용은 [라이브러리에 보고서 서버 콘텐츠 형식을 추가 &#40;Reporting Services SharePoint 통합 모드의&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)합니다.  
  
### <a name="activate-the-report-server-file-sync-feature"></a>보고서 서버 파일 동기화 기능 활성화  
 사용자가 게시된 보고서 항목을 SharePoint 문서 라이브러리에 직접 자주 업로드하는 경우 **보고서 서버 파일 동기화** 사이트 수준 기능이 유용합니다. 파일 동기화 기능은 보고서 서버 카탈로그를 문서 라이브러리의 항목과 자주 동기화합니다. 자세한 내용은 [SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능 활성화](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)를 참조하세요.  
  
##  <a name="bkmk_verify_installation"></a> 설치 확인  
 다음은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 배포를 확인하기 위해 권장되는 단계 및 절차입니다.  
  
-   확인 항목 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)에서 SharePoint 섹션을 참조하세요.  
  
-   SharePoint 문서 라이브러리에서 텍스트 상자(예: 제목)만 포함된 기본 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 만듭니다. 이 보고서에는 어떠한 데이터 원본 또는 데이터 세트도 포함되지 않습니다. 이 보고서의 목적은 보고서 작성기를 열고, 기본 보고서를 작성하고, 보고서를 미리 볼 수 있는지 확인하기 위한 것입니다.  
  
     보고서를 문서 라이브러리에 저장하고 라이브러리에서 보고서를 실행합니다. 보고서 작성기로 보고서를 만드는 방법은 [보고서 작성기 시작(보고서 작성기)](https://technet.microsoft.com/library/ms159221.aspx)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Reporting Services 업그레이드 및 마이그레이션](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [내용 로드맵: 설정 하 고 SharePoint Server 및 SQL Server BI 구성](https://technet.microsoft.com/library/dn205112.aspx)   
 [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Reporting Services SharePoint Service 및 서비스 애플리케이션](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)  
  
  
