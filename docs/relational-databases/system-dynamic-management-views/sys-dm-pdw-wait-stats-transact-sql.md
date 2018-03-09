---
title: sys.dm_pdw_wait_stats (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 146a38ad01e742fcd72dc144d5ce939e3579a2cb
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>sys.dm_pdw_wait_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  와 관련 된 정보를 보관는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다른 노드에서 실행 되는 인스턴스에 관련 된 운영 체제 상태입니다. 대기 유형 및 해당 설명을 목록, 참조 [sys.dm_os_wait_stats](http://msdn.microsoft.com/en-us/library/ms179984\(v=sql.120\).aspx)합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|이 항목에서 참조 하는 노드의 ID입니다.||  
|**wait_name**|**nvarchar(255)**|대기 유형의 이름입니다.||  
|**max_wait_time**|**bigint**|이 대기 유형의 최대 대기 시간입니다.||  
|**request_count**|**bigint**|처리 중인 유형을 대기 하는이 대기 수입니다.||  
|**signal_time**|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.||  
|**completed_count**|**bigint**|이 유형의 대기 마지막 서버가 이후 완료 된 총 수를 다시 시작 합니다.||  
|**wait_time**|**bigint**|Millisecons에서이 대기 유형의 총 대기 시간입니다. Signal_time 모두 포함 합니다.||  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
