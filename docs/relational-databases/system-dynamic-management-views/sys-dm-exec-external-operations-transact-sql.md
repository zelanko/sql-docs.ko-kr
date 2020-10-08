---
description: sys.dm_exec_external_operations (Transact-sql)
title: sys.dm_exec_external_operations (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_OPERATIONS_TSQL
- DM_EXEC_EXTERNAL_OPERATIONS
- SYS.DM_EXEC_EXTERNAL_OPERATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_external_operations management view
- dm_exec_external_operations management view
ms.assetid: d268217a-85b8-4b7f-9cd1-87865eba2be1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa130e88ec3f87c8964153528ffa65d23b798c40
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834413"
---
# <a name="sysdm_exec_external_operations-transact-sql"></a>sys.dm_exec_external_operations (Transact-sql)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  외부 PolyBase 작업에 대 한 정보를 캡처합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|PolyBase 쿼리와 연결 된 고유 쿼리 식별자|[Sys.dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 을 참조 하십시오.|  
|step_index|**int**|쿼리 단계의 인덱스|[Sys.dm_exec_distributed_request_steps &#40;&#41;transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md) step_index를 참조 하세요.|  
|operation_ 형식|**nvarchar(128)**|Hadoop 작업 또는 기타 외부 작업을 설명 합니다.|' 외부 Hadoop 작업 '|  
|operation_ 이름|**nvarchar(4000)**|작업의 상태를 백분율로 나타냅니다 (사용 된 입력의 양).|0-1-계수 100 (완료 됨)|  
|map_ 진행률|**float**|작업 (있는 경우)의 상태를 백분율로 나타냅니다.|0-1-계수 100 (완료 됨)|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
