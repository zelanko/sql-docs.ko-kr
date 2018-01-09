---
title: "설치 또는 파워 피벗에 대 한 SharePoint 추가 기능을 제거 (SharePoint 2013) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 499e2929691553884a7c52d3d46918455c8d39a8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013"></a>SharePoint용 파워 피벗 추가 기능 설치 또는 제거(SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 응용 프로그램 서버 구성 요소 및 제공 하는 백 엔드 서비스의 컬렉션인 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 데이터 액세스는 [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] 팜 합니다. SharePoint용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 추가 기능(**spPowerpivot.msi**)은 응용 프로그램 서버 구성 요소를 설치하는 데 사용되는 설치 관리자 패키지입니다.  
  
-   이 추가 기능은 SharePoint 2010 배포에 필수적 요소가 아닙니다.  
  
-   이 추가 기능은 SharePoint 2013 및 SharePoint 모드의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 를 포함하는 단일 서버 배포에 필수적 요소가 아닙니다. 이 추가 기능에서 설치하는 구성 요소는 SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버를 설치하면 포함됩니다. 추가 기능이 포함된 배포 다이어그램의 예제를 보려면 [SharePoint의 SQL Server BI 기능에 대한 배포 토폴로지](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26)를 참조하세요.  
  
 **참고:** 이 항목에서는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 솔루션 파일 및 SharePoint 2013용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구 설치에 대해 설명합니다. 설치 후 구성 도구와 추가 기능에 대한 자세한 내용은 [파워 피벗 구성 및 솔루션 배포&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) 항목을 참조하세요.  
  
 **spPowerPivot.msi**를 다운로드하는 방법에 대한 자세한 내용은 [Microsoft® SQL Server® 2014 Microsoft SharePoint®용 파워 피벗®](http://go.microsoft.com/fwlink/?LinkID=324854)을 참조하세요.  
  
 **항목 내용**  
  
-   [배경](#bkmk_background)  
  
-   [spPowerPivot.msi 설치 위치](#bkmk_where_to_install)  
  
-   [요구 사항 및 필수 구성 요소](#bkmk_prereq)  
  
-   [SharePoint용 파워 피벗을 설치하려면](#bkmk_install)  
  
-   [SharePoint 2013용 파워 피벗 구성 도구를 사용하여 SharePoint 솔루션 파일 배포](#bkmk_deploy_solution)  
  
-   [추가 기능 제거 또는 복구](#bkmk_remove_addin)  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013|  
  
##  <a name="bkmk_background"></a> 배경  
  
-   **응용 프로그램 서버:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 기능에는 통합 문서를 데이터 원본으로 사용하는 기능, 예약된 데이터 새로 고침 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 관리 대시보드가 포함됩니다.  
  
     [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 은 Analysis Services 클라이언트 라이브러리를 배포하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 설치 파일을 컴퓨터에 복사하는**Windows Installer 패키지(**spPowerpivot.msi [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] )입니다. 설치 관리자는 SharePoint의 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 기능을 배포 또는 구성하지 않습니다. 다음 구성 요소가 기본적으로 설치됩니다.  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. 이 구성 요소에는 PowerShell 스크립트(.ps1 파일), SharePoint 솔루션 패키지(.wsp) 및 SharePoint 2013 팜에서 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]을 배포하기 위한 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 2013 구성 도구가 포함되어 있습니다.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Analysis Services용 OLE DB 공급자(MSOLAP)  
  
    -   ADOMD.NET 데이터 공급자  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Management Objects  
  
-   **백 엔드 서비스:** Excel용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 를 사용해서 분석 데이터가 포함된 통합 문서를 만들 경우, SharePoint 모드로 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 를 실행하는 BI 서버에 Excel Services가 구성되어 서버 환경에서 데이터에 액세스할 수 있어야 합니다. SharePoint Server 2013이 설치된 컴퓨터 또는 SharePoint 소프트웨어가 설치되지 않은 다른 컴퓨터에서 SQL Server 설치 프로그램을 실행할 수 있습니다. Analysis Services는 SharePoint에 종속성이 없습니다.  
  
     백 엔드 서비스 설치, 제거 및 구성에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
    -   [파워 피벗 모드에서 Analysis Services 설치](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [SharePoint용 파워 피벗 제거](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> spPowerPivot.msi 설치 위치  
 권장되는 최선의 구현 방법은 구성 일치를 위해 응용 프로그램 서버 및 웹 프런트 엔드 서버를 포함하여 SharePoint 팜의 모든 서버에 **spPowerPivot.msi** 를 설치하는 것입니다. 설치 관리자 패키지에는 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 구성 도구뿐만 아니라 Analysis Services 데이터 공급자도 포함되어 있습니다. **spPowerPivot.msi** 를 설치하는 경우 개별 구성 요소를 제외하여 설치를 사용자 지정할 수 있습니다.  
  
 **데이터 공급자:** 여러 SharePoint 및 SQL Server 기술은 Excel Services, PerformancePoint Services 및 Power View 등 Analysis Services 데이터 공급자를 사용합니다. 모든 SharePoint 서버에 **spPowerPivot.msi** 를 설치하면 Analysis Services 데이터 공급자 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 연결의 전체 집합이 팜 전체에서 일관성 있게 제공됩니다.  
  
> [!NOTE]  
>  **spPowerPivot.msi**를 사용하여 SharePoint 2013 서버에 Analysis Services 데이터 공급자를 설치해야 합니다. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 기능 팩에서 사용할 수 있는 다른 설치 관리자 패키지는 이 환경에서 데이터 공급자가 요구되는 SharePoint 2013 지원 파일을 포함하지 않으므로 지원되지 않습니다.  
  
 **구성 도구:** SharePoint 2013용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구는 SharePoint 서버 중 하나에만 있으면 됩니다. 그러나 다중 서버 팜에서 권장되는 최선의 구현 방법은 두 서버 중 하나가 오프라인일 때 구성 도구에 액세스할 수 있도록 최소 2개 이상의 서버에 구성 도구를 설치하는 것입니다.  
  
##  <a name="bkmk_prereq"></a> 요구 사항 및 필수 구성 요소  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013  
  
-   SharePoint 제품 및 기술 요구 사항에 따라**spPowerPivot.msi** 는 64비트 전용입니다.  
  
-   서버에 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모드입니다. Excel Services에서는 SQL Server Analysis Services 인스턴스를 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 서버로 사용합니다. Analysis Services는 로컬 컴퓨터 또는 원격 컴퓨터에서 실행할 수 있습니다.  
  
-   **사용 권한:** [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)]을 설치하려면 현재 사용자가 컴퓨터의 관리자이며 SharePoint 팜 관리자 그룹의 멤버여야 합니다.  
  
-   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 요구 사항 및 필수 조건에 대한 자세한 내용은 [SharePoint 모드의 Analysis Services 서버 하드웨어 및 소프트웨어 요구 사항](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f)을 참조하세요.  
  
##  <a name="bkmk_install"></a> SharePoint용 파워 피벗을 설치하려면  
 **spPowerpivot.msi** 설치 관리자 패키지는 그래픽 사용자 인터페이스 및 명령줄 설치 모드를 둘 다 지원합니다. 두 설치 방법 모두 관리자 권한으로 .msi를 실행해야 합니다. 설치 후 구성 도구와 추가 기능에 대한 자세한 내용은 [파워 피벗 구성 및 솔루션 배포&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) 항목을 참조하세요.  
  
### <a name="user-interface-installation"></a>사용자 인터페이스 설치  
 그래픽 사용자 인터페이스를 사용하여 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 을 설치하려면 다음 단계를 완료하세요.  
  
1.  **SpPowerPivot.msi**를 실행합니다.  
  
2.  시작 페이지에서 **다음** 을 클릭합니다.  
  
3.  사용권 계약을 검토하고 이에 동의한 후 **다음**을 클릭합니다.  
  
4.  **기능 선택** 페이지에서 모든 기능이 기본적으로 선택되어 있습니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  **설치** 를 클릭하여 설치하고 설치를 완료합니다.  
  
### <a name="command-line-installation"></a>명령줄 설치  
 명령줄 설치의 경우 관리 권한으로 명령 프롬프트를 연 다음 **spPowerPivot.msi**를 실행합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
 `Msiexec.exe /i SpPowerPivot.msi`항목을 참조하세요.  
  
 설치 로그를 만들려면 표준 MsiExec 로깅 스위치를 사용합니다. 다음 예에서는 “v” 자세한 로깅 스위치를 사용하는 로그 파일 “Install_Log.txt”를 만듭니다.  
  
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
 모든 SharePoint 서버에 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 구성 도구가 필요한 것은 아닙니다. 그러나 구성 도구가 필요한 경우 사용할 수 있도록 최소 2개 이상의 서버에 설치하는 것이 좋습니다.  
  
 spPowerPivot.msi를 설치하는 경우 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 구성 도구가 아닌 데이터 공급자 등의 특정 항목을 설치하는 명령줄 옵션을 사용할 수 있습니다. 다음 명령줄은 구성 도구를 제외하고 모든 구성 요소를 설치하는 예입니다.  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|옵션|Description|  
|------------|-----------------|  
|Analysis_Server_SP_addin|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Configuration|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|ADOMD.net 공급자|  
|SQL_AMO|AMO 공급자|  
|SQLAS_SP_Common|SharePoint 2013용 Analysis Services 일반 구성 요소|  
  
##  <a name="bkmk_deploy_solution"></a> SharePoint 2013용 파워 피벗 구성 도구를 사용하여 SharePoint 솔루션 파일 배포  
 spPowerPivot.msi에서 하드 드라이브에 복사하는 파일 중 3개는 SharePoint 솔루션 파일입니다. 솔루션 파일의 범위는 웹 응용 프로그램 수준이지만 다른 파일의 범위는 팜 수준입니다. 파일은 다음과 같습니다.  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 솔루션 파일은 다음 폴더에 복사됩니다.  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 .msi 설치에 따라 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 구성 도구를 실행하여 SharePoint 팜의 솔루션을 구성하고 배포합니다.  
  
 **구성 도구를 시작하려면**  
  
 Windows 시작 화면에서 "power"를 입력한 다음 앱 검색 결과에서 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성**을 클릭합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 SharePoint 2010 및 SharePoint 2013에 대해 별개의 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구를 설치하기 때문에 검색 결과에 두 개의 링크가 포함될 수 있습니다. SharePoint 2013용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구를 시작하는지 확인하세요.  
  
 ![두 개의 파워 피벗 구성 도구](../../../analysis-services/instances/install-windows/media/as-powerpivot-configtools-bothicons.gif "두 개의 파워 피벗 구성 도구")  
  
 **Or**  
  
1.  **시작**, **모든 프로그램**으로 이동합니다.  
  
2.  [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]을 클릭합니다.  
  
3.  **구성 도구**를 클릭합니다.  
  
4.  **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성**을 클릭합니다.  
  
 구성 도구에 대한 자세한 내용은 [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)를 참조하십시오.  
  
##  <a name="bkmk_remove_addin"></a> 추가 기능 제거 또는 복구  
  
> [!CAUTION]  
>  **spPowerPivot.msi** 를 제거하는 경우 데이터 공급자 및 구성 도구가 제거됩니다. 데이터 공급자를 제거하면 서버가 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]에 연결할 수 없게 됩니다.  
  
 다음 방법 중 하나를 사용하여 [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 을 제거하거나 복구할 수 있습니다.  
  
1.  **Windows 제어판:** SharePoint 2013용 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 을 선택합니다.** **제거** 또는 **복구**를 클릭합니다.  
  
2.  spPowerPivot.msi를 실행하고 **제거** 옵션 또는 **복구** 옵션을 선택합니다.  
  
 **명령줄:** 명령줄을 사용하여 SharePoint 2013용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 을 복구하거나 제거하려면 **관리자 권한** 으로 명령 프롬프트를 열고 다음 명령 중 하나를 실행합니다.  
  
-   복구하려면 다음 명령을 실행합니다.  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 또는  
  
-   제거하려면 다음 명령을 실행합니다.  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  
