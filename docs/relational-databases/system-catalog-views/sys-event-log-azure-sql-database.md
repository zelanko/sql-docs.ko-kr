---
description: sys.event_log(Azure SQL Database)
title: sys.event_log (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- event_log
- sys.event_log_TSQL
- event_log_TSQL
- sys.event_log
dev_langs:
- TSQL
helpviewer_keywords:
- event_log
- sys.event_log
ms.assetid: ad5496b5-e5c7-4a18-b5a0-3f985d7c4758
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current
ms.openlocfilehash: d60c081eecf88868db4541bc79960bf1bbd8723c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97412964"
---
# <a name="sysevent_log-azure-sql-database"></a>sys.event_log(Azure SQL Database)

[!INCLUDE[Azure SQL Database](../../includes/applies-to-version/asdb.md)]

  성공적인 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 데이터베이스 연결, 연결 실패 및 교착 상태를 반환 합니다. 이 정보를 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]가 있는 데이터베이스 활동을 추적하거나 문제 해결할 수 있습니다.  
  
> [!CAUTION]  
> 다 수의 데이터베이스 또는 많은 로그인을 포함 하는 설치의 경우 sys.event_log의 작업으로 인해 성능 제한, 높은 CPU 사용량 및 로그인 실패가 발생할 수 있습니다. Sys.event_log 쿼리는 문제에 기여할 수 있습니다. Microsoft에서이 문제를 해결 하기 위해 노력 하 고 있습니다. 이 문제로 인 한 영향을 줄이기 위해 sys.event_log의 쿼리를 제한 합니다. NewRelic SQL Server 플러그인의 사용자는 추가 구성 정보에 대 한 [성능 조정 & Microsoft Azure SQL Database 플러그 인 튜닝](https://discuss.newrelic.com/t/microsoft-azure-sql-database-plugin-tuning-performance-tweaks/30729) 을 방문 해야 합니다.  
  
 `sys.event_log` 뷰는 다음 열을 포함합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|데이터베이스의 이름입니다. 연결이 실패하고 사용자가 데이터베이스 이름을 지정하지 않은 경우 이 열은 비어 있습니다.|  
|**start_time**|**datetime2**|집계 간격 시작의 UTC 날짜 및 시간입니다. 집계 이벤트에 대해 시간은 항상 5분의 배수입니다. 예를 들어:<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|집계 간격 끝의 UTC 날짜 및 시간입니다. 집계 된 이벤트의 경우 **End_time** 은 항상 같은 행의 해당 **start_time** 보다 정확히 5 분 후입니다. 집계 되지 않은 이벤트의 경우 **start_time** 및 **end_time** 이벤트의 실제 UTC 날짜 및 시간과 같습니다.|  
|**event_category**|**nvarchar (64)**|이 이벤트를 생성한 높은 수준의 구성 요소입니다.<br /><br /> 가능한 값 목록은 [이벤트 유형](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 을 참조 하세요.|  
|**event_type**|**nvarchar (64)**|이벤트의 유형입니다.<br /><br /> 가능한 값 목록은 [이벤트 유형](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 을 참조 하세요.|  
|**event_subtype**|**int**|발생 이벤트의 하위 유형입니다.<br /><br /> 가능한 값 목록은 [이벤트 유형](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 을 참조 하세요.|  
|**event_subtype_desc**|**nvarchar (64)**|이벤트 하위 유형에 대한 설명입니다.<br /><br /> 가능한 값 목록은 [이벤트 유형](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 을 참조 하세요.|  
|**severity**|**int**|오류의 심각도입니다. 가능한 값은 다음과 같습니다.<br /><br /> 0 = 정보<br />1 = 경고<br />2 = 오류|  
|**event_count**|**int**|지정 된 시간 간격 (**start_time** 및 **end_time**) 내에 지정 된 데이터베이스에 대해이 이벤트가 발생 한 횟수입니다.|  
|**description**|**nvarchar(max)**|이벤트에 대한 상세한 설명입니다.<br /><br /> 가능한 값 목록은 [이벤트 유형](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 을 참조 하세요.|  
|**additional_data**|**XML**|*참고: Azure SQL Database V12의 경우이 값은 항상 NULL입니다. V12에 대 한 교착 상태 이벤트를 검색 하는 방법에 대 한 [예제](#Deadlock) 섹션을 참조 하세요.*<br /><br /> **교착 상태** 이벤트의 경우이 열에는 교착 상태 그래프가 포함 됩니다. 이 열은 다른 이벤트 유형에 대해서는 NULL을 반환합니다. |  
  
##  <a name="event-types"></a><a name="EventTypes"></a> 이벤트 유형

 이 뷰의 각 행에서 기록 하는 이벤트는 범주 (**event_category**), 이벤트 유형 (**event_type**) 및 하위 유형 (**event_subtype**)으로 식별 됩니다. 다음 테이블에서는 이 뷰에 수집된 이벤트 유형을 나열합니다.  
  
 **연결** 범주의 이벤트의 경우 요약 정보를 sys.database_connection_stats 보기에서 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 뷰에는 여기에 나와 있는 것 외에 발생할 수 있는 다른 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터베이스 이벤트가 포함되어 있지 않습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 후속 릴리스에 범주, 이벤트 유형 및 하위 유형이 추가될 수 있습니다.  
  
|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**description**|  
|-------------------------|---------------------|------------------------|------------------------------|------------------|---------------------|  
|**connectivity**|**connection_successful**|0|**connection_successful**|0|데이터베이스에 연결되었습니다.|  
|**connectivity**|**connection_failed**|0|**invalid_login_name**|2|이 SQL Server 버전에서 로그인 이름이 잘못되었습니다.|  
|**connectivity**|**connection_failed**|1|**windows_auth_not_supported**|2|이 버전의 SQL Server에서는 Windows 로그인이 지원되지 않습니다.|  
|**connectivity**|**connection_failed**|2|**attach_db_not_supported**|2|사용자가 지원되지 않는 데이터베이스 파일 첨부를 요청했습니다.|  
|**connectivity**|**connection_failed**|3|**change_password_not_supported**|2|사용자가 지원되지 않는 사용자 로그인 암호 변경을 요청했습니다.|  
|**connectivity**|**connection_failed**|4|**login_failed_for_user**|2|로그인에 실패했습니다.|  
|**connectivity**|**connection_failed**|5|**login_disabled**|2|로그인을 사용할 수 없습니다.|  
|**connectivity**|**connection_failed**|6|**failed_to_open_db**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 데이터베이스를 열 수 없습니다. 열려는 데이터베이스가 존재하지 않거나 인증이 부족해서일 수 있습니다.|  
|**connectivity**|**connection_failed**|7|**blocked_by_firewall**|2|클라이언트 IP 주소에서 서버에 액세스할 수 없습니다.|  
|**connectivity**|**connection_failed**|8|**client_close**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 클라이언트 연결 설정 시 시간이 초과되었습니다. 연결 제한 시간을 늘려 보세요.|  
|**connectivity**|**connection_failed**|9|**다시**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 당시에 데이터베이스가 재구성 중이었으므로 연결이 실패했습니다.|  
|**connectivity**|**connection_terminated**|0|**idle_connection_timeout**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 연결이 시스템에 정의된 임계값보다 오랫동안 유휴 상태였습니다.|  
|**connectivity**|**connection_terminated**|1|**다시**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 세션이 데이터베이스 재구성으로 인해 종료되었습니다.|  
|**connectivity**|**조절은**|*\<reason code>*|**reason_code**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 요청이 정체되었습니다.  제한 이유 코드: *\<reason code>* . 자세한 내용은 [엔진 제한](/previous-versions/azure/dn338079(v=azure.100))을 참조 하세요.|  
|**connectivity**|**throttling_long_transaction**|40549|**long_transaction**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 트랜잭션을 오래 실행하여 세션이 종료됩니다. 트랜잭션을 줄여 보세요. 자세한 내용은 [리소스 제한](/previous-versions/azure/dn338081(v=azure.100))을 참조 하세요.|  
|**connectivity**|**throttling_long_transaction**|40550|**excessive_lock_usage**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 잠금을 너무 많이 획득하여 세션이 종료되었습니다. 단일 트랜잭션에서 읽거나 수정하는 행 수를 줄여 보세요. 자세한 내용은 [리소스 제한](/previous-versions/azure/dn338081(v=azure.100))을 참조 하세요.|  
|**connectivity**|**throttling_long_transaction**|40551|**excessive_tempdb_usage**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> TEMPDB 사용량이 너무 많아 세션이 종료되었습니다. 쿼리를 수정하여 임시 테이블 공간 사용량을 줄여 보세요. 자세한 내용은 [리소스 제한](/previous-versions/azure/dn338081(v=azure.100))을 참조 하세요.|  
|**connectivity**|**throttling_long_transaction**|40552|**excessive_log_space_usage**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 트랜잭션 로그 공간 사용량이 너무 많아 세션이 종료되었습니다. 단일 트랜잭션에서 수정하는 행 수를 줄여 보세요. 자세한 내용은 [리소스 제한](/previous-versions/azure/dn338081(v=azure.100))을 참조 하세요.|  
|**connectivity**|**throttling_long_transaction**|40553|**excessive_memory_usage**|2|*참고: Azure SQL Database V11 적용 됩니다.*<br /><br /> 메모리 사용량이 너무 많아 세션이 종료되었습니다. 쿼리를 수정하여 처리할 행 수를 줄여 보세요. 자세한 내용은 [리소스 제한](/previous-versions/azure/dn338081(v=azure.100))을 참조 하세요.|  
|**엔진**|**교착 상태**|0|**교착 상태**|2|교착 상태가 발생했습니다.|  
  
## <a name="permissions"></a>사용 권한

 **Master** 데이터베이스에 액세스할 수 있는 권한이 있는 사용자에 게는이 뷰에 대 한 읽기 전용 액세스 권한이 있습니다.  
  
## <a name="remarks"></a>설명  
  
### <a name="event-aggregation"></a>이벤트 집계

 5분 간격 이내로 이 뷰에 이벤트 정보가 수집 및 집계됩니다. **Event_count** 열은 특정 **event_type** 지정 된 시간 간격 내에 특정 데이터베이스에 대해 발생 한 **event_subtype** 횟수를 나타냅니다.  
  
> [!NOTE]  
> 교착 상태와 같은 일부 이벤트는 집계되지 않습니다. 이러한 이벤트의 경우 **event_count** 1이 **start_time** 되 고 **end_time** 은 이벤트가 발생 한 실제 UTC 날짜 및 시간과 같습니다.  
  
 예를 들어, 사용자가 잘못된 로그인 이름으로 인해 2012년 2월 5일 오전 11시와 11시 5분(UTC) 사이에 데이터베이스 Database1에 대한 연결을 7회 실패한 경우 이 정보는 이 뷰의 단일 행에서 확인할 수 있습니다.  
  
|**database_name**|**start_time**|**end_time**|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**event_count**|**description**|**additional_data**|  
|------------------------|---------------------|-------------------|-------------------------|---------------------|------------------------|------------------------------|------------------|----------------------|---------------------|--------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`connectivity`|`connection_failed`|`4`|`login_failed_for_user`|`2`|`7`|`Login failed for user.`|`NULL`|  
  
### <a name="interval-start_time-and-end_time"></a>간격 start_time 및 end_time  
 이벤트는 *이벤트가 발생 하거나* **start_time** 된 _후_ 또는 해당 간격에 대해 **end_time** _되기 전에_ 집계 간격에 포함 됩니다. 예를 들어, 정확히 `2012-10-30 19:25:00.0000000`에 발생하는 이벤트는 아래에 표시된 초 간격에만 표시됩니다.  
  
```
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```

### <a name="data-updates"></a>데이터 업데이트

 이 뷰의 데이터는 시간의 경과에 따라 축적됩니다. 일반적으로 데이터는 집계 간격 시작 1시간 이내로 축적되지만 뷰에 모든 데이터가 나타나는 데 최대 24시간이 걸릴 수 있습니다. 그 시간 동안 단일 행 내에서 정보가 주기적으로 업데이트될 수 있습니다.  
  
### <a name="data-retention"></a>데이터 보존

 이 뷰의 데이터는 최대 30 일 동안 보존 됩니다. 데이터베이스 수와 각 데이터베이스가 생성 하는 고유 이벤트의 수에 따라 더 적을 수 있습니다. 이 정보를 더 오래 유지하려면 데이터를 별도의 데이터베이스에 복사합니다. 뷰의 초기 복사본을 만든 후 데이터가 축적됨에 따라 이 행이 업데이트될 수 있습니다. 데이터 복사본을 최신으로 유지하려면 행을 정기적으로 테이블 검색하여 기존 행의 이벤트 수 증가를 확인하고 (시작 및 종료 시간을 사용하여 고유한 행을 식별하여) 새 행을 식별한 다음 데이터 복사본에 변경 내용을 업데이트합니다.  
  
### <a name="errors-not-included"></a>포함되지 않은 오류

 이 뷰에는 일부 연결 및 오류 정보가 포함되지 않을 수 있습니다.  
  
- 이 뷰에는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 발생할 수 있는 모든 데이터베이스 오류,이 항목의 [이벤트 유형에](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 지정 된 오류만 포함 되어 있습니다.  
- 데이터 센터 내에 컴퓨터 오류가 발생 하면 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 이벤트 테이블에서 소량의 데이터가 누락 될 수 있습니다.  
- DoSGuard를 통해 IP 주소를 차단하는 경우 해당 IP 주소로부터의 연결 시도 이벤트는 수집할 수 없으며 이 뷰에 나타나지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="simple-examples"></a>간단한 예제

 다음 쿼리는 2011년 9월 25일 정오와 2011년 9월 28일(UTC) 사이에 발생한 모든 이벤트를 반환합니다. 기본적으로 쿼리 결과는 **start_time** (오름차순)을 기준으로 정렬 됩니다.  

```sql
SELECT * FROM sys.event_log
WHERE start_time >= '2011-09-25 12:00:00'
    AND end_time <= '2011-09-28 12:00:00';  
```

다음 쿼리는 Database1 데이터베이스에 대 한 모든 교착 상태 이벤트를 반환 합니다 (Azure SQL Database V11에만 적용).  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'deadlock'
    AND database_name = 'Database1';  
```

<a name="Deadlock"></a> 다음 쿼리는 Database1 데이터베이스에 대 한 모든 교착 상태 이벤트를 반환 합니다 (Azure SQL Database V12에만 적용).  

```sql
WITH CTE AS (  
       SELECT CAST(event_data AS XML)  AS [target_data_XML]  
   FROM sys.fn_xe_telemetry_blob_target_read_file('dl', null, null, null)  
)  
SELECT target_data_XML.value('(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
target_data_XML.query('/event/data[@name=''xml_report'']/value/deadlock') AS deadlock_xml,  
target_data_XML.query('/event/data[@name=''database_name'']/value').value('(/value)[1]', 'nvarchar(100)') AS db_name  
FROM CTE  
```

다음쿼리는 2011년 9월 25일 오전 10시와 오전 11시(UTC) 사이에 발생한 SQL 작업자 스레드 이벤트에 대해 강제 일시 중지를 반환합니다.  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'throttling'
    AND event_subtype = 4194307
    AND start_time >= '2011-09-25 10:00:00'
    AND end_time <= '2011-09-25 11:00:00';  
```

### <a name="db-scoped-extended-event"></a>DB-Scoped 확장 이벤트

 다음 샘플 코드를 사용 하 여 db 범위 확장 이벤트 (XEvent) 세션을 설정 합니다.  

```sql
IF EXISTS  
    (SELECT * from sys.database_event_sessions  
        WHERE name = 'azure_monitor_deadlock_session')  
BEGIN  
    ALTER EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE  
        DROP TARGET package0.ring_buffer;  
  
    DROP EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE;  
END  
  
CREATE EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    ADD EVENT sqlserver.database_xml_deadlock_report  
    ADD TARGET package0.ring_buffer  
    (  
        SET max_memory = 2048, max_events_limit = 10  
    )  
    WITH (STARTUP_STATE = ON,  
          EVENT_RETENTION_MODE = ALLOW_SINGLE_EVENT_LOSS);  
  
ALTER EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    STATE = START;  
```

### <a name="check-for-deadlock"></a>교착 상태 확인

다음 쿼리를 사용 하 여 교착 상태가 있는지 확인 합니다.  

```sql
WITH CTE AS (  
    SELECT CAST(xet.target_data AS XML)  AS [target_data_XML]  
        FROM            sys.dm_xe_database_session_targets AS xet  
             INNER JOIN sys.dm_xe_database_sessions        AS xe  
                 ON (xe.address = xet.event_session_address)  
        WHERE xe.name = 'azure_monitor_deadlock_session'  
)  
, CTE2 AS (  
    SELECT  
            T2.EventData.query('.').value(  
                '(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
            T2.EventData.query('.').query(  
                '(/event/data/value/deadlock)[1]')     AS deadlock_xml  
        FROM CTE  
            CROSS Apply [target_data_XML].nodes(  
                '/RingBufferTarget/event') AS T2(EventData)  
)  
SELECT * FROM CTE2;  
```

## <a name="see-also"></a>참고 항목

 [Azure SQL Database의 확장 이벤트](/azure/azure-sql/database/xevent-db-diff-from-svr)  
