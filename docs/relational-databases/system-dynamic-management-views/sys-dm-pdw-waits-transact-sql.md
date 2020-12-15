---
description: sys.dm_pdw_waits (Transact-sql)
title: sys.dm_pdw_waits (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5130e498-1c77-4ae3-a80b-9aae396494e9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 3a3e3e4754b831b28be323c194f9eef70bd64f9b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477194"
---
# <a name="sysdm_pdw_waits-transact-sql"></a>sys.dm_pdw_waits (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  요청 또는 쿼리를 실행 하는 동안 발생 한 모든 대기 상태에 대 한 정보 (예를 들어, 잠금, 전송 큐 대기 등)를 포함 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|대기 상태와 연결 된 고유 숫자 id입니다.<br /><br /> 이 보기의 키입니다.|시스템의 모든 대기에서 고유 합니다.|  
|session_id|**nvarchar(32)**|대기 상태가 발생 한 세션의 ID입니다.|[Sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)에서 session_id를 참조 하세요.|  
|형식|**nvarchar(255)**|이 항목이 나타내는 대기 유형입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_type|**nvarchar(255)**|대기의 영향을 받는 개체의 형식입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_name|**nvarchar (386)**|대기의 영향을 받은 지정 된 개체의 이름 또는 GUID입니다.||  
|request_id|**nvarchar(32)**|대기 상태가 발생 한 요청의 ID입니다.|[Sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)에서 request_id를 참조 하세요.|  
|request_time|**datetime**|대기 상태가 요청 된 시간입니다.||  
|acquire_time|**datetime**|잠금 또는 리소스를 획득 한 시간입니다.||  
|state|**nvarchar(50)**|대기 상태의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|대기 중인 항목의 우선 순위입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [Transact-sql&#41;sys.dm_pdw_wait_stats &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
  
