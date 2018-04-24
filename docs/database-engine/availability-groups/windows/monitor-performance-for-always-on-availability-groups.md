---
title: Always On 가용성 그룹에 대한 성능 모니터링(SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dfd2b639-8fd4-4cb9-b134-768a3898f9e6
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6ad77dc80e9c54dffba133e06428dca24f2f704b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="monitor-performance-for-always-on-availability-groups"></a>Always On 가용성 그룹에 대한 성능 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Always On 가용성 그룹의 성능 양상은 중요 업무용 데이터베이스의 SLA(서비스 수준 약정)를 유지하기 위해 중요합니다. 가용성 그룹이 로그를 보조 복제본에 전달하는 방법을 이해하면 성능이 떨어지는 가용성 그룹 또는 복제본에서 가용성 구현의 RTO(복구 시간 목표) 및 RPO(복구 지점 목표)를 예측하고 병목 상태를 식별하는 데 도움이 될 수 있습니다. 이 문서에서는 동기화 프로세스를 설명하고 몇몇 주요 메트릭을 계산하는 방법을 보여 주고 몇 가지 일반적인 성능 문제 해결 시나리오에 대한 링크를 제공합니다.  
  
 다음과 같은 주제를 다룹니다.  
  
-   [데이터 동기화 프로세스](#BKMK_DATA_SYNC_PROCESS)  
  
-   [흐름 제어 게이트](#BKMK_FLOW_CONTROL_GATES)  
  
-   [장애 조치(failover) 시간 예측(RTO)](#BKMK_RTO)  
  
-   [잠재적 데이터 손실 예측(RPO)](#BKMK_RPO)  
  
-   [RTO 및 RPO 모니터링](#BKMK_Monitoring_for_RTO_and_RPO)  
  
-   [성능 문제 해결 시나리오](#BKMK_SCENARIOS)  
  
-   [유용한 확장 이벤트](#BKMK_XEVENTS)  
  
##  <a name="BKMK_DATA_SYNC_PROCESS"></a> 데이터 동기화 프로세스  
 전체 동기화 시간을 예측하고 병목 상태를 식별하려면 동기화 프로세스를 이해해야 합니다. 성능 병목 상태는 프로세스의 어디에서나 발생할 수 있으며 병목 상태를 찾으면 기본 문제를 더 깊이 파악하는 데 도움이 될 수 있습니다. 다음 그림과 표에서 데이터 동기화 프로세스를 보여 줍니다.  
  
 ![가용성 그룹 데이터 동기화](media/always-onag-datasynchronization.gif "가용성 그룹 데이터 동기화")  
  
|||||  
|-|-|-|-|  
|**시퀀스**|**단계 설명**|**설명**|**유용한 메트릭**|  
|1|로그 생성|로그 데이터는 디스크에 플러시됩니다. 이 로그를 보조 복제본에 복제해야 합니다. 로그 레코드에 전송 큐를 입력합니다.|[SQL Server:데이터베이스 > 플러시된 로그 바이트\sec](~/relational-databases/performance-monitor/sql-server-databases-object.md)|  
|2|캡처|각 데이터베이스에 대한 로그가 캡처되어 해당 파트너 큐(데이터베이스-복제본 쌍마다 한 개)로 전송됩니다. 이 캡처 프로세스는 가용성 복제본이 연결되고 데이터 이동이 어떤 이유로든 일시 중단되지 않는 한 지속적으로 실행되며 데이터베이스-복제본 쌍이 동기화 중이거나 동기화된 것으로 표시됩니다. 캡처 프로세스가 메시지를 충분히 빠르게 스캔하여 큐에 넣을 수 없는 경우 로그 전송 큐가 축적됩니다.|[SQL Server:가용성 복제본 > 복제본에 전송된 바이트 수\sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md)는 해당 가용성 복제본의 큐에 저장된 모든 데이터베이스 메시지의 합계를 집계한 것입니다.<br /><br /> 주 복제본의 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)(KB) 및 [log_bytes_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)(KB/sec).|  
|3|Send|각 데이터베이스 복제본 큐의 메시지가 큐에서 제거되고 유선을 통해 해당 보조 복제본으로 전송됩니다.|[SQL Server:가용성 복제본 > 전송에 보낸 바이트 수\sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 및 [SQL Server:가용성 복제본 > 메시지 승인 시간](~/relational-databases/performance-monitor/sql-server-availability-replica.md) (ms)|  
|4|수신 및 캐시|각 보조 복제본이 메시지를 수신하고 캐시합니다.|성능 카운터 [SQL Server:가용성 복제본 > 수신된 로그 바이트 수/sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|5|확정|로그가 확정을 위해 보조 복제본에 플러시됩니다. 로그가 플러시된 후 승인이 주 복제본으로 다시 보내집니다.<br /><br /> 로그가 확정된 후 데이터 손실이 방지됩니다.|성능 카운터 [SQL Server:데이터베이스 > 플러시된 로그 바이트\sec](~/relational-databases/performance-monitor/sql-server-databases-object.md)<br /><br /> 대기 유형 [HADR_LOGCAPTURE_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|6|다시 실행|보조 복제본에 대해 플러시된 페이지를 다시 실행합니다. 페이지는 다시 실행을 위해 대기하는 동안 다시 실행 큐에 보관됩니다.|[SQL Server:데이터베이스 복제본 > 다시 실행한 바이트 수/sec](~/relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)(KB) 및 [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).<br /><br /> 대기 유형 [REDO_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
  
##  <a name="BKMK_FLOW_CONTROL_GATES"></a> 흐름 제어 게이트  
 가용성 그룹은 모든 가용성 복제본에서 네트워크 및 메모리 리소스 등의 과도한 리소스 사용을 피하기 위해 주 복제본에 흐름 제어 게이트를 포함하도록 설계됩니다. 이러한 흐름 제어 게이트는 가용성 복제본의 동기화 상태에 영향을 주지 않으며 RPO를 포함한 가용성 데이터베이스의 전체 성능에 영향을 줄 수 있습니다.  
  
 로그는 주 복제본에 캡처된 후 다음 표와 같이 두 단계의 흐름 제어를 적용합니다.  
  
|||||  
|-|-|-|-|  
|**Level**|**게이트 수**|**메시지 수**|**유용한 메트릭**|  
|전송|가용성 복제본당 1개|8192|확장 이벤트 **database_transport_flow_control_action**|  
|데이터베이스|가용성 데이터베이스당 1개|11200(x64)<br /><br /> 1600(x86)|[DBMIRROR_SEND](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)<br /><br /> 확장 이벤트 **hadron_database_flow_control_action**|  
  
 두 게이트 중 하나의 메시지 임계값에 도달한 후 로그 메시지는 더 이상 특정 복제본으로 또는 특정 데이터베이스에 대해 보내지지 않습니다. 보낸 메시지 수를 임계값보다 낮게 만들기 위해 보낸 메시지에 대한 승인 메시지가 수신된 후 메시지를 보낼 수 있습니다.  
  
 흐름 제어 게이트 외에도 로그 메시지가 보내지지 않도록 할 수 있는 다른 요인이 있습니다. 복제본을 동기화하면 메시지가 확실히 LSN(로그 시퀀스 번호) 순서대로 보내지고 적용됩니다. 로그 메시지가 보내지기 전에 해당 LSN에 대해 가장 낮은 승인된 LSN 번호를 확인하여 임계값(메시지 유형에 따라 다름) 중 하나보다 낮은지 확인합니다. 두 LSN 번호 간의 간격이 임계값보다 크면 메시지가 보내지지 않습니다. 간격이 다시 임계값보다 낮아진 후 메시지가 보내집니다.  
  
 두 가지 유용한 성능 카운터 [SQL Server:가용성 복제본 > 흐름 제어/sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 및 [SQL Server:가용성 복제본 > 흐름 제어 시간(ms/sec)](~/relational-databases/performance-monitor/sql-server-availability-replica.md)은 마지막 초 이내에 흐름 제어가 활성화된 시간 및 흐름 제어를 위해 대기하면서 소비한 시간을 보여 줍니다. 흐름 제어 대기 시간이 클수록 RPO가 더 큽니다. 흐름 제어에 대한 높은 대기 시간을 야기할 수 있는 문제 유형에 대한 자세한 내용은 [문제 해결: 가용성 그룹이 RPO를 초과하는 경우](troubleshoot-availability-group-exceeded-rpo.md)를 참조하세요.  
  
##  <a name="BKMK_RTO"></a> 장애 조치(failover) 시간 예측(RTO)  
 SLA의 RTO는 지정된 시간에 Always On 구현의 장애 조치(failover) 시간에 따라 달라지며 다음 수식으로 표현될 수 있습니다.  
  
 ![가용성 그룹 RTO 계산](media/always-on-rto.gif "가용성 그룹 RTO 계산")  
  
> [!IMPORTANT]  
>  가용성 그룹이 가용성 데이터베이스를 두 개 이상 포함하는 경우 Tfailover가 가장 높은 가용성 데이터베이스가 RTO 준수를 위한 제한 값이 됩니다.  
  
 오류 검색 시간 Tdetection은 시스템이 오류를 검색하는 데 걸리는 시간입니다. 이 시간은 클러스터 수준 설정에 따라 달라지며 개별 가용성 복제본에 의존하지 않습니다. 구성된 자동 장애 조치(failover) 조건에 따라 분리된 스핀 잠금 같은 중요 SQL Server 내부 오류에 대한 순간 응답으로 장애 조치(failover)가 트리거될 수 있습니다. 이 경우 검색은 [sp_server_diagnostics &#40;Transact-SQL&#41;만큼 빠를 수 있으며](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 오류 보고가 WSFC 클러스터로 보내집니다. (기본 간격은 상태 확인 시간 제한의 1/3입니다.) 장애 조치(failover)는 클러스터 상태 확인 시간 제한이 만료했거나(기본적으로 30초) 리소스 DLL과 SQL Server 인스턴스 간의 임대 기간이 만료한(기본적으로 20초) 것과 같은 시간 제한 때문에 트리거될 수도 있습니다. 이 경우 검색 시간은 시간 제한 간격만큼 깁니다. 자세한 내용은 [가용성 그룹 자동 장애 조치(failover)에 대한 유연한 장애 조치 정책&#40;SQL Server&#41;](https://msdn.microsoft.com/library/hh710061(SQL.120).aspx)을 참조하세요.  
  
 보조 복제본이 장애 조치(failover)에 대해 준비되도록 수행해야 하는 유일한 한 가지 작업은 로그의 끝까지 캡처하기 위한 다시 실행입니다. 다시 실행 시간 Tredo는 다음 수식을 사용하여 계산됩니다.  
  
 ![가용성 그룹 다시 실행 시간 계산](media/always-on-redo.gif "가용성 그룹 다시 실행 시간 계산")  
  
 단, *redo_queue*는 [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)의 값이고 *redo_rate*는 [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)의 값입니다.  
  
 장애 조치(failover) 오버헤드 시간 Toverhead는 WSFC 클러스터를 장애 조치하고 데이터베이스를 온라인 상태로 만드는 데 걸리는 시간을 포함합니다. 이 시간은 대개 짧고 일정합니다.  
  
##  <a name="BKMK_RPO"></a> 잠재적 데이터 손실 예측(RPO)  
 SLA의 RPO는 임의의 지정된 시간에 Always On 구현의 예상 데이터 손실에 따라 달라집니다. 이 예상 데이터 손실은 다음 수식으로 나타낼 수 있습니다.  
  
 ![가용성 그룹 RPO 계산](media/always-on-rpo.gif "가용성 그룹 RPO 계산")  
  
 단, *log_send_queue*는 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)의 값이며 *log generation rate*는 [SQL Server:데이터베이스 > 플러시된 로그 바이트 수/sec](~/relational-databases/performance-monitor/sql-server-databases-object.md)입니다.  
  
> [!WARNING]  
>  가용성 그룹이 가용성 데이터베이스를 두 개 이상 포함하는 경우 Tdata_loss가 가장 높은 가용성 데이터베이스가 RPO 준수를 위한 제한 값이 됩니다.  
  
 로그 전송 큐는 치명적인 오류에서 손실될 수 있는 모든 데이터를 나타냅니다. 얼핏 보기에 로그 생성 속도가 로그 전송 속도 대신에 사용되는 것 같아 이상해 보입니다([log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 참조). 그러나 로그 전송 속도만 사용하면 동기화 시간만 제공하는 반면에 RPO는 데이터가 동기화되는 속도가 아닌 데이터가 생성되는 속도를 기반으로 데이터 손실을 측정한다는 것을 기억해야 합니다.  
  
 Tdata_loss를 예측하는 더 간단한 방법은 [last_commit_time](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)을 사용하는 것입니다. 기본 복제에 대한 DMV는 모든 복제본에 대해 이 값을 보고합니다. 기본 복제본에 대한 값과 보조 복제본에 대한 값 간의 차를 계산하면 보조 복제본의 로그가 기본 복제본에 캡처되는 속도를 예상할 수 있습니다. 앞에서 언급했듯이 이 계산은 로그가 생성되는 속도를 기반으로 잠재적 데이터 손실을 알려 주는 것이 아니라 가까운 근사값입니다.  
  
##  <a name="BKMK_Monitoring_for_RTO_and_RPO"></a> RTO 및 RPO 모니터링  
 이 섹션에서는 가용성 그룹의 RTO 및 RPO 메트릭을 모니터링하는 방법을 보여 줍니다. 이 데모는 [Always On 상태 모델, 2부: 상태 모델 확장](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)에 나오는 GUI 자습서와 유사합니다.  
  
 [예상 장애 조치(failover) 시간(RTO)](#BKMK_RTO) 및 [예상 잠재적 데이터 손실(RPO)](#BKMK_RPO)에서 장애 조치(failover) 시간과 잠재적 데이터 손실 계산의 요소는 편의상 정책 관리 패싯 **데이터베이스 복제본 상태**의 성능 메트릭으로 제공됩니다([SQL Server 개체에 대한 정책 기반 관리 패싯 보기](~/relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md) 참조). 이러한 두 메트릭을 일정에 따라 모니터링하고 메트릭이 각각 RTO 및 RPO를 초과하는 경우 경고할 수 있습니다.  
  
 데모에서 보여 주는 스크립트는 다음 특성과 함께 해당 일정에 따라 실행되는 두 가지 시스템 정책을 만듭니다.  
  
-   예측한 장애 조치(failover) 시간이 10분을 초과할 때 실패하는 RTO 정책은 매 5분마다 계산됩니다.  
  
-   예측한 데이터 손실이 1시간을 초과할 때 실패하는 RPO 정책은 매 30분마다 계산됩니다.  
  
-   두 정책은 모든 가용성 복제본에 대해 같은 구성을 포함합니다.  
  
-   정책은 모든 서버에서 평가되지만 로컬 가용성 복제본이 주 복제본인 가용성 그룹에 대해서만 평가됩니다. 로컬 가용성 복제본이 주 복제본이 아닌 경우 정책이 평가되지 않습니다.  
  
-   정책 실패는 편의상 주 복제본에서 볼 때 Always On 대시보드에 표시됩니다.  

정책을 만들려면 가용성 그룹에 참여하는 모든 서버 인스턴스에 대해 아래 지침을 따릅니다.  

1.  아직 시작되지 않은 경우 [SQL Server 에이전트 서비스를 시작](~/ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)합니다.  
  
2.  SQL Server Management Studio의 경우 **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
3.  **SQL Server Always On** 탭에서 **사용자 정의 Always On 정책 사용**을 선택하고 **확인**을 클릭합니다.  
  
     이 설정을 사용하여 Always On 대시보드에서 이전에 구성된 사용자 지정 정책을 표시할 수 있습니다.  
  
4.  다음 사양을 사용하여 [정책 기반 관리 조건](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)을 만듭니다.  
  
    -   **이름**: `RTO`  
  
    -   **패싯**: **데이터베이스 복제본 상태**  
  
    -   **필드**: `Add(@EstimatedRecoveryTime, 60)`  
  
    -   **연산자**: **<=**  
  
    -   **값**: `600`  
  
     이 조건은 잠재적 장애 조치(failover) 시간이 오류 검색과 장애 조치에 대한 오버헤드 60초를 포함하여 10분을 초과하면 실패합니다.  
  
5.  다음 사양을 사용하여 두 번째 [정책 기반 관리 조건](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)을 만듭니다.  
  
    -   **이름**: `RPO`  
  
    -   **패싯**: **데이터베이스 복제본 상태**  
  
    -   **필드**: `@EstimatedDataLoss`  
  
    -   **연산자**: **<=**  
  
    -   **값**: `3600`  
  
     이 조건은 잠재적 데이터 손실이 1시간을 초과하면 실패합니다.  
  
6.  다음 사양을 사용하여 세 번째 [정책 기반 관리 조건](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)을 만듭니다.  
  
    -   **이름**: `IsPrimaryReplica`  
  
    -   **패싯**: **가용성 그룹**  
  
    -   **필드**: `@LocalReplicaRole`  
  
    -   **연산자**: **=**  
  
    -   **값**: `Primary`  
  
     이 조건은 지정된 가용성 그룹에 대한 로컬 가용성 복제본이 주 복제본인지 여부를 확인합니다.  
  
7.  다음 사양을 사용하여 [정책 기반 관리 정책](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md)을 만듭니다.  
  
    -   **일반** 페이지:  
  
        -   **이름**: `CustomSecondaryDatabaseRTO`  
  
        -   **조건 확인**: `RTO`  
  
        -   **대상 기준**: **IsPrimaryReplica AvailabilityGroup**의 **모든 DatabaseReplicaState**  
  
             이 설정은 로컬 가용성 복제본이 주 복제본인 가용성 그룹에 대해서만 정책이 평가되도록 합니다.  
  
        -   **평가 모드**: **일정에 따라**  
  
        -   **일정**: **CollectorSchedule_Every_5min**  
  
        -   **활성화됨**: **선택됨**  
  
    -   **설명** 페이지:  
  
        -   **범주**: **가용성 데이터베이스 경고**  
  
             이 설정을 통해 정책 평가 결과가 Always On 대시보드에 표시될 수 있습니다.  
  
        -   **설명**: **현재 복제본은 검색 및 장애 조치(failover)에 대한 오버헤드가 1분이라고 가정할 때 10분을 초과하는 RTO를 포함합니다. 해당 서버 인스턴스에 대한 성능 문제를 즉시 조사해야 합니다.**  
  
        -   **표시할 텍스트**: **RTO 초과!**  
  
8.  다음 사양을 사용하여 두 번째 [정책 기반 관리 정책](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md)을 만듭니다.  
  
    -   **일반** 페이지:  
  
        -   **이름**: `CustomAvailabilityDatabaseRPO`  
  
        -   **조건 확인**: `RPO`  
  
        -   **대상 기준**: **IsPrimaryReplica AvailabilityGroup**의 **모든 DatabaseReplicaState**  
  
        -   **평가 모드**: **일정에 따라**  
  
        -   **일정**: **CollectorSchedule_Every_30min**  
  
        -   **활성화됨**: **선택됨**  
  
    -   **설명** 페이지:  
  
        -   **범주**: **가용성 데이터베이스 경고**  
  
        -   **설명**: **가용성 데이터베이스가 RPO인 1시간을 초과했습니다. 가용성 복제본에 대한 성능 문제를 즉시 조사해야 합니다.**  
  
        -   **표시할 텍스트**: **RPO 초과!**  
  
 완료되면 각 정책 평가 일정에 대해 한 개씩 새 SQL Server 에이전트 작업 두 개가 만들어집니다. 이러한 작업은 **syspolicy_check_schedule**로 시작하는 이름을 가져야 합니다.  
  
 작업 기록을 보고 평가 결과를 검사할 수 있습니다. 또한 평가 오류는 이벤트 ID 34052로 Windows 응용 프로그램(이벤트 뷰어)에 기록됩니다. 또한 정책이 실패할 경우 SQL Server 에이전트가 경고를 보내도록 구성할 수 있습니다. 자세한 내용은 [정책 관리자에게 정책 실패를 알리도록 경고 구성](~/relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md)을 참조하세요.  
  
##  <a name="BKMK_SCENARIOS"></a> 성능 문제 해결 시나리오  
 다음 표는 일반적인 성능 관련 문제 해결 시나리오를 나열합니다.  
  
|시나리오|Description|  
|--------------|-----------------|  
|[문제 해결: 가용성 그룹 초과 RTO](troubleshoot-availability-group-exceeded-rto.md)|데이터 손실 없이 자동 장애 조치(failover) 또는 계획된 수동 장애 조치 후 장애 조치 시간이 RTO를 초과합니다. 또는 동기 커밋 보조 복제본(예: 자동 장애 조치(failover) 파트너)의 장애 조치 시간을 예측할 때 RTO 초과를 발견할 수 있습니다.|  
|[문제 해결: 가용성 그룹 초과 RPO](troubleshoot-availability-group-exceeded-rpo.md)|강제 수동 장애 조치(failover)를 수행한 후 데이터 손실이 RPO보다 많습니다. 또는 비동기 커밋 보조 복제본의 잠재적 데이터 손실을 계산할 때 RPO 초과를 발견합니다.|  
|[문제 해결: 보조 복제본에 반영되지 않은 주 복제본의 변경 내용](troubleshoot-primary-changes-not-reflected-on-secondary.md)|클라이언트 응용 프로그램에서 주 복제본에 대한 업데이트를 성공적으로 완료하지만 보조 복제본 쿼리는 변경 내용이 반영되지 않았음을 보여줍니다.|  
  
##  <a name="BKMK_XEVENTS"></a> 유용한 확장 이벤트  
 다음 확장 이벤트는 **동기화** 상태에 있는 복제본을 문제 해결할 때 유용합니다.  
  
|이벤트 이름|범주|채널|가용성 복제본|  
|----------------|--------------|-------------|--------------------------|  
|redo_caught_up|트랜잭션|디버그|보조|  
|redo_worker_entry|트랜잭션|디버그|보조|  
|hadr_transport_dump_message|`alwayson`|디버그|주|  
|hadr_worker_pool_task|`alwayson`|디버그|주|  
|hadr_dump_primary_progress|`alwayson`|디버그|주|  
|hadr_dump_log_progress|`alwayson`|디버그|주|  
|hadr_undo_of_redo_log_scan|`alwayson`|Analytic|보조|  
  
  