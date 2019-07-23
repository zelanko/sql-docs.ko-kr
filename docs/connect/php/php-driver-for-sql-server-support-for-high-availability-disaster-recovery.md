---
title: SQL Server 용 Microsoft driver for PHP에 대 한 고가용성, 재해 복구 지원 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fab65d777025f59fab6566d118233febbb51aaa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992967"
---
# <a name="support-for-high-availability-disaster-recovery"></a>고가용성, 재해 복구 지원
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 고가용성 재해 복구를 위한 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 지원(버전 3.0에서 추가)인 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대해 설명합니다.  [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 지원은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 추가되었습니다. [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 3.0에서는 연결 속성에 (고가용성, 재해 복구) 가용성 그룹(AG)의 가용성 그룹 수신기를 지정할 수 있습니다. [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 애플리케이션이 장애 조치되는 AlwaysOn 데이터베이스에 연결되는 경우 장애 조치 후 작업을 계속하기 위해 원래 연결이 끊어지고 애플리케이션은 새 연결을 열어야 합니다.  
  
가용성 그룹 수신기에 연결하지 않았고 여러 IP 주소가 호스트 이름과 연결된 경우 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]는 DNS 항목과 연결된 모든 IP 주소를 순차적으로 반복합니다. DNS 서버가 반환한 첫 번째 IP 주소가 NIC(네트워크 인터페이스 카드)에 바인딩되지 않은 경우 시간이 오래 걸릴 수 있습니다. 가용성 그룹 수신기에 연결할 때 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]는 모든 IP 주소에 병렬로 연결을 설정하려고 시도하며 연결 시도가 성공하면 드라이버는 보류 중인 연결 시도를 삭제합니다.  
  
> [!NOTE]  
> 연결 제한 시간을 늘리고 연결 재시도 논리를 구현하면 애플리케이션이 가용성 그룹에 연결될 가능성이 증가합니다. 또한 가용성 그룹 장애 조치(failover)로 인해 연결이 실패할 수 있으므로 실패한 연결을 다시 연결할 때까지 다시 시도하는 연결 재시도 논리를 구현해야 합니다.  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover로 연결  
**MultiSubnetFailover** 연결 속성은 애플리케이션을 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 배포하는 중이며 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]가 모든 IP 주소에 연결을 시도하여 주 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터베이스에 연결을 시도함을 나타냅니다. 연결에 대해 **MultiSubnetFailover=true**를 지정하면 클라이언트는 운영 체제의 기본 TCP 재전송 간격보다 빠르게 TCP 연결을 다시 시도합니다. 이렇게 하면 AlwaysOn 가용성 그룹 또는 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스의 장애 조치(Failover) 후 더 빠르게 다시 연결할 수 있습니다. 이 설정은 단일/다중 서브넷 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 모두 적용됩니다.  
  
SQL Server 2012 가용성 그룹 수신기 또는 SQL Server 2012 장애 조치(Failover) 클러스터 인스턴스에 연결할 때는 항상 **MultiSubnetFailover=True**를 지정하세요. **MultiSubnetFailover**를 사용하면 SQL Server 2012에서 모든 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 대한 장애 조치(Failover)를 빠르게 수행하고 단일 및 다중 서브넷 AlwaysOn 토폴로지에 대한 장애 조치(Failover) 시간을 크게 줄일 수 있습니다. 다중 서브넷 장애 조치(Failover) 중에는 클라이언트가 연결을 병렬로 시도합니다. 서브넷을 장애 조치하는 동안 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]는 TCP 연결을 공격적으로 재시도합니다.  
  
의 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]연결 문자열 키워드에 대 한 자세한 내용은 [connection Options](../../connect/php/connection-options.md)을 참조 하세요.  
  
가용성 그룹 수신기 또는 장애 조치(Failover) 클러스터 인스턴스 이외의 다른 항목에 연결할 때 **MultiSubnetFailover=true**를 지정하면 성능에 상당히 부정적인 영향을 줄 수 있으므로 이러한 설정은 지원되지 않습니다.  
  
다음 지침에 따라 가용성 그룹의 서버에 연결하십시오.  
  
