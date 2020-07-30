---
title: SQL Server 서비스 시작, 중지, 일시 중지, 계속 및 다시 시작
description: 다양한 SQL Server 서비스를 시작, 중지, 일시 중지, 재개 또는 다시 시작하는 방법을 알아봅니다. 이러한 작업에 Transact-SQL, PowerShell 및 기타 도구를 사용하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
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
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 385e0a0d6873f8480c3d99efe9700ef938fc3abf
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363033"
---
# <a name="start-stop-pause-resume-restart-sql-server-services"></a>SQL Server 서비스 시작, 중지, 일시 중지, 계속 및 다시 시작

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 문서에서는 SQL Server 구성 관리자, SSMS(SQL Server Management Studio), 명령 프롬프트의 net 명령, Transact-SQL 또는 PowerShell을 사용하여 SQL Server 데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스를 시작, 중지, 일시 중지, 계속 또는 다시 시작하는 방법을 설명합니다.

## <a name="identify-the-service"></a>서비스 확인

SQL Server 구성 요소는 Windows 서비스로 실행되는 실행 가능한 프로그램입니다. Windows 서비스로 실행되는 프로그램은 컴퓨터 화면에 작업을 표시하지 않고도 작업을 계속할 수 있습니다.

### <a name="database-engine-service"></a>데이터베이스 엔진 서비스

SQL Server 데이터베이스 엔진인 실행 가능한 프로세스입니다. 데이터베이스 엔진은 컴퓨터당 하나로 제한되는 기본 인스턴스이거나, 데이터베이스 엔진의 명명된 여러 인스턴스 중 하나일 수 있습니다. SQL Server 구성 관리자를 사용하여 컴퓨터에 설치된 데이터베이스 엔진 인스턴스를 확인할 수 있습니다. 기본 인스턴스(설치한 경우)는 **SQL Server(MSSQLSERVER)** 로 나열됩니다. 명명된 인스턴스(설치한 경우)는 **SQL Server(<instance_name>)** 로 나열됩니다. 기본적으로 SQL Server Express는 **SQL Server(SQLEXPRESS)** 로 설치됩니다.

### <a name="sql-server-agent-service"></a>SQL Server 에이전트 서비스

작업 및 경고라고 하는 예약된 관리 태스크를 실행하는 Windows 서비스입니다. 자세한 내용은 [SQL Server Agent](../../ssms/agent/sql-server-agent.md)을 참조하세요. 일부 SQL Server 버전에서는 SQL Server 에이전트를 사용할 수 없습니다. SQL Server 버전에서 지원되는 기능 목록은 [SQL Server 2019 버전에서 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-version-15.md)을 참조하세요.

### <a name="sql-server-browser-service"></a>SQL Server Browser 서비스

SQL Server 리소스에 관한 들어오는 요청을 수신 대기하고 컴퓨터에 설치된 SQL Server 인스턴스에 대한 클라이언트 정보를 제공하는 Windows 서비스입니다. 컴퓨터에 설치된 모든 SQL Server 인스턴스에 SQL Server Browser 서비스의 단일 인스턴스가 사용됩니다.

### <a name="additional-information"></a>추가 정보

- 데이터베이스 엔진 서비스를 일시 중지하면 새 사용자는 데이터베이스 엔진에 연결할 수 없지만, 이미 연결된 사용자는 연결이 끊어질 때까지 계속해서 작업할 수 있습니다. 사용자가 작업을 완료할 때까지 기다렸다가 서비스를 중지하려면 일시 중지를 사용합니다. 이렇게 하면 사용자가 진행 중인 트랜잭션을 완료할 수 있습니다. ‘계속’을 사용하면 데이터베이스 엔진에서 새 연결을 다시 허용할 수 있습니다. SQL Server 에이전트 서비스는 일시 중지하거나 계속할 수 없습니다.  

