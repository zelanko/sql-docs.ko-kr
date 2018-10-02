---
title: SQL Server 가용성 그룹 임대 상태 확인 제한 시간 | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a80cbbbca40a48c1469c84a5c7a4968770c5ee7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647861"
---
# <a name="mechanics-and-guidelines-of-lease-cluster-and-health-check-timeouts"></a>임대, 클러스터 및 상태 확인 제한 시간의 메커니즘 및 지침 

가동 시간 및 성능에 대한 다른 응용 프로그램 요구 사항뿐만 아니라 하드웨어, 소프트웨어 및 클러스터 구성의 차이에는 임대, 클러스터 및 상태 확인 제한 시간 값에 대한 특정 구성이 필요합니다. 특정 응용 프로그램 및 워크로드에는 다음과 같은 심각한 오류로 인한 가동 중지 시간을 제한하기 위해 보다 적극적으로 모니터링이 필요합니다. 다른 기능은 일시적인 네트워크 문제에 대한 자세한 허용 오차를 필요로 하며, 높은 리소스 사용량에 대해 대기하고 느린 장애 조치에 문제가 발생하지 않습니다. 

각 노드의 여러 서비스는 오류를 검색하도록 작동합니다. 클러스터 서비스는 쿼럼 손실을 검색할 수 있습니다. 리소스 DLL은 Always On 상태 검색에서 발생한 문제를 검색할 수 있습니다. 또는 수동 장애 조치(failover)는 주 인스턴스에서 직접 시작할 수 있습니다. 클러스터 서비스, 리소스 호스트 및 SQL Server 인스턴스는 RPC, 공유 메모리 및 T-SQL을 통해 서로 동기화합니다. 대부분의 시나리오에서 이러한 서비스가 성공적으로 통신하지만 이러한 통신은 동일한 컴퓨터에서 서비스 간에도 완벽하게 신뢰할 수 없습니다. 또한 AG(가용성 그룹)는 네트워크 및 디스크 오류와 같은 시스템 범위 이벤트를 견딜 수 있어야 합니다. 그러면 통신 또는 인터럽트 기능을 방지할 수 있습니다. 실패 사례가 많고 서비스 간에 완전히 신뢰할 수 있는 통신이 없는 AG는 클러스터 상태가 항상 모든 노드에 대해 일관성 있도록 다양한 장애 조치 검색 메커니즘에 따라 서로 독립적으로 오류를 검색하고 응답합니다.  

## <a name="cluster-node-and-resource-detection"></a>클러스터 노드 및 리소스 검색 

클러스터의 각 노드는 장애 조치 클러스터를 작동하고 모든 클러스터 리소스를 모니터링하는 단일 클러스터 서비스를 실행합니다. 리소스 호스트는 별도 프로세스로 작동하는 클러스터 서비스와 클러스터 리소스 간의 인터페이스입니다. 리소스 호스트는 클러스터 서비스에서 호출될 때 클러스터 리소스에 대한 작업을 수행합니다. SQL Server와 같은 클러스터 인식 응용 프로그램은 리소스 DLL을 통해 리소스 모니터에 사용자 지정 인터페이스를 제공합니다. 리소스 DLL은 온라인 및 오프라인 작업 및 사용자 지정 리소스에 대한 모니터링 상태를 구현합니다. 리소스 호스트는 클러스터 서비스의 자식 프로세스이며 클러스터 서비스가 중단될 때마다 중단됩니다. 

SQL Server의 경우 AG 리소스 DLL은 AG 임대 메커니즘 및 Always On 상태 검색에 따른 AG의 상태를 결정합니다. AG 리소스 DLL은 `IsAlive` 작업을 통해 리소스 상태를 노출합니다. 리소스 모니터는 `CrossSubnetDelay` 및 `SameSubnetDelay` 클러스터 범위 값에서 설정한 클러스터 하트비트 간격으로 `IsAlive`를 폴링합니다. 리소스 DLL에 대한 `IsAlive` 호출이 AG의 상태가 정상이 아니라고 반환할 때마다 주 노드에서 클러스터 서비스는 장애 조치를 시작합니다. 

