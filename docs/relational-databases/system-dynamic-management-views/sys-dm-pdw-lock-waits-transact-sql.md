---
description: sys.dm_pdw_lock_waits (Transact-sql)
title: sys.dm_pdw_lock_waits (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0e3ddfbf5c6bb0aaa06a28091bce99c90bf4beb6
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035356"
---
# <a name="sysdm_pdw_lock_waits-transact-sql"></a>sys.dm_pdw_lock_waits (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  잠금을 대기 중인 요청에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|대기 목록에서 요청에 대 한 위치입니다.|0부터 기반으로 하는 서 수입니다. 이는 모든 대기 항목에서 고유 하지 않습니다.|  
|session_id|**nvarchar(32)**|대기 상태가 발생 한 세션의 ID입니다.|[Sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)에서 session_id를 참조 하세요.|  
|type|**nvarchar(255)**|이 항목이 나타내는 대기 유형입니다.|가능한 값은 다음과 같습니다.<br /><br /> 공유됨<br /><br /> 대 한 sharedupdate<br /><br /> ExclusiveUpdate<br /><br /> 단독|  
|object_type|**nvarchar(255)**|대기의 영향을 받는 개체의 형식입니다.|가능한 값은 다음과 같습니다.<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar (386)**|대기의 영향을 받은 지정 된 개체의 이름 또는 GUID입니다.|테이블과 뷰는 세 부분으로 구성 된 이름으로 표시 됩니다.<br /><br /> 인덱스와 통계는 네 부분으로 구성 된 이름으로 표시 됩니다.<br /><br /> 이름, 보안 주체 및 데이터베이스는 문자열 이름입니다.|  
|request_id|**nvarchar(32)**|대기 상태가 발생 한 요청의 ID입니다.|요청의 ID입니다.<br /><br /> 이는 로드 요청에 대 한 GUID입니다.|  
|request_time|**datetime**|잠금 또는 리소스가 요청 된 시간입니다.||  
|acquire_time|**datetime**|잠금 또는 리소스를 획득 한 시간입니다.||  
|state|**nvarchar(50)**|대기 상태의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|대기 중인 항목의 우선 순위입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
