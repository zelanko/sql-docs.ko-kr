---
title: Microsoft Azure 가상 머신에 SQL Server 데이터베이스 배포 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploymentwizard.deploymentsettings.f1
- sql12.swb.deploymentwizard.progress.f1
- sql11.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.f1
- sql12.swb.deploymentwizard.azuresignin.f1
- sql11.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.azuresignin.f1
- sql12.swb.deploymentwizard.f1
- sql12.swb.sqlvmdialog.f1
- sql11.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.results.f1
- sql11.swb.deploymentwizard.progress.f1
- sql12.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.sourcesettings.f1
- sql12.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.sourcesettings.f1
- sql11.swb.deploymentwizard.results.f1
- sql12.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.deploymentsettings.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7d84fbe56d36bd91f2b7f8b49a3df73fb383c6e
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175733"
---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>Microsoft Azure 가상 머신에 SQL Server 데이터베이스 배포
  **AZURE vm에 SQL Server 데이터베이스 배포** 마법사를 사용 하 여 azure Vm (가상 머신)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 데이터베이스를 배포할 수 있습니다. 마법사는 전체 데이터베이스 백업 작업을 사용하므로 SQL Server 사용자 데이터베이스에서 전체 데이터베이스 스키마 및 데이터를 항상 복사합니다. 마법사에서는 사용자의 편의를 위해 모든 Azure VM 구성을 실행하므로 VM을 미리 구성할 필요가 없습니다.  
  
 마법사는 같은 데이터베이스 이름을 가진 기존 데이터베이스를 덮어쓰지 않으므로 차등 백업을 위해 마법사를 사용할 수 없습니다. VM에서 기존 데이터베이스를 바꾸려면 먼저 기존 데이터베이스를 삭제하거나 데이터베이스 이름을 변경해야 합니다. 진행 중인 배포 작업의 데이터베이스 이름과 VM의 기존 데이터베이스 간에 이름 충돌이 발생할 경우 마법사에서는 작업을 완료할 수 있도록 진행 중인 데이터베이스에 대해 추가된 데이터베이스 이름을 제안합니다.  
  
##  <a name="before_you_begin"></a> 시작하기 전에  
 이 마법사를 완료하려면 다음 정보를 제공하고 이러한 구성 설정을 마련해야 합니다.  
  
-   Azure 구독과 관련 된 Microsoft 계정 세부 정보입니다.  
  
