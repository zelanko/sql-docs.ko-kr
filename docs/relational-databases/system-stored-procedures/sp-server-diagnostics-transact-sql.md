---
title: sp_server_diagnostics (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_server_diagnostics
- sp_server_diagnostics_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_diagnostics
ms.assetid: 62658017-d089-459c-9492-c51e28f60efe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a15e965cef7109d42383d1a4dc4750c5dfef7374
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213772"
---
# <a name="spserverdiagnostics-transact-sql"></a>sp_server_diagnostics(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

잠재적 오류를 감지하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 진단 데이터 및 상태 정보를 캡처합니다. 이 프로시저는 반복 모드로 실행되며 주기적으로 결과를 보냅니다. 일반 연결 또는 DAC 연결에서 호출할 수 있습니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_server_diagnostics [@repeat_interval =] 'repeat_interval_in_seconds'   
```  
  
## <a name="arguments"></a>인수  
 [ **@repeat_interval** =] **'***repeat_interval_in_seconds***'**  
 저장 프로시저가 상태 정보를 보내기 위해 반복적으로 실행되는 시간 간격을 나타냅니다.  
  
 *repeat_interval_in_seconds* 됩니다 **int** 기본값인 0 사용 하 여 합니다. 올바른 매개 변수 값은 0 또는 5보다 크거나 같은 값입니다. 전체 데이터를 반환하려면 저장 프로시저가 적어도 5초 간격으로 실행되어야 합니다. 반복 모드에서 실행되는 저장 프로시저의 최소값은 5초입니다.  
  
 이 매개 변수를 지정하지 않거나 지정한 값이 0이면 저장 프로시저가 데이터를 한 번만 반환한 후 종료됩니다.  
  
 지정한 값이 최소값보다 작으면 오류가 발생하고 아무 결과도 반환되지 않습니다.  
  
 지정한 값이 5보다 크거나 같으면 저장 프로시저가 수동으로 취소할 때까지 반복적으로 실행되어 상태를 반환합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
**sp_server_diagnostics** 다음 정보를 반환 합니다.  
  
|Column|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**creation_time**|**datetime**|행 만들기의 타임스탬프를 나타냅니다. 단일 행 집합의 각 행은 타임스탬프가 같습니다.|  
|**component_type**|**sysname**|행에 대 한 정보를 포함 하는지 여부를 나타냅니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 수준 구성 요소 또는 Always On 가용성 그룹에 대 한 합니다.<br /><br /> instance<br /><br /> Always On: AvailabilityGroup|  
|**component_name**|**sysname**|구성 요소의 이름이나 가용성 그룹의 이름을 나타냅니다.<br /><br /> 시스템<br /><br /> resource<br /><br /> query_processing<br /><br /> io_subsystem<br /><br /> 이벤트<br /><br /> *\<가용성 그룹의 이름 >*|  
|**state**|**int**|구성 요소의 상태를 나타냅니다.<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> 3|  
|**state_desc**|**sysname**|state 열을 설명합니다. state 열의 값에 해당하는 설명은 다음과 같습니다.<br /><br /> 0: 알 수 없음<br /><br /> 1: 정리<br /><br /> 2: 경고<br /><br /> 3: 오류|  
|**data**|**varchar (max)**|구성 요소와 관련된 데이터를 지정합니다.|  
  
 다음은 다섯 가지 구성 요소에 대한 설명입니다.  
  
-   **시스템**: 시스템 큐브 뷰에서 spinlock, 엄격한 처리 조건, 잠겨 있는 태스크, 페이지 폴트 및 CPU 사용에 대한 데이터를 수집합니다. 이 정보는 전반적인 상태 권장 사항을 생성합니다.  
  
-   **리소스**:  리소스 큐브 뷰에서 실제 및 가상 메모리, 버퍼 풀, 페이지, 캐시 및 기타 메모리 개체에 대한 데이터를 수집합니다. 이 정보는 전반적인 상태 권장 사항을 생성합니다.  
  
-   **query_processing**: 쿼리 처리 큐브 뷰에서 작업자 스레드, 태스크, 잠겨 있는 태스크, 대기 유형, CPU 사용량이 많은 세션 및 차단 태스크에 대한 데이터를 수집합니다. 이 정보는 전반적인 상태 권장 사항을 생성합니다.  
  
-   **io 하위 시스템은**: IO에 대한 데이터를 수집합니다. 이 구성 요소는 진단 데이터와 함께 IO 하위 시스템에 대한 정상 상태 또는 경고 상태만 생성합니다.  
  
-   **이벤트**: 오류 및 링 버퍼 예외, 메모리, 스케줄러 모니터, 버퍼 풀, spinlock에서 메모리 브로커에 대 한 링 버퍼 이벤트에 대 한 세부 정보를 포함 하 여 서버에 의해 기록 된 이벤트 데이터 및 저장된 프로시저를 통해 화면 수집 보안 및 연결 합니다. 이벤트는 항상 상태로 0을 표시합니다.  
  
-   **\<가용성 그룹의 이름 >**: 지정된 된 가용성 그룹에 대 한 데이터 수집 (경우 component_type = "항상에서: AvailabilityGroup").  
  
## <a name="remarks"></a>Remarks  
오류 큐브 뷰에서 시스템, 리소스 및 쿼리 처리 구성 요소는 오류 감지에 활용되고, IO 하위 시스템 및 이벤트 구성 요소는 진단용으로만 활용됩니다.  
  
다음 표에서는 각 구성 요소와 관련 상태를 보여 줍니다.  
  
|구성 요소|정상(1)|경고(2)|오류(3)|알 수 없음(0)|  
|----------------|-----------------|-------------------|-----------------|--------------------|  
|시스템|x|x|x||  
|resource|x|x|x||  
|query_processing|x|x|x||  
|io_subsystem|x|x|||  
|이벤트||||x|  
  
각 행의 (x)는 구성 요소에 유효한 상태를 나타냅니다. 예를 들어 IO 하위 시스템은 정상 또는 경고로 표시됩니다. 오류 상태는 표시되지 않습니다.  
 
> [!NOTE]
> Sp_server_diagnostics 내부 프로시저의 실행은 높은 우선 순위로 preemptive 스레드에서 구현 됩니다.
  
## <a name="permissions"></a>사용 권한  
을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
상태 정보를 캡처하여 SQL Server 외부에 있는 파일에 저장하려면 확장 세션을 사용하는 것이 가장 좋습니다. 이렇게 하면 오류가 발생한 경우에도 계속 액세스할 수 있습니다. 다음 예에서는 이벤트 세션의 출력을 파일에 저장합니다.  
```sql  
CREATE EVENT SESSION [diag]  
ON SERVER  
           ADD EVENT [sp_server_diagnostics_component_result] (set collect_data=1)  
           ADD TARGET [asynchronous_file_target] (set filename='c:\temp\diag.xel');  
GO  
ALTER EVENT SESSION [diag]  
      ON SERVER STATE = start;  
GO  
```  
  
아래 예의 쿼리는 확장 세션 로그 파일을 읽습니다.  
```sql  
SELECT  
    xml_data.value('(/event/@name)[1]','varchar(max)') AS Name  
  , xml_data.value('(/event/@package)[1]', 'varchar(max)') AS Package  
  , xml_data.value('(/event/@timestamp)[1]', 'datetime') AS 'Time'  
  , xml_data.value('(/event/data[@name=''component_type'']/value)[1]','sysname') AS Sysname  
  , xml_data.value('(/event/data[@name=''component_name'']/value)[1]','sysname') AS Component  
  , xml_data.value('(/event/data[@name=''state'']/value)[1]','int') AS State  
  , xml_data.value('(/event/data[@name=''state_desc'']/value)[1]','sysname') AS State_desc  
  , xml_data.query('(/event/data[@name="data"]/value/*)') AS Data  
FROM   
(  
      SELECT  
                        object_name as event  
                        ,CONVERT(xml, event_data) as xml_data  
       FROM    
      sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\*.xel', NULL, NULL, NULL)  
)   
AS XEventData  
ORDER BY time;  
```  
  
다음 예에서는 sp_server_diagnostics의 출력을 반복되지 않는 모드로 테이블에 캡처합니다.  
```sql  
CREATE TABLE SpServerDiagnosticsResult  
(  
      create_time DateTime,  
      component_type sysname,  
      component_name sysname,  
      state int,  
      state_desc sysname,  
      data xml  
);  
INSERT INTO SpServerDiagnosticsResult  
EXEC sp_server_diagnostics; 
```  

아래의 예제 쿼리는 테이블의 요약 출력을 읽습니다.  
```sql  
SELECT create_time,
       component_name,
       state_desc 
FROM SpServerDiagnosticsResult;  
``` 

아래의 예제 쿼리는 테이블의 각 구성 요소의 자세한 출력을 읽습니다.  
```sql  
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult 
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult 
where component_name like 'resource'
go

-- Nonpreemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/nonPreemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- Preemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/preemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- CPU intensive requests
select cpureq.evt.value('(@sessionId)','bigint') as 'SessionID',
   cpureq.evt.value('(@command)','varchar(100)') as 'Command',
   cpureq.evt.value('(@cpuUtilization)','bigint') as 'CPU_Utilization',
   cpureq.evt.value('(@cpuTimeMs)','bigint') as 'CPU_Time_ms'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/cpuIntensiveRequests/request') AS cpureq(evt)
where component_name like 'query_processing'
go

-- Blocked Process Report
select blk.evt.query('.') as 'Blocked_Process_Report_XML'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/blockingTasks/blocked-process-report') AS blk(evt)
where component_name like 'query_processing'
go

-- IO
select data.value('(/ioSubsystem/@ioLatchTimeouts)[1]','bigint') as 'Latch_Timeouts',
   data.value('(/ioSubsystem/@totalLongIos)[1]','bigint') as 'Total_Long_IOs'
from SpServerDiagnosticsResult 
where component_name like 'io_subsystem'
go

-- Event information
select xevts.evt.value('(@name)','varchar(100)') as 'xEvent_Name',
   xevts.evt.value('(@package)','varchar(100)') as 'Package',
   xevts.evt.value('(@timestamp)','datetime') as 'xEvent_Time',
   xevts.evt.query('.') as 'Event Data'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/events/session/RingBufferTarget/event') AS xevts(evt)
where component_name like 'events'
go  
``` 
  
## <a name="see-also"></a>관련 항목  
 [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