클러스터 서비스가 클러스터의 다른 노드로 하트비트를 보내고 여기서 수신한 하트비트를 승인합니다. 노드가 일련의 승인되지 않은 하트비트에서 통신 오류를 검색하면 연결할 수 있는 모든 노드에서 클러스터 노드 상태의 해당 보기를 조정하도록 메시지를 브로드캐스트합니다. *regroup event*라는 이 이벤트는 노드에서 클러스터 상태의 일관성을 유지합니다. regroup event를 따라 쿼럼이 손실된 경우 이 파티션의 AG를 비롯한 클러스터 리소스가 오프라인 상태로 전환됩니다. 이 파티션의 모든 노드는 확인 상태로 전환됩니다. 쿼럼을 보유한 파티션이 있는 경우 AG는 파티션에서 하나의 노드에 할당되고 주 복제본이 되는 반면 다른 모든 노드는 보조 복제본입니다. 

## <a name="always-on-health-detection"></a>Always On 상태 검색 

Always On 리소스 DLL은 내부 SQL Server 구성 요소의 상태를 모니터링합니다. `sp_server_diagnostics`는 `HealthCheckTimeout`에 의해 제어되는 간격으로 이러한 구성 요소 SQL Server의 상태를 보고합니다. `sp_server_diagnostics`는 시스템, 리소스, 쿼리 처리, io 하위 시스템 및 이벤트라는 5개 인스턴스 수준 구성 요소의 상태를 보고합니다. 또한 각 AG의 상태를 보고합니다. 각 업데이트 시 리소스 DLL은 AG의 오류 수준에 따라 AG 리소스의 상태를 업데이트합니다. 데이터가 `sp_server_diagnostics`에서 반환될 때 구성 요소의 상태를 설명하는 XML 데이터를 사용하여 정리, 경고, 오류 또는 알 수 없는 상태 중 하나로 각 구성 요소를 표시합니다. 상태 검색의 경우 구성 요소가 오류 상태일 때만 리소스 DLL이 조치를 취합니다. 

상태 검색이 여러 간격에서 리소스 DLL에 대한 업데이트를 보고하는 데 실패한 경우 AG는 비정상으로 결정되고 `IsAlive` 호출에서 오류를 보고합니다. 

## <a name="lease-mechanism"></a>임대 메커니즘  

다른 장애 조치 메커니즘과 달리 SQL Server 인스턴스는 임대 메커니즘에서 활성 역할을 수행합니다. 주 복제본인 AG를 온라인으로 전환하면 SQL Server 인스턴스는 AG에 대한 전용 임대 작업자 스레드를 생성합니다. 임대 작업자는 임대 갱신 및 임대 중지 이벤트를 비롯한 리소스 호스트와 메모리의 작은 지역을 공유합니다. 임대 작업자 및 리소스 호스트는 순환 방식으로 작동하며 고유한 임대 갱신 이벤트 또는 중지 이벤트를 알리기 위해 해당하는 임대 갱신 이벤트에 신호를 전송한 다음, 중지하고, 다른 당사자를 대기합니다. 리소스 호스트 및 SQL Server 임대 스레드는 모두 다른 스레드의 신호를 받은 후에 스레드가 다시 시작될 때마다 업데이트되는 TTL(time-to-live) 값을 유지합니다. 신호를 기다리는 동안 TTL(time-to-live)에 도달한 경우 임대가 만료된 다음, 복제본이 해당 특정 AG의 확인 상태로 전환됩니다. 임대 중지 이벤트가 신호를 보내면 복제본은 확인 역할로 전환됩니다. 

![image](media/availability-group-lease-healthcheck-timeout/image1.png) 

