---
title: sys.dm_pdw_dms_external_work (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d96a80edd474b9709e465bfb544ff457ffba5030
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843951"
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 외부 작업에 대 한 모든 데이터 이동 서비스 (DMS) 단계에 대 한 정보를 포함 하는 시스템 뷰.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 DMS 작업자를 사용 하는 쿼리입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 구성합니다.|request_id 동일 [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 DMS 작업자를 호출 하는 쿼리 단계입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 구성합니다.|step_index 동일 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|dms_step_index|**int**|DMS 계획의 현재 단계입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 구성합니다.|dms___step_index 동일 [sys.dm_pdw_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)합니다.|  
|pdw_node_id|**int**|DMS 작업자를 실행 하는 노드입니다.|에 대 한 node_id 동일 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|유형|**nvarchar(60)**|이 노드가 실행 되는 외부 작업의 형식입니다.<br /><br /> 파일 분할은 여러 작은 됩니다도 나눠진 외부 Hadoop 파일 작업 합니다.|' 파일 분할 '|  
|work_id|**int**|파일 분할 id입니다.|보다 크거나 0입니다.<br /><br /> 계산 노드 당 고유 합니다.|  
|input_name|**nvarchar(60)**|읽는 중인 입력에 대 한 이름을 문자열입니다.|Hadoop 파일에 대 한 Hadoop 파일 이름입니다.|  
|read_location|**bigint**|읽기 위치 오프셋입니다.||  
|estimated_bytes_processed|**bigint**|이 작업자에 의해 처리 된 바이트 수입니다.|보다 크거나 0입니다.|  
|length|**bigint**|파일 분할 된 바이트 수입니다.<br /><br /> Hadoop에 대 한 HDFS 블록의 크기입니다.|사용자 정의입니다. 기본값은 64MB입니다.|  
|상태|**nvarchar(32)**|작업자의 상태입니다.|보류 중으로 처리 하 고, 완료, 실패, 중단|  
|start_time|**datetime**|이 작업 자가 실행 시작 된 시간입니다.|쿼리 단계가의 시작 시간 보다 크거나이 작업자에 속합니다. 참조 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|end_time|**datetime**|실행 종료, 실패 또는 취소 된 시간입니다.|진행 중이거나 큐에 대기 중인 작업자에 대 한 NULL입니다. 이 고, 그렇지 start_time 보다 큽니다.|  
|total_elapsed_time|**int**|밀리초 단위로 실행에 소요 된 총 시간입니다.|보다 크거나 0입니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건이 "최대 값을 초과 했습니다." 경고 생성<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 정보를 참조 하세요 [시스템 뷰 최대값](http://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
