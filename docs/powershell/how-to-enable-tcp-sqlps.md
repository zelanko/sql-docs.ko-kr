---
title: SQLPS를 사용하여 TCP 프로토콜을 사용하도록 설정하는 방법
description: SQLPS를 사용하여 TCP 프로토콜을 사용하도록 설정하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: ''
ms.date: 08/06/2020
ms.openlocfilehash: 9a3b653a0e82eed4bffdf88461474a999eef152d
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714181"
---
# <a name="how-to-enable-the-tcp-protocol"></a>TCP 프로토콜을 사용하도록 설정하는 방법

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-with-sqlps"></a>SQLPS를 사용하여 콘솔에 연결할 때 TCP 프로토콜을 사용하도록 설정하는 방법입니다.

> [!Note]
> **SQLPS** 모듈은 (이전 버전과의 호환성을 위해) SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **[SqlServer](sql-server-powershell.md)** 모듈입니다.

1. 명령 프롬프트를 열고 다음을 입력합니다.

    ```console
    C:\> SQLPS.EXE
    ```

    > [!TIP]
    > SQLPS를 찾을 수 없는 경우에는 새 명령 프롬프트를 열거나 로그오프 했다가 다시 로그온해야 합니다.

2. PowerShell 명령 프롬프트에서 다음을 입력합니다.

    ```powershell
    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-not-using-sqlps"></a>SQLPS를 사용하지 않고 콘솔에 연결할 때 TCP 프로토콜을 사용하도록 설정하는 방법입니다.

1. 명령 프롬프트를 열고 다음을 입력합니다.

    ```console
    C:\> PowerShell.exe
    ```

2. PowerShell 명령 프롬프트에서 다음을 입력합니다.

    ```powershell
    # Get access to SqlWmiManagement DLL on the machine with SQL
    # we are on, which is where SQL Server was installed.
    # Note: this is installed in the GAC by SQL Server Setup.

    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SqlWmiManagement')

    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```





## <a name="next-steps"></a>다음 단계

- [SQL Server PowerShell 모듈 설치](download-sql-server-ps-module.md)
- [SQL Server PowerShell](sql-server-powershell.md)
- [서버 네트워크 프로토콜 설정 또는 해제](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
- [Server Core 설치 시 SQL Server 구성](../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md)
