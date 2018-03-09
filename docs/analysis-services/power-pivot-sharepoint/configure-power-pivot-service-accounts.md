---
title: "Power Pivot 서비스 계정 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76a85cd0-af93-40c9-9adf-9eb0f80b30c1
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 590f8ebba552477bf3622570c3cb6aa1e2a73247
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="configure-power-pivot-service-accounts"></a>Power Pivot 서비스 계정 구성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]설치에는 서버 작업을 지원하는 두 서비스가 포함됩니다. **SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])** 서비스는 응용 프로그램 서버에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 처리 및 쿼리 지원을 제공하는 Windows 서비스입니다. 이 서비스의 로그인 계정은 항상 SQL Server 설치 중 SharePoint 통합 모드의 Analysis Services를 설치할 때 지정됩니다.  
  
 SharePoint 팜에서 응용 프로그램 풀 ID로 실행되는 공유 웹 서비스인 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램에 대해 두 번째 계정을 지정해야 합니다. 이 계정은 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]구성 도구 또는 PowerShell을 사용하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치를 구성할 때 지정합니다.  
  
 각 서비스는 팜에서 Kerberos 인증 프로토콜을 사용하거나 연결을 감사할 수 있도록 전용 계정으로 실행되어야 합니다.  
  
 서비스 계정이 설정된 후에는 SharePoint 중앙 관리를 통해서만 계정을 변경할 수 있습니다. 서비스 콘솔 응용 프로그램, IIS 관리자 또는 SQL Server 구성 관리자와 같은 대체 도구를 사용하는 경우 팜의 데이터베이스 액세스 또는 물리적 서버의 로컬 파일 액세스에 대한 사용 권한이 업데이트되지 않습니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [SQL Server Analysis Services(Power Pivot) 인스턴스에 대해 만료된 암호 업데이트](#bkmk_passwordssas)  
  
 [Power Pivot 서비스 응용 프로그램에 대해 만료된 암호 업데이트](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [각 서비스가 실행되는 계정 변경](#bkmk_newacct)  
  
 [Power Pivot 서비스 응용 프로그램에 대한 응용 프로그램 풀 만들기 또는 변경](#bkmk_appPool)  
  
 [계정 요구 사항 및 사용 권한](#requirements)  
  
 [문제 해결: 수동으로 관리 권한 부여](#updatemanually)  
  
 [문제 해결: 중앙 관리 또는 SharePoint Foundation 웹 응용 프로그램 서비스의 암호 만료로 인해 발생한 HTTP 503 오류 해결](#expired)  
  
##  <a name="bkmk_passwordssas"></a> SQL Server Analysis Services(Power Pivot) 인스턴스에 대해 만료된 암호 업데이트  
  
1.  시작을 가리키고 **관리 도구**를 클릭한 다음 **서비스**를 클릭합니다. **SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**를 두 번 클릭합니다. **로그온**을 클릭한 다음 계정의 새 암호를 입력합니다.  
  
2.  중앙 관리의 보안 섹션에서 **관리 계정 구성**을 클릭합니다.  
  
3.  **편집** 을 클릭하여 해당 계정을 변경합니다.  
  
4.  **지금 암호 변경**을 선택합니다.  
  
5.  **계정 암호를 새 값으로 설정**을 선택합니다. 관리 계정에서 실행되는 모든 서비스는 업데이트된 자격 증명을 사용합니다.  
  
##  <a name="bkmk_passwordapp"></a> Power Pivot 서비스 응용 프로그램에 대해 만료된 암호 업데이트  
  
1.  중앙 관리의 보안 섹션에서 **관리 계정 구성**을 클릭합니다.  
  
2.  **편집** 을 클릭하여 해당 계정을 변경합니다.  
  
3.  **지금 암호 변경**을 선택합니다.  
  
4.  **계정 암호를 새 값으로 설정**을 선택합니다. 관리 계정에서 실행되는 모든 서비스는 업데이트된 자격 증명을 사용합니다.  
  
##  <a name="bkmk_newacct"></a> 각 서비스가 실행되는 계정 변경  
  
1.  중앙 관리의 보안 섹션에서 **서비스 계정 구성**을 클릭합니다.  
  
2.  Analysis Services 서비스 계정을 변경하려면 **Windows 서비스 - SQL Server Analysis Services** 를 선택합니다.  
  
3.  **이 서비스에 대한 계정을 선택하십시오**에서 기존 관리 계정을 선택하거나 새 계정을 만듭니다. 계정은 도메인 사용자 계정이어야 합니다.  
  
4.  기본 **서비스 응용 프로그램의 응용 프로그램 풀 ID를 변경하려면** 서비스 응용 프로그램 풀 - SharePoint 웹 서비스 시스템 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 선택합니다. 설치 구성 방식에 따라 서비스가 SharePoint 서비스용으로 만든 기존 서비스 응용 프로그램 풀로 실행될 수 있습니다. 기본적으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구는 서비스를 **기본 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램)**으로 등록합니다.  
  
     SharePoint 관리자가 서비스를 수동으로 구성한 경우 이 서비스에는 자체 서비스 응용 프로그램 풀이 있을 가능성이 높습니다.  
  
5.  **이 서비스에 대한 계정을 선택하십시오**에서 기존 관리 계정을 선택하거나 새 계정을 만듭니다. 계정은 도메인 사용자 계정이어야 합니다.  
  
6.  **확인**을 클릭합니다.  
  
##  <a name="bkmk_appPool"></a> Power Pivot 서비스 응용 프로그램에 대한 응용 프로그램 풀 만들기 또는 변경  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 선택하되 클릭하지는 않습니다. 응용 프로그램 이름을 클릭하면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드가 열립니다. 여기에는 응용 프로그램 풀을 지정하는 속성 페이지에 대한 링크가 없습니다.  행에서 빈 공백을 클릭하거나 유형 이름을 클릭해서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 선택할 수 있습니다.  
  
3.  리본에서 **속성** 을 클릭합니다.  
  
4.  **새 응용 프로그램 풀 만들기**를 선택합니다. 응용 프로그램 풀의 이름을 입력하고 ID로 관리되는 계정을 지정합니다.  
  
##  <a name="requirements"></a> 계정 요구 사항 및 사용 권한  
 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 배포를 계획할 때 다음 서비스 계정을 계획해야 합니다.  
  
-   Analysis Services 서비스 계정. Analysis Services는 팜에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 쿼리 및 데이터 새로 고침 작업을 처리합니다. 이 계정은 SQL Server 설치 프로그램에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 설치할 때 항상 지정됩니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 풀. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램은 팜에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 쿼리 처리를 위한 SharePoint 통합 및 인프라를 제공하는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스와 연결됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램에 대해 지정하는 응용 프로그램 풀은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스의 ID입니다. 팜에서 여러 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 사용할 수 있습니다. 만드는 각 PowerPivot 서비스 응용 프로그램은 자체 응용 프로그램 풀에서 실행됩니다.  
  
#### <a name="analysis-services-service-account"></a>Analysis Services 서비스 계정  
  
|요구 사항|Description|  
|-----------------|-----------------|  
|프로비전 요구 사항|이 계정은 SQL Server 설치 중 설치 마법사의 **Analysis Services - 구성 페이지** 또는 명령줄 설치의 **ASSVCACCOUNT** 설치 매개 변수를 사용하여 지정해야 합니다.<br /><br /> 중앙 관리, PowerShell 또는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 사용하여 사용자 이름 또는 암호를 수정할 수 있습니다. 다른 도구를 사용하여 계정과 암호를 변경할 수는 없습니다.|  
|도메인 사용자 계정 요구 사항|이 계정은 Windows 도메인 사용자 계정이어야 합니다. 기본 제공 컴퓨터 계정(예: 네트워크 서비스 또는 로컬 서비스)은 사용할 수 없습니다. SQL Server 설치 프로그램에서는 컴퓨터 계정이 지정되어 있으면 설치를 차단함으로써 도메인 사용자 계정 요구 사항을 강제 적용합니다.|  
|사용 권한 요구 사항|이 계정은 SQLServerMSASUser $의 구성원 이어야 합니다\<서버 > $PowerPivot 보안 그룹 및 로컬 컴퓨터의 WSS_WPG 보안 그룹입니다. 이러한 사용 권한은 자동으로 부여됩니다. 사용 권한을 확인하거나 부여하는 방법에 대한 자세한 내용은 이 항목에서 [수동으로 파워 피벗 서비스 계정 관리 권한 부여](#updatemanually) 및 [초기 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)을 참조하세요.|  
|확장 요구 사항|팜에 여러 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 인스턴스를 설치할 경우 모든 Analysis Services 서버 인스턴스가 동일한 도메인 사용자 계정으로 실행되어야 합니다. 예를 들어 첫 번째 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 인스턴스가 Contoso\ssas-srv01로 실행되도록 구성한 경우 이후에 동일한 팜에 배포하는 모든 추가 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 인스턴스도 Contoso\ssas-srv01(또는 어떤 계정이든 현재 계정)로 실행되어야 합니다.<br /><br /> 모든 서비스 인스턴스가 동일한 계정으로 실행되도록 구성하면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스에서 쿼리 처리 또는 데이터 새로 고침 작업을 팜에 있는 모든 Analysis Services 서비스 인스턴스에 할당할 수 있습니다. 또한 Analysis Services 서버 인스턴스에 대해 중앙 관리의 관리 계정 기능을 사용할 수 있습니다. 모든 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 인스턴스에 동일한 계정을 사용하는 경우 한 번만 계정이나 암호를 변경하면 해당 자격 증명을 사용하는 모든 서비스 인스턴스가 자동으로 업데이트됩니다.<br /><br /> SQL Server 설치 프로그램은 동일한 계정 요구 사항을 강제 적용합니다. 이미 설치된 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스가 있는 SharePoint 팜에 스케일 아웃 배포하는 경우 지정한 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 계정이 팜에서 이미 사용 중인 계정과 다른 경우 설치 프로그램에서 새 설치를 차단합니다.|  
  
#### <a name="power-pivot-service-application-pool"></a>Power Pivot 서비스 응용 프로그램 풀  
  
|요구 사항|Description|  
|-----------------|-----------------|  
|프로비전 요구 사항|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스는 서비스 응용 프로그램을 만들 때 사용할 수 있는 팜의 공유 리소스입니다. 서비스 응용 프로그램을 만들 때 서비스 응용 프로그램 풀을 지정해야 합니다. 이 풀은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 사용하거나 PowerShell 명령 등의 두 가지 방법으로 지정할 수 있습니다.<br /><br /> 고유 계정으로 실행되도록 응용 프로그램 풀 ID를 구성했을 수 있습니다. 그렇지 않은 경우 다른 계정으로 실행되도록 지금 변경하는 것이 좋습니다.|  
|도메인 사용자 계정 요구 사항|응용 프로그램 풀 ID는 Windows 도메인 사용자 계정이어야 합니다. 기본 제공 컴퓨터 계정(예: 네트워크 서비스 또는 로컬 서비스)은 사용할 수 없습니다.|  
|사용 권한 요구 사항|이 계정에는 컴퓨터에 대한 로컬 시스템 관리자 권한이 필요하지 않습니다. 그러나 이 계정에는 동일한 컴퓨터에 설치된 로컬 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 에 대한 Analysis Services 시스템 관리자 권한이 있어야 합니다. 이러한 권한은 SQL Server 설치 프로그램을 실행하거나 중앙 관리에서 응용 프로그램 풀 ID를 설정 또는 변경할 때 자동으로 부여됩니다.<br /><br /> [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]로 쿼리를 전달하려면 관리 권한이 필요합니다. 상태를 모니터링하고 비활성 세션을 종료하며 추적 이벤트를 수신 대기할 때도 관리 권한이 필요합니다.<br /><br /> 계정에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 데이터베이스에 대한 연결, 읽기 및 쓰기 권한이 있어야 합니다. 이러한 권한은 응용 프로그램을 만들 때 자동으로 부여되며 중앙 관리에서 계정이나 암호를 변경할 때 자동으로 업데이트됩니다.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램은 파일을 검색하기 전에 SharePoint 사용자가 데이터를 볼 권한이 있는지를 확인하지만 사용자를 가장하지는 않습니다. 가장에 대한 사용 권한 요구 사항은 없습니다.|  
|확장 요구 사항|없음|  
  
##  <a name="updatemanually"></a> 문제 해결: 수동으로 관리 권한 부여  
 자격 증명을 업데이트하는 사람이 컴퓨터의 로컬 관리자가 아닌 경우 관리 권한이 업데이트되지 않습니다. 이 경우 관리 권한을 수동으로 부여할 수 있습니다. 가장 쉬운 방법은 중앙 관리에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 타이머 작업을 실행하는 것입니다. 이 방법에서는 팜의 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버에 대한 사용 권한을 다시 설정할 수 있습니다. 이 방법은 SharePoint 타이머 작업이 관리자 및 로컬 관리자 권한으로 실행 중인 경우에만 적용됩니다.  
  
1.  모니터링 중에 **작업 정의 검토**를 클릭합니다.  
  
2.  **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 타이머 작업**을 선택합니다.  
  
3.  **지금 실행**을 클릭합니다.  
  
 마지막 수단으로 Analysis Services 시스템 관리 권한을 부여 하 여 올바른 사용 권한을 확인 수는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 한 다음 추가할 서비스 응용 프로그램 id를 SQLServerMSASUser$\<서버 이름 > $PowerPivot Windows 보안 그룹입니다. SharePoint 팜에 통합되는 모든 Analysis Services 인스턴스에 대해 이 단계를 반복해야 합니다.  
  
 Windows 보안 그룹을 업데이트하려면 로컬 관리자여야 합니다.  
  
1.  SQL Server Management Studio에서으로 Analysis Services 인스턴스에 연결 \<서버 이름 > \POWERPIVOT 합니다.  
  
2.  서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **보안**을 클릭합니다.  
  
4.  **추가**를 클릭합니다.  
  
5.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 풀에 사용되는 계정의 이름을 입력한 다음 **확인**을 클릭합니다.  
  
6.  관리 도구에서 **컴퓨터 관리**를 클릭합니다.  
  
7.  **로컬 사용자 및 그룹**을 엽니다.  
  
8.  **그룹**을 엽니다.  
  
9. SQLServerMSASUser $를 두 번 클릭\<서버 이름 > $PowerPivot 합니다.  
  
10. **추가**를 클릭합니다.  
  
11. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 풀에 사용되는 계정의 이름을 입력한 다음 **확인**을 클릭합니다.  
  
##  <a name="expired"></a> 문제 해결: 중앙 관리 또는 SharePoint Foundation 웹 응용 프로그램 서비스의 암호 만료로 인해 발생한 HTTP 503 오류 해결  
 계정 재설정 또는 암호 만료로 인해 중앙 관리 서비스 또는 SharePoint Foundation 웹 응용 프로그램 서비스가 작동을 중지한 경우 SharePoint 중앙 관리 또는 SharePoint 사이트를 열려고 하면 HTTP 503 "서비스를 사용할 수 없음" 오류 메시지가 표시됩니다. 서버를 다시 온라인으로 연결하려면 다음 단계를 따르십시오. 중앙 관리를 사용할 수 있는 경우 만료된 계정 정보를 업데이트할 수 있습니다.  
  
1.  관리 도구에서 **인터넷 정보 서비스 관리자**를 클릭합니다.  
  
2.  사이트 또는 중앙 관리 응용 프로그램 풀의 ID가 암호가 만료된 도메인 사용자 계정인 경우 다음을 수행하십시오.  
  
    1.  응용 프로그램 풀 이름을 마우스 오른쪽 단추로 클릭하고 **고급 설정**을 선택합니다.  
  
    2.  **ID** 를 선택하고 ... 버튼을 클릭하여 응용 프로그램 풀 ID 대화 상자를 엽니다.  
  
    3.  **설정**을 클릭합니다.  
  
    4.  사용자 이름과 암호를 입력합니다.  
  
3.  IISRESET을 실행합니다. 이렇게 하려면 관리자 명령 프롬프트를 열고 명령에 **iisreset** 을 입력합니다.  
  
4.  SharePoint 중앙 관리의 보안에서 **관리 계정 구성**을 선택합니다.  
  
5.  **편집** 을 클릭하여 암호가 만료된 관리 계정의 정보를 업데이트합니다.  
  
6.  **지금 암호 변경**을 선택합니다.  
  
7.  **기존 암호 사용**을 클릭합니다.  
  
8.  암호를 입력한 다음 **확인**을 클릭합니다.  
  
 Reporting Services를 설치한 경우 Reporting Services 구성 관리자를 사용하여 보고서 서버에 대한 암호와 보고서 서버 데이터베이스에 대한 연결을 업데이트합니다. 자세한 내용은 [보고서 서버의 구성 및 관리&#40;Reporting Services SharePoint 모드&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SharePoint용 PowerPivot 서버 시작 또는 중지](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [Power Pivot 무인 데이터 새로 고침 계정 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
  
