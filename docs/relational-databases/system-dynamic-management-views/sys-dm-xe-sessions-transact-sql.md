---
description: sys.dm_xe_sessions(Transact-SQL)
title: sys. dm_xe_sessions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_sessions_TSQL
- dm_xe_sessions
- sys.dm_xe_sessions_TSQL
- sys.dm_xe_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_sessions dynamic management view
- extended events [SQL Server], views
ms.assetid: defd6efb-9507-4247-a91f-dc6ff5841e17
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 16e1b53b91e5c1dca0bfd1b9bab49ad5e129e9c2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543809"
---
# <a name="sysdm_xe_sessions-transact-sql"></a>sys.dm_xe_sessions(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  활성 확장 이벤트 세션에 대한 정보를 반환합니다. 이 세션은 이벤트, 동작 및 대상의 모음입니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|address|**varbinary(8)**|세션의 메모리 주소입니다. 주소는 로컬 시스템에서 고유 합니다. Null을 허용하지 않습니다.|  
|name|**nvarchar(256)**|세션의 이름입니다. 이름은 로컬 시스템에서 고유 합니다. Null을 허용하지 않습니다.|  
|pending_buffers|**int**|처리가 보류된 가득 찬 버퍼의 수입니다. Null을 허용하지 않습니다.|  
|total_regular_buffers|**int**|세션과 연결된 정규 버퍼의 총 수입니다. Null을 허용하지 않습니다.<br /><br /> 참고: 일반 버퍼는 대부분의 시간에 사용 됩니다. 이러한 버퍼는 충분한 크기를 가지고 있어 많은 이벤트를 보유할 수 있습니다. 일반적으로 세션당 3개 이상의 버퍼가 있습니다. 정규 버퍼의 수는 MEMORY_PARTITION_MODE 옵션을 통해 설정된 메모리 분할을 기반으로 서버에 의해 자동으로 결정됩니다. 정규 버퍼의 크기는 MAX_MEMORY 옵션(기본값: 4MB) 값을 버퍼 수로 나눈 것과 동일합니다. MEMORY_PARTITION_MODE 및 MAX_MEMORY 옵션에 대 한 자세한 내용은 [CREATE EVENT SESSION &#40;transact-sql&#41;](../../t-sql/statements/create-event-session-transact-sql.md)를 참조 하세요.|  
|regular_buffer_size|**bigint**|정규 버퍼 크기(바이트 단위)입니다. Null을 허용하지 않습니다.|  
|total_large_buffers|**int**|대용량 버퍼의 총 수입니다. Null을 허용하지 않습니다.<br /><br /> 참고: 큰 버퍼는 이벤트가 정규 버퍼 보다 큰 경우에 사용 됩니다. 대용량 버퍼는 이 용도에 맞게 명시적으로 따로 설정합니다. 대용량 버퍼는 이벤트 세션이 시작될 때 할당되고 MAX_EVENT_SIZE 옵션에 따라 크기가 결정됩니다. MAX_EVENT_SIZE 옵션에 대 한 자세한 내용은 [CREATE EVENT SESSION &#40;transact-sql&#41;](../../t-sql/statements/create-event-session-transact-sql.md)를 참조 하세요.|  
|large_buffer_siz|**bigint**|대용량 버퍼 크기(바이트 단위)입니다. Null을 허용하지 않습니다.|  
|total_buffer_size|**bigint**|세션 이벤트를 저장하는 데 사용되는 메모리 버퍼의 총 크기(바이트 단위)입니다. Null을 허용하지 않습니다.|  
|buffer_policy_flags|**int**|모든 버퍼가 가득 찼는데 새 이벤트가 발생한 경우 세션 이벤트 버퍼의 동작 방법을 나타내는 비트맵입니다. Null을 허용하지 않습니다.|  
|buffer_policy_desc|**nvarchar(256)**|모든 버퍼가 가득 찼는데 새 이벤트가 발생한 경우 세션 이벤트 버퍼의 동작 방법을 나타내는 설명입니다.  Null을 허용하지 않습니다. buffer_policy_desc 다음 중 하나일 수 있습니다.<br /><br /> 이벤트 삭제<br /><br /> 이벤트 삭제 안 함<br /><br /> 가득 찬 버퍼 삭제<br /><br /> 새 버퍼 할당|  
|flags|**int**|세션에 설정된 플래그를 나타내는 비트맵입니다. Null을 허용하지 않습니다.|  
|flag_desc|**nvarchar(256)**|세션에 설정된 플래그에 대한 설명입니다.  Null을 허용하지 않습니다. flag_desc은 다음을 조합 하 여 사용할 수 있습니다.<br /><br /> 닫을 때 버퍼 플러시<br /><br /> 전용 발송자<br /><br /> 재귀 이벤트 허용|  
|dropped_event_count|**int**|버퍼가 가득 찼을 때 삭제된 이벤트 수입니다. 버퍼 정책이 "전체 버퍼 삭제" 또는 "이벤트 삭제 안 함" 인 경우이 값은 **0** 입니다. Null을 허용하지 않습니다.|  
|dropped_buffer_count|**int**|버퍼가 가득 찼을 때 삭제된 버퍼 수입니다. 버퍼 정책이 "이벤트 삭제" 또는 "이벤트 삭제 안 함"으로 설정 된 경우이 값은 **0** 입니다. Null을 허용하지 않습니다.|  
|blocked_event_fire_time|**int**|버퍼가 가득 찼을 때 이벤트 발생이 차단된 기간입니다. 버퍼 정책이 "전체 버퍼 삭제" 또는 "이벤트 삭제" 인 경우이 값은 **0** 입니다. Null을 허용하지 않습니다.|  
|create_time|**datetime**|세션을 생성한 시간입니다. Null을 허용하지 않습니다.|  
|largest_event_dropped_size|**int**|세션 버퍼에 맞지 않는 가장 큰 이벤트의 크기입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