- SQL Server 구성 관리자와 SSMS에서는 다음 아이콘을 사용하여 서비스의 현재 상태를 표시합니다.  

    **SQL Server 구성 관리자**

  - 서비스 이름 옆에 녹색 화살표가 있는 아이콘이 표시되면 서비스가 시작된 것입니다.

  - 서비스 이름 옆에 빨간색 사각형이 있는 아이콘이 표시되면 서비스가 중지된 것입니다.

  - 서비스 이름 옆에 두 개의 파란색 세로 선이 있는 아이콘이 표시되면 서비스가 일시 중지된 것입니다.

  - 데이터베이스 엔진을 다시 시작하면 서비스가 중지되었음을 나타내는 빨간색 사각형이 표시되었다가 서비스가 성공적으로 시작되었음을 나타내는 녹색 화살표가 표시됩니다.

    **SSMS(SQL Server Management Studio)**

  - 서비스 이름 옆의 녹색 원 아이콘에 흰색 화살표가 표시되면 서비스가 시작된 것입니다.  

  - 서비스 이름 옆에 흰색 사각형이 있는 빨간색 원 아이콘이 표시되면 서비스가 중지된 것입니다.  

  - 서비스 이름 옆에 두 개의 흰색 세로 선이 있는 파란색 원 아이콘이 표시되면 서비스가 일시 중지된 것입니다.  

- SQL Server 구성 관리자 또는 SSMS를 사용하는 경우 가능한 옵션만 제공됩니다. 예를 들어 서비스가 이미 시작된 경우 **시작**은 제공되지 않습니다.

- 클러스터에서 실행 중인 경우 SQL Server 데이터베이스 엔진 서비스를 가장 잘 관리하려면 클러스터 관리자를 사용합니다.  

### <a name="security"></a>보안

#### <a name="permissions"></a>사용 권한

