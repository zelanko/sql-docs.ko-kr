---
title: 가용성 그룹에 대한 확장 이벤트 구성
description: SQL Server는 Always On 가용성 그룹 관련 확장 이벤트를 정의합니다. 세션에서 이 확장 이벤트를 모니터링하면 가용성 그룹 문제를 해결할 때 근본적인 원인 진단에 도움을 줄 수도 있습니다.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 5950f98a-3950-473d-95fd-cde3557b8fc2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2301a4709585f9243073f085703a3070c813b43e
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860634"
---
# <a name="configure-extended-events-for-always-on-availability-groups"></a>Always On 가용성 그룹에 대한 확장 이벤트 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server는 Always On 가용성 그룹 관련 확장 이벤트를 정의합니다. 세션에서 이 확장 이벤트를 모니터링하면 가용성 그룹 문제를 해결할 때 근본적인 원인 진단에 도움을 줄 수도 있습니다. 다음 쿼리를 사용하여 가용성 그룹 확장 이벤트를 볼 수 있습니다.  
  
```sql  
SELECT * FROM sys.dm_xe_objects WHERE name LIKE '%hadr%'  
```  
  
 [Alwayson_health 세션](always-on-extended-events.md#BKMK_alwayson_health)  
  
 [디버깅용 확장 이벤트](always-on-extended-events.md#BKMK_Debugging)  
  
 [Always On 가용성 그룹 확장 이벤트 참조](always-on-extended-events.md#BKMK_Reference)  
  
##  <a name="BKMK_alwayson_health"></a> Alwayson_health 세션  
 Alwayson_health 확장 이벤트 세션은 가용성 그룹을 만들 때 자동으로 만들어지며 가용성 그룹 관련 이벤트의 하위 집합을 캡처합니다. 이 세션은 가용성 그룹 문제를 해결하는 동안 빨리 시작하도록 도와 주는 유용하고 편리한 도구로 미리 구성됩니다. 가용성 그룹 만들기 마법사가 해당 마법사에 구성된 모든 참여 가용성 복제본에 대해 세션을 자동으로 시작합니다.  
  
> [!IMPORTANT]  
>  **새 가용성 그룹 마법사**를 사용하여 가용성 그룹을 만들지 않은 경우 alwayson_health 세션이 자동으로 시작되지 않을 수 있습니다. 세션이 시작되지 않으면 예기치 않은 문제가 발생할 때 이벤트 데이터를 캡처할 수 없습니다. 따라서 수동으로 세션을 시작하고 세션 속성을 구성하여 세션을 자동으로 시작하도록 구성해야 합니다.  
  
 Alwayson_health 세션의 정의 보려면:  
  
1.  **개체 탐색기**에서 **관리**, **확장 이벤트**, **세션**을 차례로 확장합니다.  
  
2.  **Alwayson_health**를 마우스 오른쪽 단추로 클릭한 다음, **세션 스크립팅**, **CREATE To**를 차례로 가리키고 **새 쿼리 편집기 창**을 클릭합니다.  

Alwayson_health에서 다루는 몇몇 이벤트에 대한 자세한 내용은 [확장 이벤트 참조](always-on-extended-events.md#BKMK_Reference)를 참조하세요.  


##  <a name="BKMK_Debugging"></a> 디버깅용 확장 이벤트  
 Alwayson_health 세션에서 다루는 확장 이벤트 외에도 SQL Server는 가용성 그룹에 대한 다양한 디버그 이벤트 집합을 정의합니다. 세션에서 이러한 추가 확장 이벤트를 활용하려면 아래 절차를 따르십시오.  
  
1.  **개체 탐색기**에서 **관리**, **확장 이벤트**, **세션**을 차례로 확장합니다.  
  
2.  **세션** 을 마우스 오른쪽 단추로 클릭하고 **새 세션**을 선택합니다. 또는 **Alwayson_health**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **페이지 선택** 창에서 **이벤트**를 클릭합니다.  
  
4.  이벤트 라이브러리의 **범주** 열에서 **alwayson**을 선택하고 모든 다른 범주를 선택 취소합니다.  
  
5.  **채널** 열에서 **디버그**를 선택합니다. 아직 선택되지 않은 모든 가용성 그룹 관련 이벤트가 이제 이벤트 라이브러리에 표시됩니다.  
  
6.  이벤트 라이브러리에서 이벤트를 강조 표시한 다음, **>** 단추를 클릭하여 세션에 대해 선택합니다.  
  
7.  세션이 완료되면 **확인**을 클릭하여 닫습니다. 세션이 선택한 이벤트를 캡처하도록 시작되는지 확인합니다.  
  
##  <a name="BKMK_Reference"></a> Always On 가용성 그룹 확장 이벤트 참조  
 이 섹션에서는 가용성 그룹을 모니터링하는 데 사용되는 몇몇 확장 이벤트를 설명합니다.  
  
 [availability_replica_state_change](#BKMK_availability_replica_state_change)  
  
 [availability_group_lease_expired](#BKMK_availability_group_lease_expired)  
  
 [availability_replica_automatic_failover_validation](#BKMK_availability_replica_automatic_failover_validation)  
  
 [error_reported(여러 오류 번호): 전송 또는 연결 문제의 경우](#BKMK_error_reported)  
  
 [data_movement_suspend_resume](#BKMK_data_movement_suspend_resume)  
  
 [alwayson_ddl_executed](#BKMK_alwayson_ddl_executed)  
  
 [availability_replica_manager_state](#BKMK_availability_replica_manager_state)  
  
 [error_reported(1480): 데이터베이스 복제본 역할 변경](#BKMK_error_reported_1480)  
  
###  <a name="BKMK_availability_replica_state_change"></a> availability_replica_state_change  
 가용성 복제본의 상태가 변경되었을 때 발생합니다. 가용성 그룹을 만들거나 가용성 복제본을 조인하면 이 이벤트를 트리거할 수 있습니다. 실패한 자동 장애 조치(failover)의 진단에 유용합니다. 장애 조치 단계를 추적하는 데에도 사용할 수 있습니다.  
  
#### <a name="event-information"></a>이벤트 정보  
  
|Column|설명|  
|------------|-----------------|  
|속성|availability_replica_state_change|  
|범주|alwayson|  
|채널|Operational|  
  
#### <a name="event-fields"></a>이벤트 필드  
  
|속성|Type_name|설명|  
|----------|----------------|-----------------|  
|availability_group_id|guid|가용성 그룹의 ID입니다.|  
|availability_group_name|unicode_string|가용성 그룹의 이름입니다.|  
|availability_replica_id|guid|가용성 복제본의 ID입니다.|  
|previous_state|availability_replica_state|변경 전의 복제본 역할입니다.<br /><br /> **가능한 값은**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
|current_state|availability_replica_state|변경 후의 복제본 역할입니다.<br /><br /> **가능한 값은**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_replica_state_change  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_group_lease_expired"></a> availability_group_lease_expired  
 클러스터 및 가용성 그룹에 연결 문제가 있고 임대가 만료된 경우 발생합니다. 이 이벤트는 가용성 그룹과 기본 WSFC 클러스터 간의 연결이 끊어졌음을 나타냅니다. 주 복제본에 연결 문제가 발생한 경우 이 이벤트가 자동 장애 조치(failover)를 실행하게 하거나 가용성 그룹을 오프라인 상태로 만들 수 있습니다.  
  
#### <a name="event-information"></a>이벤트 정보  
  
|Column|설명|  
|------------|-----------------|  
|속성|availability_group_lease_expired|  
|범주|alwayson|  
|채널|Operational|  
  
#### <a name="event-fields"></a>이벤트 필드  
  
|속성|Type_name|설명|  
|----------|----------------|-----------------|  
|availability_group_id|guid|가용성 그룹의 ID입니다.|  
|availability_group_name|unicode_string|가용성 그룹의 이름입니다.|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_group_lease_expired  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_replica_automatic_failover_validation"></a> availability_replica_automatic_failover_validation  
 자동 장애 조치(failover)에서 가용성 복제본의 준비 상태에 대한 유효성을 검사하여 주 복제본으로 확인할 때 발생하며 대상 가용성 복제본이 새로운 주 복제본이 될 준비가 되었는지 여부를 나타냅니다. 예를 들어 일부 데이터베이스가 동기화되지 않았거나 조인되지 않은 경우 장애 조치(failover) 유효성 검사에서 False를 반환합니다. 이 이벤트는 장애 조치(failover) 중에 실패 지점을 제공하기 위한 설계입니다. 자동 장애 조치(failover)는 무인 작업이므로 이 정보는 특히 자동 장애 조치의 경우 데이터베이스 관리자에게 관심이 있습니다. 데이터베이스 관리자는 이벤트를 검토하여 자동 장애 조치(failover)가 실패한 이유를 알 수 있습니다.  
  
#### <a name="event-information"></a>이벤트 정보  
  
|속성|설명|  
|----------|-----------------|  
|availability_replica_automatic _failover_validation||  
|범주|alwayson|  
|채널|Analytic|  
  
#### <a name="event-fields"></a>이벤트 필드  
  
|속성|Type_name|설명|  
|----------|----------------|-----------------|  
|availability_group_id|guid|가용성 그룹의 ID입니다.|  
|availability_group_name|unicode_string|가용성 그룹의 이름입니다.|  
|availability_replica_id|guid|가용성 복제본의 ID입니다.|  
|forced_quorum|validation_result_type|값이 TRUE이면 이 가용성 복제본에서 자동 장애 조치(Failover)가 무효화됩니다.<br /><br /> TRUE<br /><br /> FALSE|  
|joined_and_synchronized|validation_result_type|값이 FALSE이면 이 가용성 복제본에서 자동 장애 조치(Failover)가 무효화됩니다.<br /><br /> TRUE<br /><br /> FALSE|  
|previous_primary_or_automatic_failover_target|validation_result_type|값이 FALSE이면 이 가용성 복제본에서 자동 장애 조치(Failover)가 무효화됩니다.<br /><br /> TRUE<br /><br /> FALSE|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_automatic_failover_validation (  
WHERE (  
[forced_quorum]=(TRUE) OR [joined_and_synchronized]=(FALSE) OR [previous_primary_or_automatic_failover_target]=(TRUE)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
  
```  
  
###  <a name="BKMK_error_reported"></a> error_reported(여러 오류 번호): 전송 또는 연결 문제의 경우  
 각 실패한 이벤트는 가용성 그룹이 의존하는 전송 또는 데이터베이스 미러링 엔드포인트에서 연결 문제가 발생했음을 나타냅니다.  
  
|Column|설명|  
|------------|-----------------|  
|속성|error_reported<br /><br /> 필터링할 번호: 35201, 35202, 35206, 35204, 35207, 9642, 9666, 9691, 9692, 9693, 28034, 28036, 28080, 28091, 33309|  
|범주|오류|  
|채널|Admin|  
  
#### <a name="error-numbers-to-filter"></a>필터링할 오류 번호  
  
|오류 번호|설명|  
|------------------|-----------------|  
|35201|가용성 복제본 '%ls'에 연결 설정을 시도하는 동안 연결 시간 제한이 발생했습니다.|  
|35202|ID [%ls]인 가용성 복제본 '%ls'에서 ID [%ls]인 '%ls'까지 가용성 그룹 '%ls'에 대한 연결이 설정되었습니다.  이 메시지는 정보 제공용이므로 사용자가 조치할 필요는 없습니다.|  
|35206|가용성 복제본 '%ls'에 대해 이전에 설정된 연결에서 연결 시간 제한이 발생했습니다.|  
|35204|엔드포인트 종료로 인해 인스턴스 '%ls' 및 '%ls' 간의 연결이 사용하지 않도록 설정되었습니다.|  
|시간 제한 + 연결됨|  
|35207|오류 %d 심각도 %d 상태 %d 때문에 복제본 ID '%ls'에서 복제본 ID '%ls'까지 가용성 그룹 ID '%ls'에 대한 연결 시도가 실패했습니다.  심각도 %d 상태 %d. (이는 좋은 DBA 사용을 포함하지 않을 수 있습니다. 그러한 경우 나중에 확인하여 제거하십시오.)|  
|9642|Service Broker/데이터베이스 미러링 전송 연결 엔드포인트에서 오류가 발생했습니다. 오류: %i 상태: %i. (근거리 엔드포인트 역할: %S_MSG  원거리 엔드포인트 주소: '%.*hs') 오류: %i 상태: %i. (근거리 엔드포인트 역할: %S_MSG 원거리 엔드포인트 주소: '%.\*hs')|  
|9666|%S_MSG 엔드포인트가 사용할 수 없거나 정지된 상태에 있습니다.|  
|9691|%S_MSG 엔드포인트가 연결 수신 대기를 중지했습니다.|  
|9692|%S_MSG 엔드포인트는 다른 프로세스에 사용 중이므로 포트 %d에서 수신 대기할 수 없습니다.|  
|9693|%S_MSG 엔드포인트가 다음 오류로 인해 연결에 대해 수신 대기할 수 없습니다: '%.*ls'.|  
|28034|연결 핸드셰이크가 실패했습니다. 로그인 '%.*ls'에 엔드포인트에 대한 CONNECT 권한이 없습니다. 상태 %d.|  
|28036|연결 핸드셰이크가 실패했습니다. 이 엔드포인트에 사용된 인증서를 찾을 수 없습니다: %S_MSG. master 데이터베이스에서 DBCC CHECKDB를 사용하여 엔드포인트의 메타데이터 무결성을 확인하세요. 상태 %d.|  
|28080|연결 핸드셰이크가 실패했습니다. %S_MSG 엔드포인트가 구성되어 있지 않습니다. 상태 %d.|  
|28091|인증이 없는 %S_MSG에 대한 시작 엔드포인트는 지원되지 않습니다.|  
|33309|기본 %S_MSG 엔드포인트 구성이 아직 로드되지 않았으므로 클러스터 엔드포인트를 시작할 수 없습니다.|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--Connectivity Error Messages  
[error_number]=(35201)   
OR [error_number]=(35202)   
OR [error_number]=(35204)   
OR [error_number]=(35206)   
OR [error_number]=(35207)   
OR [error_number]=(9642)   
--OR [error_number]=(9666)   
OR [error_number]=(9691)   
OR [error_number]=(9692)   
OR [error_number]=(9693)   
OR [error_number]=(28034)   
OR [error_number]=(28036)   
OR [error_number]=(28080)   
OR [error_number]=(28091)   
OR [error_number]=(33309)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_data_movement_suspend_resume"></a> data_movement_suspend_resume  
 데이터베이스 복제본의 데이터베이스 이동이 일시 중단되거나 다시 시작되었습니다.  
  
#### <a name="event-information"></a>이벤트 정보  
  
|Column|설명|  
|------------|-----------------|  
|속성|data_movement_suspend_resume|  
|범주|Alwayson|  
|채널|Operational|  
  
#### <a name="event-fields"></a>이벤트 필드  
  
||||  
|-|-|-|  
|속성|Type_name|설명|  
|availability_group_id|guid|가용성 그룹의 ID입니다.|  
|availability_group_name|unicode_string|사용 가능한 경우 가용성 그룹의 이름입니다.|  
|availability_replica_id|guid|가용성 복제본의 ID입니다.|  
|database_replica_id|guid|가용성 데이터베이스의 ID입니다.|  
|database_replica_name|unicode_string|가용성 데이터베이스의 이름입니다.|  
|database_id|uint32|가용성 데이터베이스의 ID입니다.|  
|suspend_status|suspend_status_type|일시 중단 상태 값입니다.<br /><br /> SUSPEND_NULL<br /><br /> RESUMED<br /><br /> SUSPENDED<br /><br /> SUSPENDED_INVALID|  
|suspend_source|suspend_source_type|일시 중단 또는 다시 시작 작업의 원본입니다.|  
|suspend_reason|unicode_string|데이터베이스 복제본 관리자에서 캡처된 일시 중단 이유입니다.|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT data_movement_suspend_resume (  
WHERE (  
[suspend_status]=(SUSPENDED)or [suspend_status]=(SUSPENDED_INVALID) or   
[suspend_status]=(SUSPEND_NULL)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_alwayson_ddl_executed"></a> alwayson_ddl_executed  
 CREATE, ALTER 또는 DROP을 포함한 가용성 그룹 DDL(데이터 정의 언어) 명령문이 실행될 때 발생합니다. 이 이벤트의 주 목적은 가용성 복제본에 대한 사용자 작업이 있는 문제를 나타내거나 운영 작업의 시작점을 나타내는 것입니다. 이 이벤트가 발생한 다음, 수동 장애 조치(failover), 강제 장애 조치(failover), 일시 중단된 데이터 이동 또는 다시 시작된 데이터 이동 등과 같은 런타임 문제가 이어집니다.  
  
#### <a name="event-information"></a>이벤트 정보  
  
|Column|설명|  
|------------|-----------------|  
|속성|alwayson_ddl_execution|  
|범주|alwayson|  
|채널|Analytic|  
  
#### <a name="event-fields"></a>이벤트 필드  
  
|속성|Type_name|설명|  
|----------|----------------|-----------------|  
|availability_group_id|Guid|가용성 그룹의 ID입니다.|  
|availability_group_name|unicode_string|가용성 그룹의 이름입니다.|  
|ddl_action|alwayson_ddl_action|DDL 작업의 유형을 나타냅니다. 생성, 변경 또는 삭제.|  
|ddl_phase|ddl_opcode|DDL 작업의 단계를 나타냅니다. BEGIN, COMMIT 또는 ROLLBACK.|  
|인수를 제거합니다.|unicode_string|실행된 명령문의 텍스트입니다.|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT alwayson_ddl_executed  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_replica_manager_state"></a> availability_replica_manager_state  
 가용성 복제본 관리자의 상태가 변경되었을 때 발생합니다. 이 이벤트는 가용성 복제본 관리자의 하트비트를 나타냅니다. 가용성 복제본 관리자가 정상 상태에 있지 않은 경우 SQL Server 인스턴스의 모든 가용성 복제본이 다운됩니다.  
  
#### <a name="event-information"></a>이벤트 정보  
  
|Column|설명|  
|------------|-----------------|  
|속성|availability_replica_manager_state_change|  
|범주|alwayson|  
|채널|Operational|  
  
#### <a name="event-fields"></a>이벤트 필드  
  
|속성|Type_name|설명|  
|----------|----------------|-----------------|  
|current_state|manager_state|가용성 복제본 관리자의 현재 상태입니다.<br /><br /> 온라인<br /><br /> 오프라인<br /><br /> WaitingForClusterCommunication|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_manager_state (  
WHERE ([current_state]=(OFFLINE))  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_error_reported_1480"></a> error_reported(1480): 데이터베이스 복제본 역할 변경  
 이 필터링된 error_reported 이벤트는 가용성 복제본 역할이 변경된 후 비동기로 발생합니다. 이 이벤트는 장애 조치(failover) 프로세스 중에 예상된 역할의 변경에 실패함을 나타냅니다.  
  
#### <a name="event-information"></a>이벤트 정보  
  
|Column|설명|  
|------------|-----------------|  
|속성|error_reported<br /><br /> 오류 번호 1480: REPLICATION_TYPE_MSG 데이터베이스 "DATABASE_NAME"이 REASON_MSG로 인해 역할을 "OLD_ROLE"에서 "NEW_ROLE"로 변경함|  
|범주|오류|  
|채널|Admin|  
  
#### <a name="alwaysonhealth-session-definition"></a>Alwayson_health 세션 정의  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--database replica role change message  
OR [error_number] = (1480)  
  
--database replica runtime error messages  
OR [error_number]=(823)   
OR [error_number]=(824)   
OR [error_number]=(829)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
## <a name="next-steps"></a>다음 단계  
 [이벤트 세션 데이터 보기](https://msdn.microsoft.com/library/hh710068(v=sql.110).aspx)   
