---
title: 장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- flexible failover policy
ms.assetid: 39ceaac5-42fa-4b5d-bfb6-54403d7f0dc9
caps.latest.revision: 43
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3b48cf86ed58813c8bcaccea0506e55feb7927a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238193"
---
# <a name="failover-policy-for-failover-cluster-instances"></a>장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스(FCI)에서는 한 번에 하나의 노드에서만 WSFC(Windows Server Failover Cluster) 클러스터 리소스 그룹을 소유할 수 있습니다. 클라이언트 요청은 FCI에서 이 노드를 통해 제공됩니다. 오류가 발생하여 다시 시작이 실패하면 그룹 소유권이 FCI의 다른 WSFC 노드로 이동합니다. 이 프로세스를 장애 조치(Failover)라고 합니다. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 는 오류 검색의 안정성이 향상되었고 유연한 장애 조치(failover) 정책을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI는 장애 조치(failover) 탐지에 대한 기본 WSFC 서비스에 따라 달라집니다. 따라서 기본 WSFC 기능과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서 추가한 기능의 두 가지 메커니즘을 통해 장애 조치(failover) 동작이 결정됩니다.  
  
-   WSFC 클러스터는 자동 장애 조치(failover)에서 고유한 장애 조치(failover) 대상을 보장하는 쿼럼 구성을 유지 관리합니다. WSFC 서비스는 클러스터가 최적의 쿼럼 상태인지 여부를 항상 확인하여 이에 따라 리소스 그룹을 온라인 및 오프라인 상태로 만듭니다.  
  
-   활성 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스는 전용 연결을 통해 WSFC 리소스 그룹에 대한 구성 요소 진단 집합을 주기적으로 보고합니다. WSFC 리소스 그룹은 다시 시작 및 장애 조치(failover)를 트리거하는 오류 상태를 정의한 장애 조치(failover) 정책을 유지 관리합니다.  
  
 이 항목에서는 위의 두 번째 메커니즘에 대해 설명합니다. 쿼럼 구성 및 상태 감지에 대한 WSFC 동작의 자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  FCI로 또는 FCI로부터의 자동 장애 조치(failover)는 AlwaysOn 가용성 그룹에서 허용되지 않습니다. 그러나 FCI로 또는 FCI로부터의 수동 장애 조치(failover)는 AlwaysOn 가용성 그룹에서 허용됩니다.  
  
##  <a name="Concepts"></a> 장애 조치(failover) 정책 개요  
 장애 조치(failover) 프로세스는 다음 단계로 세분화될 수 있습니다.  
  
