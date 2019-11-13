---
title: sys. dm_os_hosts (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: e4ff3e25accf5c499afb5e306a0eec206f6b3f82
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982548"
---
# <a name="sysdm_os_hosts-transact-sql"></a>sys.dm_os_hosts(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 등록되어 있는 모든 호스트를 반환합니다. 이 뷰는 이러한 호스트에서 사용하는 리소스도 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서이를 호출 하려면 **dm_pdw_nodes_os_hosts**이름을 사용 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8)**|호스트 개체의 내부 메모리 주소입니다.|  
|**유형**|**nvarchar(60)**|호스팅된 구성 요소의 유형입니다. 예를 들면 다음과 같습니다.<br /><br /> SOSHOST_CLIENTID_SERVERSNI= SQL Server 네이티브 인터페이스<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB 공급자<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft Data Access 런타임|  
|**name**|**nvarchar(32)**|호스트의 이름입니다.|  
|**enqueued_tasks_count**|**int**|이 호스트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 큐에 배치한 태스크의 총 개수입니다.|  
|**active_tasks_count**|**int**|이 호스트가 큐에 배치한 현재 실행 중인 태스크의 수입니다.|  
|**completed_ios_count**|**int**|이 호스트를 통해 실행되고 완료된 I/O의 총 개수입니다.|  
|**completed_ios_in_bytes**|**bigint**|이 호스트를 통해 완료된 I/O의 총 바이트 수입니다.|  
|**active_ios_count**|**int**|현재 완료 대기 중이며 이 호스트와 관련된 I/O 요청의 총 개수입니다.|  
|**default_memory_clerk_address**|**varbinary(8)**|이 호스트와 연관된 메모리 클럭 개체의 메모리 주소입니다. 자세한 내용은 [dm_os_memory_clerks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)을 참조 하세요.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 프리미엄 계층에는 데이터베이스에 대 한 `VIEW DATABASE STATE` 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard 및 Basic 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 파일의 일부가 아닌 OLE DB 공급자와 같은 구성 요소가 메모리를 할당하고 비선점형 일정에 참여할 수 있습니다. 이러한 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 호스팅되며 이러한 구성 요소에서 할당된 모든 리소스는 추적됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 호스팅을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 파일의 외부 구성 요소에서 사용하는 리소스를 효과적으로 관리할 수 있습니다.  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|일 대 일|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|일 대 일|  
  
## <a name="examples"></a>예  
 다음 예에서는 호스팅된 구성 요소에서 커밋된 총 메모리 양을 확인합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>참고 항목  

 [dm_os_memory_clerks &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [운영 체제 관련 동적 관리 뷰 &#40;transact-sql SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


