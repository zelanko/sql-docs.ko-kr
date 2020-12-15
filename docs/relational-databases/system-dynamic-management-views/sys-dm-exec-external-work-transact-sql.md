---
description: sys.dm_exec_external_work (Transact-sql)
title: sys.dm_exec_external_work (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6d373e5900cfebca38c6305bbe9e8cac3d36cb22
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477294"
---
# <a name="sysdm_exec_external_work-transact-sql"></a>sys.dm_exec_external_work (Transact-sql)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  각 계산 노드에서 작업자 당 워크 로드에 대 한 정보를 반환 합니다.  
  
 Sys.dm_exec_external_work 쿼리 하 여 외부 데이터 원본 (예: Hadoop 또는 외부 SQL Server)과 통신 하는 작업 분리을 식별 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|연결 된 PolyBase 쿼리의 고유 식별자입니다.|[Sys.dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)에서 *request_ID* 를 참조 하세요.|  
|step_index|`int`|이 작업자에서 수행 하는 요청입니다.|[Sys.dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)에서 *step_index* 를 참조 하세요.|  
|dms_step_index|`int`|이 작업자를 실행 하는 DMS 계획의 단계입니다.|[Sys.dm_exec_dms_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)를 참조 하세요.|  
|compute_node_id|`int`|Worker가 실행 되 고 있는 노드입니다.|[Sys.dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)를 참조 하세요.|  
|형식|`nvarchar(60)`|외부 작업의 형식입니다.|' 파일 분할 '|  
|work_id|`int`|실제 분할의 ID입니다.|0 보다 크거나 같습니다.|  
|input_name|`nvarchar(4000)`|읽을 입력의 이름입니다.|Hadoop을 사용 하는 경우의 파일 이름입니다.|  
|read_location|`bigint`|오프셋 또는 읽기 위치입니다.|읽을 파일의 오프셋입니다.|  
|bytes_processed|`bigint`|이 작업자의 데이터 처리를 위해 할당 된 총 바이트 수입니다. 쿼리에서 반환 되는 총 데이터를 반드시 나타내는 것은 아닙니다. |0 보다 크거나 같습니다.|  
|length|`bigint`|Hadoop의 경우 분할 또는 HDFS 블록의 길이|사용자 정의 가능. 기본값은 64M입니다.|  
|상태|`nvarchar(32)`|작업자의 상태|보류 중, 처리 중, 완료 됨, 실패, 중단 됨|  
|start_time|`datetime`|작업 시작||  
|end_time|`datetime`|작업의 끝||  
|total_elapsed_time|`int`|총 시간 (밀리초)||
|compute_pool_id|`int`|풀에 대 한 고유 식별자입니다.|

## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
