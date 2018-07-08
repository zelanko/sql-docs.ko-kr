---
title: sys.dm_db_rda_schema_update_status (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cbd99f97902dbbd3c097b76b1f119f400f97c6f6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420062"
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>-Stretch Database sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 각 스트레치 사용 테이블의 원격 데이터 보관에 대 한 각 스키마 업데이트 작업에 대 한 하나의 행을 포함 합니다. 작업은 해당 작업 id로 식별 됩니다.  
  
 **dm_db_rda_schema_update_status** 범위 현재 데이터베이스 컨텍스트를 지정 합니다. 스트레치 사용 테이블 스키마 업데이트 상태를 보려는 데이터베이스 컨텍스트에서 되는지 확인 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|원격 데이터 보관 스키마 로컬 스트레치 사용 테이블의 ID는 업데이트 중입니다.|  
|**database_id**|**int**|로컬 스트레치 사용 테이블을 포함 하는 데이터베이스의 ID입니다.|  
|**task_id**|**bigint**|원격 데이터 보관 스키마 업데이트 작업의 ID입니다.|  
|**task_type**|**int**|원격 데이터 보관 스키마 업데이트 작업의 형식입니다.|  
|**task_type_desc**|**nvarchar**|원격 데이터 보관 스키마 업데이트 작업의 형식 설명입니다.|  
|**task_state**|**int**|원격 데이터 보관 스키마 업데이트 작업의 상태입니다.|  
|**task_state_des**|**nvarchar**|원격 데이터 보관 스키마 업데이트 작업의 상태 설명입니다.|  
|**start_time_utc**|**datetime**|원격 데이터 보관 스키마 업데이트를 시작 하는 UTC 시간입니다.|  
|**end_time_utc**|**datetime**|UTC에 원격 데이터 보관 스키마 업데이트를 완료 했습니다.|  
|**error_number**|**int**|원격 데이터 보관 스키마 업데이트에 실패 하면 발생 한 오류의 오류 번호 그렇지 않으면 null입니다.|  
|**error_severity**|**int**|원격 데이터 보관 스키마 업데이트에 실패 하면 발생 한 오류의 심각도 그렇지 않으면 null입니다.|  
|**error_state**|**int**|원격 데이터 보관 스키마 업데이트에 실패 하면 발생 한 오류의 상태 그렇지 않으면 null입니다. Error_state는 조건 또는 오류가 발생 하는 위치를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
