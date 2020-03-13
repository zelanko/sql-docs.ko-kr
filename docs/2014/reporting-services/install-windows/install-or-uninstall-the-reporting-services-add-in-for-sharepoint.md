---
title: SharePoint 용 Reporting Services 추가 기능 설치 또는 제거 (SharePoint 2010 및 SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2804a9a-08ea-4f4a-805d-a2c19c68733d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63f45fa174296e4ce79985236da2d97d3f11e937
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289441"
---
# <a name="install-or-uninstall-the-reporting-services-add-in-for-sharepoint-sharepoint-2010-and-sharepoint-2013"></a>SharePoint용 Reporting Services 추가 기능 설치 또는 제거(SharePoint 2010 및 SharePoint 2013)
  Sharepoint 서버에서 sharepoint [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 제품용 설치 패키지 추가 기능 (rssharepoint.msi)을 실행 하 여 sharepoint 배포 내에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 사용 하도록 설정 합니다. 이러한 기능에는 SharePoint 사이트에서 보고서, 보고서 모델, 데이터 원본 및 기타 보고서 서버 내용을 생성, 확인 및 관리할 수 있도록 Power View, 보고서 뷰어 웹 파트, URL 프록시 엔드포인트, 콘텐츠 형식 및 애플리케이션 페이지가 포함됩니다. SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능은 SharePoint 모드에서 실행되는 보고서 서버의 필수 구성 요소입니다. 추가 기능은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 마법사에서 설치하거나 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩에서 rsSharePoint.msi를 다운로드하여 설치할 수 있습니다. 추가 기능의 버전 목록 및 다운로드 페이지는 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124; SharePoint 2010|

 **항목 내용**

-   [필수 구성 요소](#bkmk_prereq)

-   [추가 기능을 설치 하는 방법](#bkmk_whatinstalled)

-   [설치 방법 개요](#bkmk_3ways_to_install)

-   [rsSharePoint.msi 설치 파일을 사용하여 추가 기능 설치](#bkmk_install_rssharepoint)

    -   [파일만 설치](#bkmk_files_only_installation)

-   [Reporting Services 추가 기능을 제거하는 방법](#bkmk_remove_addin)

-   [명령줄에서 rssharepoint.msi를 복구 하는 방법](#bkmk_repair)

-   [설치 로그 파일](#bkmk_logfiles)

-   [업그레이드](#bkmk_upgrade)

-   [RsCustomAction.exe](#bkmk_rscustomaction)

##  <a name="bkmk_prereq"></a> 필수 조건
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 설치 작업은 보고서 서버를 SharePoint 제품 인스턴스와 통합하는 데 필요한 몇 가지 단계 중 하나입니다. SharePoint 모드 사용을 위한 전체 요구 사항 집합에 대한 자세한 내용은 [Hardware and Software Requirements for Reporting Services in SharePoint Mode](../../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md)을 참조하세요. 설치 및 구성 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대 한 자세한 내용은 [sharepoint 2013에 대 한 sharepoint 모드 설치 Reporting Services](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)를 참조 하세요.

-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 웹 프런트 엔드 애플리케이션이 여러 개 있는 SharePoint 팜과 통합하는 경우 웹 서버 프런트 엔드가 있는 팜의 각 컴퓨터에 추가 기능을 설치합니다. 이 작업은 보고서 서버 내용에 액세스하는 데 사용될 웹 프런트 엔드에 대해서만 수행합니다.

-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치하려면 컴퓨터의 관리자여야 합니다. 예를 들어 명령줄에서 rsSharePoint.msi를 실행하려면 **관리자 권한으로 실행** 옵션을 사용하여 관리자 권한으로 명령 프롬프트를 열어야 합니다.

-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치하려면 SharePoint 팜 관리자 그룹의 구성원여야 합니다.

-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 통합 기능을 활성화하려면 사이트 모음 관리자여야 합니다.

-   추가 기능을 사용 하는 예제 배포 다이어그램은 [SharePoint의 SQL SERVER BI 기능에 대 한 배포 토폴로지](../../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)를 참조 하세요.

##  <a name="bkmk_whatinstalled"></a>추가 기능을 설치 하는 방법
 추가 기능 설치 과정은 두 단계로 구성되며, 표준 설치를 완료하면 두 단계 모두 자동으로 완료됩니다.

-   첫 번째 단계에서는 파일을 적합한 폴더에 설치합니다. 폴더는 SharePoint 배포를 위한 표준 폴더입니다. 이렇게 설치되는 파일 중 하나는 rsCustomAction.exe입니다.

-   두 번째 설치 단계에서는 사용자 지정 동작 집합을 실행하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 파일을 SharePoint에 등록합니다. 사용자 지정 동작은 rsCustomAction.exe로부터 실행됩니다. 이 exe 파일은 두 단계로 이뤄진 전체 설치가 완료될 때 제거됩니다. 
  **파일만** 설치를 실행할 수 있으며, 이 경우 설치 종료 시 rsCustomAction.exe가 실행되지 않고 드라이브에 남아 있습니다.

## <a name="the-reporting-services-installation-order"></a>Reporting Services 설치 순서
 SharePoint 설치 전이나 후에 추가 기능을 설치할 수 있습니다. 추가 기능은 SharePoint 배포 전 표준을 따르며 SharePoint 설치에 사용되는 위치에 파일을 설치합니다.

> [!NOTE]
>  SharePoint 제품보다 추가 기능을 먼저 설치하면 팜에 새 서버를 추가할 경우 SharePoint 팜에서 Reporting Services 추가 기능을 구성하고 활성화한다는 이점이 있습니다.

 **SharePoint 2010**

-   SharePoint 2010 제품 준비 도구는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치합니다. 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능에 필요한 새 버전의 추가 기능이 포함됩니다.

     SharePoint 제품 준비 도구를 실행할 경우에도 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치해야 합니다.

-   
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 먼저 설치하면 SharePoint 제품 준비 도구를 실행할 때 준비 도구에서 새 버전이 감지되어 이전 버전의 추가 기능이 설치되지 않았음을 알리는 대화 상자가 표시됩니다. 이 동작은 정상적인 동작입니다.

     ![SSRS 추가 기능이 이미 설치되었음](../../../2014/sql-server/install/media/rs-sharepointprereq-complete.gif "SSRS 추가 기능이 이미 설치되었음")

 **SharePoint 2013**

 SharePoint 20103 제품 준비 도구는 SharePoint **Not** 제품용 추가 기능 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 을 설치 하지 않습니다.

##  <a name="bkmk_3ways_to_install"></a>설치 방법 개요
 다음 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 두 가지 방법 중 하나를 사용 하 여 SharePoint 제품용 추가 기능을 설치할 수 있습니다.

-   **설치 마법사:** ![note](../../../2014/reporting-services/media/rs-fyinote.png "참고")에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]대 한 새로운 정보, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 통해 추가 기능을 설치할 수 있습니다. 마법사의 **기능 선택** 페이지에서 **SharePoint 제품용 Reporting Services 추가 기능** 을 선택합니다.

-   **rssharepoint.msi:** 추가 기능을 설치 미디어에서 직접 설치 하거나 다운로드 하 여 설치할 수 있습니다. rsSharepoint.msi는 그래픽 사용자 인터페이스 및 명령줄 설치를 둘 다 지원합니다. 먼저 승격된 권한으로 명령 프롬프트 창을 연 다음 명령줄에서 rsSharepoint.msi를 실행하여 관리자 권한으로 .msi를 실행해야 합니다. 추가 기능 다운로드에 대한 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.

    > [!NOTE]
    >  자동 명령줄 설치를 위해 **/q** 스위치를 사용할 경우 최종 사용자 사용권 계약이 표시되지 않습니다. 설치 방법에 관계없이 본 소프트웨어의 설치는 사용권 계약에 의해 제한되며 사용자는 사용권 계약을 준수해야 합니다.

##  <a name="bkmk_install_rssharepoint"></a>Rssharepoint.msi 설치 파일을 사용 하 여 추가 기능을 설치 합니다.
 이 섹션은 .msi 설치 마법사를 실행하거나 명령줄 설치를 실행하여 rssharepoint.msi를 직접 설치하는 방법과 관련이 있습니다. SQL Server 설치 마법사를 사용하여 추가 기능을 설치한 경우 이 단계를 수행할 필요가 없습니다.

 명령줄 스위치의 전체 목록은 다음 명령을 실행하여 확인할 수 있습니다.

```
Rssharepoint.msi /?
```

1.  추가 기능에 대 한`rsSharepoint.msi`설치 프로그램 ()을 다운로드 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 다운로드에 대한 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.

2.  관리자 권한으로 `rsSharepoint.msi`를 실행하여 설치 마법사를 실행합니다. 그러면 시작 페이지, 소프트웨어 사용 조건 및 등록 정보 페이지가 표시됩니다. 설치 프로그램은 다음 경로 아래에 폴더를 만들고 이 폴더에 파일을 복사합니다.

     `%program files%\common files\Microsoft Shared\Web Server Extensions\14\`

     또는

     `%program files%\common files\Microsoft Shared\Web Server Extensions\15\`

3.  SharePoint 중앙 관리에서 보고서 서버 설정 및 기능 활성화를 구성합니다. . 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 설치 및 구성에 대한 자세한 내용은 [SharePoint 2010용 Reporting Services SharePoint 모드 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)를 참조하세요.

###  <a name="bkmk_files_only_installation"></a>파일만 설치
 파일을 설치하고 설치 중 사용자 지정 동작 단계를 건너뛰려면 SKIPCA 옵션을 사용하여 명령줄에서 rssharepoint.msi를 실행합니다.

1.  **관리자 권한으로**명령 프롬프트를 엽니다.

2.  다음 명령 실행:

    ```cmd
    Msiexec.exe /i rsSharePoint.msi SKIPCA=1
    ```

 설치 사용자 인터페이스가 열려 일반적인 방식으로 실행되고 `rsCustomAction.exe` 파일이 설치됩니다. 그러나 설치가 끝난 후에도 .exe가 실행되지 않으며, 설치 완료 시 `rsCustomAction.exe`가 컴퓨터에 남아 있습니다.

### <a name="use-a-two-step-installation-to-troubleshoot-installation-issues-or-install-the-content-types"></a>2단계 설치로 설치 문제 해결 또는 콘텐츠 형식 설치
 설치 중 오류가 발생하거나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 콘텐츠 형식이 문서 라이브러리 설정에 나타나지 않는 경우, 명령줄에서 설치 프로그램을 두 단계 프로세스로 실행할 수 있습니다.

1.  
  **관리자 권한으로** 명령 프롬프트를 열고 이전 섹션에 설명된 대로 파일만 설치를 실행합니다.

2.  사용자 지정 동작 실행 파일 실행:

    1.  
  `rsCustomAction.exe` 파일이 포함된 폴더로 이동합니다. 이 파일은 추가 기능의 파일만 설치에 따라 컴퓨터에 복사됩니다. `rsCustomAction.exe`**% Temp%** 디렉터리에 있습니다. 파일로 이동하려면 명령 프롬프트에서 다음을 입력합니다.

         **CD% temp%** 입니다.

         이 파일은 다음 위치에 있습니다. **/Users\\<사용자 이름\>/AppData/Local/Temp**

    2.  다음 명령을 입력합니다. 이 구성 단계를 마치는 데 몇 분 정도 걸릴 수 있습니다. 이 프로세스 중 W3SVC 서비스가 다시 시작됩니다. 프로그램이 파일을 복사하고, 구성 요소를 등록하고, SharePoint 제품 구성 마법사를 실행하면서 해당 상태 메시지가 표시됩니다.

        ```cmd
        rsCustomAction.exe /i
        ```

    3.  변경 내용을 적용하는 데 걸리는 시간은 서버 환경에 따라 다를 수 있습니다. 또한 빠른 업데이트를 적용하기 위해 **iisreset** 를 실행할 수도 있습니다.

### <a name="quiet-installation-for-scripting"></a>스크립팅을 위한 자동 설치
 대화 상자 또는 경고가 표시되지 않는 "자동" 설치를 위해 **/q** 또는 **/quiet** 스위치를 사용할 수 있습니다. 자동 설치는 추가 기능 설치를 스크립팅하려는 경우에 유용합니다.

> [!NOTE]
>  자동 명령줄 설치를 위해 **/q** 스위치를 사용할 경우 최종 사용자 사용권 계약이 표시되지 않습니다. 설치 방법에 관계없이 본 소프트웨어의 설치는 사용권 계약에 의해 제한되며 사용자는 사용권 계약을 준수해야 합니다.

 자동 설치를 수행하려면

1.  **관리자 권한으로**명령 프롬프트를 엽니다.

2.  다음 명령 실행:

    ```cmd
    Msiexec.exe /i rsSharePoint.msi /q
    ```

##  <a name="bkmk_remove_addin"></a>Reporting Services 추가 기능을 제거 하는 방법
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows 제어판이나 명령줄에서 SharePoint 제품용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 추가 기능을 제거할 수 있습니다.

1.  제어판을 사용하면 현재 컴퓨터에서 파일 전체 제거가 실행되며 **또한** SharePoint 팜에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개체 및 기능이 제거됩니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개체 및 기능이 제거되면 더 이상 보고서를 검토하고 업데이트할 수 없습니다.

2.  추가 기능을 제거하기 위한 명령줄 방법을 사용하면 LocalOnly 매개 변수를 사용하여 로컬 컴퓨터에서는 추가 기능 파일만 제거하고 팜의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개체 및 기능은 변경되지 않습니다.

 추가 기능을 제거하면 보고서 서버에서 보고서를 처리하는 데 사용되는 서버 통합 기능이 제거됩니다. SharePoint 중앙 관리의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지 및 기타 사용자 지정 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지도 제거됩니다. SharePoint 사이트에서 더 이상 사용하지 않는 보고서와 다른 보고서 서버 항목을 제거할 수도 있습니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 제거한 후에는 이러한 항목이 실행되지 않습니다.

 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 제거하려면 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 설치가 실행 중이어야 합니다. SharePoint 2010을 먼저 제거한 경우 다시 설치해야 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 제거할 수 있습니다.

 추가 기능을 제거하는 단계는 독립 실행형 서버 및 서버 팜 모두에서 같습니다. 설치 프로그램에서는 설치 중 추가된 프로그램 파일과 모든 구성 설정을 제거합니다.

 추가 기능을 제거해도 다음 항목은 제거되지 않습니다.

-   SharePoint 구성 및 콘텐츠 데이터베이스에 액세스하는 데 사용되는 보고서 서버 서비스 계정에 대해 생성된 로그인. SharePoint 데이터베이스를 호스트 하는 데 사용 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 보고서 서버 서비스 계정에 대 한 로그인을 모두 삭제 해야 합니다.

-   보고서 사용자에 대해 만든 사용 권한 또는 그룹. 보고서 서버 기능에 대한 액세스 권한을 부여하기 위해 사용자 지정 권한 수준이나 SharePoint 그룹을 만든 경우 더 이상 필요하지 않은 사용 권한을 취소해야 합니다.

-   보고서 정의 파일(.rdl), 공유 데이터 원본 파일(.rsds) 및 게시된 보고서 항목 파일(.rsc)을 비롯하여 SharePoint 라이브러리에 업로드한 데이터 파일. 이러한 파일의 경우 삭제되지는 않지만 더 이상 실행되지 않습니다. 해당 파일은 직접 삭제해야 합니다.

-   설치 프로그램에서는 보고서 서버 데이터베이스를 삭제하지 않으며 통합 작업에 사용되는 보고서 서버 인스턴스를 수정하지 않습니다.

### <a name="to-uninstall-from-windows-control-panel"></a>Windows 제어판에서 제거하려면
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 제어판에서 마법사를 시작하고 추가 기능을 제거하려면

1.  제어판의 **프로그램**에서 **프로그램 제거**를 선택합니다.

2.  
  **SharePoint용 Microsoft SQL Server RS 추가 기능**을 선택합니다. 명령 프롬프트에서 스위치 없이 **rssharepoint.msi** 를 실행하여 제거 마법사를 시작할 수도 있습니다.

3.  **제거**를 클릭합니다.

### <a name="uninstall-from-the-command-line"></a>명령줄에서 제거
 명령줄에서 추가 기능을 제거하려면

1.  **관리자 권한으로**명령 프롬프트를 엽니다.

2.  다음 명령 실행:

    ```cmd
    msiexec.exe /uninstall rsSharePoint.msi
    ```

3.  확인 메시지 상자가 표시됩니다. **예**를 클릭합니다.

### <a name="uninstall-the-add-in-from-the-local-server-only"></a>로컬 서버에서만 추가 기능 제거
 이전 방법으로 추가 기능을 제거하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능 및 개체가 팜에서 제거됩니다. 다중 서버 팜에서 로컬 컴퓨터의 추가 기능만 제거하고 SharePoint 팜은 계속 작동하게 유지하려면 다음 단계를 완료합니다.

1.  **관리자 권한으로**명령 프롬프트를 엽니다.

2.  다음 명령 실행:

    ```cmd
    Msiexec.exe /uninstall rsSharePoint.msi LocalOnly=1
    ```

 이 옵션은 로컬 컴퓨터에서만 SharePoint에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 등록을 해제하고 파일을 제거합니다.

 SharePoint에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능의 등록을 해제하지만 나중에 사용할 수 있도록 디스크에 파일을 남겨 두려면 다음 단계를 완료합니다.

1.  **관리자 권한으로**명령 프롬프트를 엽니다.

2.  다음 명령 실행:

    ```cmd
    rsCustomAction.exe /p
    ```

 SkipCA=1을 사용하여 .msi를 설치하고 rscusstomaction.exe를 사용할 수 있다는 가정 하에 위의 단계가 진행됩니다. 자세한 내용은 파일만 설치 설명 섹션을 참조하세요.

##  <a name="bkmk_repair"></a>명령줄에서 rssharepoint.msi를 복구 하는 방법
 명령줄을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 복구하거나 제거하려면 다음 단계를 완료합니다.

1.  **관리자 권한으로**명령 프롬프트를 엽니다.

2.  다음 명령 실행:

    ```cmd
    msiexec.exe /f rssharepoint.msi
    ```

##  <a name="bkmk_logfiles"></a>설치 로그 파일
 설치 프로그램을 실행하면 **%temp%** 폴더의 로그 파일에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치한 사용자에 대한 정보가 기록됩니다. 예: **c:\Users\\<username\>\AppData\Local\Temp**. 파일 이름은 **RS_SP_\<number>.log**, 형식으로 지정됩니다(예: **RS_SP_0.log**). 로그의 각 오류는 문자열 "SSRSCustomActionError"로 시작합니다.

> [!NOTE]
>  AppData는 Windows 운영 체제의 숨겨진 폴더입니다. 숨겨진 파일과 폴더를 표시할 수 있도록 Windows 탐색기 폴더 설정을 수정해야 할 수 있습니다.

#### <a name="view-a-log-file-with-windows-notepad"></a>Windows 메모장으로 로그 파일 보기

1.  다음 명령을 수행하면 명령 프롬프트 경로가 변경되고 rs 로그 파일이 나열된 후 파일 중 하나가 Windows 메모장으로 열립니다.

    ```cmd
    cd %temp%
    ```

    ```cmd
    dir rs_sp*.log
    ```

    ```cmd
    notepad rs_sp_3.log
    ```

#### <a name="view-a-log-file-with-powershell"></a>PowerShell에서 로그 파일 보기

1.  파일에서 "ssrscustomactionerror"가 포함된 필터링된 행 목록을 반환하려면 SharePoint 관리 셸에서 다음 명령을 입력합니다.

    ```powershell
    Get-Content -Path C:\Users\<UserName\AppData\Local\Temp\rs_sp_0.log | Select-String "ssrscustomactionerror"
    ```

2.  출력은 다음과 유사합니다.

     `2011-05-23 12:40:12: SSRSCustomActionError: SharePoint is installed, but not configured`.

##  <a name="bkmk_upgrade"></a>업그레이드할
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 이미 설치되어 있으면 현재 버전으로 업그레이드할 수 있습니다. 추가 기능 설치 프로그램이 기존 버전을 감지하여 업데이트할 것인지 확인하는 메시지를 표시합니다. 메시지는 다음과 유사합니다.

 **시스템에서이 제품의 하위 버전이 검색 되었습니다. 기존 설치를 업그레이드 하 시겠습니까?**

 확인하면 이전 버전의 추가 기능이 제거되고 새 버전이 설치됩니다.

 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능은 인스턴스를 인식하지 못하므로 컴퓨터에서 하나의 추가 기능 인스턴스만 실행할 수 있습니다. 따라서 다른 버전을 현재 버전과 함께 실행할 수 없습니다.

##  <a name="bkmk_rscustomaction"></a>Rscustomaction.exe
 다음 표에서는 rscustomaction.exe 스위치를 요약해서 보여 줍니다.

|스위치|Description|
|------------|-----------------|
|i|사용자 지정 동작을 설치합니다. 그러면 SharePoint의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소가 등록되고 W3SVCservice가 다시 시작됩니다.|
|r|Repair|
|u|제거. 이 스위치는 전체 SharePoint 팜에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 등록을 해제하지만 디스크에 파일을 남겨 둡니다. W3SVCservice가 다시 시작됩니다.|
|p|로컬 제거. 이 스위치는 로컬 컴퓨터에서만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 등록을 해제합니다. 파일은 디스크에 유지되고 W3SVCservice가 다시 시작됩니다.|
|t|SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 2005에만 해당 스위치는 보고서 서버에 보고서 서버 데이터베이스에 대한 작업 연결이 있는지를 테스트합니다.|

## <a name="configuring-reporting-services"></a>Reporting Services 구성
 모든 필요한 컴퓨터에 추가 기능을 설치한 다음에는 SharePoint 중앙 관리에서 보고서 서버를 구성해야 합니다. 필요한 단계는 설치된 여러 기술의 순서에 따라 달라집니다. 자세한 내용은 sharepoint [2010에 대 한 Sharepoint 모드 설치 Reporting Services](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) 및 [Reporting Services 보고서 서버 &#40;sharepoint 모드](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md) 를 참조 하세요&#41;

## <a name="see-also"></a>참고 항목
 Sharepoint 2010 [Reporting Services 보고서 서버 &#40;Sharepoint 모드](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md) [에 대 한 Reporting Services sharepoint 모드 설치](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)&#41;
