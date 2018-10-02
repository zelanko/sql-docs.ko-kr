---
title: 데이터베이스 상태 검색 장애 조치 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 04/28/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- AlwaysOn
- DB_FAILOVER
- Always On
- High Availability
- SQL Server
ms.assetid: d74afd28-25c3-48a1-bc3f-e353bee615c2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 649ebf4f39013ccc44b26c74acd311fe4f712f9a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730878"
---
# <a name="availability-group-database-level-health-detection-failover-option"></a>가용성 그룹 데이터베이스 수준의 상태 검색 장애 조치 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
SQL Server 2016부터는 Always On 가용성 그룹을 구성할 때 데이터베이스 수준 상태 검색(DB_FAILOVER) 옵션을 사용할 수 있습니다. 데이터베이스가 더 이상 온라인 상태가 아니거나 문제가 발생하면 데이터베이스 수준 상태 검색에서 해당 상태를 알려주고 가용성 그룹의 자동 장애 조치를 트리거합니다.

가용성 그룹 전체에 대해 데이터베이스 수준 상태 검색을 사용하도록 설정되므로 데이터베이스 수준 상태 검색은 가용성 그룹의 모든 데이터베이스를 모니터링합니다. 가용성 그룹의 특정 데이터베이스에 대해 선택적으로 사용하도록 설정될 수는 없습니다.

## <a name="benefits-of-database-level-health-detection-option"></a>데이터베이스 수준 상태 검색 옵션의 이점
---
가용성 그룹 데이터베이스 수준의 상태 검색 옵션은 데이터베이스의 고가용성을 보장하는 데 도움이 되는 좋은 옵션으로 광범위하게 권장됩니다. 모든 가용성 그룹에 대해 설정하는 것이 좋습니다. 응용 프로그램에서 여러 데이터베이스를 항상 사용하는 경우 데이터베이스 상태 옵션을 사용하도록 설정한 가용성 그룹으로 그룹화합니다.

예를 들어 데이터베이스 수준의 상태 검색 옵션을 설정하면, SQL Server에서 데이터베이스 중 하나에 대한 트랜잭션 로그 파일에 쓸 수 없는 경우, 해당 데이터베이스의 상태가 실패를 표시하도록 변경되어 가용성 그룹에서 곧 장애 조치를 수행하고, 데이터베이스가 다시 온라인 상태가 되면 응용 프로그램이 다시 연결되어 중단을 최소화하면서 작업을 계속할 수 있습니다.

<a name="enabling-database-level-health-detection"></a>데이터베이스 수준 상태 검색 사용
----
일반적으로 권장되지만 이전 버전의 기본 설정과 호환성을 유지하기 위해 데이터베이스 상태 옵션은 **기본적으로 off(해제)** 로 설정되어 있습니다.

데이터베이스 수준 상태 검색 설정을 사용하도록 설정하는 몇 가지 쉬운 방법이 있습니다.

1. SQL Server Management Studio에서 SQL Server 데이터베이스 엔진에 연결합니다. [개체 탐색기] 창을 사용하여 AlwaysOn 고가용성 노드를 마우스 오른쪽 단추로 클릭하고 **새 가용성 그룹 마법사**를 실행합니다. [이름 지정] 페이지에서 **데이터베이스 수준 상태 검색** 확인란을 선택합니다. 그런 다음 마법사의 나머지 페이지를 완료합니다.

   ![Always On 데이터베이스 상태 사용 확인란](../../../database-engine/availability-groups/windows/media/always-on-enable-database-health-checkbox.png)

2. SQL Server Management Studio에서 기존 가용성 그룹의 **속성**을 봅니다. SQL Server에 연결합니다. [개체 탐색기] 창을 사용하여 Always On 고가용성 노드를 펼칩니다. 가용성 그룹을 펼칩니다. 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 [속성]을 선택합니다. **데이터베이스 수준 상태 검색** 옵션을 선택한 다음 [확인] 또는 [스크립트 변경]을 클릭합니다.

   ![Always On AG 속성 - 데이터베이스 수준 상태 검색](../../../database-engine/availability-groups/windows/media/always-on-ag-properties-database-level-health-detection.png)


