---
description: sys.dm_pdw_dms_external_work (Transact-sql)
title: sys.dm_pdw_dms_external_work (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 2baa21665d7fae6f87acbbebb88e55ca6c4624fc
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482634"
---
# <a name="sysdm_pdw_dms_external_work-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 외부 작업의 모든 DMS (데이터 이동 서비스) 단계에 대 한 정보를 포함 하는 시스템 뷰입니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 DMS 작업자를 사용 하는 쿼리입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 dms_step_index 구성 합니다.|[Transact-sql&#41;&#40;sys.dm_pdw_exec_requests ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)request_id와 동일 합니다.|  
|step_index|**int**|이 DMS 작업자를 호출 하는 쿼리 단계입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 dms_step_index 구성 합니다.|[Transact-sql&#41;&#40;sys.dm_pdw_request_steps ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)step_index와 동일 합니다.|  
|dms_step_index|**int**|DMS 계획의 현재 단계입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 dms_step_index 구성 합니다.|[Transact-sql&#41;&#40;sys.dm_pdw_dms_workers ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)dms___step_index와 동일 합니다.|  
|pdw_node_id|**int**|DMS 작업자를 실행 하는 노드입니다.|[Transact-sql&#41;&#40;sys.dm_pdw_nodes ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)node_id와 동일 합니다.|  
|형식|**nvarchar(60)**|이 노드가 실행 중인 외부 작업의 유형입니다.<br /><br /> 파일 분할은 여러 개의 작은 부분으로 분할 된 외부 Hadoop 파일의 작업입니다.|' 파일 분할 '|  
|work_id|**int**|파일 분할 ID입니다.|0 보다 크거나 같습니다.<br /><br /> Compute 노드당 고유 합니다.|  
|input_name|**nvarchar(60)**|읽고 있는 입력의 문자열 이름입니다.|Hadoop 파일의 경우 Hadoop 파일 이름입니다.|  
|read_location|**bigint**|읽기 위치의 오프셋입니다.||  
|estimated_bytes_processed|**bigint**|이 작업자에서 처리 한 바이트 수입니다.|0 보다 크거나 같습니다.|  
|length|**bigint**|분할 된 파일의 바이트 수입니다.<br /><br /> Hadoop의 경우 HDFS 블록의 크기입니다.|사용자 정의. 기본값은 64입니다.|  
|상태|**nvarchar(32)**|작업자의 상태입니다.|보류 중, 처리 중, 완료 됨, 실패, 중단 됨|  
|start_time|**datetime**|이 작업자의 실행이 시작 된 시간입니다.|이 작업자가 속한 쿼리 단계의 시작 시간 보다 크거나 같습니다. [Sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)를 참조 하세요.|  
|end_time|**datetime**|실행이 종료, 실패 또는 취소 된 시간입니다.|진행 중이거나 지연 된 작업자의 경우 NULL입니다. 그렇지 않으면 start_time 보다 큽니다.|  
|total_elapsed_time|**int**|실행에 소요 된 총 시간 (밀리초)입니다.|0 보다 크거나 같습니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하는 경우 total_elapsed_time는 최대 값으로 계속 됩니다. 이 경우 "최 댓 값이 초과 되었습니다." 라는 경고가 생성 됩니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
  
 이 보기에 의해 유지 되는 최대 행에 대 한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목에서 메타 데이터 섹션을 참조 하세요.
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)  
  
