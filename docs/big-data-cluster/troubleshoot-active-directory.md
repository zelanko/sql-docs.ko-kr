---
title: Active Directory 모드 배포 문제 해결
titleSuffix: SQL Server Big Data Cluster
description: Active Directory 도메인에서 SQL Server 빅 데이터 클러스터의 배포 문제를 해결합니다.
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d887eadd021641241516a1478c6ac13e0d0bdec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79191214"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-mode-deployment"></a>SQL Server 빅 데이터 클러스터 Active Directory 모드 배포 문제 해결

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Active Directory 모드에서 SQL Server 빅 데이터 클러스터의 배포 문제를 해결하는 방법을 설명합니다.

## <a name="check-deployment-progress"></a>배포 진행률 확인

배포에는 몇 분 정도 걸릴 수 있습니다. 15분 후에도 클러스터가 준비되지 않으면 컨트롤러 로그에서 자세한 내용을 확인합니다.

클러스터가 배포되는 동안 Pod를 확인합니다.

```console
kubectl get pods -n mssql-cluster
```

반환된 Pod 목록에 다음이 포함되어 있는지 확인합니다.

- `compute-`$
- `data-`
- `storage-`

컴퓨팅, 데이터 및 스토리지 Pod가 생성되지 않은 경우 로그에서 이유를 확인합니다.

## <a name="check-logs"></a>로그 확인

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

  위의 예제에서는 도메인 그룹의 범위가 도메인 로컬로 지정되었으므로 배포에서 도메인 사용자의 로그인을 만들지 못합니다. 도메인 글로벌 또는 도메인 유니버설 범위의 그룹을 사용합니다. [Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](deploy-active-directory.md)에서는 AD 그룹 범위 요구 사항을 설명합니다.

## <a name="check-the-scope-of-domain-groups"></a>도메인 그룹의 범위를 확인합니다.

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

## <a name="check-security-support-container"></a>보안 지원 컨테이너 확인 

보안 지원 컨테이너 로그를 검토합니다.

다음 명령은 `mssql-cluster` 네임스페이스의 클러스터에 있는 보안 지원 로그를 수집합니다.

```console
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

로그를 추출한 다음, `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`를 찾습니다.

로그에서 다음 항목을 찾습니다.

```
ERROR    | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform.
```

이러한 항목은 도메인 컨트롤러 DNS 서버에 역방향 DNS 항목(PTR 레코드)이 없는 경우에 발생할 수 있습니다.

## <a name="verify-reverse-lookup-ptr-record"></a>역방향 조회(PTR 레코드) 확인
    
다음 PowerShell 스크립트를 실행하여 역방향 DNS 항목(PTR 레코드)이 구성되어 있는지 확인합니다.

```powershell
#Domain Controller FQDN 'DCserver01.contoso.local'
$Domain_controller_FQDN = 'DCserver01.contoso.local'

#Performing Domain Controller DNS record, reverse PTR Checks...
$DcControllerDnsPtr_Result = New-Object System.Collections.ArrayList
try {
    $Domain_controller_DNS_Record = Resolve-DnsName $Domain_controller_FQDN -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop
    foreach ($ip in $Domain_controller_DNS_Record.IPAddress) {
        #resolving hostname by IP address to make sure we have reverse PTR record 
        if ((Resolve-DnsName $ip).NameHost -eq $Domain_controller_FQDN) {
            [void]$DcControllerDnsPtr_Result.add("OK - $Domain_controller_FQDN has an A record with an IP $ip, Reverse PTR record is in place") 
        }
        else {
            [void]$DcControllerDnsPtr_Result.add("Missing - $Domain_controller_FQDN has an A record with an IP $ip, But no reverse PTR record was found for the host")
        }
    }
}
catch {
    [void]$DcControllerDnsPtr_Result.add("Error - " + $_.exception.message)
}

#show the results 
$DcControllerDnsPtr_Result
```

[도메인 컨트롤러의 역방향 DNS 항목(PTR 레코드)을 확인](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)합니다.