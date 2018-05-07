---
title: restorehistory (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72f788cf3248ba87bfa4ded7efed219ef3043cf5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="restorehistory-transact-sql"></a>restorehistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 복원 작업에 대해 하나의 행을 포함합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|각 복원 작업을 식별하는 고유 ID입니다. ID, 즉 기본 키입니다.|  
|**restore_date**|**datetime**|복원 작업의 완료 날짜 및 시간입니다. NULL일 수 있습니다.|  
|**destination_database_name**|**nvarchar(128)**|복원 작업용 대상 데이터베이스의 이름입니다. NULL일 수 있습니다.|  
|**user_name**|**nvarchar(128)**|복원 작업을 수행한 사용자의 이름입니다. NULL일 수 있습니다.|  
|**backup_set_id**|**int**|복원되는 백업 세트를 나타내는 고유 ID입니다. 참조 **backupset (backup_set_id)** 합니다.|  
|**restore_type**|**char(1)**|복원 작업의 유형입니다.<br /><br /> D = 데이터베이스<br /><br /> F = 파일<br /><br /> G = 파일 그룹<br /><br /> I = 차등<br /><br /> L = 로그<br /><br /> V = Verifyonly<br /><br /> NULL일 수 있습니다.|  
|**replace**|**bit**|복원 작업이 REPLACE 옵션을 지정했는지 여부를 나타냅니다.<br /><br /> 1 = 지정됨<br /><br /> 0 = 지정되지 않음<br /><br /> NULL일 수 있습니다.<br /><br /> 데이터베이스가 데이터베이스 스냅숏으로 되돌린 경우 0만 사용합니다.|  
|**recovery**|**bit**|복원 작업이 RECOVERY 또는 NORECOVERY 옵션을 지정했는지 여부를 나타냅니다.<br /><br /> 1 = RECOVERY<br /><br /> NULL일 수 있습니다.<br /><br /> 데이터베이스를 데이터베이스 스냅숏으로 되돌린 경우 1이 유일한 옵션입니다.<br /><br /> 0 = NORECOVERY|  
|**restart**|**bit**|복원 작업이 RESTART 옵션을 지정했는지 여부를 나타냅니다.<br /><br /> 1 = 지정됨<br /><br /> 0 = 지정되지 않음<br /><br /> NULL일 수 있습니다.<br /><br /> 데이터베이스가 데이터베이스 스냅숏으로 되돌린 경우 0만 사용합니다.|  
|**stop_at**|**datetime**|데이터베이스를 복구한 지정 시간입니다. NULL일 수 있습니다.|  
|**device_count**|**tinyint**|복원 작업에 포함된 장치의 수입니다. 이 수는 백업용 미디어 패밀리 수보다 작을 수 있습니다. NULL일 수 있습니다.<br /><br /> 데이터베이스를 데이터베이스 스냅숏으로 되돌리면 항상 1입니다.|  
|**stop_at_mark_name**|**nvarchar(128)**|명명된 표시가 포함된 트랜잭션으로의 복구를 나타냅니다. NULL일 수 있습니다.<br /><br /> 데이터베이스가 데이터베이스 스냅숏으로 되돌린 경우 이 값은 NULL입니다.|  
|**stop_before**|**bit**|명명된 표시가 포함된 트랜잭션이 복구에 포함되었는지 여부를 나타냅니다.<br /><br /> 0 = 표시된 트랜잭션 앞에서 복구가 중단되었습니다.<br /><br /> 1 = 표시된 트랜잭션까지 포함하여 복구되었습니다.<br /><br /> NULL일 수 있습니다.<br /><br /> 데이터베이스가 데이터베이스 스냅숏으로 되돌린 경우 이 값은 NULL입니다.|  
  
## <a name="remarks"></a>주의  
 이 테이블의 다른 백업 및 기록 테이블에서 행의 수를 줄이려면 실행는 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [백업 및 복원 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorefilegroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
