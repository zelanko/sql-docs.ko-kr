---
title: sys. dm_db_rda_schema_update_status (Transact-sql) | Microsoft Docs
description: 데이터베이스의 각 스트레치 사용 테이블에 대 한 원격 데이터 보관에 대 한 각 스키마 업데이트 태스크에 대 한 행을 dm_db_rda_schema_update_status에 포함 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 313eb868a49507b96e31bcd1966165175bf96f0a
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243794"
---
# <a name="stretch-database---sysdm_db_rda_schema_update_status"></a>Stretch Database dm_db_rda_schema_update_status
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  현재 데이터베이스의 각 스트레치 사용 테이블에 대 한 원격 데이터 보관에 대 한 각 스키마 업데이트 태스크에 대해 하나의 행을 포함 합니다. 태스크는 작업 id로 식별 됩니다.  
  
 **dm_db_rda_schema_update_status** 은 현재 데이터베이스 컨텍스트로 범위가 지정 됩니다. 스키마 업데이트 상태를 보려는 스트레치 사용 테이블의 데이터베이스 컨텍스트에 있는지 확인 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|원격 데이터 보관 스키마가 업데이트 되 고 있는 로컬 스트레치 사용 테이블의 ID입니다.|  
|**database_id**|**int**|로컬 스트레치 사용 테이블을 포함 하는 데이터베이스의 ID입니다.|  
|**task_id**|**bigint**|원격 데이터 보관 스키마 업데이트 태스크의 ID입니다.|  
|**task_type**|**int**|원격 데이터 보관 스키마 업데이트 태스크의 유형입니다.|  
|**task_type_desc**|**nvarchar**|원격 데이터 보관 스키마 업데이트 태스크의 유형에 대 한 설명입니다.|  
|**task_state**|**int**|원격 데이터 보관 스키마 업데이트 태스크의 상태입니다.|  
|**task_state_des**|**nvarchar**|원격 데이터 보관 스키마 업데이트 태스크의 상태에 대 한 설명입니다.|  
|**start_time_utc**|**datetime**|원격 데이터 보관 스키마 업데이트가 시작 된 UTC 시간입니다.|  
|**end_time_utc**|**datetime**|원격 데이터 보관 스키마 업데이트가 완료 된 UTC 시간입니다.|  
|**error_number**|**int**|원격 데이터 보관 스키마 업데이트가 실패할 경우 발생 한 오류의 오류 번호입니다. 그렇지 않으면 null입니다.|  
|**error_severity**|**int**|원격 데이터 보관 스키마 업데이트가 실패 하는 경우 발생 한 오류의 심각도입니다. 그렇지 않으면 null입니다.|  
|**error_state**|**int**|원격 데이터 보관 스키마 업데이트가 실패 하는 경우 발생 한 오류의 상태입니다. 그렇지 않으면 null입니다. Error_state은 오류가 발생 한 조건 또는 위치를 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
