---
description: backupfilegroup(Transact-SQL)
title: backupfilegroup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2e84ad652e1253a9026d61ec0f0a28b571b699a3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525105"
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  백업 당시 데이터베이스의 각 파일 그룹마다 하나의 행을 포함합니다. **backupfilegroup** 은 **msdb** 데이터베이스에 저장 됩니다.  
  
> [!NOTE]  
>  **Backupfilegroup** 테이블은 백업 집합이 아니라 데이터베이스의 파일 그룹 구성을 보여 줍니다. 파일이 백업 세트에 포함 되어 있는지 여부를 확인 하려면 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) 테이블의 **is_present** 열을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|이 파일 그룹이 포함된 백업 세트입니다.|  
|**name**|**sysname**|파일 그룹의 이름입니다.|  
|**filegroup_id**|**int**|데이터베이스에서 고유한 파일 그룹의 ID입니다. 는 **sys. 파일 그룹**의 **data_space_id** 에 해당 합니다.|  
|**filegroup_guid**|**uniqueidentifier**|파일 그룹의 GUID(Globally Unique Identifier)입니다. NULL일 수 있습니다.|  
|**type**|**char(2)**|다음 중 하나의 내용 유형<br /><br /> FG = "행" 파일 그룹<br /><br /> SL = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일 그룹|  
|**type_desc**|**nvarchar(60)**|다음 중 하나의 함수 유형 설명<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP|  
|**is_default**|**bit**|CREATE TABLE 또는 CREATE INDEX에서 파일 그룹을 지정하지 않은 경우 사용되는 기본 파일 그룹입니다.|  
|**is_readonly**|**bit**|1 = 읽기 전용 파일 그룹입니다.|  
|**log_filegroup_guid**|**uniqueidentifier**|NULL일 수 있습니다.|  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]  
>  여러 데이터베이스에 같은 파일 그룹 이름이 나타날 수 있지만 각 파일 그룹에는 고유 GUID가 있습니다. 따라서 **(backup_set_id, filegroup_guid)** 는 **backupfilegroup**에서 파일 그룹을 식별 하는 고유 키입니다.  
  
 LOADHISTORY를 사용 하는 *backup_device* 에서만 RESTORE verifyonly는 **backupmediaset** 테이블의 열을 미디어 세트 헤더의 적절 한 값으로 채웁니다.  
  
 이 테이블의 행 수와 다른 백업 및 기록 테이블의 행 수를 줄이려면 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 백업 및 복원 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
