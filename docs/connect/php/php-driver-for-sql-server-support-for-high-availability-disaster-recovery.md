---
title: Microsoft Drivers for PHP for SQL Server에 대한 고가용성, 재해 복구 지원 | Microsoft Docs
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
ms.openlocfilehash: 9f67a0cc7f564683ed11ce7d7de9da5200128434
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76929175"
---
# <a name="support-for-high-availability-disaster-recovery"></a>고가용성, 재해 복구 지원
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 고가용성, 재해 복구를 위한 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 지원(버전 3.0에서 추가)에 대해 설명합니다.

Microsoft Drivers for PHP for SQL Server 버전 3.0부터 연결 문자열에 고가용성, 재해 복구 가용성 그룹 또는 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기를 서버로 지정할 수 있습니다.

**MultiSubnetFailover** 연결 속성은 애플리케이션을 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 배포하는 중이며 드라이버가 모든 IP 주소에 연결을 시도하여 주 SQL Server 인스턴스의 데이터베이스에 연결을 시도함을 나타냅니다. SQL Server 가용성 그룹 수신기 또는 SQL Server 장애 조치(Failover) 클러스터 인스턴스에 연결할 때는 항상 **MultiSubnetFailover=True**를 지정하세요. 애플리케이션이 장애 조치되는 AlwaysOn 데이터베이스에 연결되는 경우 장애 조치 후 작업을 계속하기 위해 원래 연결이 끊어지고 애플리케이션은 새 연결을 열어야 합니다.

Always On 가용성 그룹에 대한 자세한 내용은 [고가용성, 재해 복구](https://docs.microsoft.com/sql/relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery) 문서 페이지에서 확인할 수 있습니다.

## <a name="transparent-network-ip-resolution-tnir"></a>TNIR(투명 네트워크 IP 확인)

TNIR(투명 네트워크 IP 확인)은 기존 **MultiSubnetFailover** 기능의 수정 버전입니다. 이 기능은 호스트 이름의 첫 번째 확인된 IP가 응답하지 않고 호스트 이름과 연결된 여러 IP가 있는 경우 드라이버의 연결 시퀀스에 영향을 미칩니다. 해당 연결 옵션은 **TransparentNetworkIPResolution**입니다. **MultiSubnetFailover**와 함께 다음 네 가지 연결 시퀀스를 제공합니다. 

- TNIR 사용 및 **MultiSubnetFailover** 사용 안 함: 하나의 IP를 시도한 후 모든 IP를 병렬로 시도
- TNIR 사용 및 **MultiSubnetFailover** 사용: 모든 IP를 병렬로 시도
- TNIR 사용 안 함 및 **MultiSubnetFailover** 사용 안 함: 모든 IP를 한 번 시도
- TNIR 사용 안 함 및 **MultiSubnetFailover** 사용: 모든 IP를 병렬로 시도

TNIR은 기본적으로 사용하도록 설정되어 있으며 **MultiSubnetFailover**은 기본적으로 사용하지 않도록 설정되어 있습니다.

다음은 PDO_SQLSRV 드라이버를 사용하여 TNIR 및 **MultiSubnetFailover**를 모두 사용하도록 설정하는 예입니다.

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
연결 문자열에 **MultiSubnetFailover** 및 **Failover_Partner** 연결 키워드가 있으면 연결 오류가 발생합니다. **MultiSubnetFailover**가 사용되고 SQL Server가 데이터베이스 미러링 쌍의 일부임을 나타내는 장애 조치(failover) 파트너 응답을 반환하는 경우에도 오류가 발생합니다.  
  
현재 데이터베이스 미러링을 사용 중인 PHP 애플리케이션을 다중 서브넷 시나리오로 업그레이드할 경우에는 **Failover_Partner** 연결 속성을 제거하고, 이를**True**로 설정된 **MultiSubnetFailover**로 바꾸고, 연결 문자열에서 서버 이름을 가용성 그룹 수신기로 바꿉니다. 연결 문자열에서 **Failover_Partner** 및 **MultiSubnetFailover=true**를 사용하는 경우 드라이버에서 오류가 발생합니다. 그러나 연결 문자열에서 **Failover_Partner** 및 **MultiSubnetFailover=false**(또는 **ApplicationIntent=ReadWrite**)를 사용하면 애플리케이션에서 데이터베이스 미러링을 사용합니다.  
  
AG의 주 데이터베이스에서 데이터베이스 미러링이 사용되고 가용성 그룹 수신기가 아닌 주 데이터베이스에 연결하는 연결 문자열에 **MultiSubnetFailover=true**가 사용될 경우 드라이버에서는 오류를 반환합니다.  

[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>참고 항목  
[서버에 연결](../../connect/php/connecting-to-the-server.md)  
  
