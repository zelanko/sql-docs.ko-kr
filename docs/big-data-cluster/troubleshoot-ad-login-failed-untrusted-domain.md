---
title: AD 모드 로그인 실패 - 신뢰할 수 없는 도메인
titleSuffix: SQL Server Big Data Cluster
description: 동작 수정 - 엔드포인트 DNS 항목이 별칭 이름을 가리키는 CNAME으로 구성되면 클라이언트가 인증에 실패합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 05/01/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2cc173ca162ea69e65bce477f83e5ff6f75ac69a
ms.sourcegitcommit: f6200d3d9cdf2627b243384835dc37d2bd40480e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82785272"
---
# <a name="symptom-ad-mode-login-fails---untrusted-domain-big-data-clusters"></a>증상: AD 모드 로그인 실패 - 신뢰할 수 없는 도메인(빅 데이터 클러스터)

Active Directory 모드의 SQL Server BDC(빅 데이터 클러스터)에서 연결 시도가 실패하고 연결 시도에서 다음 오류를 반환합니다.

`Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.`

이는 Kubernetes 노드에 트래픽을 배포하는 역방향 프록시의 별칭 이름을 가리키는 CNAME으로 DNS 항목을 구성한 경우에 발생할 수 있습니다.

## <a name="root-cause"></a>근본 원인

CNAME이 포함된 DNS 항목으로 엔드포인트를 구성하는 경우 CNAME이 Kubernetes 노드에 트래픽을 배포하는 역방향 프록시의 별칭 이름을 가리킵니다.

- Kerberos 인증 프로세스에서는 Active Directory의 BDC에서 등록된 진짜 SPN이 아닌 CNAME의 항목과 일치하는 SPN(서비스 사용자 이름)을 찾습니다.
- 인증에 실패하게 됩니다. 

## <a name="confirm-root-cause"></a>근본 원인 확인

인증에 실패한 후 Kerberos 티켓의 캐시를 확인합니다. 

티켓의 캐시를 확인하려면 `klist` 명령을 사용합니다. 

연결하려는 엔드포인트와 일치하는 SPN을 사용하여 티켓을 찾습니다.

예상했던 티켓이 없습니다.

이 예제에서 마스터 엔드포인트 `bdc-sql` DNS 레코드는 `ServerReverseProxy`라는 CNAME 역방향 프록시로 설정됩니다.

```PowerShell
Resolve-DnsName bdc-sql
```

다음 섹션에서는 이전 명령의 결과를 보여 줍니다.

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
bdc-sql.mydomain.com           CNAME  3600  Answer     ReverseProxyServer.mydomain.com

Name       : ReverseProxyServer.mydomain.com
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 193.168.5.10
```

>[!NOTE]
>다음 섹션에서는 [`tshark`](https://www.wireshark.org/docs/man-pages/tshark.html)를 참조합니다. `tshark`는 [Wireshark](https://www.wireshark.org/docs/) 네트워크 추적 유틸리티의 일부로 설치되는 명령줄 유틸리티입니다.

Active Directory에서 요청된 SPN을 보려면 `tshark`를 사용합니다. 다음 명령은 네트워크 추적 캡처를 Kerberos 프로토콜 통신으로 제한하고 `krb-error (30)` 메시지만 표시합니다. 이러한 메시지는 실패한 SPN 요청 메시지를 포함해야 합니다.

```bash
tshark -Y "kerberos && kerberos.msg_type == 30" -T fields -e kerberos.error_code -e kerberos.SNameString
```

다른 명령 셸에서 마스터 Pod에 연결해 봅니다.

```bash
klist purge

sqlcmd -S bdc-sql.mydomain.com,31433 -E
```

다음 예제 출력을 참조하세요.

```bash
klist purge

Current LogonId is 0:0xf6b58
        Deleting all tickets:
        Ticket(s) purged!