임대 메커니즘은 SQL Server와 Windows Server 장애 조치(failover) 클러스터 간에 동기화를 적용합니다. 장애 조치 명령이 실행될 때 클러스터 서비스는 현재 주 복제본의 리소스 DLL에 오프라인 호출을 수행합니다. 먼저 리소스 DLL은 저장 프로시저를 사용하여 AG를 오프라인으로 전환하려고 합니다. 이 저장 프로시저가 실패하거나 시간 제한을 초과하면 클러스터 서비스에 다시 오류가 보고됩니다. 그러면 종료 명령이 발급됩니다. 종료는 다시 동일한 저장 프로시저를 실행하려고 하지만 이번에 클러스터는 새 복제본에서 AG를 온라인 상태로 전환하기 전에 리소스 DLL가 성공 또는 실패를 보고하기를 기다리지 않습니다. 이 두 번째 프로시저 호출에 실패하는 경우 리소스 호스트는 인스턴스를 오프라인 상태로 전환하는 임대 메커니즘을 사용해야 합니다. 리소스 DLL을 호출하여 AG를 오프라인 상태로 전환하면 리소스 DLL은 임대 중지 이벤트에 신호를 보내며 SQL Server 임대 작업자 스레드를 다시 시작하여 AG를 오프라인 상태로 전환합니다. 이 중지 이벤트가 신호를 보내지 않더라도 임대는 만료되고 복제본은 확인 상태로 전환됩니다. 

임대는 주로 기본 인스턴스와 클러스터 간의 동기화 메커니즘이지만 그렇지 않으면 장애 조치하지 않아도 되는 실패 조건을 만들 수도 있습니다. 예를 들어 높은 CPU 또는 tempdb 가중으로 인해 임대 작업자 스레드가 부족해져서 SQL 인스턴스의 임대 갱신 메모리를 방해하고 장애 조치를 발생시킬 수 있습니다. 

## <a name="guidelines-for-cluster-timeout-values"></a>클러스터 제한 시간 값에 대한 지침 

SQL Server 클러스터의 모니터링을 적게 사용하는 경우 장단점을 신중하게 고려하고 결과를 이해합니다. 클러스터 제한 시간 값이 증가하면 일시적인 네트워크 문제에 대한 허용 오차가 증가하지만 심각한 오류에 대한 반응이 느려집니다. 리소스 가중 또는 대량 지역 대기 시간을 처리하는 시간 제한이 증가하면 하드 또는 복구할 수 없는 오류로부터 복구하는 시간이 늘어납니다. 그러면 여러 응용 프로그램을 허용할 수 있지만 모든 경우에 이상적이지 않습니다. 

기본 설정은 심각한 오류 및 제한 가동 중지 시간의 증상에 신속하게 대응하도록 최적화되어 있지만 이러한 설정은 특정 작업 및 구성에서 과도하게 공격적일 수도 있습니다. 해당 기본값 이외에 `LeaseTimeout`, `CrossSubnetDelay`, `CrossSubnetThreshold`, `SameSubnetDelay`, `SameSubnetThreshold` 또는 `HealthCheckTimeout` 중 하나를 줄이지 않는 것이 좋습니다. 올바른 설정은 각 배포마다 다르고 미세 조정 기간이 더 오래 걸릴 수 있습니다. 이 값 중 하나를 변경하는 경우 이러한 값 간의 관계 및 종속성을 고려하여 점진적으로 수행합니다. 

### <a name="relationship-between-cluster-timeout-and-lease-timeout"></a>클러스터 제한 시간과 임대 시간 제한 간의 관계 

