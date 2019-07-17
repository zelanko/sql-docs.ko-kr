---
title: sys.dm_pdw_sql_requests (TRANSACT-SQL) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bca9930ef51de28c8059223c93ea0bb2651f971d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089153"
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  쿼리에서 SQL 단계의 일부로 모든 SQL Server 쿼리 배포에 대 한 정보를 보유합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 SQL 쿼리 분배 속한 쿼리의 고유 식별자입니다.<br /><br /> request_id, step_index, 및 distribution_id이이 보기에 대 한 키를 구성합니다.|참조의 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 배포의 일부인 쿼리 단계의 인덱스입니다.<br /><br /> request_id, step_index, 및 distribution_id이이 보기에 대 한 키를 구성합니다.|step_index를 참조 하세요 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|pdw_node_id|**int**|이 쿼리 배포 실행 되는 노드의 고유 식별자입니다.|에 대 한 node_id를 참조 하세요 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|distribution_id|**int**|이 쿼리 배포 실행 되는 배포의 고유 식별자입니다.<br /><br /> request_id, step_index, 및 distribution_id이이 보기에 대 한 키를 구성합니다.|distribution_id를 참조 하세요 [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)합니다. 배포 범위 하지 노드 범위에서 실행 되는 요청에 대 한-1로 설정 합니다.|  
|상태|**nvarchar(32)**|쿼리 분포의 현재 상태입니다.|보류 중, 실행, 실패, 취소 됨, 완료, 중단 CancelSubmitted|  
|error_id|**nvarchar(36)**|있는 경우이 쿼리 분산을 사용 하면 연결 오류의 고유 식별자입니다.|error_id를 참조 하세요 [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)합니다. 오류가 발생 하지 않은 경우 NULL로 설정 합니다.|  
|start_time|**datetime**|배포는 쿼리 실행을 시작 하는 시간입니다.|이 쿼리 분배 속한 작은 또는 현재 같음 및 크거나 쿼리 단계의 start_time|  
|end_time|**datetime**|이 쿼리 배포 실행을 완료, 취소 되었거나 실패 한 시간입니다.|크거나 같음 시작 시간, 또는 진행 중이거나 큐에 대기 중인 쿼리 분포는 경우 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|밀리초 단위로 쿼리 배포 실행 시간을 나타냅니다.|보다 크거나 0입니다. 내용의 start_time 및 end_time 완료, 실패 또는 쿼리 배포를 취소 합니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건이 "최대 값을 초과 했습니다." 경고 생성<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
|row_count|**bigint**|행 수가 변경 되거나이 쿼리 배포에 따라 읽기.|CREATE TABLE 및 DROP TABLE 등의 데이터를 반환 하거나 변경 하지 않는 작업에 대 한-1입니다.|  
|spid|**int**|쿼리 배포를 실행 하는 SQL Server 인스턴스에 세션 id입니다.||  
|command|**nvarchar(4000)**|전체 텍스트 쿼리 배포용이 명령입니다.|모든 유효한 요청 또는 쿼리 문자열입니다.|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에서 메타 데이터 섹션을 참조 합니다 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목입니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