기본적으로 로컬 관리자 그룹의 멤버만 서비스를 시작, 중지, 일시 중지, 계속 또는 다시 시작할 수 있습니다. 관리자가 아닌 사용자에게 서비스 관리 권한을 부여하려면 [Windows Server 2003에서 사용자에게 서비스 관리 권한을 부여하는 방법](https://support.microsoft.com/kb/325349)을 참조하세요. 이 프로세스는 다른 Windows Server 버전에서도 비슷합니다.

Transact-SQL **SHUTDOWN** 명령을 사용하여 데이터베이스 엔진을 중지하려면 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버 자격이 있어야 하며, 이 권한은 양도할 수 없습니다.

## <a name="sql-server-configuration-manager"></a>SQL Server 구성 관리자

### <a name="starting-sql-server-configuration-manager"></a>SQL Server 구성 관리자 시작

**시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.

SQL Server 구성 관리자는 독립 실행형 프로그램이 아니라 Microsoft Management Console 프로그램용 스냅인이므로, 최신 Windows 버전에서는 SQL Server 구성 관리자가 애플리케이션으로 표시되지 않습니다. Windows가 C 드라이브에 설치되어 있는 경우 최신 4개 버전의 경로는 다음과 같습니다.  

|버전|경로|
|-|-|
|SQL Server 2019|C:\Windows\SysWOW64\SQLServerManager15.msc|
|SQL Server 2017|C:\Windows\SysWOW64\SQLServerManager14.msc|
|SQL Server 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|
|SQL Server 2014|C:\Windows\SysWOW64\SQLServerManager12.msc|
|SQL Server 2012|C:\Windows\SysWOW64\SQLServerManager11.msc|

#### <a name="to-start-stop-pause-resume-or-restart-an-instance-of-the-sql-server-database-engine"></a><a name="configmande"></a> SQL Server 데이터베이스 엔진 인스턴스를 시작, 중지, 일시 중지, 계속 또는 다시 시작하려면 다음을 수행합니다.

1. 위의 지침에 따라 SQL Server 구성 관리자를 시작합니다.

2. **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.

3. SQL Server 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 클릭합니다.

4. 결과 창에서 **SQL Server(MSSQLServer)** 또는 명명된 인스턴스를 마우스 오른쪽 단추로 클릭하고 **시작**, **중지**, **일시 중지**, **재개**또는 **다시 시작**을 클릭합니다.

5. **확인**을 클릭하여 SQL Server 구성 관리자를 닫습니다.

> [!NOTE]
> 시작 옵션을 사용하여 SQL Server 데이터베이스 엔진 인스턴스를 시작하려면 [서버 시작 옵션 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)를 참조하세요.  

#### <a name="to-start-stop-pause-resume-or-restart-the-sql-server-browser-or-an-instance-of-the-sql-server-agent"></a>SQL Server Browser 또는 SQL Server 에이전트 인스턴스를 시작, 중지, 일시 중지, 계속 또는 다시 시작하려면 다음을 수행합니다.

1. 위의 지침에 따라 SQL Server 구성 관리자를 시작합니다.

2. **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.

3. SQL Server 구성 관리자의 왼쪽 창에서 **SQL Server 서비스**를 클릭합니다.

4. 결과 창에서 **SQL Server Browser**, **SQL Server 에이전트(MSSQLServer)** 또는 명명된 인스턴스의 **SQL Server 에이전트(<instance_name>)** 를 마우스 오른쪽 단추로 클릭하고 **시작**, **중지**, **일시 중지**, **계속** 또는 **다시 시작**을 클릭합니다.  

5. **확인**을 클릭하여 SQL Server 구성 관리자를 닫습니다.  

> [!NOTE]
> SQL Server 에이전트는 일시 중지할 수 없습니다.

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

### <a name="to-start-stop-pause-resume-or-restart-an-instance-of-the-sql-server-database-engine"></a><a name="ssmsde"></a> SQL Server 데이터베이스 엔진 인스턴스를 시작, 중지, 일시 중지, 계속 또는 다시 시작하려면 다음을 수행합니다.

1. 개체 탐색기에서 데이터베이스 엔진 인스턴스에 연결하고 시작할 데이터베이스 엔진 인스턴스를 마우스 오른쪽 단추로 클릭한 다음, **시작**, **중지**, **일시 중지**, **계속** 또는 **다시 시작**을 클릭합니다.

    또는 등록된 서버에서 시작할 데이터베이스 엔진 인스턴스를 마우스 오른쪽 단추로 클릭하고 **서비스 제어**를 가리킨 다음, **시작**, **중지**, **일시 중지**, **계속** 또는 **다시 시작**을 클릭합니다.

2. **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.

3. 작업을 수행할지 여부를 묻는 메시지가 표시되면 **예**를 클릭합니다.  

#### <a name="to-start-stop-or-restart-an-instance-of-the-sql-server-agent"></a>SQL Server 에이전트 인스턴스를 시작, 중지 또는 다시 시작하려면 다음을 수행합니다.

1. 개체 탐색기에서 데이터베이스 엔진 인스턴스에 연결하고 **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음, **시작**, **중지** 또는 **다시 시작**을 클릭합니다.

2. **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.

3. 작업을 수행할지 여부를 묻는 메시지가 표시되면 **예**를 클릭합니다.

## <a name="command-prompt-window-using-net-commands"></a><a name="CommandPrompt"></a> 명령 프롬프트 창 net 명령 사용

Microsoft Windows **net** 명령을 사용하여 Microsoft SQL Server 서비스를 시작, 중지 또는 일시 중지할 수 있습니다.

### <a name="to-start-the-default-instance-of-the-database-engine"></a><a name="dbDefault"></a> 데이터베이스 엔진의 기본 인스턴스를 시작하려면 다음을 수행합니다.

- 명령 프롬프트에서 다음 명령 중 하나를 입력합니다.  
  
    **net start "SQL Server (MSSQLSERVER)"**

   또는  

    **net start MSSQLSERVER**

### <a name="to-start-a-named-instance-of-the-database-engine"></a><a name="dbNamed"></a> 데이터베이스 엔진의 명명된 인스턴스를 시작하려면 다음을 수행합니다.

- 명령 프롬프트에서 다음 명령 중 하나를 입력합니다. *\<instancename>* 을 관리할 인스턴스 이름으로 바꿉니다.  
  
    **net start “SQL Server (** *instancename* **)”**
  
   또는  
  
    **net start MSSQL$** *instancename*  
  
### <a name="to-start-the-database-engine-with-startup-options"></a><a name="dbStartup"></a> 시작 옵션을 사용하여 데이터베이스 엔진을 시작하려면 다음을 수행합니다.  

- **net start "SQL Server (MSSQLSERVER)"** 문 끝에 공백으로 구분된 시작 옵션을 추가합니다. **net start**를 사용하여 시작하는 경우에는 시작 옵션에 하이픈(-) 대신 슬래시(/)를 사용합니다.  
  
    **net start "SQL Server (MSSQLSERVER)" /f /m**
  
   또는  
  
    **net start MSSQLSERVER /f /m**
  
  > [!NOTE]
  >  시작 옵션에 대한 자세한 내용은 [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)을 참조하세요.  
  
###  <a name="to-start-the-sql-server-agent-on-the-default-instance-of-sql-server"></a><a name="agDefault"></a> SQL Server의 기본 인스턴스에서 SQL Server 에이전트를 시작하려면 다음을 수행합니다.
  
- 명령 프롬프트에서 다음 명령 중 하나를 입력합니다.  
  
    **net start "SQL Server Agent (MSSQLSERVER)"**
  
   또는  
  
    **net start SQLSERVERAGENT**
  
###  <a name="to-start-the-sql-server-agent-on-a-named-instance-of-sql-server"></a><a name="agNamed"></a> SQL Server의 명명된 인스턴스에서 SQL Server 에이전트를 시작하려면 다음을 수행합니다.  
  
- 명령 프롬프트에서 다음 명령 중 하나를 입력합니다. *instancename* 을 관리할 인스턴스 이름으로 바꿉니다.  
  
    **net start "SQL Server Agent(** *instancename* **)"**
  
   또는  
  
    **net start SQLAgent$** *instancename*  
  
 문제 해결을 위해 SQL Server 에이전트를 자세한 정보 표시 모드로 실행하는 방법에 대한 자세한 내용은 [sqlagent90 애플리케이션](../../tools/sqlagent90-application.md)을 참조하세요.  

### <a name="to-start-the-sql-server-browser"></a><a name="Browser"></a> SQL Server Browser를 시작하려면 다음을 수행합니다.  

- 명령 프롬프트에서 다음 명령 중 하나를 입력합니다.  
  
    **net start "SQL Server Browser"**
  
   또는  
  
    **net start SQLBrowser**
  
### <a name="to-pause-or-stop-services-from-the-command-prompt-window"></a><a name="pauseStop"></a> 명령 프롬프트 창에서 서비스를 일시 중지하거나 중지하려면  

- 서비스를 일시 중지하거나 중지하려면 다음과 같은 방법으로 명령을 수정합니다.  

- 서비스를 일시 중지하려면 **net start** 를 **net pause**로 바꿉니다.  

- 서비스를 중지하려면 **net start** 를 **net stop**으로 바꿉니다.  

## <a name="transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL

**SHUTDOWN** 문을 사용하여 데이터베이스 엔진을 중지할 수 있습니다.  

### <a name="to-stop-the-database-engine-using-transact-sql"></a>Transact-SQL을 사용하여 데이터베이스 엔진을 중지하려면 다음을 수행합니다.

- 현재 실행 중인 Transact-SQL 문과 저장 프로시저가 완료될 때까지 기다린 후에 데이터베이스 엔진을 중지하려면 다음 문을 실행합니다.  
  
    ```sql
    SHUTDOWN;
    ```
  
- 데이터베이스 엔진을 즉시 중지하려면 다음 문을 실행합니다.  
  
    ```sql
    SHUTDOWN WITH NOWAIT;
    ```

**SHUTDOWN** 문에 대한 자세한 내용은 [SHUTDOWN&#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)을 참조하세요.  

## <a name="powershell"></a><a name="PowerShellProcedure"></a> PowerShell

### <a name="to-start-and-stop-database-engine-services"></a>데이터베이스 엔진 서비스를 시작하고 중지하려면 다음을 수행합니다.

1. 명령 프롬프트 창에서 다음 명령을 실행하여 SQL Server PowerShell을 시작합니다.  

    ```cmd
    sqlps
    ```

2. SQL Server PowerShell 명령 프롬프트에서 다음 명령을 실행합니다. `computername` 을 사용 중인 컴퓨터의 이름으로 바꿉니다.  

    ```powershell
    # Get a reference to the ManagedComputer class.
    CD SQLSERVER:\SQL\computername
    $Wmi = (get-item .).ManagedComputer
    ```

3. 중지하거나 시작할 서비스를 확인합니다. 다음 줄 중 하나를 선택합니다. `instancename` 을 명명된 인스턴스의 이름으로 바꿉니다.

    - 데이터베이스 엔진의 기본 인스턴스에 대한 참조를 가져오려면 다음을 수행합니다.

        ```powershell
        $DfltInstance = $Wmi.Services['MSSQLSERVER']
        ```

    - 데이터베이스 엔진의 명명된 인스턴스에 대한 참조를 가져오려면 다음을 수행합니다.

        ```powershell
        $DfltInstance = $Wmi.Services['MSSQL$instancename']
        ```

    - 데이터베이스 엔진의 기본 인스턴스에서 SQL Server 에이전트 서비스에 대한 참조를 가져오려면 다음을 수행합니다.  

        ```powershell
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']
        ```

    - 데이터베이스 엔진의 명명된 인스턴스에서 SQL Server 에이전트 서비스에 대한 참조를 가져오려면 다음을 수행합니다.  

        ```powershell
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']
        ```

    - SQL Server Browser 서비스에 대한 참조를 가져오려면 다음을 수행합니다.

        ```powershell
        $DfltInstance = $Wmi.Services['SQLBROWSER']
        ```

4. 예를 완료하여 선택한 서비스를 시작한 다음 중지합니다.
  
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
  
##  <a name="using-service-controller-class"></a><a name="ServiceController"></a> ServiceController 클래스 사용

ServiceController 클래스를 사용하여 SQL Server 서비스 또는 다른 Windows 서비스를 제어할 수 있습니다. 이 작업을 수행하는 방법에 대한 예제는 [ServiceController 클래스](https://docs.microsoft.com/dotnet/api/system.serviceprocess.servicecontroller?view=netframework-4.8)를 참조 하세요.

## <a name="manage-the-sql-server-service-on-linux"></a>Linux에서 SQL Server 서비스 관리

### <a name="to-start-stop-or-restart-an-instance-of-the-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진 인스턴스를 시작, 중지 또는 다시 시작하려면 다음을 수행합니다.

아래에서는 [Linux에서 SQL Server 서비스](../../linux/sql-server-linux-troubleshooting-guide.md#manage-the-sql-server-service)를 시작, 중지, 다시 시작하고 해당 상태를 확인하는 방법을 보여 줍니다.

다음 명령을 사용하여 SQL Server 서비스의 상태를 확인합니다.

   ```bash
   sudo systemctl status mssql-server
   ```

다음 명령을 사용하여 필요에 따라 SQL Server 서비스를 중지, 시작 또는 다시 시작할 수 있습니다.

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

## <a name="next-steps"></a>다음 단계

- [SQL Server 설치 설명서 개요](https://msdn.microsoft.com/library/2620439a-f9d3-4b3c-9968-48f60b4bb9a5)
- [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)
- [최소 구성으로 SQL Server 시작](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)
- [SQL Server 2016 버전에서 지원되는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)