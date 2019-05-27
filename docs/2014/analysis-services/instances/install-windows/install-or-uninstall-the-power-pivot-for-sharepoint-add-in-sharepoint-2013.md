---
title: 설치 하거나 PowerPivot에 대 한 SharePoint 추가 기능 제거 (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b1fb1e718f8b2ab0257651ff47674d293a9e6a95
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079883"
---
# <a name="install-or-uninstall-the-powerpivot-for-sharepoint-add-in-sharepoint-2013"></a>SharePoint용 PowerPivot 추가 기능 설치 또는 제거(SharePoint 2013)
  [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 팜에서 [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] 데이터 액세스를 제공하는 응용 프로그램 서버 구성 요소 및 백 엔드 서비스의 컬렉션입니다. SharePoint용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 추가 기능(**spPowerpivot.msi**)은 애플리케이션 서버 구성 요소를 설치하는 데 사용되는 설치 관리자 패키지입니다.  
  
-   이 추가 기능은 SharePoint 2010 배포에 필수적 요소가 아닙니다.  
  
-   이 추가 기능은 SharePoint 2013 및 SharePoint 모드의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 를 포함하는 단일 서버 배포에 필수적 요소가 아닙니다. 이 추가 기능에서 설치하는 구성 요소는 SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버를 설치하면 포함됩니다. 예제 배포에서 추가 기능을 사용 하 여 다이어그램을 참조 하세요 [SharePoint의 SQL Server BI 기능에 대 한 배포 토폴로지](../../../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)합니다.  
  
 **참고:** 이 항목에서는 설치에 대해 설명 합니다 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 솔루션 파일 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 2013 구성 도구에 대 한 합니다. 설치 후 구성 도구 및 추가 기능에 자세한 내용은 다음 항목을 참조 [PowerPivot 구성 및 솔루션 배포 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)합니다.  
  
 **spPowerPivot.msi**를 다운로드하는 방법은 [Microsoft® SQL Server® 2014 PowerPivot® for Microsoft SharePoint®](https://go.microsoft.com/fwlink/?LinkID=324854)를 참조하세요.  
  
 **항목 내용**  
  
-   [배경](#bkmk_background)  
  
-   [spPowerPivot.msi 설치 위치](#bkmk_where_to_install)  
  
-   [요구 사항 및 필수 구성 요소](#bkmk_prereq)  
  
-   [SharePoint 용 PowerPivot을 설치 하려면](#bkmk_install)  
  
-   [SharePoint 2013 구성 도구에 대 한 PowerPivot 사용 하 여 SharePoint 솔루션 파일 배포](#bkmk_deploy_solution)  
  
-   [추가 기능 제거 또는 복구](#bkmk_remove_addin)  
  
##  <a name="bkmk_background"></a> 배경  
  
-   **응용 프로그램 서버:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 기능에는 통합 문서를 데이터 원본으로 사용하는 기능, 예약된 데이터 새로 고침 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 관리 대시보드가 포함됩니다.  
  
     [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 은 Analysis Services 클라이언트 라이브러리를 배포하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 설치 파일을 컴퓨터에 복사하는**Windows Installer 패키지(** spPowerpivot.msi [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] )입니다. 설치 관리자는 SharePoint의 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 기능을 배포 또는 구성하지 않습니다. 다음 구성 요소가 기본적으로 설치됩니다.  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. 이 구성 요소에는 PowerShell 스크립트(.ps1 파일), SharePoint 솔루션 패키지(.wsp) 및 SharePoint 2013 팜에서 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]을 배포하기 위한 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 2013 구성 도구가 포함되어 있습니다.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Analysis Services용 OLE DB 공급자(MSOLAP)  
  
    -   ADOMD.NET 데이터 공급자  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Management Objects  
  
-   **백 엔드 서비스:** 사용 하는 경우 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] excel의 분석 데이터가 포함 된 통합 문서를 만드는 경우 Excel 서비스를 실행 하는 BI 서버를 사용 하 여 구성 있어야 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버 환경에서 데이터에 액세스 하려면 SharePoint 모드에서. SharePoint Server 2013이 설치된 컴퓨터 또는 SharePoint 소프트웨어가 설치되지 않은 다른 컴퓨터에서 SQL Server 설치 프로그램을 실행할 수 있습니다. Analysis Services는 SharePoint에 종속성이 없습니다.  
  
     백 엔드 서비스 설치, 제거 및 구성에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
    -   [SharePoint 2013용 PowerPivot 설치](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [SharePoint용 PowerPivot 제거](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> spPowerPivot.msi 설치 위치  
 권장되는 최선의 구현 방법은 구성 일치를 위해 애플리케이션 서버 및 웹 프런트 엔드 서버를 포함하여 SharePoint 팜의 모든 서버에 **spPowerPivot.msi** 를 설치하는 것입니다. 설치 관리자 패키지에는 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 구성 도구뿐만 아니라 Analysis Services 데이터 공급자도 포함되어 있습니다. **spPowerPivot.msi** 를 설치하는 경우 개별 구성 요소를 제외하여 설치를 사용자 지정할 수 있습니다.  
  
 **데이터 공급자:** 여러 SharePoint 및 SQL Server 기술은 Excel Services, PerformancePoint Services 및 Power View 등 Analysis Services 데이터 공급자를 사용 합니다. 모든 SharePoint 서버에 **spPowerPivot.msi** 를 설치하면 Analysis Services 데이터 공급자의 전체 집합과 PowerPivot 연결이 팜에서 일관적으로 사용할 수 있음을 확인할 수 있습니다.  
  
> [!NOTE]  
>  **spPowerPivot.msi**를 사용하여 SharePoint 2013 서버에 Analysis Services 데이터 공급자를 설치해야 합니다. [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 기능 팩에서 사용할 수 있는 다른 설치 관리자 패키지는 이 환경에서 데이터 공급자가 요구되는 SharePoint 2013 지원 파일을 포함하지 않으므로 지원되지 않습니다.  
  
 **구성 도구:** PowerPivot for SharePoint 2013 구성 도구는 SharePoint 서버 중 하나 에서만 필요 합니다. 그러나 다중 서버 팜에서 권장되는 최선의 구현 방법은 두 서버 중 하나가 오프라인일 때 구성 도구에 액세스할 수 있도록 최소 2개 이상의 서버에 구성 도구를 설치하는 것입니다.  
  
##  <a name="bkmk_prereq"></a> 요구 사항 및 필수 구성 요소  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013  
  
-   SharePoint 제품 및 기술 요구 사항에 따라**spPowerPivot.msi** 는 64비트 전용입니다.  
  
-   PowerPivot 모드의 [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] 서버. Excel Services에서는 SQL Server Analysis Services 인스턴스를 PowerPivot 서버로 사용합니다. Analysis Services는 로컬 컴퓨터 또는 원격 컴퓨터에서 실행할 수 있습니다.  
  
-   **사용 권한:** 설치 하려면 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)], 현재 사용자 컴퓨터에서 SharePoint 팜 관리자 그룹에 관리자 권한이 필요 합니다.  
  
-   에 대 한 자세한 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 로 이동 하는 요구 사항 및 필수 조건 [하드웨어 및 소프트웨어 요구 사항 SharePoint 모드의 Analysis Services 서버에 대 한 &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md)합니다.  
  
##  <a name="bkmk_install"></a> SharePoint 용 PowerPivot을 설치 하려면  
 **spPowerpivot.msi** 설치 관리자 패키지는 그래픽 사용자 인터페이스 및 명령줄 설치 모드를 둘 다 지원합니다. 두 설치 방법 모두 관리자 권한으로 .msi를 실행해야 합니다. 설치 후 구성 도구 및 추가 기능에 자세한 내용은 다음 항목을 참조 [PowerPivot 구성 및 솔루션 배포 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)합니다.  
  
### <a name="user-interface-installation"></a>사용자 인터페이스 설치  
 그래픽 사용자 인터페이스를 사용하여 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 을 설치하려면 다음 단계를 완료하세요.  
  
1.  **SpPowerPivot.msi**를 실행합니다.  
  
2.  시작 페이지에서 **다음** 을 클릭합니다.  
  
3.  사용권 계약을 검토하고 이에 동의한 후 **다음**을 클릭합니다.  
  
4.  **기능 선택** 페이지에서 모든 기능이 기본적으로 선택되어 있습니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  **설치** 를 클릭하여 설치하고 설치를 완료합니다.  
  
### <a name="command-line-installation"></a>명령줄 설치  
 명령줄 설치의 경우 관리 권한으로 명령 프롬프트를 연 다음 **spPowerPivot.msi**를 실행합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 `Msiexec.exe /i SpPowerPivot.msi`항목을 참조하세요.  
  
 설치 로그를 만들려면 표준 MsiExec 로깅 스위치를 사용합니다. 다음 예제에서는 "Install_Log.txt" "v" 자세한 로깅 스위치를 사용 하 여 로그 파일을 만듭니다.  
  
```  
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>스크립팅을 위한 자동 명령줄 설치  
 대화 상자 또는 경고가 표시되지 않는 "자동" 설치를 위해 **/q** 또는 **/quiet** 스위치를 사용할 수 있습니다. 자동 설치는 추가 기능 설치를 스크립팅하려는 경우에 유용합니다.  
  
> [!IMPORTANT]  
>  자동 명령줄 설치를 위해 **/q** 스위치를 사용할 경우 최종 사용자 사용권 계약이 표시되지 않습니다. 설치 방법에 관계없이 본 소프트웨어의 설치는 사용권 계약에 의해 제한되며 사용자는 사용권 계약을 준수해야 합니다.  
  
 **자동 설치를 수행하려면**  
  
1.  **관리자 권한으로**명령 프롬프트를 엽니다.  
  
2.  다음 명령을 실행합니다.  
  
    ```  
    Msiexec.exe /i spPowerPivot.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>특정 구성 요소를 포함하는 명령줄 설치  
 모든 SharePoint 서버에 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 구성 도구가 필요한 것은 아닙니다. 그러나 구성 도구가 필요한 경우 사용할 수 있도록 최소 2개 이상의 서버에 설치하는 것이 좋습니다.  
  
 spPowerPivot.msi를 설치하는 경우 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 구성 도구가 아닌 데이터 공급자 등의 특정 항목을 설치하는 명령줄 옵션을 사용할 수 있습니다. 다음 명령줄은 구성 도구를 제외하고 모든 구성 요소를 설치하는 예입니다.  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=" SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common"  
```  
  
|옵션|Description|  
|------------|-----------------|  
|Analysis_Server_SP_addin|PowerPivot 구성|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|ADOMD.net 공급자|  
|SQL_AMO|AMO 공급자|  
|SQLAS_SP_Common|SharePoint 2013용 Analysis Services 일반 구성 요소|  
  
##  <a name="bkmk_deploy_solution"></a> SharePoint 2013 구성 도구에 대 한 PowerPivot 사용 하 여 SharePoint 솔루션 파일 배포  
 spPowerPivot.msi에서 하드 드라이브에 복사하는 파일 중 3개는 SharePoint 솔루션 파일입니다. 솔루션 파일의 범위는 웹 애플리케이션 수준이지만 다른 파일의 범위는 팜 수준입니다. 파일은 다음과 같습니다.  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 솔루션 파일은 다음 폴더에 복사됩니다.  
  
 `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 .msi 설치에 따라 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 구성 도구를 실행하여 SharePoint 팜의 솔루션을 구성하고 배포합니다.  
  
 **구성 도구를 시작하려면**  
  
 Windows 시작 화면에서 "power"를 입력 앱 검색 결과에서 클릭 **SharePoint 용 PowerPivot 2013 구성**합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 SharePoint 2010 및 SharePoint 2013에 대해 별개의 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구를 설치하기 때문에 검색 결과에 두 개의 링크가 포함될 수 있습니다. SharePoint 2013용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구를 시작하는지 확인하세요.  
  
 ![두 개의 powerpivot 구성 도구](../../../analysis-services/media/as-powerpivot-configtools-bothicons.gif "두 개의 powerpivot 구성 도구")  
  
 **Or**  
  
1.  **시작**, **모든 프로그램**으로 이동합니다.  
  
2.  **Microsoft SQL Server 2014**를 클릭합니다.  
  
3.  **구성 도구**를 클릭합니다.  
  
4.  **SharePoint 2013용 PowerPivot 구성**을 클릭합니다.  
  
 구성 도구에 대한 자세한 내용은 [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md)를 참조하세요.  
  
##  <a name="bkmk_remove_addin"></a> 추가 기능 제거 또는 복구  
  
> [!CAUTION]  
>  **spPowerPivot.msi** 를 제거하는 경우 데이터 공급자 및 구성 도구가 제거됩니다. 데이터 공급자를 제거하면 서버가 PowerPivot에 연결할 수 없게 됩니다.  
  
 다음 방법 중 하나를 사용하여 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 을 제거하거나 복구할 수 있습니다.  
  
1.  **Windows 제어판:** 선택 **SharePoint 2013 용 Microsoft SQL Server 2012 PowerPivot**합니다. **제거** 또는 **복구**를 클릭합니다.  
  
2.  spPowerPivot.msi를 실행하고 **제거** 옵션 또는 **복구** 옵션을 선택합니다.  
  
 **명령줄:** 를 복구 하거나 명령줄을 사용 하 여 SharePoint 2013 용 PowerPivot을 제거 하려면 명령 프롬프트를 열고 **관리자 권한으로** 다음 명령 중 하나를 실행 합니다.  
  
-   복구하려면 다음 명령을 실행합니다.  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 또는  
  
-   제거하려면 다음 명령을 실행합니다.  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  
