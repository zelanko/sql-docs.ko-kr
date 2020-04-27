---
title: DAC를 사용하여 데이터베이스 배포 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbdeployment.settings.f1
- sql12.swb.dbdeployment.progress.f1
- sql12.swb.dbdeployment.summary.f1
- sql12.swb.dbdeployment.results.f1
- sql12.swb.dbdeployment.welcome.f1
helpviewer_keywords:
- deploy database wizard
- database deploy [SQL Server]
ms.assetid: 08c506e8-4ba0-4a19-a066-6e6a5c420539
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2dfc75b2af19165931dc50e76f04bc7362b59ea8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62873054"
---
# <a name="deploy-a-database-by-using-a-dac"></a>DAC를 사용 하여 데이터베이스 배포
  **SQL Azure에 데이터베이스 배포** 마법사를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스와 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버 간에 또는 두 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]서버 간에 데이터베이스를 배포합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeBegin"></a> 시작하기 전에  
 마법사는 DAC(데이터 계층 애플리케이션) BACPAC 아카이브 파일을 사용하여 데이터 및 데이터베이스 개체의 데이터 및 정의를 배포합니다. 원본 데이터베이스에서 DAC 내보내기 작업과 대상으로 DAC 가져오기 작업을 수행합니다.  
  
###  <a name="database-options-and-settings"></a><a name="DBOptSettings"></a> 데이터베이스 옵션 및 설정  
 기본적으로 배포 중에 생성된 데이터베이스에는 CREATE DATABASE 문의 기본 설정이 적용됩니다. 예외는 데이터베이스 데이터 정렬 및 호환성 수준이 원본 데이터베이스의 값으로 설정된다는 점입니다.  
  
 TRUSTWORTHY, DB_CHAINING 및 HONOR_BROKER_PRIORITY와 같은 데이터베이스 옵션은 배포 프로세스 도중 조정할 수 없습니다. 파일 그룹의 수, 파일의 수 및 크기와 같은 물리적 속성은 배포 프로세스 도중 변경할 수 없습니다. 배포가 완료된 후 ALTER DATABASE 문, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell을 사용하여 데이터베이스를 맞춤 구성할 수 있습니다.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 제한 사항  
 **데이터베이스 배포** 마법사는 다음과 같은 데이터베이스 배포를 지원합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에서 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]로 배포  
  
