---
title: sys.dm_os_memory_brokers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc48ab35ce0a2897b0167fd8609c21f46926966a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802901"
---
# <a name="sysdmosmemorybrokers-transact-sql"></a>sys.dm_os_memory_brokers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부의 할당은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자를 사용합니다. 프로세스 메모리 카운터 간의 차이 추적 **sys.dm_os_process_memory** 되며 내부 카운터에서 외부 구성 요소의 메모리 사용을 나타낼 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 공간입니다.  
  
 메모리 Broker는 현재 및 예상 사용량에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 다양한 구성 요소 사이에 메모리 할당을 적절하게 분산합니다 메모리 Broker는 할당을 수행하지 않고, 분산을 계산하기 위해 할당을 추적만합니다.  
  
 다음 표에서는 메모리 Broker에 대한 정보를 제공합니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_memory_brokers**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|리소스 관리자 풀과 연관된 경우 리소스 풀의 ID입니다.|  
|**memory_broker_type**|**nvarchar(60)**|메모리 Broker의 유형입니다. 현재 메모리 브로커에 세 가지 유형의 가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 해당 설명과 함께 아래 나열 합니다.<br /><br /> **MEMORYBROKER_FOR_CACHE** : 캐시 된 개체 (없습니다 버퍼 풀 캐시)에서 사용 하기 위해 할당 된 메모리입니다.<br /><br /> **MEMORYBROKER_FOR_STEAL** : 버퍼 풀에서 빼앗긴 메모리입니다. 현재 소유자가 이 메모리를 해제하기 전까지 이 메모리는 다른 구성 요소에서 다시 사용할 수 없습니다.<br /><br /> **MEMORYBROKER_FOR_RESERVE** : 현재 요청을 실행 하 여 사용 하도록 예약 하는 메모리입니다.|  
|**allocations_kb**|**bigint**|이 유형의 Broker에 할당된 메모리 양(KB)입니다.|  
|**allocations_kb_per_sec**|**bigint**|초당 메모리 할당 비율(KB)입니다. 메모리 할당 취소의 경우 이 값은 음수가 될 수 있습니다.|  
|**predicted_allocations_kb**|**bigint**|Broker에서 할당된 메모리의 예상 양입니다. 이 값은 메모리 양 패턴에 기반합니다.|  
|**target_allocations_kb**|**bigint**|현재 설정 및 메모리 사용량 패턴에 따라 제안되는 할당된 메모리 양(KB)입니다. 이 Broker는 이 수만큼 증가하거나 축소해야 합니다.|  
|**future_allocations_kb**|**bigint**|다음 몇 초 동안 완료되는 예상 할당 수(LB)입니다.|  
|**overall_limit_kb**|**bigint**|Broker가 할당할 수 있는 최대 메모리 양(KB)입니다.|  
|**last_notification**|**nvarchar(60)**|현재 설정 및 사용량 패턴에 따라 권장되는 메모리 사용량입니다. 유효한 값은 다음과 같습니다.<br /><br /> 증가<br /><br /> 축소<br /><br /> 안정|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
  
## <a name="see-also"></a>관련 항목  

  [SQL Server 운영 체제 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


