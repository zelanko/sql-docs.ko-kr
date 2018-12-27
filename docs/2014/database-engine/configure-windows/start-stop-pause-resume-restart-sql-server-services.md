---
title: 시작, 중지, 일시 중지, 재개, 데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스를 다시 시작 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8e451c01400fcf32a3676e0904bf44f226718985
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140721"
---
# <a name="start-stop-pause-resume-restart-the-database-engine-sql-server-agent-or-sql-server-browser-service"></a>데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작
  이 항목에서는 시작, 중지, 일시 중지, 재개 또는 다시 시작 하는 방법을 설명 합니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트, 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], **net** 명령 프롬프트에서 명령을 [!INCLUDE[tsql](../../includes/tsql-md.md)], 또는 PowerShell입니다.  
  
-   **시작하기 전 주의 사항:**  
  
    -   [SQL Server Database Engine, SQL Server 에이전트 및 SQL Server Browser 서비스 정의](#Services)  
  
    -   [추가 정보](#MoreInformation)  
  
    -   [보안](#Security)  
  
-   **사용 지침**  
  
    -   [SQL Server 구성 관리자](#SSCMProcedure)  
  
    -   다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [명령 프롬프트 창의 net 명령](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Services"></a>[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스 정의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 Windows 서비스로 실행되는 실행 가능한 프로그램입니다. Windows 서비스로 실행되는 프로그램은 컴퓨터 화면에 작업을 표시하지 않고도 작업을 계속할 수 있습니다.  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스**  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인 실행 가능한 프로세스입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 컴퓨터당 하나로 제한되는 기본 인스턴스이거나 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 명명된 여러 인스턴스 중 하나일 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 컴퓨터에 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 확인할 수 있습니다. 기본 인스턴스(설치한 경우)는 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](MSSQLSERVER)** 로 나열됩니다. 명명된 인스턴스(설치한 경우)는 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](<instance_name>)** 로 나열됩니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express는 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLEXPRESS)** 로 설치됩니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스**  
 작업 및 경고라고 하는 예약된 관리 태스크를 실행하는 Windows 서비스입니다. 자세한 내용은 [SQL Server Agent](../../ssms/agent/sql-server-agent.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 일부 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스에 대해 들어오는 요청을 수신하고 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 정보를 제공하는 Windows 서비스입니다. 컴퓨터에 설치된 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스의 단일 인스턴스가 사용됩니다.  
  
###  <a name="MoreInformation"></a> 추가 정보  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스를 일시 중지하면 새 사용자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 수 없지만 이미 연결되어 있는 사용자는 연결이 끊어질 때까지 계속해서 작업할 수 있습니다. 사용자가 작업을 완료할 때까지 기다렸다가 서비스를 중지하려면 일시 중지를 사용합니다. 이렇게 하면 사용자가 진행 중인 트랜잭션을 완료할 수 있습니다. 재개를 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 새 연결을 다시 허용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 일시 중지하거나 재개할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 다음 아이콘을 사용하여 서비스의 현재 상태를 표시합니다.  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자**  
  
    -   서비스 이름 옆에 녹색 화살표가 있는 아이콘이 표시되면 서비스가 시작된 것입니다.  
  
    -   서비스 이름 옆에 빨간색 사각형이 있는 아이콘이 표시되면 서비스가 중지된 것입니다.  
  
    -   서비스 이름 옆에 두 개의 파란색 세로 선이 있는 아이콘이 표시되면 서비스가 일시 중지된 것입니다.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 다시 시작하면 서비스가 중지되었음을 나타내는 빨간색 사각형이 표시되었다가 서비스가 성공적으로 시작되었음을 나타내는 녹색 화살표가 표시됩니다.  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   서비스 이름 옆의 녹색 원 아이콘에 흰색 화살표가 표시되면 서비스가 시작된 것입니다.  
  
    -   서비스 이름 옆에 흰색 사각형이 있는 빨간색 원 아이콘이 표시되면 서비스가 중지된 것입니다.  
  
    -   서비스 이름 옆에 두 개의 흰색 세로 선이 있는 파란색 원 아이콘이 표시되면 서비스가 일시 중지된 것입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하는 경우 가능한 옵션만 사용할 수 있습니다. 예를 들어 서비스가 이미 시작된 경우 **시작** 은 사용할 수 없습니다.  
  
-   클러스터에서 실행 중인 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스는 클러스터 관리자를 사용하면 가장 완벽하게 관리할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 기본적으로 로컬 Administrators 그룹의 멤버만 서비스를 시작, 중지, 일시 중지, 재개 또는 다시 시작할 수 있습니다. 관리자가 아닌 사용자에게 서비스 관리 권한을 부여하려면 [Windows Server 2003에서 사용자에게 서비스 관리 권한을 부여하는 방법](http://support.microsoft.com/kb/325349)을 참조하세요. 이 프로세스는 다른 Windows 버전에서도 비슷합니다.  
  
 중지를 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 를 사용 하 여 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] `SHUTDOWN` 명령의 멤버 자격이 필요 합니다 **sysadmin** 또는 **serveradmin** 고정 서버 역할 되며 양도할 수 없습니다.  
  
##  <a name="SSCMProcedure"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 사용  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>다음 인스턴스를 시작, 중지, 일시 중지, 재개 또는 다시 시작하기: [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 클릭합니다.  
  
4.  결과 창에서 **SQL Server(MSSQLServer)** 또는 명명된 인스턴스를 마우스 오른쪽 단추로 클릭하고 **시작**, **중지**, **일시 중지**, **재개**또는 **다시 시작**을 클릭합니다.  
  
5.  **확인** 을 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 닫습니다.  
  
> [!NOTE]  
>  시작 옵션을 사용하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스를 시작하려면 [서버 시작 옵션 구성&#40;SQL Server 구성 관리자&#41;](scm-services-configure-server-startup-options.md)을 참조하세요.  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-includessnoversionincludesssnoversion-mdmd-browser-or-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 인스턴스를 시작, 중지, 일시 중지, 재개 또는 다시 시작하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 클릭합니다.  
  
4.  결과 창에서 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser**나 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트(MSSQLServer)** 또는 명명된 인스턴스의 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트(<instance_name>)** 를 마우스 오른쪽 단추로 클릭하고 **시작**, **중지**, **일시 중지**, **재개** 또는 **다시 시작**을 클릭합니다.  
  
5.  **확인** 을 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 닫습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 일시 중지할 수 없습니다.  
  
##  <a name="SSMSProcedure"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio 사용  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>다음 인스턴스를 시작, 중지, 일시 중지, 재개 또는 다시 시작하기: [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결하고 시작할 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **시작**, **중지**, **일시 중지**, **재개**또는 **다시 시작**을 클릭합니다.  
  
     또는 등록된 서버에서 시작할 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭하고 **서비스 제어**를 가리킨 다음 **시작**, **중지**, **일시 중지**, **재개**또는 **다시 시작**을 클릭합니다.  
  
2.  **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.  
  
3.  작업을 수행할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 인스턴스를 시작, 중지 또는 다시 시작하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결하고 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **시작**, **중지**또는 **다시 시작**을 클릭합니다.  
  
2.  **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.  
  
3.  작업을 수행할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
##  <a name="CommandPrompt"></a> 명령 프롬프트 창에서 net 명령 사용  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net [!INCLUDE[msCoName](../../includes/msconame-md.md)] 명령을 사용하여 **,** 서비스를 시작, 중지 또는 일시 중지할 수 있습니다.  
  
###  <a name="dbDefault"></a> 다음 기본 인스턴스 시작하기: [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   명령 프롬프트에서 다음 명령 중 하나를 입력합니다.  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     -또는-  
  
     **net start MSSQLSERVER**  
  
###  <a name="dbNamed"></a> 다음 명명된 인스턴스 시작하기: [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   명령 프롬프트에서 다음 명령 중 하나를 입력합니다. *\<instancename>* 을 관리할 인스턴스의 이름으로 바꿉니다.  
  
     **net start "SQL Server (** *instancename* **)"**  
  
     -또는-  
  
     **net start MSSQL$** *instancename*  
  
###  <a name="dbStartup"></a> 시작 옵션으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 시작하려면  
  
-   **net start "SQL Server (MSSQLSERVER)"** 문 끝에 공백으로 구분된 시작 옵션을 추가합니다. **net start**를 사용하여 시작하는 경우에는 시작 옵션에 하이픈(-) 대신 슬래시(/)를 사용합니다.  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     -또는-  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  시작 옵션에 대한 자세한 내용은 [데이터베이스 엔진 서비스 시작 옵션](database-engine-service-startup-options.md)을 참조하세요.  
  
###  <a name="agDefault"></a> 시작 옵션으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   명령 프롬프트에서 다음 명령 중 하나를 입력합니다.  
  
     **net start "SQL Server Agent (MSSQLSERVER)"**  
  
     -또는-  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="agNamed"></a> 시작 옵션으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 명명된 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   명령 프롬프트에서 다음 명령 중 하나를 입력합니다. *instancename* 을 관리할 인스턴스 이름으로 바꿉니다.  
  
     **net start "SQL Server Agent(** *instancename* **)"**  
  
     -또는-  
  
     **net start SQLAgent$** *instancename*  
  
 문제 해결을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 세부 정보 표시 모드로 실행하는 방법은 [sqlagent90 애플리케이션](../../tools/sqlagent90-application.md)을 참조하세요.  
  
###  <a name="Browser"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser를 시작하려면  
  
-   명령 프롬프트에서 다음 명령 중 하나를 입력합니다.  
  
     **net start "SQL Server Browser"**  
  
     -또는-  
  
     **net start SQLBrowser**  
  
###  <a name="pauseStop"></a> 명령 프롬프트 창에서 서비스를 일시 중지하거나 중지하려면  
  
-   서비스를 일시 중지하거나 중지하려면 다음과 같은 방법으로 명령을 수정합니다.  
  
    -   서비스를 일시 중지하려면 **net start** 를 **net pause**로 바꿉니다.  
  
    -   서비스를 중지하려면 **net start** 를 **net stop**으로 바꿉니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 `SHUTDOWN` 문을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 중지할 수 있습니다.  
  
#### <a name="to-stop-the-includessdeincludesssde-mdmd-using-includetsqlincludestsql-mdmd"></a>다음을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 중지하기: [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   현재 실행 중인 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 저장 프로시저가 완료될 때까지 기다린 다음 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 중지하려면 다음 문을 실행합니다.  
  
    ```tsql  
    SHUTDOWN;   
    ```  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 즉시 중지하려면 다음 문을 실행합니다.  
  
    ```tsql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 에 대 한 자세한 내용은 합니다 `SHUTDOWN` 문을 참조 [종료 &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/shutdown-transact-sql)합니다.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
  
#### <a name="to-start-and-stop-includessdeincludesssde-mdmd-services"></a>[!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스를 시작 및 중지하려면  
  
1.  명령 프롬프트 창에서 다음 명령을 실행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell을 시작합니다.  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 명령 프롬프트에서 다음 명령을 실행합니다. `computername` 을 사용 중인 컴퓨터의 이름으로 바꿉니다.  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (get-item .).ManagedComputer  
  
    ```  
  
3.  중지하거나 시작할 서비스를 확인합니다. 다음 줄 중 하나를 선택합니다. `instancename` 을 명명된 인스턴스의 이름으로 바꿉니다.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 기본 인스턴스에 대한 참조를 가져오려면  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 명명된 인스턴스에 대한 참조를 가져오려면  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 인스턴스에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에이전트 서비스에 대한 참조를 가져오려면  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 명명된 인스턴스에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에이전트 서비스에 대한 참조를 가져오려면  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스에 대한 참조를 가져오려면  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  예를 완료하여 선택한 서비스를 시작한 다음 중지합니다.  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [최소 구성으로 SQL Server 시작](start-sql-server-with-minimal-configuration.md)   
 [SQL Server 2014 버전에서 지원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