1.  [상태 모니터링](failover-policy-for-failover-cluster-instances.md#monitor)  
  
2.  [실패 확정](failover-policy-for-failover-cluster-instances.md#determine)  
  
3.  [실패에 대한 응답](failover-policy-for-failover-cluster-instances.md#respond)  
  
###  <a name="monitor"></a> 상태 모니터링  
 모니터링되는 FCI 상태에는 다음의 세 가지 유형이 있습니다.  
  
-   [SQL Server 서비스의 상태](failover-policy-for-failover-cluster-instances.md#service)  
  
-   [SQL Server 인스턴스의 응답](failover-policy-for-failover-cluster-instances.md#instance)  
  
-   [SQL Server 구성 요소 진단](failover-policy-for-failover-cluster-instances.md#component)  
  
####  <a name="service"></a> SQL Server 서비스의 상태  
 WSFC 서비스는 활성 FCI 노드에 대한 SQL Server 서비스의 시작 상태를 모니터링하여 SQL Server 서비스가 중지된 시간을 감지합니다.  
  
####  <a name="instance"></a> SQL Server 인스턴스의 응답  
 SQL Server를 시작하는 동안 WSFC 서비스는 SQL Server 데이터베이스 엔진 리소스 DLL을 사용하여, 상태 모니터링을 위해 배타적으로 사용되는 별도의 스레드로 새 연결을 만듭니다. 이렇게 하면 로드가 있는 상황에서 SQL 인스턴스가 자신의 상태를 보고하는 데 필요한 리소스를 가지고 있도록 보장됩니다. 이 전용 연결을 통해 SQL Server는 [sp_server_diagnostics&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) 시스템 저장 프로시저를 반복적으로 실행하여 리소스 DLL에 대한 SQL Server 구성 요소의 상태를 주기적으로 보고합니다.  
  
 리소스 DLL은 상태 확인 제한 시간을 사용하여 SQL 인스턴스의 응답을 확인합니다. HealthCheckTimeout 속성은 리소스 DLL이 SQL 인스턴스가 WSFC Server 서비스에 응답하지 않는 것으로 보고하기 전에 sp_server_diagnostics 저장 프로시저를 대기해야 하는 시간을 정의합니다. 이 속성은 장애 조치(failover) 클러스터 관리자 스냅인뿐만 아니라 T-SQL을 사용하여 구성할 수 있습니다. 자세한 내용은 [Configure HealthCheckTimeout Property Settings](configure-healthchecktimeout-property-settings.md)을 참조하세요. 다음 항목에서는 이 속성이 제한 시간 및 반복 간격 설정에 어떻게 영향을 주는지에 대해 설명합니다.  
  
-   리소스 DLL은 sp_server_diagnostics 저장 프로시저를 호출하고 반복 간격을 HealthCheckTimeout 설정의 1/3로 설정합니다.  
  
-   sp_server_diagnostics 저장 프로시저가 느리거나 정보를 반환하지 않는 경우 리소스 DLL은 SQL 인스턴스가 응답하지 않는 것으로 WSFC 서비스에 보고하기 전에 HealthCheckTimeout에서 지정된 간격 동안 대기합니다.  
  
-   전용 연결이 손실된 경우 리소스 DLL은 SQL 인스턴스가 응답하지 않는 것으로 WSFC 서비스에 보고하기 전에 HealthCheckTimeout에서 지정된 간격 동안 SQL 인스턴스에 연결을 다시 시도합니다.  
  
####  <a name="component"></a> SQL Server 구성 요소 진단  
 sp_server_diagnostics 시스템 저장 프로시저는 SQL 인스턴스에 대한 구성 요소 진단을 주기적으로 수집합니다. 수집된 진단 정보는 다음 각 구성 요소의 행으로 표시되고 호출 스레드에 전달됩니다.  
  
1.  시스템  
  
2.  resource  
  
3.  쿼리 프로세스  
  
4.  io_subsystem  
  
5.  이벤트  
  
 시스템, 리소스 및 쿼리 프로세스 구성 요소는 실패 감지에 사용됩니다. IO 하위 시스템 및 이벤트 구성 요소는 진단용으로만 사용됩니다.  
  
 또한 정보의 각 행 집합이 SQL Server 클러스터 진단 로그에 기록됩니다. 자세한 내용은 [장애 조치(failover) 클러스터 인스턴스 진단 로그 보기 및 읽기](view-and-read-failover-cluster-instance-diagnostics-log.md)를 참조하세요.  
  
> [!TIP]  
>  sp_server_diagnostic 저장 프로시저는 SQL Server AlwaysOn 기술에서 사용되는 동안 문제를 감지하고 해결하는 데 도움이 되도록 SQL Server 인스턴스에서 사용이 가능합니다.  
  
####  <a name="determine"></a> 실패 확정  
 SQL Server 데이터베이스 엔진 리소스 DLL은 FailureConditionLevel 속성을 사용하여 감지된 상태가 오류 상태인지 여부를 결정합니다. FailureConditionLevel 속성은 감지된 상태 중에서 다시 시작 또는 장애 조치(failover)의 원인이 된 상태를 결정합니다. 자동 다시 시작 또는 장애 조치(failover) 사용 안 함에서부터 자동 다시 시작 또는 장애 조치(failover)를 초래하는 모든 오류 상태에 이르기까지 다양한 수준의 옵션을 사용할 수 있습니다. 이 속성을 구성하는 방법은 [Configure FailureConditionLevel Property Settings](configure-failureconditionlevel-property-settings.md)을 참조하십시오.  
  
 실패 조건은 증가하는 범위로 설정됩니다. 수준 1-5의 경우 각 수준에는 자체 조건과 함께 이전 수준의 모든 조건이 포함됩니다. 이는 수준이 높을수록 장애 조치(Failover) 또는 다시 시작 확률이 증가함을 의미합니다. 다음 표에서는 실패 조건 수준에 대해 설명합니다.  
  
 이 시스템 저장 프로시저는 오류 상태 수준에서 중요한 역할을 하므로 [sp_server_diagnostics&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)를 검토하세요.  
  
|Level|조건|Description|  
|-----------|---------------|-----------------|  
|0|자동 장애 조치(Failover) 또는 다시 시작 안 함|어떤 실패 조건에서도 장애 조치(Failover) 또는 다시 시작이 자동으로 트리거되지 않음을 나타냅니다. 이 수준은 시스템 유지 관리 목적으로만 제공됩니다.|  
|1|서버 다운 시 장애 조치(Failover) 또는 다시 시작|다음 조건이 발생한 경우 서버가 다시 시작되거나 장애 조치(Failover)됨을 나타냅니다.<br /><br /> SQL Server 서비스가 다운된 경우|  
|2|서버가 응답하지 않는 경우 장애 조치(Failover) 또는 다시 시작|다음 조건 중 하나가 발생한 경우 서버가 다시 시작되거나 장애 조치(Failover)됨을 나타냅니다.<br /><br /> SQL Server 서비스가 다운된 경우<br /><br /> SQL 서버 인스턴스가 응답하지 않을 경우(리소스 DLL이 HealthCheckTimeout 설정의 sp_server_diagnostics에서 데이터를 받을 수 없음)|  
|3*|심각한 서버 오류 시 장애 조치(Failover) 또는 다시 시작|다음 조건 중 하나가 발생한 경우 서버가 다시 시작되거나 장애 조치(Failover)됨을 나타냅니다.<br /><br /> SQL Server 서비스가 다운된 경우<br /><br /> SQL 서버 인스턴스가 응답하지 않을 경우(리소스 DLL이 HealthCheckTimeout 설정의 sp_server_diagnostics에서 데이터를 받을 수 없음)<br /><br /> 시스템 저장 프로시저 sp_server_diagnostics가 '시스템 오류'를 반환할 경우|  
|4|일반적인 서버 오류 시 장애 조치(Failover) 또는 다시 시작|다음 조건 중 하나가 발생한 경우 서버가 다시 시작되거나 장애 조치(Failover)됨을 나타냅니다.<br /><br /> SQL Server 서비스가 다운된 경우<br /><br /> SQL 서버 인스턴스가 응답하지 않을 경우(리소스 DLL이 HealthCheckTimeout 설정의 sp_server_diagnostics에서 데이터를 받을 수 없음)<br /><br /> 시스템 저장 프로시저 sp_server_diagnostics가 '시스템 오류'를 반환할 경우<br /><br /> 시스템 저장 프로시저 sp_server_diagnostics가 '리소스 오류'를 반환할 경우|  
|5|임의의 실패 조건 발생 시 장애 조치(Failover) 또는 다시 시작|다음 조건 중 하나가 발생한 경우 서버가 다시 시작되거나 장애 조치(Failover)됨을 나타냅니다.<br /><br /> SQL Server 서비스가 다운된 경우<br /><br /> SQL 서버 인스턴스가 응답하지 않을 경우(리소스 DLL이 HealthCheckTimeout 설정의 sp_server_diagnostics에서 데이터를 받을 수 없음)<br /><br /> 시스템 저장 프로시저 sp_server_diagnostics가 '시스템 오류'를 반환할 경우<br /><br /> 시스템 저장 프로시저 sp_server_diagnostics가 '리소스 오류'를 반환할 경우<br /><br /> 시스템 저장 프로시저 sp_server_diagnostics가 'query_processing 오류'를 반환할 경우|  
  
 *기본값  
  
####  <a name="respond"></a> 실패에 대한 응답  
 하나 이상의 오류 상태가 감지된 경우 WSFC 서비스의 오류 대응 방법은 FCI 리소스 그룹의 다시 시작 및 장애 조치(failover) 설정과 WSFC 쿼럼 상태에 따라 다릅니다. FCI에 손실된 WSFC 쿼럼이 있으면 전체 FCI가 오프라인 상태가 되고 해당 FCI의 고가용성이 손실됩니다. 이 FCI가 계속 WSFC 쿼럼을 유지하면 WSFC 서비스는 실패한 노드의 다시 시작을 처음 시도하여 대응하고 다시 시작 시도가 실패할 경우 장애 조치(failover)할 수도 있습니다. 다시 시작 및 장애 조치(failover) 설정은 장애 조치(failover) 클러스터 관리자 스냅인에서 구성됩니다. 이러한 설정에 대한 자세한 내용은 [\<리소스> 속성: 정책 탭](http://technet.microsoft.com/library/cc725685.aspx)을 참조하세요.  
  
 쿼럼 상태의 유지 관리에 대한 자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
