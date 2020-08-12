---
title: Active Directory 도메인 그룹 범위 문제 해결
titleSuffix: SQL Server Big Data Cluster
description: Active Directory 도메인에서 SQL Server 빅 데이터 클러스터의 배포 문제를 해결합니다.
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 302731f3f0c37f60c4944b7df44d02b2cfc64a8b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772879"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-integration"></a>SQL Server 빅 데이터 클러스터 Active Directory 통합 문제 해결

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 Active Directory 모드에서 SQL Server 빅 데이터 클러스터의 배포 문제를 해결하는 방법을 설명합니다.

## <a name="symptom"></a>증상

AD 모드로 BDC 배포를 시작했지만 배포가 중단되어 더 이상 진행되지 않습니다.

다음 예제에서는 bash 셸에서의 배포 결과를 보여 줍니다.

```
The privacy statement can be viewed at:
https://go.microsoft.com/fwlink/?LinkId=853010
 
The license terms for SQL Server Big Data Cluster can be viewed at:
Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292
Standard: https://go.microsoft.com/fwlink/?linkid=2104294
Developer: https://go.microsoft.com/fwlink/?linkid=2104079
 
Cluster deployment documentation can be viewed at:
https://aka.ms/bdc-deploy
 
NOTE: Cluster creation can take a significant amount of time depending on
configuration, network speed, and the number of nodes in the cluster.
 
Starting cluster deployment.
Cluster controller endpoint is available at bdc-control.contoso.com:30080, 193.168.5.14:30080.
Waiting for control plane to be ready after 5 minutes.
Waiting for control plane to be ready after 10 minutes.
Waiting for control plane to be ready after 15 minutes.
Waiting for control plane to be ready after 20 minutes.
Waiting for control plane to be ready after 25 minutes.
```

현재 배포된 Pod를 확인합니다.

```bash
kubectl get pods -n mssql-cluster
```

다음 목록에는 컨트롤러에 속한 Pod만 배포된 것으로 표시됩니다. 컴퓨팅, 데이터 또는 스토리지 풀 Pod는 생성되고 있지 않습니다.

```
NAME              READY   STATUS    RESTARTS   AGE
appproxy-6q4rm    2/2     Running   0          32m
compute-0-0       3/3     Running   0          32m
control-n8jqh     3/3     Running   0          35m
controldb-0       2/2     Running   0          35m
controlwd-fgpj8   1/1     Running   0          34m
data-0-0          3/3     Running   0          32m
data-0-1          3/3     Running   0          32m
dns-fjp7n         2/2     Running   0          34m
gateway-0         2/2     Running   0          32m
logsdb-0          1/1     Running   0          34m
logsui-d26c5      1/1     Running   0          34m
master-0          3/4     Running   0          32m
master-1          3/4     Running   0          32m
master-2          3/4     Running   0          32m
metricsdb-0       1/1     Running   0          34m
metricsdc-c2kbh   1/1     Running   0          34m
metricsdc-lmqzx   1/1     Running   0          34m
metricsdc-r6499   1/1     Running   0          34m
metricsdc-tj99w   1/1     Running   0          34m
metricsui-dg8rz   1/1     Running   0          34m
mgmtproxy-dvzpc   2/2     Running   0          34m
nmnode-0-0        2/2     Running   0          32m
nmnode-0-1        2/2     Running   0          32m
operator-27gt9    1/1     Running   0          32m
sparkhead-0       4/4     Running   0          31m
sparkhead-1       4/4     Running   0          31m
storage-0-0       4/4     Running   0          31m
storage-0-1       4/4     Running   0          31m
storage-0-2       4/4     Running   0          31m
zookeeper-0       2/2     Running   0          32m
zookeeper-1       2/2     Running   0          32m
zookeeper-2       2/2     Running   0          32m
```

### <a name="check-logs"></a>로그 확인

컴퓨팅, 데이터 및 스토리지 Pod를 만들지 않고 배포가 종료되는 이유를 확인하려면 다음 로그를 확인합니다. 

- `controller.log`(`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`)를 확인합니다. 다음 항목을 찾습니다.

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- `master-0` `provisioner.log`(`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`)를 확인합니다.

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

## <a name="cause"></a>원인

위의 예제에서는 도메인 그룹의 범위가 도메인 로컬로 지정되었으므로 배포에서 도메인 사용자의 로그인을 만들지 못합니다. 전역 또는 유니버설 범위 그룹을 사용합니다. [Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](deploy-active-directory.md)에서는 AD 그룹 범위 요구 사항을 설명합니다.

## <a name="verify"></a>확인

도메인 그룹(<`domain-group`>)의 범위를 확인합니다. [get-adgroup](/powershell/module/addsadministration/get-adgroup/)을 사용합니다.

`<domain-group>` 그룹 범위가 도메인 로컬(`DomainLocal`)이면 배포에 실패합니다. 

다음 PowerShell 스크립트는 `bdcadmins` 및 `bdcusers`라는 두 AD 그룹의 범위를 확인합니다. 사용자 그룹의 이름으로 이름을 바꿉니다. 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="resolution"></a>해결 방법

이 문제를 해결하려면 유니버설 또는 글로벌 범위를 사용하여 AD 그룹을 만들고 배포를 다시 실행합니다.