-   [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스로 배포  
  
-   두 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버 간에 배포  
  
 마법사는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 두 인스턴스 간의 배포를 지원하지 않습니다.  
  
 마법사를 작동하려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4(서비스 팩 4) 이상을 실행하고 있어야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 데이터베이스에 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 지원되지 않는 개체가 포함되는 경우 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 데이터베이스를 배포하는 데 마법사를 사용할 수 없습니다. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 의 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되지 않는 개체가 포함되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 데이터베이스를 배포하는 데 마법사를 사용할 수 없습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 보안을 개선하기 위해 SQL Server 인증 로그인은 암호 없이 DAC BACPAC 파일에 저장됩니다. BACPAC를 가져오면 생성된 암호와 함께 비활성 로그인이 생성됩니다. 로그인을 활성화하려면 ALTER ANY LOGIN 권한이 있는 로그인을 사용하여 로그인하고 ALTER LOGIN을 사용하여 로그인을 활성화하여 사용자에게 알려 줄 수 있는 새 암호를 할당합니다. Windows 인증 로그인의 경우 암호가 SQL Server에서 관리되지 않으므로 이 과정이 필요 없습니다.  
  
#### <a name="permissions"></a>사용 권한  
 마법사에 원본 데이터베이스에 대한 DAC 내보내기 권한이 필요합니다. 로그인하려면 **sys.sql_expression_dependencies**에 대한 SELECT 권한뿐만 아니라 최소한 ALTER ANY LOGIN 및 데이터베이스 범위 VIEW DEFINITION 권한이 있어야 합니다. DAC를 내보내려면 securityadmin 고정 서버 역할의 멤버이면서 DAC를 내보내는 데이터베이스의 database_owner 고정 데이터베이스 역할의 멤버여야 합니다. sysadmin 고정 서버 역할의 멤버 또는 기본 제공 SQL Server 시스템 관리자 계정인 **sa** 는 DAC를 내보낼 수 있습니다.  
  
 마법사에 대상 인스턴스 또는 서버에 대한 DAC 가져오기 권한이 필요합니다. 로그인은 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버이거나 **dbcreator** 고정 서버 역할에 포함되고 ALTER ANY LOGIN 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sa **라는 기본 제공** 시스템 관리자 계정도 DAC를 가져올 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 대한 로그인이 있는 DAC를 가져오려면 loginmanager 또는 serveradmin 역할의 멤버 자격이 필요합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 대한 로그인이 없는 DAC를 가져오려면 dbmanager 또는 serveradmin 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-the-deploy-database-wizard"></a><a name="UsingDeployDACWizard"></a> 데이터베이스 배포 마법사 사용  
 **데이터베이스 배포 마법사를 사용하여 데이터베이스를 마이그레이션하려면**  
  
1.  배포하려는 데이터베이스의 위치에 연결합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 서버를 지정할 수 있습니다.  
  
2.  **개체 탐색기**에서 데이터베이스가 있는 인스턴스에 대한 노드를 확장합니다.  
  
3.  **데이터베이스** 노드를 확장합니다.  
  
4.  배포하려는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음, **SQL Azure에 데이터베이스 배포...** 를 선택합니다.  
  
5.  다음 마법사 대화 상자를 완료합니다.  
  
    -   [소개 페이지](#Introduction)  
  
    -   [배포 설정](#Deployment_settings)  
  
    -   [요약 페이지](#Summary)  
  
    -   [결과](#Results)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 **데이터베이스 배포** 마법사의 단계를 설명합니다.  
  
 **옵션**  
  
-   **이 페이지를 다시 표시 안 함** - 앞으로 소개 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
-   **다음** - **배포 설정** 페이지로 진행합니다.  
  
-   **취소** -작업을 취소 하 고 마법사를 닫습니다.  
  
##  <a name="deployment-settings-page"></a><a name="Deployment_settings"></a>배포 설정 페이지  
 이 페이지에서는 대상 서버를 지정하고 새 데이터베이스에 대한 세부 정보를 제공할 수 있습니다.  
  
 **로컬 호스트:**  
  
-   **서버 연결** – 서버 연결 세부 정보를 지정한 다음, **연결** 을 클릭하여 연결을 확인합니다.  
  
-   **새 데이터베이스 이름** – 새 데이터베이스 이름을 지정합니다.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]데이터베이스 설정:**  
  
-   버전-드롭다운 메뉴 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에서 버전을 선택 합니다. ** [!INCLUDE[ssSDS](../../includes/sssds-md.md)] **  
  
-   **최대 데이터베이스 크기** – 드롭다운 메뉴에서 최대 데이터베이스 크기를 선택합니다.  
  
 **기타 설정:**  
  
-   BACPAC 아카이브 파일인 임시 파일의 로컬 디렉터리를 지정합니다. 지정된 위치에 파일이 만들어지고 작업이 완료된 후에도 해당 위치에 유지됩니다.  
  
##  <a name="summary-page"></a><a name="Summary"></a> 요약 페이지  
 이 페이지에서 작업에 대해 지정한 원본 및 대상 설정을 검토할 수 있습니다. 지정한 설정을 사용하여 배포 작업을 완료하려면 **마침**을 클릭합니다. 배포 작업을 취소하고 마법사를 종료하려면 **취소**를 클릭합니다.  
  
##  <a name="progress-page"></a><a name="Progress"></a>진행률 페이지  
 이 페이지에는 작업 상태를 나타내는 진행률 표시줄이 표시됩니다. 자세한 상태를 보려면 **자세히 보기** 옵션을 클릭합니다.  
  
##  <a name="results-page"></a><a name="Results"></a>결과 페이지  
 이 페이지에서는 배포 작업의 성공 또는 실패를 보고하고 각 작업의 결과를 보여 줍니다. 오류가 발생한 동작에는 모두 **결과** 열에 링크가 있습니다. 링크를 클릭하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **마침** 을 클릭 하 여 마법사를 닫습니다.  
  
## <a name="using-a-net-framework-application"></a>.Net Framework 애플리케이션 사용  
 **.Net Framework 애플리케이션에서 DacStoreExport() 및 Import() 메서드를 사용하여 데이터베이스를 배포합니다.**  
  
 코드 예제를 보려면 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=219575)에서 DAC 샘플 애플리케이션을 다운로드합니다.  
  
1.  SMO Server 개체를 만든 후 이 개체를 배포할 데이터베이스를 포함하는 인스턴스 또는 서버로 설정합니다.  
  
2.  `ServerConnection` 개체를 열고 동일한 인스턴스에 연결합니다.  
  
3.  `Export` 형식의 `Microsoft.SqlServer.Management.Dac.DacStore` 메서드를 사용하여 데이터베이스를 BACPAC 파일로 내보냅니다. 내보낼 데이터베이스의 이름과 BACPAC 파일을 배치할 폴더의 경로를 지정합니다.  
  
4.  SMO Server 개체를 만든 다음 대상 인스턴스 또는 서버로 설정합니다.  
  
5.  `ServerConnection` 개체를 열고 동일한 인스턴스에 연결합니다.  
  
6.  `Import` 형식의 `Microsoft.SqlServer.Management.Dac.DacStore` 메서드를 사용하여 BACPAC를 가져옵니다. 내보내기에 의해 생성되는 BACPAC 파일을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 계층 응용 프로그램](data-tier-applications.md)   
 [데이터 계층 응용 프로그램 내보내기](export-a-data-tier-application.md)   
 [BACPAC 파일을 가져와 새 사용자 데이터베이스 만들기](import-a-bacpac-file-to-create-a-new-user-database.md)  
  
  
