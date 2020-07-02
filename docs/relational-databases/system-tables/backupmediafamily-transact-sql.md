---
title: backupmediafamily (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be1df53780b7472d613c49d2d105c606a09de8df
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750374"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  각 미디어 패밀리에 대해 한 행을 포함합니다. 미디어 패밀리가 미러된 미디어 세트에 있을 경우 이 미디어 패밀리에는 미디어 세트의 각 미러에 대한 별도의 행이 있습니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|패밀리가 멤버인 미디어 세트를 표시하는 고유한 ID 번호입니다. **Backupmediaset (media_set_id)** 참조|  
|**family_sequence_number**|**tinyint**|미디어 세트에서 해당 미디어 패밀리의 위치입니다.|  
|**media_family_id**|**uniqueidentifier**|미디어 패밀리를 표시하는 고유한 ID 번호입니다. NULL일 수 있습니다.|  
|**media_count**|**int**|미디어 패밀리에서 미디어의 개수입니다. NULL일 수 있습니다.|  
|**logical_device_name**|**nvarchar(128)**|**Sys. backup_devices**에 있는이 백업 장치의 이름입니다. **Backup_devices**에 있는 영구 백업 장치와는 달리 임시 백업 장치인 경우에는 **logical_device_name** 의 값이 NULL입니다.|  
|**physical_device_name**|**nvarchar(260)**|백업 디바이스의 물리적 이름입니다. NULL일 수 있습니다. 이 필드는 백업 및 복원 프로세스 사이에서 공유 됩니다. 원본 백업 대상 경로 또는 원본 복원 원본 경로를 포함할 수 있습니다. 백업 또는 복원이 데이터베이스의 서버에서 먼저 발생 했는지 여부에 따라 달라 집니다. 동일한 백업 파일에서 연속 복원은 복원 시의 위치에 관계 없이 경로를 업데이트 하지 않습니다. 이로 인해 **physical_device_name** 필드를 사용 하 여 사용 된 복원 경로를 확인할 수 없습니다.|  
|**device_type**|**tinyint**|백업 디바이스의 유형입니다.<br /><br /> 2 = 디스크<br /><br /> 5 = 테이프<br /><br /> 7 = 가상 디바이스<br /><br /> 9 = Azure Storage<br /><br /> 105 = 영구 백업 디바이스<br /><br /> NULL일 수 있습니다.<br /><br /> 모든 영구 장치 이름 및 장치 번호는 **sys. backup_devices**에서 찾을 수 있습니다.|  
|**physical_block_size**|**int**|미디어 패밀리를 기록하는 데 사용하는 물리적 블록 크기입니다. NULL일 수 있습니다.|  
|**mirror**|**tinyint**|미러 번호(0-3)입니다.|  
  
## <a name="remarks"></a>설명  
 LOADHISTORY를 사용 하는 *backup_device* 에서만 RESTORE verifyonly는 **backupmediaset** 테이블의 열을 미디어 세트 헤더의 적절 한 값으로 채웁니다.  
  
 이 테이블의 행 수와 다른 백업 및 기록 테이블의 행 수를 줄이려면 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
