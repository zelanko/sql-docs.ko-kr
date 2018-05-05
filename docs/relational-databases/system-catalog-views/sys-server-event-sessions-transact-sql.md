---
title: sys.server_event_sessions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_event_sessions
- server_event_sessions_TSQL
- sys.server_event_sessions_TSQL
- sys.server_event_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_sessions catalog view
- xe
ms.assetid: 796f3093-6a3e-4d67-8da6-b9810ae9ef5b
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b6a09a6f303683104669a60e83cc8fd47bb37145
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysservereventsessions-transact-sql"></a>sys.server_event_sessions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 있는 이벤트 세션 정의를 모두 나열합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|이벤트 세션의 고유한 ID입니다. Null을 허용하지 않습니다.|  
|name|**sysname**|이벤트 세션을 식별하기 위한 사용자 정의 이름입니다. 이름은 고유 합니다. Null을 허용하지 않습니다.|  
|event_retention_mode|**nchar(1)**|이벤트 손실의 처리 방식을 결정합니다. 기본값은 S이며 Null을 허용하지 않습니다. 다음 중 하나일 수 있습니다.<br /><br /> S.는 Event_retention_mode_desc 매핑됨 ALLOW_SINGLE_EVENT_LOSS =<br /><br /> 13. Event_retention_mode_desc 매핑됨 = ALLOW_MULTIPLE_EVENT_LOSS<br /><br /> 14. Event_retention_mode_desc 매핑됨 NO_EVENT_LOSS =|  
|event_retention_mode_desc|**sysname**|이벤트 손실의 처리 방식을 설명합니다. 기본값은 ALLOW_SINGLE_EVENT_LOSS이며 Null을 허용하지 않습니다. 다음 중 하나일 수 있습니다.<br /><br /> ALLOW_SINGLE_EVENT_LOSS. 여러 이벤트가 세션에서 손실될 수 있습니다. 모든 이벤트 버퍼가 가득 찬 경우에만 한 개의 이벤트가 삭제됩니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 허용되는 성능 특성으로, 처리된 이벤트 스트림에서 데이터가 손실되는 것을 최소화합니다.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS. 가득 찬 이벤트 버퍼가 세션에서 손실될 수 있습니다. 손실되는 이벤트 수는 세션에 할당된 메모리 크기, 메모리 분할 및 버퍼에 있는 이벤트의 크기에 따라 달라집니다. 이 옵션은 이벤트 버퍼가 빠른 속도로 채워질 때 서버에 미치는 영향을 최소화하지만 많은 수의 이벤트가 세션에서 손실될 수 있습니다.<br /><br /> NO_EVENT_LOSS. 이벤트 손실이 허용되지 않습니다. 이 옵션을 사용하면 발생한 모든 이벤트가 보존되며, 이벤트 버퍼에 사용 가능한 공간이 생길 때까지 이벤트를 발생시키는 모든 태스크가 대기합니다. 따라서 이벤트 세션이 활성 상태인 동안에는 성능이 저하될 수 있습니다.|  
|max_dispatch_latency|**int**|이벤트가 세션 대상에 전달되기 전에 메모리에 버퍼링될 시간(밀리초)을 나타냅니다. 유효한 값은 -1과 1 - 2147483648 범위의 숫자입니다. 값 -1은 발송 대기 시간이 무한대임을 나타냅니다. Null을 허용합니다.|  
|max_memory|**int**|이벤트 버퍼링을 위해 세션에 할당되는 최대 메모리 양을 나타내며 기본값은 4MB입니다. Null을 허용합니다.|  
|max_event_size|**int**|이벤트 세션 버퍼에 맞지 않는 이벤트를 위해 예약된 메모리 양을 나타냅니다. max_event_size가 계산된 버퍼 크기를 초과할 경우 max_event_size의 두 버퍼가 추가로 이벤트 세션에 할당됩니다. Null을 허용합니다.|  
|memory_partition_mode|**nchar(1)**|이벤트 버퍼가 만들어지는 메모리 내의 위치입니다. 기본 파티션 모드는 G이며 Null을 허용하지 않습니다. memory_partition_mode 중 하나입니다.<br /><br /> G - NONE<br /><br /> C - PER_CPU<br /><br /> N - PER_NODE|  
|memory_partition_mode_desc|**sysname**|기본값은 NONE이며 Null을 허용하지 않습니다. 다음 중 하나일 수 있습니다.<br /><br /> NONE. SQL Server 인스턴스 내에 한 개의 버퍼 집합이 만들어집니다.<br /><br /> PER_CPU. CPU당 한 개의 버퍼 집합이 만들어집니다.<br /><br /> PER_NODE. NUMA(Non-Uniform Memory Access) 노드당 한 개의 버퍼 집합이 만들어집니다.|  
|track_causality|**bit**|인과 관계 추적을 설정하거나 해제합니다. 1(ON)로 설정된 경우 추적이 활성화되어 다른 서버 연결에 있는 관련 이벤트가 상호 관련될 수 있습니다. 기본 설정은 0(OFF)이며 Null을 허용하지 않습니다.|  
|startup_state|**bit**|서버가 시작될 때 세션을 자동으로 시작할지 여부를 결정하는 값으로, 기본값은 0입니다. Null을 허용하지 않습니다. 다음 중 하나일 수 있습니다.<br /><br /> 0(OFF). 서버가 시작될 때 이벤트 세션이 시작되지 않습니다.<br /><br /> 1(ON). 서버가 시작될 때 이벤트 세션이 시작됩니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [확장 이벤트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
