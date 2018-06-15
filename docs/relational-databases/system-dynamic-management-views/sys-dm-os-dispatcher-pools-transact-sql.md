---
title: sys.dm_os_dispatcher_pools (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 65f149f5fc1478fabaff8735c55f16fc8e32f421
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34465099"
---
# <a name="sysdmosdispatcherpools-transact-sql"></a>sys.dm_os_dispatcher_pools(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  세션 발송자 풀에 대한 정보를 반환합니다. 발송자 풀은 백그라운드 처리를 수행하기 위해 시스템 구성 요소에서 사용하는 스레드 풀입니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_dispatcher_pools**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|디스패처 풀의 주소입니다. 이며 dispatcher_pool_address는 고유 합니다. Null을 허용하지 않습니다.|  
|유형|**nvarchar(256)**|발송자 풀의 유형입니다. Null을 허용하지 않습니다. 다음과 같은 두 가지 유형의 발송자 풀이 있습니다.<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> 전체 목록에 대 한 DMV 쿼리|  
|name|**nvarchar(256)**|발송자 풀의 이름입니다. Null을 허용하지 않습니다.|  
|dispatcher_count|**int**|활성 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|dispatcher_ideal_count|**int**|발송자 풀이 증가하여 사용할 수 있게 되는 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|dispatcher_timeout_ms|**int**|발송자가 종료되기 전에 새로운 작업을 기다리는 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|dispatcher_waiting_count|**int**|유휴 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|queue_length|**int**|발송자 풀에서 처리되기 위해 대기 중인 작업 항목의 수입니다. Null을 허용하지 않습니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="see-also"></a>관련 항목:  
  
  


