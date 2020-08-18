---
description: sys. dm_exec_distributed_sql_requests (Transact-sql)
title: sys. dm_exec_distributed_sql_requests (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_distributed_requests management view
- dm_exec_distributed_requests management view
ms.assetid: d065dc01-35d4-472f-9554-53ac41e7d104
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fdda8279e49c5e1884cbd539e1a3158431e53b41
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88398849"
---
# <a name="sysdm_exec_distributed_sql_requests-transact-sql"></a>sys. dm_exec_distributed_sql_requests (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  모든 SQL 쿼리 배포에 대 한 정보를 쿼리에 있는 SQL 단계의 일부로 저장 합니다.  이 보기는 마지막 1000 요청에 대 한 데이터를 표시 합니다. 활성 요청은 항상이 뷰에 있는 데이터를 가집니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id 및 step_index이 보기에 대 한 키를 구성 합니다. 요청과 연결 된 고유 숫자 id입니다.|[Dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 을 참조 하십시오.|  
|step_index|**int**|이 배포가 속한 쿼리 단계의 인덱스입니다.|[Dm_exec_distributed_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)에서 step_index를 참조 하세요.|  
|compute_node_id|**int**|이 단계가 나타내는 작업의 유형입니다.|[Dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)에서 compute_node_id를 참조 하세요.|  
|distribution_id|**int**|단계가 실행 되는 위치입니다.|배포 범위가 아닌 노드 범위에서 실행 되는 요청의 경우-1로 설정 합니다.|  
|상태|**nvarchar(32)**|이 단계의 상태|활성, 취소 됨, 완료 됨, 실패, 대기 중|  
|error_id|**nvarchar (36)**|이 단계와 연결 된 오류의 고유 id입니다 (있는 경우).|[Dm_exec_compute_node_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)을 참조 하십시오. 오류가 발생 하지 않은 경우 NULL입니다.|  
|start_time|**datetime**|단계가 실행을 시작한 시간입니다.|현재 시간 보다 작거나 같고이 단계가 속한 쿼리의 end_compile_time 보다 크거나 같습니다.|  
|end_time|**datetime**|이 단계가 실행을 완료 하거나 취소 했거나 실패 한 시간입니다.|현재 시간 보다 작거나 같고 start_time 보다 크거나 같은 경우 현재 실행 중이거나 큐에 대기 중인 단계에 대해 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|쿼리 단계가 실행 된 총 시간 (밀리초)입니다.|0과 start_time 사이의 차이를 end_time 합니다. 대기 단계에 대해 0입니다.|  
|row_count|**bigint**|이 요청에서 변경 되거나 반환 된 총 행 수입니다.|0은 데이터를 변경 하거나 반환 하지 않은 단계의 경우에는 그렇지 않은 경우 영향을 받는 행 수입니다. DMS 단계에 대해-1로 설정 합니다.|  
|spid|**int**|쿼리 배포를 실행 하는 SQL Server 인스턴스의 세션 id||  
|명령을 사용합니다.|nvarchar(4000)|이 단계의 명령에 대 한 전체 텍스트를 포함 합니다.|단계에 대 한 유효한 모든 요청 문자열입니다. 4000 자 보다 길면 잘립니다.|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
