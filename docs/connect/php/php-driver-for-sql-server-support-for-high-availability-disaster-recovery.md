---
title: 고가용성 Microsoft Drivers for PHP for SQL Server에 대 한 재해 복구에 대 한 지원 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6cb7f145f14861720d11401a3d60db0ce0efcfd9
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="support-for-high-availability-disaster-recovery"></a>고가용성, 재해 복구 지원
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 설명 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 고가용성, 재해 복구를 위한 지원 (버전 3.0에서에서 추가) [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]합니다.  [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 지원은 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]에서 추가되었습니다. [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서를 참조하십시오.  
  
버전 3.0은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 가용성 그룹 수신기를 지정할 수 있습니다 (고가용성, 재해 복구) 가용성 그룹 (AG) 연결 속성에 있습니다. 경우는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 응용 프로그램이 장애 조치 되는 AlwaysOn 데이터베이스에 연결 되어, 원래 연결이 끊어지고 및 응용 프로그램 장애 조치 후 작업을 계속 하려면 새 연결을 열어야 합니다.  
  
가용성 그룹 수신기에 연결 하지 하는 경우와 여러 IP 주소는 호스트 이름으로 관련 되어 있는 경우는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] DNS 항목과 연결 된 모든 IP 주소를 순차적으로 반복 됩니다. DNS 서버가 반환한 첫 번째 IP 주소가 NIC(네트워크 인터페이스 카드)에 바인딩되지 않은 경우 시간이 오래 걸릴 수 있습니다. 가용성 그룹 수신기에 연결할 때는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] parallel 및 연결을 시도 하는 경우 모든 IP 주소에 대 한 연결을 설정 하려고 시도 성공 하면, 드라이버는 보류 중인 연결 시도 삭제 합니다.  
  
> [!NOTE]  
> 연결 제한 시간을 늘리고 연결 재시도 논리를 구현하면 응용 프로그램이 가용성 그룹에 연결될 가능성이 증가합니다. 또한 가용성 그룹 장애 조치(failover)로 인해 연결이 실패할 수 있으므로 실패한 연결을 다시 연결할 때까지 다시 시도하는 연결 재시도 논리를 구현해야 합니다.  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover로 연결  
**MultiSubnetFailover** 가용성 그룹 또는 장애 조치 클러스터 인스턴스 및 사용 하는 응용 프로그램은 배포 되는 연결 속성 나타냅니다는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 주데이터베이스에연결하려고합니다[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 모든 IP에 연결 하려고 시도 하 여 인스턴스 주소입니다. 때 **MultiSubnetFailover = true** 연결에 대해 지정 된 클라이언트 운영 체제의 기본 TCP 재전송 간격 보다 빠르게 TCP 연결 시도 다시 시도 합니다. 이렇게 하면 AlwaysOn 가용성 그룹 또는 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스의 장애 조치(Failover) 후 더 빠르게 다시 연결할 수 있습니다. 이 설정은 단일/다중 서브넷 가용성 그룹 및 장애 조치(Failover) 클러스터 인스턴스에 모두 적용됩니다.  
  
항상 지정 **MultiSubnetFailover = True** SQL Server 2012 가용성 그룹 수신기 또는 SQL Server 2012 장애 조치 클러스터 인스턴스에 연결할 때. **MultiSubnetFailover** 모든 가용성 그룹 및 SQL Server 2012에서 장애 조치 클러스터 인스턴스에 대 한 보다 빠르게 장애 조치할 수 있도록 하 고 단일 및 다중 서브넷 AlwaysOn 토폴로지에 대 한 장애 조치 시간을 크게 줄여 줍니다. 다중 서브넷 장애 조치(Failover) 중에는 클라이언트가 연결을 병렬로 시도합니다. 서브넷 장애 조치 동안는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] TCP 연결을 공격적으로 재시도 합니다.  
  
연결 문자열 키워드에 대 한 자세한 내용은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], 참조 [연결 옵션](../../connect/php/connection-options.md)합니다.  
  
지정 **MultiSubnetFailover = true** 때 가용성 그룹 수신기 또는 장애 조치 클러스터 인스턴스 이외의 대상에 연결할 성능에 부정적인 영향이 있으며 지원 되지 않습니다.  
  
다음 지침에 따라 가용성 그룹의 서버에 연결하십시오.  
  
-   단일 서브넷 또는 다중 서브넷에 연결할 때 **MultiSubnetFailover** 연결 속성을 사용하면 두 서브넷의 성능이 향상됩니다.  
  
-   가용성 그룹에 연결하려면 가용성 그룹에 대한 가용성 그룹 수신기를 연결 문자열의 서버로 지정합니다.  
  
-   IP 주소가 64개 이상으로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 연결하면 연결 오류가 발생합니다.  
  
-   **MultiSubnetFailover** 연결 속성을 사용하는 응용 프로그램 동작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증, Kerberos 인증, Windows 인증과 같은 인증 유형의 영향을 받지 않습니다.  
  
-   값 늘리기 **loginTimeout** 하 장애 조치 시간을 수용 하 고 응용 프로그램 연결 재시도 횟수를 줄입니다.  
  
-   분산 트랜잭션은 지원되지 않습니다.  
  
읽기 전용 라우팅이 적용되지 않으면 다음과 같은 경우 가용성 그룹의 보조 복제본 위치에 대한 연결이 실패합니다.  
  
1.  보조 복제본 위치가 연결을 허용하도록 구성되어 있지 않은 경우  
  
2.  응용 프로그램에서 **ApplicationIntent=ReadWrite**(아래에서 설명)를 사용하고 보조 복제본 위치가 읽기 전용 액세스용으로 구성되어 있는 경우  
  
주 복제본이 읽기 전용 작업을 거부하도록 구성되어 있고 연결 문자열에 **ApplicationIntent=ReadOnly**가 포함되어 있으면 연결이 실패합니다.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>데이터베이스 미러링에서 다중 서브넷 클러스터를 사용하도록 업그레이드  
연결 문자열에 **MultiSubnetFailover** 및 **Failover_Partner** 연결 키워드가 있으면 연결 오류가 발생합니다. **MultiSubnetFailover**가 사용되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서 데이터베이스 미러링 쌍의 일부임을 나타내는 장애 조치(failover) 파트너 응답을 반환하는 경우에도 오류가 발생합니다.  
  
업그레이드 하는 경우는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 제거 해야 하는 다중 서브넷 시나리오에 데이터베이스 미러링을 사용 중인 응용 프로그램의 **에서 Failover_Partner** 연결 속성이로 바꿉니다 **MultiSubnetFailover**  로 설정 **예** 연결 문자열에서 서버 이름을 가용성 그룹 수신기로 바꿉니다. 연결 문자열을 사용 하는 경우 **에서 Failover_Partner** 및 **MultiSubnetFailover = true**, 드라이버에서 오류가 발생 합니다. 그러나 연결 문자열을 사용 하는 경우 **에서 Failover_Partner** 및 **MultiSubnetFailover = false** (또는 **ApplicationIntent = ReadWrite**), 응용 프로그램에서는 데이터베이스를 사용 합니다. 미러링입니다.  
  
드라이버는 AG의 주 데이터베이스에서 데이터베이스 미러링이 사용 되 고 오류가 반환 됩니다 **MultiSubnetFailover = true** 대신 가용성 그룹에 주 데이터베이스에 연결 하는 연결 문자열에 사용 됩니다 수신기 수 있습니다.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>관련 항목  
[서버에 연결](../../connect/php/connecting-to-the-server.md)  
  
