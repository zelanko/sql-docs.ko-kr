---
title: sys.dm_pdw_wait_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a62b88ae5c5e0589b54781c85ff43cc39babe2fb
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51667812"
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>sys.dm_pdw_wait_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  와 관련 된 정보를 보유 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OS 상태 관련 다른 노드에서 실행 되는 인스턴스. 대기 유형 및 해당 설명의 목록을 참조 하세요 [sys.dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|이 항목이 참조 하는 노드의 ID입니다.||  
|**wait_name**|**nvarchar(255)**|대기 유형의 이름입니다.||  
|**max_wait_time**|**bigint**|이 대기 유형의 최대 대기 시간입니다.||  
|**request_count**|**bigint**|이 대기 횟수가 대기 유형의 대기 중인입니다.||  
|**signal_time**|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.||  
|**completed_count**|**bigint**|이 유형의 대기는 마지막 서버 이후 완료의 총 수를 다시 시작 합니다.||  
|**wait_time**|**bigint**|Millisecons에서이 대기 유형의 총 대기 시간입니다. Signal_time 모두 포함 합니다.||  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