임대 메커니즘의 기본 기능은 다른 노드로 장애 조치를 수행하는 동안 클러스터 서비스가 인스턴스와 통신할 수 없는 경우에 SQL Server 리소스를 사용하는 것입니다. 클러스터거 AG 클러스터 리소스에서 오프라인 작업을 수행할 때 클러스터 서비스는 rhs.exe에 대한 RPC 호출을 통해 리소스를 오프라인으로 전환합니다. 리소스 DLL은 저장 프로시저를 사용하여 SQL Server에서 AG를 오프라인으로 전환하지만 이 저장 프로시저는 실패하거나 시간이 초과할 수 있습니다. 또한 리소스 호스트가 오프라인 호출 중에 고유한 해당 임대 갱신 스레드를 중지할 수도 있습니다. 최악의 경우에 SQL Server에서 임대가 ½ \* LeaseTimeout 내에 만료되고 인스턴스를 확인 상태로 전환하게 됩니다. 장애 조치는 여러 당사자에 의해 시작될 수 있지만 클러스터 상태 보기가 클러스터 및 SQL Server 인스턴스에서 일관적이어야 합니다. 예를 들어 기본 인스턴스가 나머지 클러스터와 연결이 끊어진 시나리오를 가정해 보세요. 클러스터의 각 노드는 클러스터 제한 시간 값으로 인해 비슷한 시간에 실패를 결정하지만 주 노드는 주 SQL Server 인스턴스와 상호작용하여 주 역할을 포기하도록 강제할 수 있습니다. 

주 노드의 관점에서 클러스터 서비스가 쿼럼을 손실하면 서비스는 자동으로 종료되기 시작합니다. 클러스터 서비스는 리소스 호스트에 대한 RPC 호출을 발급하여 프로세스를 종료합니다. 이 종료 호출은 SQL Server 인스턴스에서 AG를 오프라인으로 전환하는 작업을 담당합니다. 이 오프라인 호출은 T-SQL을 통해 수행되었지만 SQL과 리소스 DLL 간에 연결이 성공적으로 설정되도록 보장할 수 없습니다. 

클러스터의 나머지 관점에서는 현재 주 복제본이 없고, 클러스터의 나머지 노드에 새로운 단일 주 복제본을 설정합니다. 리소스 DLL에서 호출된 프로시저가 실패하거나 시간을 초과할 경우 클러스터는 분할 브레인 시나리오에 대해 취약할 수 있습니다. 

임대 시간 제한은 통신 오류가 발생할 때 분할 브레인 시나리오를 방해합니다. 모든 통신에서 오류가 발생하더라도 리소스 DLL 프로세스는 종료되고 임대를 업데이트할 수 없습니다. 임대가 만료되면 AG를 자체적으로 오프라인 상태로 전환합니다. 클러스터가 새로운 복제본을 설정하기 전에 SQL Server의 인스턴스에서는 더 이상 주 복제본을 호스트하지 않습니다. 새로운 주 복제본을 선택하는 나머지 클러스터에 현재 주 복제본과 조정할 방법이 없기 때문에 시간 제한 값은 현재 주 복제본이 오프라인 상태로 전환되기 전에 새로운 주 복제본을 설정하지 않도록 합니다. 

클러스터가 장애 조치할 때 새로운 주 복제본이 온라인 상태가 되기 전에 이전의 주 복제본을 호스트하는 SQL Server의 인스턴스는 확인 상태로 전환되어야 합니다. 언제든지 SQL Server 임대 스레드에는 ½ \* LeaseTimeout의 남은 TTL(time-to-live)이 있습니다. 임대가 갱신될 때마다 새로운 TTL(time-to-live)이 `LeaseInterval` 또는 ½ \* LeaseTimeout으로 업데이트되기 때문입니다. 클러스터 서비스 또는 리소스 호스트가 임대 중지 이벤트의 신호를 보내지 않고 중지되거나 종료될 경우 클러스터는 `SameSubnetThreshold`\ `SameSubnetDelay` 밀리초 뒤에 주 노드를 배달 못한 것으로 선언합니다. 주 복제본이 오프라인 상태가 되도록 이 시간 내에 임대가 만료되어야 합니다. 임대 시간 제한에 대한 최대 TTL(time-to-live)은 ½ \* `LeaseTimeout`이기 때문에, ½ \* `LeaseTimeout`은 `SameSubnetThreshold` \* `SameSubnetDelay` 미만이어야 합니다. 

