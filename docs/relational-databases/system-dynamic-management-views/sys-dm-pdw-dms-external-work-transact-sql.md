---
title: sys.dm_pdw_dms_external_work (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b1fe850d6cee5938773695cecd2664b972110205
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 외부 작업에 대 한 모든 데이터 이동 서비스 (DMS) 단계에 대 한 정보를 보유 하는 시스템 뷰.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 DMS 작업자를 사용 하는 쿼리.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성합니다.|request_id 동일 [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 DMS 작업자를 호출 하는 쿼리 단계입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성합니다.|step_index 동일 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|dms_step_index|**int**|DMS 계획의 현재 단계입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성합니다.|dms___step_index 동일 [sys.dm_pdw_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)합니다.|  
|pdw_node_id|**int**|DMS 작업자를 실행 하는 노드입니다.|에 대 한 node_id 동일 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|유형|**nvarchar(60)**|이 노드가 실행 되 고 외부 작업의 형식입니다.<br /><br /> 파일 분할에 여러 개의 더 작은 까지의 나눠진 외부 Hadoop 파일에 대 한 작업입니다.|' 파일 분할 '|  
|work_id|**int**|파일 id입니다. 분했습니다|보다 크거나 0입니다.<br /><br /> 계산 노드 마다 고유 합니다.|  
|input_name|**nvarchar(60)**|읽는 중인 입력에 대 한 이름을 문자열입니다.|Hadoop 파일에 대 한 Hadoop 파일 이름입니다.|  
|read_location|**bigint**|읽기 위치 오프셋입니다.||  
|estimated_bytes_processed|**bigint**|이 작업자에 의해 처리 되는 바이트 수입니다.|보다 크거나 0입니다.|  
|length|**bigint**|파일 분할 된 바이트 수입니다.<br /><br /> Hadoop, HDFS 블록의 크기입니다.|사용자 정의입니다. 기본값인 64MB입니다.|  
|상태|**nvarchar(32)**|작업자의 상태입니다.|보류 중 이며, 처리, 완료, 실패, 중단|  
|start_time|**datetime**|이 작업자의 실행 시작 시간입니다.|쿼리 단계의 시작 시간 보다 크거나이 작업자에 속해 있습니다. 참조 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|end_time|**datetime**|시간을 실행 종료, 실패 또는 취소 되었습니다.|진행 중이거나 대기 중인 작업자에 대 한 NULL입니다. 그 외, start_time 보다 큽니다.|  
|total_elapsed_time|**int**|실행 시간 (밀리초)에에서 소요 된 총 시간입니다.|보다 크거나 0입니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건에는 "최 댓 값 초과 했습니다." 경고가 생성 됩니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 정보를 참조 하십시오. [최대 시스템 뷰의 값](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
