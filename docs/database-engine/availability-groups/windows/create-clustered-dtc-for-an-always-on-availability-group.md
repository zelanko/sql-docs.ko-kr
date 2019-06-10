---
title: 가용성 그룹에 대한 클러스터형 DTC 리소스 만들기
description: 이 항목에서는 SQL Server Always On 가용성 그룹에 대한 클러스터형 DTC 리소스의 전체 구성에 대해 안내합니다.
ms.custom: seodec18
ms.date: 08/30/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 0e332aa4-2c48-4bc4-a404-b65735a02cea
author: MashaMSFT
ms.author: mathoma
manager: jroth
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 92a75d72a280d3d9e329f38a661a65f9c491cb3b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793481"
---
# <a name="create-clustered-dtc-resource-for-an-always-on-availability-group"></a>Always On 가용성 그룹에 대한 클러스터형 DTC 리소스 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 항목에서는 SQL Server Always On 가용성 그룹에 대한 클러스터형 DTC 리소스의 전체 구성에 대해 안내합니다. 전체 구성을 완료하는 데 최대 한 시간이 걸릴 수 있습니다. 

이 연습에서는 클러스터된 DTC 리소스와 SQL Server 가용성 그룹을 만들어 [SQL Server 가용성 그룹에 대한 DTC 클러스터링](../../../database-engine/availability-groups/windows/cluster-dtc-for-sql-server-2016-availability-groups.md)의 요구 사항에 맞춥니다.

