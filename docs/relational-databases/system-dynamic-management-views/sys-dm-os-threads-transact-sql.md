---
title: sys. dm_os_threads (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef8eeeaaf59934d6c3307641b6c93f110ab5738f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73982540"
---
# <a name="sysdm_os_threads-transact-sql"></a>sys.dm_os_threads(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 실행되고 있는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 운영 체제 스레드를 목록으로 반환합니다.  
  
> [!NOTE]  
>  또는 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 이름 **sys. dm_pdw_nodes_os_threads**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary(8)**|스레드의 메모리 주소(기본 키)입니다.|  
|started_by_sqlservr|**bit**|스레드 시작자를 나타냅니다.<br /><br /> 1 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 스레드를 시작했습니다.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 확장 저장 프로시저와 같은 다른 구성 요소에서 스레드를 시작했습니다.|  
|os_thread_id|**int**|운영 체제가 할당한 스레드의 ID입니다.|  
|상태|**int**|내부 상태 플래그입니다.|  
|instruction_address|**varbinary(8)**|현재 실행 중인 명령의 주소입니다.|  
|creation_time|**datetime**|이 스레드가 생성된 시간입니다.|  
|kernel_time|**bigint**|이 스레드가 사용하는 커널 시간입니다.|  
|usermode_time|**bigint**|이 스레드가 사용하는 사용자 시간입니다.|  
|stack_base_address|**varbinary(8)**|이 스레드에 대한 최상위 스택 주소의 메모리 주소입니다.|  
|stack_end_address|**varbinary(8)**|이 스레드에 대한 최하위 스택 주소의 메모리 주소입니다.|  
|stack_bytes_committed|**int**|스택에서 커밋된 바이트 수입니다.|  
|stack_bytes_used|**int**|스레드에서 사용하고 있는 바이트 수입니다.|  
|affinity|**bigint**|이 스레드가 실행되고 있는 CPU 마스크입니다. **ALTER SERVER CONFIGURATION SET PROCESS AFFINITY** 문에 의해 구성 된 값에 따라 달라 집니다. 소프트 선호도의 경우 스케줄러와 다를 수 있습니다.|  
|우선 순위|**int**|이 스레드의 우선 순위 값입니다.|  
|Locale|**int**|스레드의 캐시된 로캘 LCID입니다.|  
|토큰|**varbinary(8)**|스레드의 캐시된 가장 토큰 핸들입니다.|  
|is_impersonating|**int**|이 스레드의 Win32 가장 사용 여부를 나타냅니다.<br /><br /> 1 = 스레드에서 프로세스의 기본값과 다른 보안 자격 증명을 사용하고 있습니다. 이것은 스레드가 프로세스를 만든 엔터티와 다른 엔터티를 가장하고 있다는 것을 나타냅니다.|  
|is_waiting_on_loader_lock|**int**|스레드가 로더 잠금을 기다리는 중인지 여부를 나타내는 운영 체제 상태입니다.|  
|fiber_data|**varbinary(8)**|스레드에서 실행 중인 현재의 Win32 파이버입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 경량 풀링이 구성된 경우에만 적용됩니다.|  
|thread_handle|**varbinary(8)**|내부적으로만 사용됩니다.|  
|event_handle|**varbinary(8)**|내부적으로만 사용됩니다.|  
|scheduler_address|**varbinary(8)**|이 스레드와 연관된 스케줄러의 메모리 주소입니다. 자세한 내용은 [dm_os_schedulers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)을 참조 하십시오.|  
|worker_address|**varbinary(8)**|이 스레드에 바인딩된 작업자의 메모리 주소입니다. 자세한 내용은 [dm_os_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)을 참조 하십시오.|  
|fiber_context_address|**varbinary(8)**|내부 파이버 컨텍스트 주소입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 경량 풀링이 구성된 경우에만 적용됩니다.|  
|self_address|**varbinary(8)**|내부 일관성 포인터입니다.|  
|processor_group|**smallint**|**적용 대상**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 이상<br /><br /> 프로세서 그룹 ID입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="notes-on-linux-version"></a>Linux 버전에 대 한 참고 사항

Linux에서 SQL 엔진의 작동 방식으로 인해이 정보 중 일부는 Linux 진단 데이터와 일치 하지 않습니다. 예 `os_thread_id` 를 들어는, `ps``top` 또는 procfs (/proc/`pid`)와 같은 도구의 결과와 일치 하지 않습니다.  이는 SQL Server 구성 요소와 운영 체제 간의 레이어인 SQLPAL (Platform 추상화 계층) 때문입니다.

## <a name="examples"></a>예  
 시작 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 스레드를 시작한 다음 작업자를 해당 스레드에 연결합니다. 그러나 확장 저장 프로시저와 같은 외부 구성 요소가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 스레드를 시작할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이러한 스레드를 제어하지 않습니다. dm_os_threads [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 리소스를 사용 하는 rogue 스레드에 대 한 정보를 제공할 수 있습니다.  
  
 다음 쿼리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 시작하지 않은 스레드를 실행하는 작업자와 실행 소요 시간을 확인하는 데 사용됩니다.  
  
> [!NOTE]
>  간단하게 다음 쿼리에서는 `*` 문에 별표(`SELECT`)를 사용합니다. 특히 카탈로그 뷰, 동적 관리 뷰 및 시스템 테이블 반환 함수에 대해서는 별표(*)를 사용하지 않아야 합니다. 이후 업그레이드 및 릴리스에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열을 추가 하 고 이러한 뷰 및 함수에 열 순서를 변경할 수 있습니다. 그렇게 되면 특정 열 순서 및 열 수를 예상하는 애플리케이션에서 오류가 발생할 수 있습니다.  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>참고 항목  
  [dm_os_workers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


