---
title: sys.dm_exec_external_work (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: de0f740586cb37ac1e041d881271c8aed7ca703f
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  각 계산 노드에 대 한 작업자에 당 작업에 대 한 정보를 반환합니다.  
  
 외부 데이터 원본 (예: Hadoop 또는 외부 SQL Server)와 통신 하는 작업을 식별 하는 쿼리 sys.dm_exec_external_work로 작동 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|PolyBase 쿼리 연결된에 대 한 고유 식별자입니다.|참조 *request_ID* 에 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 작업 자가 수행 하는 요청입니다.|참조 *step_index* 에 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)합니다.|  
|dms_step_index|**int**|이 작업 자가 실행 되 고 있는 DMS 계획의 단계입니다.|참조 [sys.dm_exec_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)합니다.|  
|compute_node_id|**int**|노드는 작업자에서 실행 됩니다.|참조 [sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)합니다.|  
|유형|**nvarchar(60)**|외부 작업의 형식입니다.|' Split file'|  
|work_id|**int**|실제 분할의 ID입니다.|보다 크거나 0입니다.|  
|input_name|**nvarchar(4000)**|읽을 수에 대 한 입력의 이름|Hadoop을 사용 하는 경우 파일 이름입니다.|  
|read_location|**bigint**|오프셋 하거나 읽기 위치 합니다.|읽을 파일의 오프셋입니다.|  
|bytes_processed|**bigint**|이 작업자에 의해 처리 된 총 바이트 수입니다.|보다 크거나 0입니다.|  
|length|**bigint**|분할 또는 Hadoop 발생할 경우 HDFS 블록의 길이|사용자 정의 가능한 합니다. 기본값은 64 M|  
|상태|**nvarchar(32)**|작업자의 상태|보류 중 이며, 처리, 완료, 실패, 중단|  
|start_time|**datetime**|작업의 시작 부분||  
|end_time|**datetime**|작업의 끝||  
|total_elapsed_time|**int**|총 시간 (밀리초)||  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 동적 관리 뷰를 사용한 문제 해결](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