sqlcmd -S bdc-sql.mydomain.com,31433 -E
sqlcmd: Error: Microsoft ODBC Driver 17 for SQL Server : Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.
```

`tshark` 출력을 확인합니다. 

```bash
Capturing on 'Ethernet 3'
25      krbtgt,RLAZURE.COM
7       MSSQLSvc,ReverseProxyServer.mydomain.com:31433
2 packets captured
```

클라이언트 요청 `SPN MSSQLSvc,ReverseProxyServer.mydomain.com:31433`은 존재하지 않는 것을 알 수 있습니다. 결국 연결 시도는 오류 7 때문에 실패합니다. 오류 7은 `KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN Server not found in Kerberos database`를 의미합니다.

올바른 구성에서 클라이언트는 BDC에서 등록된 SPN을 요청합니다. 이 예제에서 올바른 SPN은 `MSSQLSvc,bdc-sql.mydomain.com:31433`입니다.

>[!NOTE]
>오류 25는 `KDC_ERR_PREAUTH_REQUIRED` - 추가 사전 인증이 필요함을 의미합니다. 이 오류는 무시해도 안전합니다. `KDC_ERR_PREAUTH_REQUIRED`는 초기 Kerberos AD 요청에서 반환됩니다. 기본적으로 Windows Kerberos 클라이언트는 이 첫 번째 요청에서 사전 인증 정보를 포함하지 않습니다.

마스터 엔드포인트에 대한 BDC에서 등록된 SPN 목록을 보려면 `setspn -L mssql-master`를 실행합니다. 

다음 예제 출력을 참조하세요.

```bash
Registered ServicePrincipalNames for CN=mssql-master,OU=bdc,DC=mydomain,DC=com:
        MSSQLSvc/bdc-sqlread.mydomain.com:31436
        MSSQLSvc/-sqlread:31436
        MSSQLSvc/bdc-sqlread.mydomain.com
        MSSQLSvc/bdc-sqlread
        MSSQLSvc/bdc-sql.mydomain.com:31433
        MSSQLSvc/bdc-sql:31433
        MSSQLSvc/bdc-sql.mydomain.com
        MSSQLSvc/bdc-sql
        MSSQLSvc/master-p-svc.mydomain.com:1533
        MSSQLSvc/master-p-svc:1533
        MSSQLSvc/master-p-svc.mydomain.com:1433
        MSSQLSvc/master-p-svc:1433
        MSSQLSvc/master-p-svc.mydomain.com
        MSSQLSvc/master-p-svc
        MSSQLSvc/master-svc.mydomain.com:1533
        MSSQLSvc/master-svc:1533
        MSSQLSvc/master-svc.mydomain.com:1433
        MSSQLSvc/master-svc:1433
        MSSQLSvc/master-svc.mydomain.com
        MSSQLSvc/master-svc
```

위의 결과에서 역방향 프록시 주소는 등록되지 않아야 합니다.

## <a name="resolve"></a>해결

이 섹션에서는 문제를 해결하는 두 가지 방법을 보여 줍니다. 적절한 변경을 수행한 후 클라이언트에서 `ipconfig -flushdns` 및 `klist purge`를 실행합니다. 그런 다음 연결을 다시 시도합니다.

### <a name="option-1"></a>옵션 1

DNS의 각 BDC 엔드포인트에 대한 CNAME 레코드를 제거하고, 둘 이상의 마스터가 있는 경우 각 Kubernetes 노드 또는 Kubernetes 마스터를 가리키는 여러 개의 `A` 레코드로 대체합니다.

>[!TIP]
>아래에 설명된 스크립트는 PowerShell을 사용합니다. 자세한 내용은 [Linux에서 PowerShell 설치하기](/powershell/scripting/install/installing-powershell-core-on-linux)를 참조하세요.

다음 PowerShell 스크립트를 사용하여 DNS 엔드포인트 레코드를 업데이트할 수 있습니다. 동일한 도메인에 연결된 모든 컴퓨터에서 스크립트를 실행합니다.

```powershell
#Specify the DNS server, example contoso.local
$Domain_DNS_name=mydomain.com'

#DNS records for bdc endpoints
$Controller_DNS_name = 'bdc-control'
$Managment_proxy_DNS_name= 'bdc-proxy'
$Master_Primary_DNS_name = 'bdc-sql'
$Master_Secondary_DNS_name = 'bdc-sqlread'
$Gateway_DNS_name = 'bdc-gateway'
$AppProxy_DNS_name = 'bdc-appproxy'

#Performing Endpoint DNS records Checks..

#Build array of endpoints 
$BdcEndpointsDns = New-Object System.Collections.ArrayList

[void]$BdcEndpointsDns.Add($Controller_DNS_name)
[void]$BdcEndpointsDns.Add($Managment_proxy_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Primary_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Secondary_DNS_name)
[void]$BdcEndpointsDns.Add($Gateway_DNS_name)
[void]$BdcEndpointsDns.Add($AppProxy_DNS_name)

#Build arrary for results 
$BdcEndpointsDns_Result = New-Object System.Collections.ArrayList

foreach ($DnsName in $BdcEndpointsDns) {
    try {
        $endpoint_DNS_record = Resolve-DnsName $DnsName -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop 
        foreach ($ip in $endpoint_DNS_record.IPAddress) {
            [void]$BdcEndpointsDns_Result.Add("OK - $DnsName is an A record with an IP $ip")
        }
    }
    catch {
        [void]$BdcEndpointsDns_Result.Add("MisConfiguration - $DnsName is not an A record or does not exists")
    }  
}

#show the results 
$BdcEndpointsDns_Result
```

### <a name="option-2"></a>옵션 2

또는 역방향 프록시 이름이 아닌 역방향 프록시의 IP 주소를 가리키도록 CNAME을 수정하여 문제를 해결할 수 있습니다.

## <a name="confirm-resolution"></a>해결 방법 확인

위의 옵션 중 하나로 해결한 후 Active Directory를 사용하여 빅 데이터 클러스터에 연결하여 픽스를 확인합니다.

## <a name="next-steps"></a>다음 단계

[도메인 컨트롤러의 역방향 DNS 항목(PTR 레코드)을 확인](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)합니다.