3. **CREATE AVAILABILITY GROUP**에 대한 Transact-SQL 구문 - DB_FAILOVER 매개 변수에는 ON 또는 OFF 값이 허용됩니다.

   ```Transact-SQL
   CREATE AVAILABILITY GROUP [Contoso-ag]
   WITH (DB_FAILOVER=ON)
   FOR DATABASE [AutoHa-Sample]
   REPLICA ON
       N'SQLSERVER-0' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-0.DOMAIN.COM:5022',
         FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
       N'SQLSERVER-1' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-1.DOMAIN.COM:5022',
        FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
    ```

4. **ALTER AVAILABILITY GROUP**에 대한 Transact-SQL 구문 - DB_FAILOVER 매개 변수에는 ON 또는 OFF 값이 허용됩니다.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = ON);

   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = OFF);
   ```

### <a name="caveats"></a>제한 사항

데이터베이스 수준 상태 검색 옵션은 현재 SQL Server에서 디스크 작동 시간을 모니터링하지 않으며 데이터베이스 파일 가용성을 직접 모니터링하지 않도록 한다는 점에 유의해야 합니다. 디스크 드라이브에 장애가 발생하거나 사용할 수 없게 되면 자동으로 장애 조치하도록 가용성 그룹이 반드시 트리거되는 것은 아닙니다.

예를 들어 데이터베이스가 활성 트랜잭션 없이 유휴 상태이고 물리적 쓰기가 수행되지 않을 때 일부 데이터베이스 파일에 액세스할 수 없으면, SQL Server에서 파일에 대한 읽기 또는 쓰기 I/O를 수행하지 않을 수 있으며 해당 데이터베이스의 상태를 즉시 변경할 수 없으므로 장애 조치가 트리거되지 않습니다. 나중에 데이터베이스 검사점이 발생하거나 쿼리를 수행하기 위해 물리적 읽기 또는 쓰기가 수행되면, SQL Server에서 파일 문제를 인식하고 데이터베이스 상태를 변경함으로써 대응한 후에, 데이터베이스 수준 상태 검색이 설정된 가용성 그룹에서 데이터베이스 상태 변경에 따른 장애 조치를 수행합니다.

또 다른 예로, 쿼리를 수행하기 위해 SQL Server 데이터베이스 엔진에서 데이터 페이지를 읽어야 할 때 데이터 페이지가 버퍼 풀 메모리에 캐시된 경우, 쿼리 요청을 수행하기 위해 물리적 액세스를 통해 디스크를 읽을 필요가 없습니다. 따라서 데이터베이스 상태가 즉시 적용되지 않기 때문에 데이터베이스 상태 옵션이 사용하도록 설정된 경우에도 누락되었거나 사용할 수 없는 데이터 파일로 인한 자동 장애 조치를 즉시 트리거하지 않을 수 있습니다.


## <a name="database-failover-is-separate-from-flexible-failover-policy"></a>유연한 장애 조치 정책과는 별개인 데이터베이스 장애 조치
데이터베이스 수준 상태 검색은 장애 조치 정책에 대한 SQL Server 프로세스 상태의 임계값을 구성하는 유연한 장애 조치 정책을 구현합니다. 데이터베이스 수준 상태 검색은 DB_FAILOVER 매개 변수를 사용하여 구성되지만, FAILURE_CONDITION_LEVEL 가용성 그룹 옵션은 SQL Server 프로세스 상태 검색을 구성하는 데 별도로 사용됩니다. 두 옵션은 독립적입니다.

## <a name="managing-and-monitoring-database-level-health-detection"></a>데이터베이스 수준 상태 검색 관리 및 모니터링

### <a name="dynamic-management-views"></a>동적 관리 뷰

sys.availability_groups 시스템 DMV는 데이터베이스 수준 상태 검색 옵션이 해제(0) 또는 사용(1)인지 여부를 나타내는 db_failover 열을 표시합니다.

```Transact-SQL
select name, db_failover from sys.availability_groups
```


예제 DMV 출력:

NAME  |  db_failover
---------|---------
| Contoso-ag |  1  |

### <a name="errorlog"></a>ErrorLog
데이터베이스 수준의 상태 검색 검사로 인해 가용성 그룹이 장애 조치되었을 때 SQL Server 오류 로그(또는 sp_readerrorlog의 텍스트)에서는 41653 오류 메시지를 표시합니다.

예를 들어 이 오류 로그 발췌문에서는 디스크 문제로 인해 트랜잭션 로그 쓰기가 실패한 후에 AutoHa-Sample이라는 데이터베이스가 종료되어 데이터베이스 수준 상태 검색을 트리거하여 가용성 그룹을 장애 조치했습니다.

>2016-04-25 12:20:21.08 spid1s      오류: 17053, 심각도: 16, 상태: 1.
>
>2016-04-25 12:20:21.08 spid1s      SQLServerLogMgr::LogWriter: 운영 체제 오류 21(장치가 준비되지 않음)이(가) 발생했습니다.
>2016-04-25 12:20:21.08 spid1s      로그 플러시 중 쓰기 오류입니다.
>
>2016-04-25 12:20:21.08 spid79      오류: 9001, 심각도: 21, 상태: 4.
>
>2016-04-25 12:20:21.08 spid79      'AutoHa-Sample' 데이터베이스의 로그를 사용할 수 없습니다. 관련 오류 메시지의 이벤트 로그를 확인하십시오. 모든 오류를 해결하고 데이터베이스를 다시 시작하십시오.
>
>**2016-04-25 12:20:21.15 spid79      오류: 41653, 심각도: 21, 상태: 1.**
>
>**2016-04-25 12:20:21.15 spid79      데이터베이스 'AutoHa-Sample'에서 가용성 그룹 'Contoso-ag'이(가) 실패하게 하는 오류(오류 유형: 2 'DB_SHUTDOWN')가 발생했습니다.  발생한 오류에 대한 자세한 내용은 SQL Server의 오류 로그를 참조하십시오.  이 상태가 계속되면 시스템 관리자에게 문의하십시오.**
>
>2016-04-25 12:20:21.17 spid79      데이터베이스 'AutoHa-Sample'의 상태 정보 - 확정된 LSN: '(34:664:1)'    커밋 LSN: '(34:656:1)'    커밋 시간: 'Apr 25 2016 12:19PM'
>
>2016-04-25 12:20:21.19 spid15s     복제본 ID가 {c4ad5ea4-8a99-41fa-893e-189154c24b49}인 가용성 복제본 'SQLServer-0'에서 주 데이터베이스 'AutoHa-Sample'에 대해 보조 데이터베이스와 Always On 가용성 그룹의 연결이 종료되었습니다. 이 메시지는 정보 제공용이므로 사용자가 조치할 필요는 없습니다.
>
>2016-04-25 12:20:21.21 spid75      WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 요청에 대한 응답으로 가용성 그룹 'Contoso-ag'의 로컬 복제본을 확인 역할로 전환하기 위해 준비하는 중입니다. 이 메시지는 정보 제공용이므로 사용자가 조치할 필요는 없습니다.
>
>2016-04-25 12:20:21.21 spid75      가용성 그룹 'ag'에서 로컬 가용성 복제본의 상태가 'PRIMARY_NORMAL'에서 'RESOLVING_NORMAL'(으)로 변경되었습니다.  가용성 그룹이 오프라인 상태로 전환되었기 때문에 상태가 변경되었습니다.  연결된 가용성 그룹이 삭제되었거나, 사용자가 WSFC(Windows Server 장애 조치 클러스터링) 관리 콘솔에서 연결된 가용성 그룹을 오프라인으로 전환했거나, 가용성 그룹이 다른 SQL Server 인스턴스로 장애 조치하고 있기 때문에 복제본이 오프라인 상태로 전환되었습니다.  자세한 내용은 SQL Server 오류 로그, WSFC(Windows Server 장애 조치 클러스터링) 관리 콘솔 또는 WSFC 로그를 참조하세요.

### <a name="extended-event-sqlserveravailabilityreplicadatabasefaultreporting"></a>sqlserver.availability_replica_database_fault_reporting 확장 이벤트

SQL Server 2016에서 정의되기 시작한 새로운 확장 이벤트가 있으며, 이는 데이터베이스 수준 상태 검색으로 트리거됩니다.  이벤트 이름은 **sqlserver.availability_replica_database_fault_reporting**입니다.

이 확장 이벤트는 주 복제본에서만 트리거되며, 가용성 그룹에서 호스팅되는 데이터베이스에 대해 데이터베이스 수준 상태 문제가 검색될 때 트리거됩니다.

다음은 이 이벤트를 캡처하는 확장 이벤트 세션을 만드는 예제입니다. 경로를 지정하지 않았으므로 기본 SQL Server 오류 로그 경로에 확장 이벤트 출력 파일이 있어야 합니다. 가용성 그룹의 주 복제본에서 이 작업을 실행합니다.

확장 이벤트 세션 스크립트 예제
```
CREATE EVENT SESSION [AlwaysOn_dbfault] ON SERVER
ADD EVENT sqlserver.availability_replica_database_fault_reporting
ADD TARGET package0.event_file(SET filename=N'dbfault.xel',max_file_size=(5),max_rollover_files=(4))
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,
    MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO
