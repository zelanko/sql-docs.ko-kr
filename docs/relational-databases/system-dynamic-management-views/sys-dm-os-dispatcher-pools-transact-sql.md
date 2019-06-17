---
title: sys.dm_os_dispatcher_pools (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a7a03063ad61c380f72e9a52b71f268b06d822d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62506006"
---
# <a name="sysdmosdispatcherpools-transact-sql"></a>sys.dm_os_dispatcher_pools(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  세션 발송자 풀에 대한 정보를 반환합니다. 발송자 풀은 백그라운드 처리를 수행하기 위해 시스템 구성 요소에서 사용하는 스레드 풀입니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_dispatcher_pools**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|디스패처 풀의 주소입니다. 이며 dispatcher_pool_address는 고유 합니다. Null을 허용하지 않습니다.|  
|유형|**nvarchar(256)**|발송자 풀의 유형입니다. Null을 허용하지 않습니다. 다음과 같은 두 가지 유형의 발송자 풀이 있습니다.<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> 전체 목록은 DMV를 쿼리 합니다.|  
|NAME|**nvarchar(256)**|발송자 풀의 이름입니다. Null을 허용하지 않습니다.|  
|dispatcher_count|**int**|활성 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|dispatcher_ideal_count|**int**|발송자 풀이 증가하여 사용할 수 있게 되는 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|dispatcher_timeout_ms|**int**|발송자가 종료되기 전에 새로운 작업을 기다리는 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|dispatcher_waiting_count|**int**|유휴 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|queue_length|**int**|발송자 풀에서 처리되기 위해 대기 중인 작업 항목의 수입니다. Null을 허용하지 않습니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   

## <a name="see-also"></a>관련 항목  
  
  


