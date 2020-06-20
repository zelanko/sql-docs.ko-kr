---
title: 서버 네트워크 프로토콜 설정 또는 해제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], disabling
- remote connections [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], disabling using Configuration Manager
- disabling network protocols, Configuration Manager
- network protocols [SQL Server], enabling
- enabling network protocols, Configuration Manager
- surface area configuration [SQL Server], connection protocols
- connections [SQL Server], enabling remote using Configuration Manager
ms.assetid: ec5ccb69-61c9-4576-8843-014b976fd46e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e6261e223513c4a33362ef41d6977c04bcfb430a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935324"
---
# <a name="enable-or-disable-a-server-network-protocol"></a>서버 네트워크 프로토콜 설정 또는 해제
  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 모든 네트워크 프로토콜이 설치되지만 일부 프로토콜이 설정되거나 설정되지 않을 수 있습니다. 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 또는 PowerShell을 사용하여 서버 네트워크 프로토콜을 설정하거나 해제하는 방법에 대해 설명합니다. 변경 내용을 적용하려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 중지한 뒤 다시 시작해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설치 중에 BUILTIN\Users 그룹에 대한 로그인이 추가됩니다. 이 로그인을 사용하면 컴퓨터의 모든 인증된 사용자가 public 역할의 멤버로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스에 액세스할 수 있습니다. BUILTIN\Users 로그인은 개별 로그인이 있거나 로그인이 있는 기타 Windows 그룹의 멤버인 컴퓨터 사용자에 대한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 액세스를 제한하기 위해 안전하게 제거할 수 있습니다.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 데이터 공급자는 TLS 1.0 및 SSL 3.0을 지원합니다. 운영 체제 SChannel 계층을 변경하여 다른 프로토콜 (예: TLS 1.1 또는 TLS 1.2)를 적용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 연결이 실패할 수 있습니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 서버 네트워크 프로토콜을 설정하거나 해제합니다.**  
  
     [SQL Server 구성 관리자](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a>SQL Server 구성 관리자 사용  
  
#### <a name="to-enable-a-server-network-protocol"></a>서버 네트워크 프로토콜을 설정하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자의 콘솔 창에서 **SQL Server 네트워크 구성**을 확장합니다.  
  
2.  콘솔 창에서 **에 대 한 프로토콜** 을 클릭 *\<instance name>* 합니다.  
  
3.  세부 정보 창에서 변경할 프로토콜을 마우스 오른쪽 단추로 클릭한 다음 **사용** 또는 **사용 안 함**을 클릭합니다.  
  
4.  콘솔 창에서 **SQL Server 서비스**를 클릭합니다.  
  
5.  세부 정보 창에서 **SQL Server ( ***\<instance name>*** )** 를 마우스 오른쪽 단추로 클릭 한 다음 **다시 시작**을 클릭 하 여 서비스를 중지 하 고 다시 시작 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
##  <a name="using-sql-server-powershell"></a><a name="PowerShellProcedure"></a> SQL Server PowerShell 사용  
  
#### <a name="to-enable-a-server-network-protocol-using-powershell"></a>PowerShell을 사용하여 서버 네트워크 프로토콜을 설정하려면  
  
1.  관리자 권한으로 명령 프롬프트를 엽니다.  
  
2.  작업 표시줄에서 Windows PowerShell 2.0을 시작하거나, 시작, 모든 프로그램, 보조프로그램, Windows PowerShell, Windows PowerShell을 차례로 클릭합니다.  
  
3.  다음을 입력 하 여 **sqlps** 모듈을 가져옵니다.`Import-Module "sqlps"`  
  
4.  다음 문을 실행하여 TCP 및 명명된 파이프 프로토콜을 모두 사용하도록 설정합니다. `<computer_name>` 을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행 중인 컴퓨터의 이름으로 바꿉니다. 명명된 인스턴스를 구성할 경우 `MSSQLSERVER` 를 인스턴스의 이름으로 바꿉니다.  
  
     프로토콜을 해제하려면 `IsEnabled` 속성을 `$false`로 설정합니다.  
  
    ```powershell
    $smo = 'Microsoft.SqlServer.Management.Smo.'  
    $wmi = new-object ($smo + 'Wmi.ManagedComputer').  
  
    # List the object properties, including the instance names.  
    $Wmi  
  
    # Enable the TCP protocol on the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    $Tcp = $wmi.GetSmoObject($uri)  
    $Tcp.IsEnabled = $true  
    $Tcp.Alter()  
    $Tcp  
  
    # Enable the named pipes protocol for the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Np']"  
    $Np = $wmi.GetSmoObject($uri)  
    $Np.IsEnabled = $true  
    $Np.Alter()  
    $Np  
    ```  
  
#### <a name="to-configure-the-protocols-for-the-local-computer"></a>로컬 컴퓨터의 프로토콜을 구성하려면  
  
-   스크립트가 로컬로 실행되고 로컬 컴퓨터를 구성할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell은 로컬 컴퓨터의 이름을 동적으로 확인하여 보다 유연한 스크립트를 실행할 수 있습니다. 로컬 컴퓨터 이름을 가져오려면 `$uri` 변수 설정 행을 다음 행으로 바꿉니다.  
  
    ```powershell
    $uri = "ManagedComputer[@Name='" + (Get-Item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    ```  
  
#### <a name="to-restart-the-database-engine-by-using-sql-server-powershell"></a>SQL Server PowerShell을 사용하여 데이터베이스 엔진을 다시 시작하려면  
  
-   프로토콜을 설정하거나 해제한 후에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 중지하고 다시 시작해야만 변경 내용이 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell을 사용하여 다음 문을 실행함으로써 기본 인스턴스를 중지한 후 다시 시작합니다. 명명된 인스턴스를 중지한 후 다시 시작하려면 `'MSSQLSERVER'` 를 `'MSSQL$<instance_name>'`으로 바꿉니다.  
  
    ```powershell
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\<computer_name>  
    $Wmi = (Get-Item .).ManagedComputer  
    # Get a reference to the default instance of the Database Engine.  
    $DfltInstance = $Wmi.Services['MSSQLSERVER']  
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Start the service again.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache and display the state of the service.  
    $DfltInstance.Refresh(); $DfltInstance  
    ```  