-   Azure 게시 프로필.  
  
    > [!CAUTION]  
    >  SQL Server는 현재 프로필 버전 2.0 게시를 지원합니다. 게시 프로필의 지원되는 버전을 다운로드하려면 [게시 프로필 2.0 다운로드](https://go.microsoft.com/fwlink/?LinkId=396421)를 참조하세요.  
  
-   Azure 구독에 업로드 된 관리 인증서입니다.  
  
-   마법사가 실행 중인 컴퓨터에서 개인 인증서 저장소에 저장된 관리 인증서입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 호스팅되는 컴퓨터에서 사용할 수 있는 임시 저장소 위치가 있어야 합니다. 임시 스토리지 위치는 마법사를 실행 중인 컴퓨터에서도 사용할 수 있어야 합니다.  
  
-   데이터베이스를 기존의 VM에 배포하는 경우 TCP/IP 포트를 수신하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 구성해야 합니다.  
  
-   VM을 생성 하는 데 사용할 Azure VM 또는 갤러리 이미지에 SQL Server 클라우드 어댑터 구성 되 고 실행 중 이어야 합니다.  
  
-   개인 포트 11435을 사용 하 여 Azure 게이트웨이에서 SQL Server 클라우드 어댑터에 대해 열린 끝점을 구성 해야 합니다.  
  
 또한 데이터베이스를 기존 Azure VM에 배포 하려는 경우 다음을 제공할 수 있어야 합니다.  
  
-   VM을 호스팅하는 클라우드 서비스의 DNS 이름.  
  
-   VM에 대한 관리자 자격 증명.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원본 인스턴스에서 배포할 데이터베이스에 대한 백업 운영자 권한의 자격 증명.  
  
 Azure 가상 컴퓨터에서 SQL Server를 실행 하는 방법에 대 한 자세한 내용은 [azure Virtual Machines에서 SQL Server로 마이그레이션 준비](https://msdn.microsoft.com/library/dn133142.aspx)하기를 참조 하세요.  
  
 Windows Server 운영 체제를 실행 중인 컴퓨터에서 다음 구성 설정을 사용하여 이 마법사를 실행해야 합니다.  
  
-   보안 강화 구성 해제: 서버 관리자 사용 > Internet Explorer ESC(보안 강화 구성)를 설정할 로컬 서버 **해제**  
  
-   JavaScript 사용:  Internet Explorer > 인터넷 옵션 > 보안 > 사용자 지정 수준 > 스크립팅 > 액티브 스크립팅: **사용**  
  
###  <a name="limitations"></a> 제한 사항  
 이 작업에 대한 데이터베이스 크기 제한은 1TB입니다.  
  
 이 배포 기능은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]용 SQL Server Management Studio에서 사용할 수 있습니다.  
  
 이 배포 기능은 사용자 데이터베이스에서만 사용할 수 있습니다. 시스템 데이터베이스 배포는 지원되지 않습니다.  
  
 배포 기능은 선호도 그룹이 연관되어 있는 호스팅된 서비스를 지원하지 않습니다. 예를 들어, 선호도 그룹과 연관된 스토리지 계정은 이 마법사의 **배포 설정** 페이지에서 사용하도록 선택할 수 없습니다.  
  
 VM의 SQL Server 버전이 원본 SQL Server 버전과 동일하거나 최신 버전이어야 합니다. 이 마법사를 사용 하 여 Azure VM에 배포할 수 있는 데이터베이스 버전을 SQL Server 합니다.  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 Azure VM 데이터베이스에서 실행 되는 SQL Server 데이터베이스 버전은 다음에 배포할 수 있습니다.  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 진행 중인 배포 작업의 데이터베이스 이름과 VM의 기존 데이터베이스 간에 이름 충돌이 발생할 경우 마법사에서는 작업을 완료할 수 있도록 진행 중인 데이터베이스에 대해 추가된 데이터베이스 이름을 제안합니다.  
  
###  <a name="filestream"></a> Azure VM에 FILESTREAM 사용 데이터베이스를 배포하기 위한 고려 사항  
 FILESTREAM 개체에 BLOB이 저장된 데이터베이스 배포 시 다음 지침 및 제한 사항을 참조하세요.  
  
-   배포 기능을 통해 새 VM으로 FILESTREAM 사용 데이터베이스를 배포할 수 없습니다. 마법사를 실행하기 전에는 VM에서 FILESTREAM을 사용할 수 없는 경우 데이터베이스 복원 작업이 실패하고 마법사 작업을 성공적으로 완료할 수 없습니다. FILESTREAM을 사용하는 데이터베이스를 성공적으로 배포하려면 마법사를 실행하기 전에 호스트 VM의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 FILESTREAM을 사용하도록 설정하세요. 자세한 내용은 [FILESTREAM(SQL Server)](https://msdn.microsoft.com/library/gg471497.aspx)을 참조하세요.  
  
-   데이터베이스에서 메모리 내 OLTP를 활용하는 경우 데이터베이스를 수정하지 않고도 Azure VM에 데이터베이스를 배포할 수 있습니다. 자세한 내용은 [메모리 내 OLTP(메모리 내 최적화)](https://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx)를 참조하세요.  
  
###  <a name="geography"></a> 자산의 지리적 분포에 대한 고려 사항  
 다음 자산은 동일한 지역에 위치해야 합니다.  
  
-   클라우드 서비스  
  
-   VM 위치  
  
-   데이터 디스크 스토리지 서비스  
  
 위에 나열된 자산이 동일한 위치에 없으면 마법사를 성공적으로 완료할 수 없습니다.  
  
###  <a name="configuration_settings"></a> 마법사 구성 설정  
 다음 구성 정보를 사용하여 Azure VM에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 배포 설정을 수정합니다.  
  
-   **구성 파일 기본 경로** - %LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM\DeploymentSettings.xml  
  
-   **구성 파일 구조**  
  
    -   \<DeploymentSettings>  
  
        -   <OtherSettings  
  
            -   TraceLevel="Debug" \<!-- 로깅 수준 -->  
  
            -   BackupPath="\\\\[server name]\\[volume]\\" \<!-- 백업에 사용된 마지막 경로입니다. 마법사에서 기본값으로 사용됩니다. -->  
  
            -   CleanupDisabled = False/> \<!--마법사는 중간 파일 및 Azure 개체 (VM, CS, SA)를 삭제 하지 않습니다. -->  
  
        -   <PublishProfile \<!-- 마지막으로 사용된 게시 프로필 정보입니다. -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- 마법사에서 사용할 인증서입니다. -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- 마법사에서 사용할 구독입니다. -->  
  
            -   Name="My Subscription" \<!-- 구독 이름입니다. -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **구성 파일 값**  
  
###  <a name="permissions"></a> 사용 권한  
 배포 중인 데이터베이스는 정상 상태에 있어야 하고 데이터베이스는 마법사를 실행 중인 사용자 계정에 액세스할 수 있어야 하며 사용자 계정은 백업 작업을 수행할 권한이 있어야 합니다.  
  
##  <a name="launch_wizard"></a>Azure VM에 데이터베이스 배포 마법사 사용  
 **마법사를 시작하려면 다음 단계를 따르십시오.**  
  
1.  SQL Server Management Studio를 사용하여 배포하려는 데이터베이스가 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 연결합니다.  
  
2.  **개체 탐색기**에서 인스턴스 이름을 확장한 다음 **데이터베이스** 노드를 확장합니다.  
  
3.  배포 하려는 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **작업**을 선택한 다음 **Azure VM에 데이터베이스 배포 ...를** 선택 합니다.  
  

  
##  <a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 **AZURE VM에 SQL Server 데이터베이스 배포** 마법사에 대해 설명 합니다.  
  
 **옵션**  
  
-   **이 페이지를 다시 표시 안 함** - 앞으로 소개 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
-   **다음** - **소스 설정** 페이지로 진행합니다.  
  
-   **취소** - 작업을 취소하고 마법사를 닫습니다.  
  
-   **도움말** -마법사에 대 한 MSDN 도움말 항목을 시작 합니다.  
  
##  <a name="Source_settings"></a> 소스 설정  
 이 페이지를 사용 하 여 Azure VM에 배포 하려는 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다. 또한 파일을 Azure로 전송 하기 전에 로컬 컴퓨터에서 저장할 파일의 임시 위치를 지정 합니다. 이 위치는 공유 네트워크 위치일 수 있습니다.  
  
 **옵션**  
  
-   **연결 ...** 을 클릭 한 다음 배포할 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대 한 연결 세부 정보를 지정 합니다.  
  
-   **데이터베이스 선택** 드롭다운 목록을 사용하여 배포할 데이터베이스를 지정합니다.  
  
-   **기타 설정** 필드에서 Azure VM 서비스에 액세스할 수 있는 공유 폴더를 지정 합니다.  
  
##  <a name="Azure_sign-in"></a>Azure 로그인  
 이 페이지를 사용 하 여 Azure에 연결 하 고 관리 인증서 또는 게시 프로필 세부 정보를 제공 합니다.  
  
 **옵션**  
  
-   **관리 인증서** -이 옵션을 사용 하 여 Azure의 관리 인증서와 일치 하는 로컬 인증서 저장소의 인증서를 지정 합니다.  
  
-   **게시 프로필** -이미 게시 프로필을 컴퓨터에 다운로드 한 경우이 옵션을 사용 합니다.  
  
-   **로그인** -이 옵션을 사용 하 여 Microsoft 계정 (예: Live ID 또는 Hotmail 계정)를 사용 하 여 Azure에 로그인 하 고 새 관리 인증서를 생성 하 고 다운로드 합니다. 구독당 인증서 수는 제한됩니다.  
  
-   **구독** -로컬 인증서 저장소 또는 게시 프로필의 관리 인증서와 일치 하는 AZURE 구독 ID를 선택, 입력 또는 붙여 넣습니다.  
  
##  <a name="Deployment_settings"></a> 배포 설정 페이지  
 이 페이지에서는 대상 서버를 지정하고 새 데이터베이스에 대한 세부 정보를 제공할 수 있습니다.  
  
 **옵션**  
  
-   **Azure 가상 머신** -SQL Server 데이터베이스를 호스팅할 VM에 대 한 세부 정보를 지정 합니다.  
  
-   **클라우드 서비스 이름** -VM을 호스트 하는 서비스의 이름을 지정 합니다. 새 클라우드 서비스를 만들려면 새 클라우드 서비스의 이름을 지정합니다.  
  
-   **가상 컴퓨터 이름** -SQL Server 데이터베이스를 호스팅할 VM의 이름을 지정 합니다. 새 Azure VM을 만들려면 새 VM의 이름을 지정 합니다.  
  
-   **설정** -설정 단추를 사용 하 여 SQL Server 데이터베이스를 호스트할 새 VM을 만듭니다. 기존 VM을 사용하는 경우 사용자가 제공하는 정보를 사용하여 자격 증명을 인증합니다.  
  
-   **저장소 계정** -드롭다운 목록에서 저장소 계정을 선택 합니다. 새 스토리지 계정을 만들려면 새 계정의 이름을 지정합니다. 선호도 그룹과 연관된 스토리지 계정은 드롭다운 목록에서 사용할 수 없습니다.  
  
-   **대상 데이터베이스** -대상 데이터베이스에 대 한 세부 정보를 지정 합니다.  
  
-   **서버 연결** -서버에 대 한 연결 정보입니다.  
  
-   **데이터베이스** -새 데이터베이스의 이름을 지정 하거나 확인 합니다. 데이터베이스 이름이 대상 SQL Server 인스턴스에 이미 있는 경우 수정된 데이터베이스 이름을 지정하는 것이 좋습니다.  
  
##  <a name="Summary"></a> 요약 페이지  
 이 페이지에서 작업에 대해 지정한 설정을 검토할 수 있습니다. 지정한 설정을 사용하여 배포 작업을 완료하려면 **마침**을 클릭합니다. 배포 작업을 취소하고 마법사를 종료하려면 **취소**를 클릭합니다.  
  
 Azure VM의 SQL Server 데이터베이스에 데이터베이스 세부 정보를 배포 하는 데 필요한 수동 단계가 있을 수 있습니다. 이러한 단계를 자세히 설명하겠습니다.  
  
##  <a name="Results"></a> 결과 페이지  
 이 페이지에서는 배포 작업의 성공 또는 실패를 보고하고 각 작업의 결과를 보여 줍니다. 오류가 발생한 동작에는 모두 **결과** 열에 표시가 있습니다. 링크를 클릭하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **마침** 을 클릭하여 마법사를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server용 클라우드 어댑터](../../database-engine/cloud-adapter-for-sql-server.md)   
 [데이터베이스 수명 주기 관리](../database-lifecycle-management.md)   
 [데이터 계층 애플리케이션 내보내기](../data-tier-applications/export-a-data-tier-application.md)   
 [BACPAC 파일을 가져와 새 사용자 데이터베이스 만들기](../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Azure SQL 데이터베이스 백업 및 복원](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [Azure Virtual Machines에서 SQL Server 배포](https://msdn.microsoft.com/library/dn133141.aspx)   
 [Azure Virtual Machines에서 SQL Server로 마이그레이션 준비](https://msdn.microsoft.com/library/dn133142.aspx)  
  
  