`SameSubnetThreshold \<= CrossSubnetThreshold` 및 `SameSubnetDelay \<= CrossSubnetDelay`는 모든 SQL Server 클러스터에 true여야 합니다. 

### <a name="health-check-timeout-operation"></a>상태 확인 제한 시간 작업 

다른 장애 조치 메커니즘이 직접 종속되어 있으므로 상태 확인 제한 시간은 보다 유연합니다. 30초라는 기본값은 제한 시간에 15초의 최소값 및 5초 간격을 포함하여 `sp_server_diagnostics` 간격을 10초로 설정합니다. 보다 일반적으로 `sp_server_diagnositcs` 업데이트 간격은 항상 1/3 \* `HealthCheckTimeout`입니다. 리소스 DLL이 간격에서 새로운 일련의 상태 데이터를 수신하지 못하면 계속 이전 간격에서 상태 데이터를 사용하여 현재 AG 및 인스턴스 상태를 확인합니다. 하지만 상태 확인 제한 시간 값이 증가하면 주 복제본이 더 많은 CPU 가중을 허용할 수 있습니다. 그러면 `sp_server_diagnostics`에서 각 간격에 새 데이터를 제공하지 않도록 방지하지만 오랫동안 만료된 데이터 상태 검사를 사용하게 됩니다. 제한 시간 값에 관계 없이 데이터에서 복제본 상태가 정상이 아님을 나타내는 신호를 수신하면 다음 `IsAlive` 호출은 인스턴스가 비정상적임을 반환하고 클러스터 서비스는 장애 조치를 시작합니다. 

AG의 실패 조건 수준은 상태 검사에 대한 오류 조건을 변경합니다. 오류 수준의 경우 `sp_server_diagnostics`에서 AG 요소가 비정상이라고 보고될 경우 상태 검사에 실패합니다. 각 수준은 그 아래 수준에서 모든 오류 조건을 상속합니다. 


| Level | 인스턴스가 배달되지 못한 것으로 간주되는 조건
|:---|---
| 1: OnServerDown | 상태 검사는 AG 외에도 리소스가 실패하는 경우에 조치를 취하지 않습니다. AG 데이터가 5개 간격 또는 5/3 \* HealthCheckTimeout 내에서 수신되지 않는 경우
| 2: OnServerUnresponsive | HealthCheckTimeout의 `sp_server_diagnostics`에서 수신된 데이터가 없는 경우
| 3: OnCriticalServerError | (기본값)시스템 구성 요소가 오류를 보고하는 경우
| 4: OnModerateServerError | 리소스 구성 요소가 오류를 보고하는 경우 
| 5:  OnAnyQualifiedFailureConitions |  쿼리 처리 구성 요소가 오류를 보고하는 경우

## <a name="updating-cluster-and-always-on-timeout-values"></a>클러스터 및 Always On 시간 제한 값 업데이트 

### <a name="cluster-values"></a>클러스터 값 

클러스터 제한 시간 값을 결정하는 WSFC 구성에는 4개의 값이 있습니다. 

  - SameSubnetDelay 
  - SameSubnetThreshold 
  - CrossSubnetDelay 
  - CrossSubnetThreshold 

지연 값은 클러스터 서비스의 하트 비트 사이에 대기 시간을 결정하고, 임계값은 클러스터에서 배달 못한 개체로 선언하기 전에 대상 노드 또는 리소스에서 승인을 받을 수 없는 하트비트 수를 설정합니다. `SameSubnetDelay \* SameSubnetThreshold` 밀리초 이상의 경우 동일한 서브넷에서 노드 간에 하트비트가 성공하지 못한 경우 노드는 배달 못한 것으로 결정됩니다. 서브넷 간 값을 사용하는 서브넷 통신 간에서도 마찬가지입니다. 

현재 모든 클러스터 값을 나열하려면 대상 클러스터의 모든 노드에서 관리자 권한의 PowerShell 터미널을 엽니다. 다음 명령을 실행합니다.

