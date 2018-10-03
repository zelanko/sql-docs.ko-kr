---
title: sys.dm_pdw_lock_waits (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2e60f30972eb98e0b02ce38a142d018c37a56768
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630551"
---
# <a name="sysdmpdwlockwaits-transact-sql"></a>sys.dm_pdw_lock_waits (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  잠금에 대 한 대기 중인 요청에 대 한 정보를 보유 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|대기 목록에서 위치 요청입니다.|0부터 시작 서 수입니다. 이 고유 하지 않습니다 모든 대기 항목.|  
|session_id|**nvarchar(32)**|대기 상태에서 발생 한 세션의 ID입니다.|Session_id를 참조 하세요 [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)합니다.|  
|유형|**nvarchar(255)**|이 항목을 나타내는 대기 유형입니다.|가능한 값은 다음과 같습니다.<br /><br /> Shared<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> 단독|  
|object_type|**nvarchar(255)**|대기 영향을 받는 개체의 형식입니다.|가능한 값은 다음과 같습니다.<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar(386)**|이름 또는 영향을 받은 대기 지정된 된 개체의 GUID입니다.|테이블 및 뷰는 세 부분으로 된 이름을 사용 하 여 표시 됩니다.<br /><br /> 인덱스와 통계는 네 부분으로 된 이름으로 표시 됩니다.<br /><br /> 이름, 주체 및 데이터베이스는 문자열 이름입니다.|  
|request_id|**nvarchar(32)**|대기 상태에서 발생 한 요청의 ID입니다.|요청의 ID입니다.<br /><br /> 로드 요청에 대 한 GUID입니다.|  
|request_time|**datetime**|잠금 또는 리소스를 요청한 시간입니다.||  
|acquire_time|**datetime**|잠금 또는 리소스를 획득 하는 시간입니다.||  
|state|**nvarchar(50)**|대기 상태의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|대기 중인 항목의 우선 순위입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
