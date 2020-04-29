---
title: AD 모드 배포 중지됨 - DC에 대한 역방향 조회 영역 항목이 없음
titleSuffix: SQL Server Big Data Cluster
description: 도메인 컨트롤러 DNS 서버의 도메인 컨트롤러에 대한 역방향 조회 영역 항목이 누락되어 AD 모드를 사용한 BDC 배포가 중단되었습니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4cac5fe891533d623a686a02641f63cb25d4b17f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154158"
---
# <a name="ad-mode-deployment-stopped---missing-reverse-lookup-zone-entry-for-dc"></a>AD 모드 배포 중지됨 - DC에 대한 역방향 조회 영역 항목이 없음

AD(Active Directory) 모드에서 배포가 중지됩니다. 증상을 확인하여 도메인 컨트롤러 DNS 서버에 역방향 조회 영역 항목이 누락되었는지 확인합니다. 

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

아래 결과는 컨트롤러에 속하는 Pod만 배포되었음을 표시합니다. 컴퓨팅, 데이터 또는 스토리지용 Pod는 생성되지 않습니다.

```
NAME              READY   STATUS    RESTARTS   AGE
control-rts5t     3/3     Running   0          18m
controldb-0       2/2     Running   0          18m
controlwd-csgst   1/1     Running   0          16m
dns-7kfnz         2/2     Running   0          16m
logsdb-0          1/1     Running   0          16m
logsui-2pc29      1/1     Running   0          16m
metricsdb-0       1/1     Running   0          16m
metricsdc-4rtm4   1/1     Running   0          16m
metricsdc-6lr2t   1/1     Running   0          16m
metricsdc-ftx9m   1/1     Running   0          16m
metricsdc-h59jb   1/1     Running   0          16m
metricsui-lvdpt   1/1     Running   0          16m
mgmtproxy-mkmxp   2/2     Running   0          16m
```

보안 지원 컨테이너 로그를 검사합니다. LDAP 오류를 찾습니다. 

## <a name="check-security-support-container"></a>보안 지원 컨테이너 확인 

보안 지원 컨테이너 로그를 검토합니다.

다음 명령은 `mssql-cluster` 네임스페이스의 클러스터에 있는 보안 지원 로그를 수집합니다.

```bash
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

로그를 추출한 다음, `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`를 찾습니다.

> [!TIP]
> 로그를 수집하는 방법은 여러 가지가 있습니다. `azdata`를 사용하여 로그를 복사하는 대신 Azure Data Studio에서 노트북을 사용할 수 있습니다.
> Azure Data Studio에서 Kubernetes 클러스터에 연결하고 적절한 문제 해결 노트북을 실행합니다. 노트북의 예는 다음과 같습니다.
>
> - TSG027 - 클러스터 배포 관찰
> - TSG061 - BDC 네임스페이스의 Pod에 대한 모든 컨테이너 로그의 끝부분 가져오기
> - TSG001 - `azdata` copy-logs 실행
>

## <a name="inspect-the-logs"></a>로그를 검사합니다.

로그를 찾습니다. 다음 예제에서는 컨트롤러 배포 로그를 가리킵니다. 

`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-YYYYMMDD-HHMMSS\<namespace>\control-<identifier>\controller\control-<identifier>-controller-stdout.log`"

```
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
```

## <a name="cause"></a>원인

도메인 컨트롤러 DNS 항목의 도메인 컨트롤러에 대한 역방향 조회 영역 항목이 없습니다. 

## <a name="resolution"></a>해결 방법

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

## <a name="next-steps"></a>다음 단계

[도메인 컨트롤러의 역방향 DNS 항목(PTR 레코드)을 확인](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)합니다.
