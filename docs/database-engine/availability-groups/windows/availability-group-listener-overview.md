---
title: 가용성 그룹 수신기란?
description: 'Always On 가용성 그룹 수신기와 이 수신기가 트래픽을 의도한 서버로 자동으로 보내는 방법을 간략하게 설명합니다. '
ms.custom: seodec18
ms.date: 02/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bd425438dc4a06faea489ac9cba4b607492fcde8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900406"
---
# <a name="what-is-an-availability-group-listener"></a>가용성 그룹 수신기란?  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

가용성 그룹 수신기는 Always On 가용성 그룹의 주 복제본 또는 보조 복제본에 있는 데이터베이스에 액세스하기 위해 클라이언트가 연결할 수 있는 VNN(가상 네트워크 이름)입니다. 수신기를 사용하면 클라이언트가 SQL Server의 실제 인스턴스 이름을 몰라도 복제본에 연결할 수 있습니다. 수신기가 트래픽을 라우팅하기 때문에 장애 조치(failover) 후에 클라이언트 연결 문자열을 수정하지 않아도 됩니다. 

가용성 그룹 수신기는 DNS(Domain Name System) 수신기 이름, 수신기 포트 지정 및 하나 이상의 IP 주소로 구성됩니다. 가용성 그룹 수신기는 TCP 프로토콜만 지원합니다.  수신기의 DNS 이름은 도메인 및 NetBIOS에서 고유해야 합니다.  수신기를 만들면, 연결된 VNN(가상 네트워크 이름), VIP(가상 IP) 및 가용성 그룹 종속성이 있는 클러스터의 리소스가 됩니다. 클라이언트는 DNS를 사용하여 VNN을 여러 IP 주소로 확인한 다음 연결 요청이 성공하거나 연결 요청 시간이 초과될 때까지 각 주소로 연결을 시도합니다.  
  
하나 이상의 [읽기 가능한 보조 복제본](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)에 대해 읽기 전용 라우팅을 구성할 경우, 수신기에 대한 읽기 전용 클라이언트 연결이 읽기 가능한 보조 복제본으로 자동 리디렉션됩니다. 
  
이 문서에서는 가용성 그룹 수신기를 간략하게 설명합니다. [수신기를 구성](create-or-configure-an-availability-group-listener-sql-server.md)한 다음, [수신기에 연결](listeners-client-connectivity-application-failover.md)하는 방법을 알아볼 수도 있습니다.
  
  
##  <a name="listener-parameters"></a><a name="AGlConfig"></a> 수신기 매개 변수  

 가용성 그룹 수신기는 다음을 사용합니다.
  
 **고유 DNS 이름**  
 이것은 VNN(가상 네트워크 이름)이라고도 합니다. DNS 호스트 이름에 대한 Active Directory 명명 규칙이 적용됩니다. 자세한 내용은 [컴퓨터, 도메인, 사이트 및 OU에 대한 Active Directory 명명 규칙(](https://support.microsoft.com/kb/909264) KB 문서를 참조하세요.  
  
**하나 이상의 VIP(가상 IP 주소)**  
 VIP는 가용성 그룹이 장애 조치(failover)할 수 있는 하나 이상의 서브넷에 대해 구성됩니다.  
  
**IP 주소 구성**  
 지정된 가용성 그룹 수신기의 경우 IP 주소에서 DHCP(Dynamic Host Configuration Protocol) 또는 하나 이상의 고정 IP 주소를 사용할 수 있습니다. DHCP를 사용하면 장애 조치(failover) 중에 연결이 지연될 수 있으므로, 프로덕션 환경에서는 사용하지 않는 것이 좋습니다. 여러 서브넷에 걸쳐 확장되거나 하이브리드 네트워크 구성을 사용하는 가용성 그룹은 고정 IP 주소를 사용해야 합니다. 
 
  
##  <a name="listener-port"></a><a name="SelectListenerPort"></a> 수신기 포트 
 가용성 그룹 수신기를 구성할 때 포트를 지정해야 합니다.  클라이언트 연결 문자열을 간소화하기 위해 기본 포트를 1433으로 구성할 수 있습니다. 1433을 사용하는 경우에는 연결 문자열에서 포트 번호를 지정할 필요가 없습니다. 또한 가용성 그룹 수신기마다 별도의 가상 네트워크 이름이 있으므로 단일 WSFC에 구성된 각 가용성 그룹 수신기가 동일한 기본 포트 1433을 참조하도록 구성할 수 있습니다.  
  
 비표준 수신기 포트를 지정할 수도 있지만, 이렇게 할 경우 가용성 그룹 수신기에 연결할 때마다 연결 문자열에서 대상 포트를 명시적으로 지정해야 합니다.  또한 비표준 포트의 경우 방화벽에 대한 열기 권한이 있어야 합니다.  
  
 가용성 그룹 수신기 VNN에 대해 기본 포트 1433을 사용할 경우 클러스터 노드에 이 포트를 사용 중인 다른 서비스가 없어야 합니다. 그렇지 않으면 포트 충돌이 발생합니다.  
  
 SQL Server의 인스턴스 중 하나가 인스턴스 수신기를 통해 TCP 포트 1433을 이미 수신 중이고 컴퓨터에 포트 1433을 수신 중인 다른 서비스(SQL Server의 추가 인스턴스 포함)가 없는 경우에는 가용성 그룹 수신기와 포트 충돌이 발생하지 않습니다.  이는 가용성 그룹 수신기가 동일한 서비스 프로세스 내에서 동일한 TCP 포트를 공유할 수 있기 때문입니다.  그러나 SQL Server의 여러 인스턴스에서 동일한 포트를 동시에 수신하도록 구성하면 안 됩니다.  
  
  
##  <a name="behavior-of-client-connections-on-failover"></a><a name="CCBehaviorOnFailover"></a> 장애 조치(Failover) 시 클라이언트 연결 동작  

 가용성 그룹 장애 조치(failover)가 발생하면 가용성 그룹에 대한 기존의 영구 연결이 종료되므로 클라이언트는 동일한 주 데이터베이스 또는 읽기 전용 보조 데이터베이스로 계속 작업하려면 새 연결을 설정해야 합니다.  서버측에서 장애 조치(failover)가 수행 중인 동안에는 가용성 그룹에 연결할 수 없으며, 주 데이터베이스가 다시 온라인으로 전환될 때까지 클라이언트 애플리케이션에서 연결을 다시 시도합니다.  
  
 클라이언트 애플리케이션의 연결 시도 중에 연결 제한 시간 이전에 가용성 그룹이 다시 온라인으로 전환되는 경우에는 내부적으로 연결을 재시도하는 과정에서 클라이언트 드라이버가 성공적으로 연결될 수 있으며 이 경우 애플리케이션에 오류가 표시되지 않습니다.  


## <a name="next-steps"></a>다음 단계

이제 가용성 그룹 수신기의 작동 방식을 알고 있으므로, [수신기를 만든](create-or-configure-an-availability-group-listener-sql-server.md) 후에 [수신기에 연결](listeners-client-connectivity-application-failover.md)하도록 애플리케이션을 구성합니다. 다양한 [가용성 그룹 모니터링 전략](monitoring-of-availability-groups-sql-server.md)을 검토하여 가용성 그룹의 상태를 확인할 수도 있습니다. 

가용성 그룹에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요. 
  

  
  
