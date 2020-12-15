---
description: sys.dm_pdw_sql_requests (Transact-sql)
title: sys.dm_pdw_sql_requests (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 360d6c5f5535b0e0702d1c7aede8721f27f88daf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482482"
---
# <a name="sysdm_pdw_sql_requests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  쿼리에서 SQL 단계의 일부로 모든 SQL Server 쿼리 배포에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 SQL 쿼리 배포가 속한 쿼리의 고유 식별자입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 distribution_id 구성 합니다.|[Sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)에서 request_id를 참조 하세요.|  
|step_index|**int**|이 배포가 속한 쿼리 단계의 인덱스입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 distribution_id 구성 합니다.|[Sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)에서 step_index를 참조 하세요.|  
|pdw_node_id|**int**|이 쿼리 배포가 실행 되는 노드의 고유 식별자입니다.|[Sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)에서 node_id를 참조 하세요.|  
|distribution_id|**int**|이 쿼리 배포가 실행 되는 배포의 고유 식별자입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 distribution_id 구성 합니다.|[Sys.pdw_distributions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)에서 distribution_id를 참조 하세요. 배포 범위가 아니라 노드 범위에서 실행 되는 요청에 대해-1로 설정 합니다.|  
|상태|**nvarchar(32)**|쿼리 분포의 현재 상태입니다.|보류 중, 실행 중, 실패, 취소 됨, 완료 됨, 중단 됨, CancelSubmitted 됨|  
|error_id|**nvarchar (36)**|이 쿼리 배포와 연결 된 오류의 고유 식별자입니다 (있는 경우).|[Sys.dm_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)에서 error_id를 참조 하세요. 오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|start_time|**datetime**|쿼리 배포에서 실행을 시작한 시간입니다.|현재 시간 보다 작거나 같고이 쿼리 배포가 속한 쿼리 단계의 start_time 보다 크거나 같습니다.|  
|end_time|**datetime**|이 쿼리 배포가 실행을 완료 하거나 취소 했거나 실패 한 시간입니다.|시작 시간 보다 크거나 같거나 쿼리 배포가 진행 중이거나 큐에 대기 중인 경우 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|쿼리 배포가 실행 된 시간 (밀리초)을 나타냅니다.|0 보다 크거나 같습니다. 완료, 실패 또는 취소 된 쿼리 배포에 대 한 start_time 및 end_time의 델타와 동일 합니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하는 경우 total_elapsed_time는 최대 값으로 계속 됩니다. 이 경우 "최 댓 값이 초과 되었습니다." 라는 경고가 생성 됩니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
|row_count|**bigint**|이 쿼리 배포에서 변경 하거나 읽은 행 수입니다.|CREATE TABLE 및 DROP TABLE과 같은 데이터를 변경 하거나 반환 하지 않는 작업의 경우-1입니다.|  
|spid|**int**|쿼리 배포를 실행 하는 SQL Server 인스턴스의 세션 id입니다.||  
|명령을 사용합니다.|**nvarchar(4000)**|이 쿼리 배포에 대 한 명령의 전체 텍스트입니다.|모든 유효한 쿼리 또는 요청 문자열입니다.|  
  
 이 보기에 의해 유지 되는 최대 행에 대 한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목에서 메타 데이터 섹션을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