여기에서는 PowerShell과 T-SQL(TRANSACT-SQL) 스크립트를 사용합니다.  대부분의 T-SQL 스크립트에서는 **SQLCMD 모드** 를 사용하도록 설정해야 합니다.  **SQLCMD 모드**대한 자세한 내용은 [쿼리 편집기에서 SQLCMD 스크립팅을 설정](../../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)을 참조하세요.  PowerShell 모듈 **FailoverClusters** 를 가져와야 합니다.  PowerShell 모듈을 가져오는 방법에 대한 자세한 내용은 [PowerShell 모듈 가져오기](https://msdn.microsoft.com/library/dd878284(v=vs.85).aspx)를 참조하세요.  이 연습은 다음 사항을 기반으로 합니다.
- [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항(SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)의 모든 요구 사항을 충족합니다.  
- 도메인은 `contoso.lab`입니다.
- 사용자에게 DTC 네트워크 이름 리소스가 만들어지는 OU에 컴퓨터 만들기 개체 권한이 있습니다.
- 사용자가 클러스터의 모든 노드에 대해 관리자 권한이 있는 도메인 사용자입니다.
- 백업을 위해 `sqlbackups` 라는 파일 공유를 만들었습니다.
- SQL Server의 기본 인스턴스가 명명된 `SQLNODE1` 및 `SQLNODE2`입니다.
- SQL Server의 모든 인스턴스에서 동일한 서비스 계정이 사용됩니다.
- 사용자가 SQL Server의 모든 인스턴스에서 고정되는 SQL Server 역할 sysadmin의 멤버입니다.
- DTC에서 확인할 수 없는 트랜잭션의 기본 결과는 `presume commit`로 설정됩니다.
- 미러링 엔드포인트에서 `5022`포트를 사용합니다.
- 다른 가용성 그룹 또는 클러스터형 DTC 리소스가 없습니다.
- 클러스터 세부 정보(기존):
  - 이름: `Cluster`
  - 네트워크 이름: `Cluster Network 1`
  - 노드: `SQLNODE1, SQLNODE2`
  - 공유 스토리지: `Cluster Disk 3`(`SQLNODE1` 소유)
- 클러스터 세부 정보(만들 예정):
  - 네트워크 이름 리소스: `DTCnet1`
  - DTC 네트워크 이름 리소스: `DTC1`
  - DTC 실제 디스크 리소스: `DTCDisk1`
  - DTC IP 및 서브넷 리소스: `192.168.2.54`, `255.255.255.0`
  - DTC IP 리소스: `DTCIP1`

## <a name="1-check-operating-system"></a>1. 운영 체제 확인
지원되는 분산 트랜잭션의 경우 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]은 Windows Server 2016 또는 Windows Server 2012 R2에서 실행되어야 합니다.  Windows Server 2012 R2의 경우 [https://support.microsoft.com/kb/3090973](https://support.microsoft.com/kb/3090973)에서 제공되는 KB3090973의 업데이트를 설치해야 합니다.  이 스크립트는 운영 체제 버전 및 3090973 핫픽스를 설치해야 하는지 여부를 확인합니다.  `SQLNODE1`에서 다음 PowerShell 스크립트를 실행합니다.

```powershell  
# A few OS checks

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$nodes = (Get-ClusterNode).Name;
foreach ($node in $nodes) {

    # At least 2012 R2
    $os = (Get-WmiObject -class Win32_OperatingSystem -ComputerName $node).caption;
    IF($os -like "*2012 R2*" -or $os -like "*2016*")
    {
        Write-Host "$os is supported on $node.";
    }
    ELSE
    {
        Write-Host "STOP!  $os is not supported on $node.";
    }
    
    # KB 3090973
    IF($os -like "*2012 R2*")
    {
        $kb = Get-Hotfix -ComputerName $node | Where {$_.HotFixID -eq 'KB3090973'};
        IF($kb)
        {
            Write-Host "KB3090973 is installed on $node."
        }
        ELSE
        {
            Write-Host "HotFixID KB3090973 must be applied on $node.  See https://support.microsoft.com/kb/3090973 for additional information and to download the hotfix.";
        }
    }
    ELSE
    {
        Write-Host "KB3090973 is not applicable to $os on $node."
    }
}
```  
## <a name="2---configure-firewall-rules"></a>2.   방화벽 규칙 구성
이 스크립트에서는 가용성 그룹 복제본을 호스트하는 각 SQL Server와 분산 트랜잭션에 참여하는 다른 모든 서버에 DTC 트래픽을 허용하도록 방화벽을 구성합니다.  데이터베이스 미러링 엔드포인트에 대한 연결을 허용하도록 방화벽을 구성하기도 합니다.  `SQLNODE1`에서 다음 PowerShell 스크립트를 실행합니다.

```powershell  
# Configure Firewall

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$nodes = (Get-ClusterNode).Name;
foreach ($node in $nodes) {
    Get-NetFirewallRule -CimSession $node -DisplayGroup 'Distributed Transaction Coordinator' -Enabled False -ErrorAction SilentlyContinue | Enable-NetFirewallRule;
    New-NetFirewallRule -CimSession $node -DisplayName 'SQL Server Mirroring' -Description 'Port 5022 for SQL Server Mirroring' -Action Allow -Direction Inbound -Protocol TCP -LocalPort 5022 -RemotePort Any -LocalAddress Any -RemoteAddress Any;
    };
```  
## <a name="3--configure-in-doubt-xact-resolution"></a>3.  **in-doubt xact resolution** 구성 
이 스크립트에서는 미결 트랜잭션에 대한 "커밋 가정"을 위해 **in-doubt xact resolution** 서버 구성 옵션을 구성합니다.  `SQLNODE1`에 대해 **SQLCMD 모드**로 SSMS(SQL Server Management Studio)에서 다음 T-SQL 스크립트를 실행합니다.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- Configure in-doubt xact resolution on all SQL Server instances to presume commit
IF (SELECT CAST(value_in_use as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'show advanced options') = 0
BEGIN   
    EXEC sp_configure 'show advanced options', 1;
    RECONFIGURE;
END

-- Configure the server to presume commit for in-doubt transactions.
IF (SELECT CAST(value as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'in-doubt xact resolution') <> 1
BEGIN   
    EXEC sp_configure 'in-doubt xact resolution', 1;
    RECONFIGURE;
END
GO
-----------------------------------------------------------------------------

:connect SQLNODE2
IF (SELECT CAST(value_in_use as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'show advanced options') = 0
BEGIN   
    EXEC sp_configure 'show advanced options', 1;
    RECONFIGURE;
END

-- Configure the server to presume commit for in-doubt transactions.
IF (SELECT CAST(value as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'in-doubt xact resolution') <> 1
BEGIN   
    EXEC sp_configure 'in-doubt xact resolution', 1;
    RECONFIGURE;
END
GO
-----------------------------------------------------------------------------
```

## <a name="4-create-test-databases"></a>4. 테스트 데이터베이스 만들기
스크립트에서 `AG1`에 `SQLNODE1`라는 데이터베이스와, `dtcDemoAG1`에 `SQLNODE2`라는 데이터베이스를 만듭니다.  `SQLNODE1`에 대해 **SQLCMD 모드**로 SSMS에서 다음 T-SQL 스크립트를 실행합니다.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- On SQLNODE1 
USE master;
SET NOCOUNT ON;

IF  EXISTS (SELECT * FROM sys.databases WHERE name = N'AG1')
BEGIN
    DROP DATABASE AG1;
END
GO

CREATE DATABASE AG1;
ALTER DATABASE AG1 SET RECOVERY FULL WITH NO_WAIT;
ALTER AUTHORIZATION ON DATABASE::AG1 to sa;
GO

USE AG1;
CREATE TABLE [dbo].[Names] (
        [Name] [varchar](64) NULL,
        [EditDate] datetime
        );

INSERT Names
VALUES ('AG1', GETDATE());
GO


-- Against SQNODE2
:connect SQLNODE2
USE master;
SET NOCOUNT ON;

IF  EXISTS (SELECT * FROM sys.databases WHERE name = N'dtcDemoAG1')
BEGIN
    DROP DATABASE dtcDemoAG1;
END
GO

CREATE DATABASE dtcDemoAG1;
ALTER DATABASE dtcDemoAG1 SET RECOVERY SIMPLE WITH NO_WAIT;
ALTER AUTHORIZATION ON DATABASE::dtcDemoAG1 to sa;
GO

USE dtcDemoAG1;
CREATE TABLE [dbo].[Names] (
        [Name] [varchar](64) NULL,
        [EditDate] datetime
        );
GO    
----------------------------------------------------------------
```
## <a name="5---create-endpoints"></a>5.   엔드포인트 만들기
이 스크립트에서는 TCP 포트 `AG1_endpoint` 에서 수신하는 `5022`라는 엔드포인트를 만듭니다.  `SQLNODE1`에 대해 **SQLCMD 모드**로 SSMS에서 다음 T-SQL 스크립트를 실행합니다.

```sql  
/**********************************************
Execute on SQLNODE1 in SQLCMD mode
**********************************************/

-- Create endpoint on server instance that hosts the primary replica:
IF NOT EXISTS (SELECT * FROM sys.database_mirroring_endpoints)
BEGIN
    CREATE ENDPOINT AG1_endpoint
    AUTHORIZATION [sa]
        STATE=STARTED 
        AS TCP (LISTENER_PORT=5022) 
        FOR DATABASE_MIRRORING (ROLE=ALL);
END
GO
-----------------------------------------------------------------------------

:connect SQLNODE2
IF NOT EXISTS (SELECT * FROM sys.database_mirroring_endpoints)
BEGIN
    CREATE ENDPOINT AG1_endpoint
    AUTHORIZATION [sa]
        STATE=STARTED 
        AS TCP (LISTENER_PORT=5022) 
        FOR DATABASE_MIRRORING (ROLE=ALL);
END
GO
-----------------------------------------------------------------------------
```

## <a name="6---prepare-databases-for-availability-group"></a>6.   가용성 그룹에 대한 데이터베이스 준비
스크립트에서는 `SQLNODE1`에서 `AG1`을 백업하고 `SQLNODE2`로 복원합니다.  `SQLNODE1`에 대해 **SQLCMD 모드**로 SSMS에서 다음 T-SQL 스크립트를 실행합니다.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- Backup database
BACKUP DATABASE AG1 
TO DISK = N'\\sqlnode1\sqlbackups\AG1.bak' 
WITH FORMAT, STATS = 10;

-- Backup transaction log
BACKUP LOG AG1
TO DISK = N'\\sqlnode1\sqlbackups\AG1_Log.bak'
WITH FORMAT, STATS = 10;
GO


-- Restore database and logs on secondary WITH NORECOVERY
:connect SQLNODE2
USE [master]
RESTORE DATABASE AG1 
FROM DISK = N'\\sqlnode1\sqlbackups\AG1.bak' 
WITH NORECOVERY, STATS = 10;

RESTORE LOG AG1 
FROM DISK = N'\\sqlnode1\sqlbackups\AG1_Log.bak'
WITH NORECOVERY, STATS = 10;
GO
```

## <a name="7---create-availability-group"></a>7.   가용성 그룹 만들기
**CREATE AVAILABILITY GROUP** 명령 및 **WITH DTC_SUPPORT = PER_DB** 절을 사용하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 만들어야 합니다.  현재는 기존 가용성 그룹을 변경할 수 없습니다.  새 가용성 그룹 마법사에서는 새 가용성 그룹에 대한 DTC를 지원할 수 없습니다.  다음 스크립트에서는 새 가용성 그룹을 만들고 보조를 조인합니다.  `SQLNODE1` 에 대해 **SQLCMD 모드**로 SSMS에서 다음 T-SQL 스크립트를 실행합니다.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

--  Create Availability Group on SQLNODE1 
USE master;
CREATE AVAILABILITY GROUP DTCAG1
WITH (DTC_SUPPORT = PER_DB) 
FOR DATABASE AG1
REPLICA ON 
  'SQLNODE1' WITH
     (
     ENDPOINT_URL = 'TCP://SQLNODE1.contoso.lab:5022', 
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
     FAILOVER_MODE = MANUAL
     ),
  'SQLNODE2' WITH 
     (
     ENDPOINT_URL = 'TCP://SQLNODE2.contoso.lab:5022',
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
     FAILOVER_MODE = MANUAL
     ); 
GO


-- SQLNODE2
-- Join secondary replica to the Availability Group 
:connect SQLNODE2
ALTER AVAILABILITY GROUP DTCag1 JOIN;

-- Join database to the Availability Group
ALTER DATABASE AG1 SET HADR AVAILABILITY GROUP = DTCAG1;
GO
```

> [!IMPORTANT]
> 기존 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서는 DTC를 사용하도록 설정할 수 없습니다.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 기존 가용성 그룹에 대해 다음 구문을 허용합니다.  
> 
> USE master;    
> ALTER AVAILABILITY GROUP \<availability_group\>  
> SET (DTC_Support = Per_DB)  
> 
> 그러나 실제로 변경되는 구성은 없습니다.  다음 T-SQL 쿼리로 **dtc_support** 구성을 확인할 수 있습니다.  
> 
> SELECT name, dtc_support FROM sys.availability_groups  
> 
> 가용성 그룹에 DTC 지원을 사용하도록 설정하는 유일한 방법은 Transact-SQL을 사용하여 가용성 그룹을 만드는 것입니다.
 
## <a name="ClusterDTC"></a>8.  클러스터 리소스 준비

이 스크립트는 다음 DTC 종속 리소스를 준비합니다. 디스크 및 IP.  공유 스토리지는 Windows 클러스터에 추가됩니다.  네트워크 리소스가 만들어지고 DTC 생성되어 가용성 그룹에 리소스로 적용됩니다.  `SQLNODE1`에서 다음 PowerShell 스크립트를 실행합니다. 스크립트에 대해 [Allan Hirt](https://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/)에게 감사드립니다.

```powershell  
# Create a clustered Microsoft Distributed Transaction Coordinator properly in the resource group with SQL Server

\<#----------------------------------- Begin User Input -----------------------------------#>
$AGgrp = "DTCag1";                          # Name of the WSFC resource group that will contain the DTC resource

$WSFC = (Get-Cluster).Name;                 # Windows Failover Cluster name
$DTCnetwk = "Cluster Network 1"             # WSFC Network to use for the DTC IP address

$ClusterAvailableDisk = "Cluster Disk 3";   # Designated disk that can support failover clustering and is visible to all nodes, but not yet part of the set of clustered disks
$DTCdisk = "DTCDisk1";                      # Name of the disk to be used with DTC

$DTCipresnm = "DTCIP1";                     # WSFC Friendly Name of the DTC's IP resource 
$DTCipaddr = "192.168.2.54";                # IP address of the DTC resource 
$DTCsubnet = "255.255.255.0";               # Subnet for the DTC IP address 
$DTCnetnm = "DTCNet1";                      # WSFC Friendly Name of the Network Name resource
$DTCresnm = "DTC1";                         # Name of the WSFC DTC Network Name resource; Name must be unique in AD
\<#------------------------------------ End User Input ------------------------------------#>


# Make a new disk available for use in a failover cluster.
Get-ClusterAvailableDisk | Where {$_.Name -eq $ClusterAvailableDisk} | Add-ClusterDisk;

# Rename disk
$resource = Get-ClusterResource $ClusterAvailableDisk; $resource.Name = $DTCdisk;

# Create the IP resource
Add-ClusterResource -Name $DTCipresnm -ResourceType "IP Address" -Group $AGgrp;

# Set the network to use, IP address, and subnet
# All three have to be configured at the same time
$DTCIPres = Get-ClusterResource $DTCipresnm;
$ntwk = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,Network,$DTCnetwk;
$ipaddr = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,Address,$DTCipaddr;
$subnet = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,SubnetMask,$dtcsubnet;

$setdtcipparams = $ntwk,$ipaddr,$subnet;
$setdtcipparams | Set-ClusterParameter;

# Create the Network Name resource
Add-ClusterResource $DTCnetnm -ResourceType "Network Name" -Group $AGgrp;

# Set the value for the Network Name resource
Get-ClusterResource $DTCnetnm | Set-ClusterParameter DnsName $DTCresnm;

# Add the IP address as a depenency of the Network Name resource
Add-ClusterResourceDependency $DTCnetnm $DTCipresnm;

# Create the Distributed Transaction Coordinator resource
Add-ClusterResource $DTCresnm -ResourceType "Distributed Transaction Coordinator" -Group $AGgrp;

# Add the Network Name as a depenency of the DTC resource
Add-ClusterResourceDependency $DTCresnm $DTCnetnm;

# Move the disk into the resource group with SQL Server
Move-ClusterResource -Name $DTCdisk -Group $AGgrp;

# Add the disk as a depenency of the DTC resource
Add-ClusterResourceDependency $DTCresnm $DTCdisk;

# Bring the IP resource online
Start-ClusterResource $DTCipresnm;

# Bring the Network Name resource online
Start-ClusterResource $DTCnetnm;

# Bring the DTC resource online
Start-ClusterResource $DTCresnm;
```  

## <a name="9---enable-network-dtc"></a>9.   네트워크 DTC를 사용하도록 설정 

다음 스크립트에서는 클러스터된 DTC 서비스에 대한 네트워크 DTC 액세스를 통해 원격 컴퓨터를 네트워크에서 분산 트랜잭션에 등록할 수 있습니다.  `SQLNODE1`에서 다음 PowerShell 스크립트를 실행합니다.

```powershell  
# Enable Network DTC access for the clustered DTC service

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

# Enter Name of DTC resource

$DtcName = "DTC1";
\<# ------- End of User Input ------- #>

[bool]$restart = 0;
$node = (Get-ClusterResource -Name $DtcName).OwnerNode.Name;
$DtcSettings = Get-DtcNetworkSetting -DtcName $DtcName;

IF ($DtcSettings.InboundTransactionsEnabled -eq $false)   
{
    Set-DtcNetworkSetting -CimSession $node -DtcName $DtcName -AuthenticationLevel "Mutual" -InboundTransactionsEnabled $true -Confirm:$false;
    $restart = 1;
}

IF ($DtcSettings.OutboundTransactionsEnabled -eq $false)   
{
    Set-DtcNetworkSetting -CimSession $node -DtcName $DtcName -AuthenticationLevel "Mutual" -OutboundTransactionsEnabled $true -Confirm:$false;
    $restart = 1;
}

IF ($restart -eq 1)
{
    Stop-Dtc -CimSession $node -DtcName $DTCname -Confirm:$false;
    Start-Dtc -CimSession $node -DtcName $DTCname;
}
```  

## <a name="10--disable-and-stop-the-local-dtc-service-on-each-node"></a>10.  각 노드에서 로컬 DTC 서비스를 사용하지 않도록 설정하고 중지

분산 트랜잭션이 클러스터된 DTC 리소스를 사용하도록 하려면 두 노드에서 모두 로컬 DTC를 사용하지 않도록 설정합니다.  다음 스크립트는 각 노드에서 로컬 DTC 서비스를 사용하지 않도록 설정하고 중지합니다.  `SQLNODE1`에서 다음 PowerShell 스크립트를 실행합니다.
```powershell  
# Disable local DTC service

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$DTCname = 'Local';
$nodes = (Get-ClusterNode).Name;

 foreach ($node in $nodes) {

    $service = Get-WmiObject -class Win32_Service -computername $node -Filter "Name='MSDTC'";
    IF ($service.StartMode -ne 'Disabled')
    {
        $service.ChangeStartMode('Disabled');
    }
    
    IF ($service.State -ne 'Stopped')
    {
        $service.StopService();
    }
}
```  

## <a name="11--cycle-the-includessnoversionincludesssnoversion-mdmd-service-for-each-instance"></a>11.  각 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 순환

클러스터된 DTC 서비스가 완전히 구성되면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 이 DTC 서비스를 사용하도록 등록되기 위해 가용성 그룹의 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 중지하고 다시 시작해야 합니다.

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 분산 트랜잭션이 처음 필요할 때 DTC 서비스에 등록됩니다. SQL Server 서비스는 다시 시작될 때까지 해당 DTC 서비스를 계속 사용합니다. 클러스터된 DTC 서비스를 사용할 수 있으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 클러스터된 DTC 서비스에 등록됩니다. 클러스터된 DTC 서비스를 사용할 수 없으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 로컬 DTC 서비스에 등록됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 클러스터된 DTC 서비스에 등록되었는지 확인하기 위해 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 중지하고 다시 시작합니다. 

다음 T-SQL 스크립트에 포함된 단계를 따르세요.
```sql  
/*
Gracefully cycle the SQL Server service and failover the Availability Group
    a.  On SQLNODE2, cycle the SQL Server service from SQL Server Configuration Manger

    b.  On SQLNODE2 failover the Availability Group to SQLNODE2
        Execute T-SQL script, below, on SQLNODE2 (Use Results to Text)

    c.  On SQLNODE1, cycle the SQL Server service from SQL Server Configuration Manger

    d.  On SQLNODE1 failover the Availability Group to SQLNODE1 once the databases are back in sync.
        Execute T-SQL script, below, on SQLNODE1 (Use Results to Text)
*/

SET NOCOUNT ON;

-- Ensure replica is secondary
IF (
SELECT rs.is_primary_replica 
    FROM sys.availability_groups ag
    JOIN sys.dm_hadr_database_replica_states rs
    ON  ag.group_id = rs.group_id
    WHERE ag.name = N'DTCag1'
    AND rs.is_local = 1) = 0
BEGIN
    -- Wait for SYNCHRONIZED state
    DECLARE @ctr tinyint = 0;
    declare @msg varchar(128);
    WHILE (SELECT synchronization_state 
        FROM sys.availability_groups ag
        JOIN sys.dm_hadr_database_replica_states rs
        ON  ag.group_id = rs.group_id
        WHERE ag.name = N'DTCag1'
        AND rs.is_primary_replica = 0
        AND rs.is_local = 1) <> 2
    BEGIN
        WAITFOR DELAY '00:00:01'
        SET @ctr += 1
        SET @msg = 'Waiting for databases to become synchronized. Duration in seconds: ' + cast(@ctr AS varchar(3))
        RAISERROR (@msg, 0, 1) WITH NOWAIT
    END

    ALTER AVAILABILITY GROUP DTCAG1 FAILOVER;
    SELECT 'Failover complete' AS [Sucess]
END
ELSE BEGIN
    SELECT 'This instance is the primary replica.  Connect to the secondary replica and try again.' AS [Error]
END

```

## <a name="12--test-configuration"></a>12.  구성 테스트

이 테스트에서는 `SQLNODE1`에서 `SQLNODE2`로 연결된 서버를 사용하여 분산 트랜잭션을 만듭니다.  가용성 그룹의 주 복제본이 `SQLNODE1`에 있는지 확인합니다. 구성을 테스트하려면 다음을 수행합니다.

- 연결된 서버 만들기
- 분산 트랜잭션 실행

### <a name="create-linked-servers"></a>연결된 서버 만들기  
다음 스크립트는 `SQLNODE1`두 개의 연결된 서버를 만듭니다.  `SQLNODE1`에 대해 SSMS에서 다음 T-SQL 스크립트를 실행합니다.

```sql  
-- SQLNODE1
IF NOT EXISTS (SELECT * FROM sys.servers where name = N'SQLNODE1')
BEGIN
    EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE1';   
END

IF NOT EXISTS (SELECT * FROM sys.servers where name = N'SQLNODE2')
BEGIN
    EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE2';   
END
 ```

### <a name="execute-a-distributed-transaction"></a>분산 트랜잭션 실행
이 스크립트는 먼저 현재 DTC 트랜잭션 통계를 반환합니다.  그런 다음 스크립트에서 `SQLNODE1` 및 `SQLNODE2`의 데이터베이스를 활용하여 분산 트랜잭션을 실행합니다.  그런 다음 스크립트에서 이제 숫자가 늘어난 DTC 트랜잭션 정적 변수를 다시 반환합니다.  `SQLNODE1` 물리적으로 연결하고 `SQLNODE1` 에 대해 **SQLCMD 모드**SSSMS에서 다음 T-SQL 스크립트를 실행합니다.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
    Must be physically connected to SQLNODE1
*******************************************************************/

USE AG1;
SET NOCOUNT ON;

-- Get Baseline
!! Powershell; $DtcNameC = Get-DtcClusterDefault; Get-DtcTransactionsStatistics -DtcName $DtcNameC;

SET XACT_ABORT ON
BEGIN DISTRIBUTED TRANSACTION
    INSERT INTO SQLNODE1.[AG1].[dbo].[Names] VALUES ('TestValue1', GETDATE());
    INSERT INTO SQLNODE2.[dtcDemoAG1].[dbo].[Names] VALUES ('TestValue2', GETDATE());
COMMIT TRAN
GO

-- Review DTC Transaction Statistics
!! Powershell; $DtcNameC = Get-DtcClusterDefault; Get-DtcTransactionsStatistics -DtcName $DtcNameC;
```

> [!IMPORTANT]
> 데이터베이스 컨텍스트가 `USE AG1` 로 설정되도록 `AG1`문을 실행해야 합니다.  그러지 않으면 다음과 같은 오류 메시지가 나타납니다. "다른 세션에서 트랜잭션 컨텍스트를 사용 중입니다."
