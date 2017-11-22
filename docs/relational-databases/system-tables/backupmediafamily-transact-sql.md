---
title: backupmediafamily (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e814887bb97d14d165c39ad4a8d634bf84947b1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 미디어 패밀리에 대해 한 행을 포함합니다. 미디어 패밀리가 미러된 미디어 세트에 있을 경우 이 미디어 패밀리에는 미디어 세트의 각 미러에 대한 별도의 행이 있습니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|패밀리가 멤버인 미디어 세트를 표시하는 고유한 ID 번호입니다. 참조 **backupmediaset (media_set_id)**|  
|**family_sequence_number**|**tinyint**|미디어 세트에서 해당 미디어 패밀리의 위치입니다.|  
|**media_family_id**|**uniqueidentifier**|미디어 패밀리를 표시하는 고유한 ID 번호입니다. NULL일 수 있습니다.|  
|**media_count**|**int**|미디어 패밀리에서 미디어의 개수입니다. NULL일 수 있습니다.|  
|**logical_device_name**|**nvarchar (128)**|이 백업 장치의 이름을 **sys.backup_devices.name**합니다. 이 장치가 임시 백업 장치 (에 있는 영구 백업 장치와 반대로 **sys.backup_devices**), 값 **logical_device_name** 은 NULL입니다.|  
|**physical_device_name**|**nvarchar (260)**|백업 장치의 물리적 이름입니다. NULL일 수 있습니다.|  
|**device_type**|**tinyint**|백업 장치의 유형입니다.<br /><br /> 2 = 디스크<br /><br /> 5 = 테이프<br /><br /> 7 = 가상 장치<br /><br /> 105 = 영구 백업 장치<br /><br /> NULL일 수 있습니다.<br /><br /> 모든 영구 장치 이름 및 장치 번호를 확인할 수 있습니다 **sys.backup_devices**합니다.|  
|**physical_block_size**|**int**|미디어 패밀리를 기록하는 데 사용하는 물리적 블록 크기입니다. NULL일 수 있습니다.|  
|**미러**|**tinyint**|미러 번호(0-3)입니다.|  
  
## <a name="remarks"></a>주의  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY의 열을 채우는 **backupmediaset** 미디어 세트 헤더의 적절 한 값으로는 테이블입니다.  
  
 이 테이블의 다른 백업 및 기록 테이블에서 행의 수를 줄이려면 실행는 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [백업 및 복원 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [시스템 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
