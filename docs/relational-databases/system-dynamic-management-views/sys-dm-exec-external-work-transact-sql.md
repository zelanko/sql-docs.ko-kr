---
title: sys.dm_exec_external_work (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a53a32f01dcf4646ee0bc12843c188b9b0e8e4c0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418627"
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  각 compute 노드에 작업자 당 워크 로드에 대 한 정보를 반환합니다.  
  
 외부 데이터 원본 (예: Hadoop 또는 외부 SQL Server)와 통신 하는 작업을 식별 하는 쿼리 sys.dm_exec_external_work 스핀업 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|연결 된 PolyBase 쿼리에 대 한 고유 식별자입니다.|참조 *request_ID* 에 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|이 작업 자가 수행 하는 요청입니다.|참조 *step_index* 에 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|**int**|이 작업 자가 실행 되는 DMS 계획의 단계입니다.|참조 [sys.dm_exec_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)합니다.|  
|compute_node_id|**int**|노드는 작업자에서 실행 됩니다.|참조 [sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)합니다.|  
|유형|**nvarchar(60)**|외부 작업의 형식입니다.|' 파일 분할 '|  
|work_id|**int**|실제 분할의 ID입니다.|보다 크거나 0입니다.|  
|input_name|**nvarchar(4000)**|읽을 입력의 이름|Hadoop을 사용 하는 경우 파일 이름입니다.|  
|read_location|**bigint**|오프셋 또는 위치를 읽습니다.|읽을 파일의 오프셋입니다.|  
|bytes_processed|**bigint**|이 작업자에 의해 처리 된 총 바이트 수입니다.|보다 크거나 0입니다.|  
|length|**bigint**|분할의 경우 Hadoop HDFS 블록 길이|사용자 정의 가능한 합니다. 기본값은 64 M|  
|상태|**nvarchar(32)**|작업자의 상태|보류 중으로 처리 하 고, 완료, 실패, 중단|  
|start_time|**datetime**|작업 시작||  
|end_time|**datetime**|작업의 끝||  
|total_elapsed_time|**int**|총 시간 (밀리초)||  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 동적 관리 뷰를 사용 하 여 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
