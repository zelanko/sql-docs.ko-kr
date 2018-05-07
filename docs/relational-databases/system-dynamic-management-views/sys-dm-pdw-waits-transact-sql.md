---
title: sys.dm_pdw_waits (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5130e498-1c77-4ae3-a80b-9aae396494e9
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 027aa6fef8df7b5b81febb923980319780b401bd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwwaits-transact-sql"></a>sys.dm_pdw_waits (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  모든 작업에 대 한 정보 상태 요청을 실행 하는 동안 발생 한 대기 또는 전송 큐에 대기 잠금을 포함 한 쿼리를 보유 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|대기 상태와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기에 대 한 키입니다.|시스템의 대기 시간을 모두에서 고유 합니다.|  
|session_id|**nvarchar(32)**|대기 상태에서 발생 한 세션의 ID입니다.|세션 id를 참조 하십시오. [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)합니다.|  
|유형|**nvarchar(255)**|이 항목을 나타내는 대기 유형입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_type|**nvarchar(255)**|대기 영향을 받는 개체의 형식입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_name|**nvarchar(386)**|이름 또는 영향을 받은 대기 지정된 된 개체의 GUID입니다.||  
|request_id|**nvarchar(32)**|대기 상태에서 수행 된 요청의 ID입니다.|참조에서 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|request_time|**datetime**|대기 상태에서 요청한 시간입니다.||  
|acquire_time|**datetime**|잠금 또는 리소스 획득 하는 시간입니다.||  
|state|**nvarchar(50)**|대기 상태에서의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|대기 중인 항목의 우선 순위입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
  
