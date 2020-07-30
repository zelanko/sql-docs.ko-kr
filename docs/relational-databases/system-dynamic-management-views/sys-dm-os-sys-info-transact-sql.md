---
title: sys. dm_os_sys_info (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b384190b6ffeee077f6658d0701f036c3f7746a
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396838"
---
# <a name="sysdm_os_sys_info-transact-sql"></a>sys.dm_os_sys_info(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 사용할 수 있고 소비하는 리소스 및 컴퓨터에 대한 기타 유용한 정보를 반환합니다.  
  
> **참고:** 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_os_sys_info**을 사용 합니다.  
  
|열 이름|데이터 형식|설명 및 버전별 참고 사항 |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|현재 CPU 틱 수를 지정합니다. CPU 틱은 프로세서의 RDTSC 카운터에서 가져오며 단순하게 증가하는 숫자입니다. Null을 허용하지 않습니다.|  
|**ms_ticks**|**bigint**|컴퓨터가 시작된 이후 경과한 시간(밀리초)을 지정합니다. Null을 허용하지 않습니다.|  
|**cpu_count**|**int**|시스템의 논리적 CPU 수를 지정합니다. Null을 허용하지 않습니다.|  
|**hyperthread_ratio**|**int**|하나의 실제 프로세서 패키지에 표시되는 논리적 또는 물리적 코어의 비율을 지정합니다. Null을 허용하지 않습니다.|  
|**physical_memory_in_bytes**|**bigint**|**적용 대상:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .<br /><br /> 컴퓨터에 있는 실제 메모리의 전체 크기를 지정합니다. Null을 허용하지 않습니다.|  
|**physical_memory_kb**|**bigint**|**적용 대상:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 컴퓨터에 있는 실제 메모리의 전체 크기를 지정합니다. Null을 허용하지 않습니다.|  
|**virtual_memory_in_bytes**|**bigint**|**적용 대상:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .<br /><br /> 사용자 모드로 프로세스에 사용할 수 있는 가상 메모리의 양입니다. 3-GB 스위치를 사용하여 SQL Server가 시작되었는지 확인하는 데 사용할 수 있습니다.|  
|**virtual_memory_kb**|**bigint**|**적용 대상:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 사용자 모드로 프로세스에 사용할 수 있는 가상 주소 공간의 전체 크기를 지정합니다. Null을 허용하지 않습니다.|  
|**bpool_committed**|**int**|**적용 대상:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .<br /><br /> 메모리 관리자의 커밋된 메모리(KB)를 나타냅니다. 메모리 관리자의 예약된 메모리는 포함하지 않습니다. Null을 허용하지 않습니다.|  
|**committed_kb**|**int**|**적용 대상:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 메모리 관리자의 커밋된 메모리(KB)를 나타냅니다. 메모리 관리자의 예약된 메모리는 포함하지 않습니다. Null을 허용하지 않습니다.|  
|**bpool_commit_target**|**int**|**적용 대상:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .<br /><br /> SQL Server 메모리 관리자가 소비할 수 있는 메모리 크기(KB)를 나타냅니다.|  
|**committed_target_kb**|**int**|**적용 대상:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> SQL Server 메모리 관리자가 소비할 수 있는 메모리 크기(KB)를 나타냅니다. 다음과 같이 다양한 입력을 사용하여 필요한 메모리 양을 계산합니다.<br /><br /> -로드를 포함 하는 시스템의 현재 상태입니다.<br /><br /> -현재 프로세스에서 요청 하는 메모리<br /><br /> -컴퓨터에 설치 된 메모리의 양<br /><br /> -구성 매개 변수<br /><br /> **Committed_target_kb** **committed_kb**보다 크면 메모리 관리자가 추가 메모리를 얻으려고 시도 합니다. **Committed_target_kb** **committed_kb**보다 작으면 메모리 관리자가 커밋된 메모리 양을 축소 하려고 시도 합니다. **Committed_target_kb** 은 항상 도난당 하 고 예약 된 메모리를 포함 합니다. Null을 허용하지 않습니다.|  
|**bpool_visible**|**int**|**적용 대상:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .<br /><br /> 프로세스 가상 주소 공간에서 직접 액세스할 수 있는 버퍼 풀의 8KB 버퍼 수입니다. AWE(Address Windowing Extensions)를 사용하지 않을 때 버퍼 풀이 해당 메모리 대상을 획득한 경우(bpool_committed = bpool_commit_target), bpool_visible 값은 bpool_committed 값과 동일합니다. 32비트 버전의 SQL Server에서 AWE를 사용할 때, bpool_visible은 버퍼 풀로 할당된 물리적 메모리에 액세스하는 데 사용된 AWE 매핑 창의 크기를 나타냅니다. 이 매핑 창의 크기는 프로세스 주소 공간에 의해 바인딩되므로 표시되는 양은 커밋된 양보다 작으며 데이터베이스 페이지 이외의 용도로 메모리를 사용하는 내부 구성 요소에 의해 더욱 축소될 수 있습니다. bpool_visible 값이 너무 작으면 메모리 부족 오류가 표시될 수도 있습니다.|  
|**visible_target_kb**|**int**|**적용 대상:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> **Committed_target_kb**와 동일 합니다. Null을 허용하지 않습니다.|  
|**stack_size_in_bytes**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 만든 각 스레드의 호출 스택 크기를 지정합니다. Null을 허용하지 않습니다.|  
|**os_quantum**|**bigint**|비우선 태스크에 대한 퀀텀을 나타내며 밀리초 단위로 측정됩니다. 퀀텀 (초) = **os_quantum** /CPU 클록 속도입니다. Null을 허용하지 않습니다.|  
|**os_error_mode**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 오류 모드를 지정합니다. Null을 허용하지 않습니다.|  
|**os_priority_class**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 대한 우선 순위 클래스를 지정합니다. Null을 허용합니다.<br /><br /> 32 = 정상(오류 로그는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 보통 우선 순위(=7)에서 시작함을 나타냄)<br /><br /> 128 = 높음(오류 로그는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 높은 우선 순위에서 실행됨을 나타냄)  (=13).)<br /><br /> 자세한 내용은 [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)을 참조하세요.|  
|**max_workers_count**|**int**|만들 수 있는 최대 작업자 수를 나타냅니다. Null을 허용하지 않습니다.|  
|**scheduler_count**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 구성된 사용자 스케줄러 수를 나타냅니다. Null을 허용하지 않습니다.|  
|**scheduler_total_count**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 총 스케줄러 수를 나타냅니다. Null을 허용하지 않습니다.|  
|**deadlock_monitor_serial_number**|**int**|현재 교착 상태 모니터 시퀀스의 ID를 지정합니다. Null을 허용하지 않습니다.|  
|**sqlserver_start_time_ms_ticks**|**bigint**|마지막으로 시작 된 **ms_tick** 번호를 나타냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 현재 ms_ticks 열과 비교됩니다. Null을 허용하지 않습니다.|  
|**sqlserver_start_time**|**datetime**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 마지막으로 시작된 날짜와 시간을 지정합니다. Null을 허용하지 않습니다.|  
|**affinity_type**|**int**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> 현재 사용 중인 서버 CPU 프로세스 선호도의 유형을 지정합니다. Null을 허용하지 않습니다. 자세한 내용은 [ALTER SERVER CONFIGURATION &#40;transact-sql&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)를 참조 하세요.<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> **Affinity_type** 열에 대해 설명 합니다. Null을 허용하지 않습니다.<br /><br /> MANUAL = 하나 이상의 CPU에 선호도가 설정되었습니다.<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CPU 간에 스레드를 자유롭게 이동할 수 있습니다.|  
|**process_kernel_time_ms**|**bigint**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> 커널 모드에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스레드에 걸린 총 시간(밀리초)입니다. 이 값은 서버에 있는 모든 프로세서의 시간을 포함하므로 단일 프로세서 클럭보다 클 수 있습니다. Null을 허용하지 않습니다.|  
|**process_user_time_ms**|**bigint**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> 사용자 모드에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스레드에 걸린 총 시간(밀리초)입니다. 이 값은 서버에 있는 모든 프로세서의 시간을 포함하므로 단일 프로세서 클럭보다 클 수 있습니다. Null을 허용하지 않습니다.|  
|**time_source**|**int**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 벽시계 시간(wall clock time)을 검색하는 데 사용하는 API를 나타냅니다. Null을 허용하지 않습니다.<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> **Time_source** 열에 대해 설명 합니다. Null을 허용하지 않습니다.<br /><br /> QUERY_PERFORMANCE_COUNTER = [Queryperformancecounter](https://go.microsoft.com/fwlink/?LinkId=163095) API는 벽 시계 시간을 검색 합니다.<br /><br /> MULTIMEDIA_TIMER = 벽 시계 시간을 검색 하는 [멀티미디어 타이머](https://go.microsoft.com/fwlink/?LinkId=163094) API입니다.|  
|**virtual_machine_type**|**int**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 가상화된 환경에서 실행되고 있는지 여부를 나타냅니다.  Null을 허용하지 않습니다.<br /><br /> 0 = 없음<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**적용 대상:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> **Virtual_machine_type** 열에 대해 설명 합니다. Null을 허용하지 않습니다.<br /><br /> NONE = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 (가) 가상 머신 내에서 실행 되 고 있지 않습니다.<br /><br /> 하이퍼바이저 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하이퍼바이저를 실행 하는 os (하드웨어 지원 가상화를 활용 하는 호스트 os)에서 호스트 되는 가상 컴퓨터 내에서 실행 되 고 있습니다.<br /><br /> 기타 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft VIRTUAL PC와 같은 하드웨어 길잡이를 사용 하지 않는 OS에서 호스트 되는 가상 컴퓨터 내에서 실행 되 고 있습니다.|  
|**softnuma_configuration**|**int**|**적용 대상:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상<br /><br /> NUMA 노드를 구성 하는 방법을 지정 합니다. Null을 허용하지 않습니다.<br /><br /> 0 = OFF는 하드웨어 기본값을 나타냅니다.<br /><br /> 1 = 자동 소프트 NUMA<br /><br /> 2 = 레지스트리를 통한 수동 소프트 NUMA|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**적용 대상:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상<br /><br /> OFF = 소프트 NUMA 기능이 해제 되어 있습니다.<br /><br /> ON = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소프트 numa에 대 한 numa 노드 크기를 자동으로 결정 합니다.<br /><br /> 수동 = 수동으로 구성 된 소프트 NUMA|
|**process_physical_affinity**|**nvarchar (3072)** |**적용 대상:** 부터 시작 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 합니다.<br /><br />아직 정보를 얻을 수 없습니다. |
|**sql_memory_model**|**int**|**적용 대상:** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상.<br /><br />에서 메모리를 할당 하는 데 사용 하는 메모리 모델을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Null을 허용하지 않습니다.<br /><br />1 = 기본 메모리 모델<br />2 = 메모리의 페이지 잠금<br /> 3 = 메모리의 많은 페이지|
|**sql_memory_model_desc**|**nvarchar(120)**|**적용 대상:** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 이상.<br /><br />에서 메모리를 할당 하는 데 사용 하는 메모리 모델을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Null을 허용하지 않습니다.<br /><br />**CONVENTIONAL**  =  기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 기본 메모리 모델을 사용 하 여 메모리를 할당 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]시작 하는 동안 서비스 계정에 메모리의 잠금 페이지가 없는 경우 기본 sql 메모리 모델입니다.<br />**LOCK_PAGES**  =  LOCK_PAGES [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리의 페이지 잠금을 사용 하 여 메모리를 할당 합니다. SQL Server 시작 하는 동안 서비스 계정에 메모리의 페이지 잠금 권한이 SQL Server 때 기본 sql 메모리 관리자입니다.<br /> **LARGE_PAGES**  =  LARGE_PAGES [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 메모리를 할당 하기 위해 메모리의 많은 페이지를 사용 하 고 있습니다. SQL Server는 서버를 시작 하는 동안 및 추적 플래그 834가 설정 된 경우 SQL Server 서비스 계정에 메모리의 페이지 잠금 권한이 있는 경우에만 Large Pages 할당자를 사용 하 여 Enterprise edition에 메모리를 할당 합니다.|
|**pdw_node_id**|**int**|**적용 대상:** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
|**socket_count** |**int** | **적용 대상:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 이상.<br /><br />시스템에서 사용할 수 있는 프로세서 소켓 수를 지정 합니다. |  
|**cores_per_socket** |**int** | **적용 대상:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 이상.<br /><br />시스템에서 사용할 수 있는 소켓 당 프로세서 수를 지정 합니다. |  
|**numa_node_count** |**int** | **적용 대상:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 이상.<br /><br />시스템에서 사용할 수 있는 numa 노드 수를 지정 합니다. 이 열에는 실제 numa 노드 뿐만 아니라 소프트 numa 노드도 포함 됩니다. |  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



