---
description: sys.dm_os_memory_brokers(Transact-SQL)
title: sys.dm_os_memory_brokers (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fdf1b7c25f6bad8947433106d789a04583f2c722
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97321873"
---
# <a name="sysdm_os_memory_brokers-transact-sql"></a>sys.dm_os_memory_brokers(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부의 할당은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자를 사용합니다. **Sys.dm_os_process_memory** 에서 프로세스 메모리 카운터 간의 차이점을 추적 하 고 내부 카운터는 메모리 공간의 외부 구성 요소에서 메모리 사용을 나타낼 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 메모리 Broker는 현재 및 예상 사용량에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 다양한 구성 요소 사이에 메모리 할당을 적절하게 분산합니다 메모리 Broker는 할당을 수행하지 않고, 분산을 계산하기 위해 할당을 추적만합니다.  
  
 다음 표에서는 메모리 Broker에 대한 정보를 제공합니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_os_memory_brokers** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|리소스 관리자 풀과 연관된 경우 리소스 풀의 ID입니다.|  
|**memory_broker_type**|**nvarchar(60)**|메모리 Broker의 유형입니다. 에는 현재 다음과 같은 세 가지 유형의 메모리 브로커가 나와 있습니다 .이에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대 한 설명은 아래에 나와 있습니다.<br /><br /> **MEMORYBROKER_FOR_CACHE** : 캐시 된 개체에서 사용 하도록 할당 된 메모리입니다 (버퍼 풀 캐시 아님).<br /><br /> **MEMORYBROKER_FOR_STEAL** : 버퍼 풀에서 도난당 한 메모리입니다. 현재 소유자가 이 메모리를 해제하기 전까지 이 메모리는 다른 구성 요소에서 다시 사용할 수 없습니다.<br /><br /> **MEMORYBROKER_FOR_RESERVE** : 현재 실행 중인 요청에서 나중에 사용 하도록 예약 된 메모리입니다.|  
|**allocations_kb**|**bigint**|이 유형의 Broker에 할당된 메모리 양(KB)입니다.|  
|**allocations_kb_per_sec**|**bigint**|초당 메모리 할당 비율(KB)입니다. 메모리 할당 취소의 경우 이 값은 음수가 될 수 있습니다.|  
|**predicted_allocations_kb**|**bigint**|Broker에서 할당된 메모리의 예상 양입니다. 이 값은 메모리 양 패턴에 기반합니다.|  
|**target_allocations_kb**|**bigint**|현재 설정 및 메모리 사용량 패턴에 따라 제안되는 할당된 메모리 양(KB)입니다. 이 Broker는 이 수만큼 증가하거나 축소해야 합니다.|  
|**future_allocations_kb**|**bigint**|다음 몇 초 동안 완료되는 예상 할당 수(LB)입니다.|  
|**overall_limit_kb**|**bigint**|브로커가 할당할 수 있는 최대 메모리 양 (KB)입니다.|  
|**last_notification**|**nvarchar(60)**|현재 설정 및 사용량 패턴에 따라 권장되는 메모리 사용량입니다. 유효한 값은 다음과 같습니다.<br /><br /> 증가<br /><br /> 축소<br /><br /> 안정|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   
  
## <a name="see-also"></a>참고 항목  

  [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