ALTER EVENT SESSION AlwaysOn_dbfault ON SERVER STATE=START
GO
```

#### <a name="extended-event-output"></a>확장 이벤트 출력
SQL Server Management Studio를 사용하여 주 SQL Server에 연결하고, 관리 노드를 펼친 다음, 확장 이벤트를 펼칩니다. 세션(AlwaysOn_dbfault는 위의 샘플에 있는 이름이었음)을 찾은 다음 해당 세션을 펼쳐 출력 파일을 확인합니다. 출력 파일을 클릭하면 새 탭에서 해당 이벤트 파일이 열립니다.

필드에 대한 설명:

|열 데이터    | 설명
|---------|---------
|availability_group_id  |가용성 그룹의 ID입니다.
|availability_group_name    |가용성 그룹의 이름입니다.
|availability_replica_id    |가용성 복제본의 ID입니다.
|availability_replica_name  |가용성 복제본의 이름입니다.
|database_name  |오류를 보고하는 데이터베이스의 이름입니다.
|database_replica_id    |가용성 복제본 데이터베이스의 ID입니다.
|failover_ready_replicas    |동기화되는 자동 장애 조치 보조 복제본의 수입니다.
|fault_type     | 보고된 오류 ID입니다. 가능한 값은 다음과 같습니다.  <br/> 0 - 없음 <br/>1 - 알 수 없음<br/>2 - 종료
|is_critical    | 이 값은 SQL Server 2016 현재로 확장 이벤트에 대해 항상 true를 반환해야 합니다.


이 예제 출력에서 fault_type은 데이터베이스 이름이 AutoHa-Sample2이고, 오류 유형이 2 - 종료인 SQLSERVER-1이라는 복제본에서 Contoso-ag 가용성 그룹에 중요한 이벤트가 발생했음을 나타냅니다.

|필드  | 값
|---------|---------
|availability_group_id |    24E6FE58-5EE8-4C4E-9746-491CFBB208C1
|availability_group_name |  Contoso-ag
|availability_replica_id    | 3EAE74D1-A22F-4D9F-8E9A-DEFF99B1F4D1
|availability_replica_name |    SQLSERVER-1
|database_name |    AutoHa-Sample2
|database_replica_id | 39971379-8161-4607-82E7-098590E5AE00
|failover_ready_replicas |  1
|fault_type |   2
|is_critical    | True


### <a name="related-references"></a>관련 참조

* [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)

* [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)

* [가용성 그룹 자동 장애 조치에 대한 유연한 장애 조치 정책(SQL Server)](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)

* [Always On 장애 조치 정책을 향상시켜 SQL Server 데이터베이스 데이터 및 로그 드라이브 테스트(영문)](https://blogs.msdn.microsoft.com/alwaysonpro/2016/01/14/enhance-alwayson-failover-policy-to-test-sql-server-database-data-and-log-drives/)

* [확장 이벤트](../../../relational-databases/extended-events/extended-events.md)