```PowerShell
 Get-Cluster | fl \
``` 

이러한 값을 업데이트하려면 관리자 권한의 PowerShell 터미널에서 다음 명령을 실행합니다.

```PowerShell
(Get-Cluster).<ValueName> = <NewValue>
```

지연 \* 임계값 제품이 증가하여 클러스터 제한 시간이 길어지면 임계값을 증가시키기 전에 먼저 지연 값을 증가시키는 것이 더 효과적입니다. 지연을 늘려서 하트비트 간격을 증가시킵니다. 하트비트 간격을 증가시키면 일시적인 네트워크 문제가 저절로 해결되고 동일한 기간에 더 많은 하트비트를 보내는 기준으로 네트워크 정체를 줄이는 데 더 많은 시간을 사용할 수 있습니다. 

### <a name="lease-timeout"></a>임대 시간 제한 

임대 메커니즘은 WSFC 클러스터의 각 AG에 특정된 단일 값에서 제어합니다. 장애 조치(Failover) 클러스터 관리자에서 이 값을 탐색하려면:

1. 역할 탭에서 대상 AG 역할을 찾습니다. 대상 AG 역할을 클릭합니다. 
2. 창의 맨 아래에 AG 리소스를 마우스 오른쪽 단추로 클릭하고, **속성**을 선택합니다. 

   ![장애 조치(Failover) 클러스터 관리자](media/availability-group-lease-healthcheck-timeout/image2.png) 

3. 팝업 창에서 속성 탭으로 이동하면 이 AG에 특정된 값 목록이 표시됩니다. LeaseTimeout 값을 변경하려면 클릭합니다. 

   ![속성](media/availability-group-lease-healthcheck-timeout/image3.png) 


   AG의 구성에 따라 수신기, 공유 디스크, 파일 공유 등에 대한 추가 리소스가 있을 수 있습니다. 이러한 리소스에는 추가 구성이 필요하지 않습니다. 

   
### <a name="health-check-values"></a>상태 확인 값 

Always On 상태 검사를 제어하는 두 개의 값: FailureConditionLevel 및 HealthCheckTimeout입니다. FailureConditionLevel은 `sp_server_diagnostics`에서 보고한 특정 오류 조건에 대한 허용 오차 수준을 나타내고, HealthCheckTimeout은 리소스 DLL이 `sp_server_diagnostics`의 업데이트를 수신하지 않고 실행할 수 있는 시간을 구성합니다. `sp_server_diagnostics`의 업데이트 간격은 항상 HealthCheckTimeout/3입니다. 

장애 조치 상태 수준을 구성하려면 `CREATE` 또는 `ALTER` `AVAILABILITY GROUP` 문의 `FAILURE_CONDITION_LEVEL = <n>` 옵션을 사용합니다. 여기서 `<n>`는 1~5 사이의 정수입니다. 다음 명령은 AG 'AG1'에서 오류 상태 수준을 1로 설정합니다. 

```sql
ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1); 
```

상태 확인 제한 시간을 구성하려면 `CREATE` 또는 `ALTER` `AVAILABILITY GROUP` 문의 `HEALTH_CHECK_TIMEOUT` 옵션을 사용합니다. 다음 명령은 AG AG1에서 상태 확인 제한 시간을 60000밀리초로 설정합니다. 


```sql
ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT =60000);
```

## <a name="summary-of-timeout-guidelines"></a>제한 시간 지침 요약 

  - 해당 기본값 아래로 제한 시간 값을 줄이지 않는 것이 좋습니다. 

  - 임대 간격(½ \* LeaseTimeout)은 다음보다 짧아야 합니다. SameSubnetThreshold \* SameSubnetDelay 

  - SameSubnetThreshold \<= CrossSubnetThreshold 

  - SameSubnetDelay \<= SameSubnetDelay 

## <a name="see-also"></a>참고 항목    

[활성 보조: 보조 복제본에 백업&#40;Always On 가용성 그룹&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)

[ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)         

