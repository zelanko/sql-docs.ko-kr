---
title: restorefile (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 82f338a31cf23b6ab151e2dc731f2a15d9f4de66
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881456"
---
# <a name="restorefile-transact-sql"></a>restorefile(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  파일 그룹 이름을 사용하여 간접적으로 복원된 파일을 비롯하여 복원된 각 파일에 대한 행을 포함합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|해당되는 복원 작업을 식별하는 고유 ID입니다. **Restorehistory (restore_history_id)** 를 참조 합니다.|  
|**file_number**|**숫자 (10, 0)**|복원된 파일의 파일 ID입니다. 이 번호는 각 데이터베이스 내에서 고유해야 합니다. NULL일 수 있습니다.<br /><br /> 데이터베이스를 데이터베이스 스냅샷으로 되돌릴 경우 이 값은 전체 복원과 같은 방식으로 채워집니다.|  
|**destination_phys_drive**|**nvarchar(260)**|파일이 복원된 드라이브 또는 파티션입니다. NULL일 수 있습니다.<br /><br /> 데이터베이스를 데이터베이스 스냅샷으로 되돌릴 경우 이 값은 전체 복원과 같은 방식으로 채워집니다.|  
|**destination_phys_name**|**nvarchar(260)**|드라이브 또는 파티션 정보 없이 파일이 복원된 위치에 있는 파일의 이름입니다. NULL일 수 있습니다.<br /><br /> 데이터베이스를 데이터베이스 스냅샷으로 되돌릴 경우 이 값은 전체 복원과 같은 방식으로 채워집니다.|  
  
## <a name="remarks"></a>설명  
 이 테이블의 행 수와 다른 백업 및 기록 테이블의 행 수를 줄이려면 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [restorehistory &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
