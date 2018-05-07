---
title: backupfilegroup (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backupfilegroup_TSQL
- backupfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], backupfilegroup system table
- backupfilegroup system table
ms.assetid: d26e8fbe-f5c5-4e10-b2bd-0d8e16ea21f9
caps.latest.revision: 53
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 040e55c50c91ed40b7e43bfc71d8ea5fbca0273c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  백업 당시 데이터베이스의 각 파일 그룹마다 하나의 행을 포함합니다. **backupfilegroup** 에 저장 되는 **msdb** 데이터베이스입니다.  
  
> [!NOTE]  
>  **backupfilegroup** 테이블 백업 세트가 아닌 데이터베이스의 파일 그룹 구성을 보여 줍니다. 백업 세트에는 파일을 포함할지 여부를 식별 하려면 사용 하 여는 **is_present** 의 열은 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) 테이블입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|이 파일 그룹이 포함된 백업 세트입니다.|  
|**name**|**sysname**|파일 그룹의 이름입니다.|  
|**filegroup_id**|**int**|데이터베이스에서 고유한 파일 그룹의 ID입니다. 에 해당 **data_space_id** 에 **sys.filegroups**합니다.|  
|**filegroup_guid**|**uniqueidentifier**|파일 그룹의 GUID(Globally Unique Identifier)입니다. NULL일 수 있습니다.|  
|**type**|**char(2)**|다음 중 하나의 내용 유형<br /><br /> FG = "행" 파일 그룹<br /><br /> SL = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일 그룹|  
|**type_desc**|**nvarchar(60)**|다음 중 하나의 함수 유형 설명<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP|  
|**is_default**|**bit**|CREATE TABLE 또는 CREATE INDEX에서 파일 그룹을 지정하지 않은 경우 사용되는 기본 파일 그룹입니다.|  
|**is_readonly**|**bit**|1 = 읽기 전용 파일 그룹입니다.|  
|**log_filegroup_guid**|**uniqueidentifier**|NULL일 수 있습니다.|  
  
## <a name="remarks"></a>주의  
  
> [!IMPORTANT]  
>  여러 데이터베이스에 같은 파일 그룹 이름이 나타날 수 있지만 각 파일 그룹에는 고유 GUID가 있습니다. 따라서 **(backup_set_id, filegroup_guid)** 의 파일 그룹을 식별 하는 고유 키가 **backupfilegroup**합니다.  
  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY의 열을 채우는 **backupmediaset** 미디어 세트 헤더의 적절 한 값으로는 테이블입니다.  
  
 이 테이블의 다른 백업 및 기록 테이블에서 행의 수를 줄이려면 실행는 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [백업 및 복원 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
