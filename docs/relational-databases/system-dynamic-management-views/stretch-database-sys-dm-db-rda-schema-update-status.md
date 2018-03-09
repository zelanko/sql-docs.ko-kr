---
title: sys.dm_db_rda_schema_update_status (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3889c9985bad47e192937f7ee8c2608be225ed1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>스트레치 데이터베이스-sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 각 스트레치 사용 테이블의 원격 데이터 보관에 대 한 각 스키마 업데이트 작업에 대 한 행을 포함 합니다. 작업은 해당 작업 id로 식별 됩니다.  
  
 **dm_db_rda_schema_update_status** 범위는 현재 데이터베이스 컨텍스트를 지정 합니다. 스트레치 사용 테이블 스키마 업데이트 상태를 확인 하려는 데이터베이스 컨텍스트에서 인지 확인 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|원격 데이터 보관 스키마 로컬 스트레치 사용 테이블의 ID는 업데이트 중입니다.|  
|**database_id**|**int**|로컬 스트레치 사용 테이블을 포함 하는 데이터베이스의 ID입니다.|  
|**task_id**|**bigint**|원격 데이터 보관 스키마 업데이트 작업의 ID입니다.|  
|**task_type**|**int**|원격 데이터 보관 스키마 업데이트 작업의 형식입니다.|  
|**task_type_desc**|**nvarchar**|설명 된 원격 데이터 보관 스키마 업데이트 작업의 형식입니다.|  
|**task_state**|**int**|원격 데이터 보관 스키마 업데이트 작업의 상태입니다.|  
|**task_state_des**|**nvarchar**|원격 데이터 보관 스키마 업데이트 작업의 상태 설명 합니다.|  
|**start_time_utc**|**datetime**|원격 데이터 보관 스키마 업데이트가 시작 UTC 시간입니다.|  
|**end_time_utc**|**datetime**|UTC 시간을 원격 데이터 보관 스키마 업데이트가 완료 되었습니다.|  
|**error_number**|**int**|원격 데이터 보관 스키마 업데이트가 실패 하면;에 발생 한 오류의 오류 번호 그렇지 않으면 null입니다.|  
|**error_severity**|**int**|원격 데이터 보관 스키마 업데이트가 실패 하면;에 발생 한 오류의 심각도 그렇지 않으면 null입니다.|  
|**error_state**|**int**|원격 데이터 보관 스키마 업데이트가 실패 하면;에 발생 한 오류의 상태 그렇지 않으면 null입니다. Error_state는 오류가 발생 한 위치 또는 조건을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