-   단일 서브넷 또는 다중 서브넷에 연결할 때 **MultiSubnetFailover** 연결 속성을 사용하면 두 서브넷의 성능이 향상됩니다.  
  
-   가용성 그룹에 연결하려면 가용성 그룹에 대한 가용성 그룹 수신기를 연결 문자열의 서버로 지정합니다.  
  
-   IP 주소가 64개 이상으로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 연결 오류가 발생합니다.  
  
-   **MultiSubnetFailover** 연결 속성을 사용하는 애플리케이션 동작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증, Kerberos 인증, Windows 인증과 같은 인증 유형의 영향을 받지 않습니다.  
  
-   장애 조치(failover) 시간을 수용하고 애플리케이션의 연결 재시도 횟수를 줄이기 위해 **loginTimeout** 값을 증가시킵니다.  
  
-   분산 트랜잭션은 지원되지 않습니다.  
  
읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
- 보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
- 애플리케이션에서 **ApplicationIntent=ReadWrite**(아래에서 설명)를 사용하고 보조 복제본 위치가 읽기 전용 액세스용으로 구성되어 있는 경우  
  
주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 **ApplicationIntent=ReadOnly**가 포함되어 있으면 연결이 실패합니다.  

## <a name="transparent-network-ip-resolution-tnir"></a>TNIR(투명 네트워크 IP 확인)

TNIR (투명 네트워크 IP 확인)은 기존 MultiSubnetFailover 기능을 수정한 것입니다. 호스트 이름에 대 한 첫 번째 확인 된 IP가 응답 하지 않고 호스트 이름과 연결 된 여러 ip가 있는 경우 드라이버의 연결 시퀀스에 영향을 줍니다. MultiSubnetFailover와 함께 다음 네 가지 연결 시퀀스를 제공 합니다. 

- TNIR 사용 & MultiSubnetFailover 사용 안 함: 하나의 IP가 시도 된 후 모든 ip가 병렬로 수행 됩니다.
- TNIR Enabled & MultiSubnetFailover Enabled: 모든 Ip가 병렬로 시도 됩니다.
- TNIR 사용 안 함 & MultiSubnetFailover 사용 안 함: 모든 Ip를 한 후에 시도 합니다.
- TNIR Disabled & MultiSubnetFailover Enabled: 모든 Ip가 병렬로 시도 됩니다.

TNIR은 기본적으로 사용 하도록 설정 되며 MultiSubnetFailover는 기본적으로 사용 하지 않도록 설정 됩니다.

다음은 PDO_SQLSRV 드라이버를 사용 하 여 TNIR 및 MultiSubnetFailover를 모두 사용 하도록 설정 하는 예입니다.

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>데이터베이스 미러링에서 다중 서브넷 클러스터를 사용하도록 업그레이드  
연결 문자열에 **MultiSubnetFailover** 및 **Failover_Partner** 연결 키워드가 있으면 연결 오류가 발생합니다. **MultiSubnetFailover**가 사용되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 미러링 쌍의 일부임을 나타내는 장애 조치(failover) 파트너 응답을 반환하는 경우에도 오류가 발생합니다.  
  
현재 데이터베이스 미러링을 사용 중인 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 애플리케이션을 다중 서브넷 시나리오로 업그레이드할 경우에는 **Failover_Partner** 연결 속성을 제거하고, 이를 **Yes**로 설정된 **MultiSubnetFailover**로 바꾸고, 연결 문자열에서 서버 이름을 가용성 그룹 수신기로 바꿔야 합니다. 연결 문자열에서 **Failover_Partner** 및 **MultiSubnetFailover=true**를 사용하는 경우 드라이버에서 오류가 발생합니다. 그러나 연결 문자열에서 **Failover_Partner** 및 **MultiSubnetFailover=false**(또는 **ApplicationIntent=ReadWrite**)를 사용하면 애플리케이션에서 데이터베이스 미러링을 사용합니다.  
  
AG의 주 데이터베이스에서 데이터베이스 미러링이 사용되고 가용성 그룹 수신기가 아닌 주 데이터베이스에 연결하는 연결 문자열에 **MultiSubnetFailover=true**가 사용될 경우 드라이버에서는 오류를 반환합니다.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>참고 항목  
[서버에 연결](../../connect/php/connecting-to-the-server.md)  
  
