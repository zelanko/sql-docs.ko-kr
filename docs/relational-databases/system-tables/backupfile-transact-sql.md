---
title: backupfile (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: adc995b312ea396c8fba84cbb5e5b43d2f3545e4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="backupfile-transact-sql"></a>backupfile(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스의 각 데이터 또는 로그 파일마다 하나의 행을 포함합니다. 이 열은 백업 당시의 파일 구성을 설명합니다. 파일의 백업에 포함 되는지 여부에 따라 결정 됩니다는 **is_present** 열입니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|백업 세트를 포함한 파일의 고유한 ID입니다. 참조 **backupset (backup_set_id)**합니다.|  
|**first_family_number**|**tinyint**|해당 백업 파일을 포함한 첫 번째 미디어의 패밀리 번호입니다. NULL일 수 있습니다.|  
|**first_media_number**|**smallint**|해당 백업 파일을 포함한 첫 번째 미디어의 미디어 번호입니다. NULL일 수 있습니다.|  
|**filegroup_name**|**nvarchar(128)**|백업된 데이터베이스 파일이 포함된 파일 그룹의 이름입니다. NULL일 수 있습니다.|  
|**page_size**|**int**|페이지 크기(바이트)입니다.|  
|**file_number**|**numeric(10,0)**|데이터베이스 내에서 고유한 파일 id 번호 (해당 **sys.database_files**. **file_id**).|  
|**backed_up_page_count**|**numeric(10,0)**|백업된 페이지의 수입니다. NULL일 수 있습니다.|  
|**file_type**|**char(1)**|백업된 파일이며 다음 중 하나입니다.<br /><br /> D = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일<br /><br /> L = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일<br /><br /> F = 전체 텍스트 카탈로그<br /><br /> NULL일 수 있습니다.|  
|**source_file_block_size**|**numeric(10,0)**|백업될 때, 원본 데이터 또는 로그 파일이 있는 장치입니다. NULL일 수 있습니다.|  
|**file_size**|**numeric(20,0)**|백업된 파일의 길이(바이트)입니다. NULL일 수 있습니다.|  
|**logical_name**|**nvarchar(128)**|백업된 파일의 논리적 이름입니다. NULL일 수 있습니다.|  
|**physical_drive**|**nvarchar(260)**|물리적 드라이브 또는 파티션 이름입니다. NULL일 수 있습니다.|  
|**physical_name**|**nvarchar(260)**|물리적(운영 체제) 파일 이름의 남은 부분입니다. NULL일 수 있습니다.|  
|**상태**|**tinyint**|파일 상태이며 다음 중 하나입니다.<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY PENDING<br /><br /> 4 = SUSPECT<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT<br /><br /> 8 = 삭제<br /><br /> 참고: 값 5는 이러한 값은 데이터베이스 상태에 대 한 값을 해당 있도록 건너뜁니다.|  
|**state_desc**|**nvarchar(64)**|파일 상태에 대한 설명이며 다음 중 하나입니다.<br /><br /> ONLINE RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**numeric(25,0)**|파일이 생성된 시점의 로그 시퀀스 번호입니다.|  
|**drop_lsn**|**numeric(25,0)**|파일이 삭제된 시점의 로그 시퀀스 번호입니다. NULL일 수 있습니다.<br /><br /> 파일이 아직 삭제되지 않은 경우 이 값은 NULL입니다.|  
|**file_guid**|**uniqueidentifier**|파일의 고유 식별자입니다.|  
|**read_only_lsn**|**numeric(25,0)**|해당 파일이 포함된 파일 그룹이 읽기/쓰기에서 읽기 전용으로 변경된 시점(가장 최근 변경)의 로그 시퀀스 번호입니다. NULL일 수 있습니다.|  
|**read_write_lsn**|**numeric(25,0)**|해당 파일이 포함된 파일 그룹이 읽기 전용에서 읽기/쓰기로 변경된 시점(가장 최근의 변경)의 로그 시퀀스 번호입니다. NULL일 수 있습니다.|  
|**differential_base_lsn**|**numeric(25,0)**|차등 백업에 대한 기본 LSN입니다. 차등 백업은 데이터 익스텐트는 로그 시퀀스 번호 보다 크거나 같은 포함 **differential_base_lsn**합니다.<br /><br /> 다른 백업 유형의 경우 값은 NULL입니다.|  
|**differential_base_guid**|**uniqueidentifier**|차등 백업에서 파일의 차등 기반을 구성하는 가장 최근 데이터 백업의 고유 식별자입니다. 값이 NULL이면 파일이 차등 백업에 포함되었지만 기반이 생성된 후 추가된 것입니다.<br /><br /> 다른 백업 유형의 경우 값은 NULL입니다.|  
|**backup_size**|**numeric(20,0)**|이 파일의 백업의 크기(바이트)입니다.|  
|**filegroup_guid**|**uniqueidentifier**|파일 그룹의 ID입니다. Backupfilegroup 테이블을 파일 그룹 정보를 찾으려면 **filegroup_guid** 와 **backup_set_id**합니다.|  
|**is_readonly**|**bit**|1 = 파일이 읽기 전용입니다.|  
|**is_present**|**bit**|1 = 파일이 백업 세트에 포함되었습니다.|  
  
## <a name="remarks"></a>주의  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY의 열을 채우는 **backupmediaset** 미디어 세트 헤더의 적절 한 값으로는 테이블입니다.  
  
 이 테이블의 다른 백업 및 기록 테이블에서 행의 수를 줄이려면 실행는 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [백업 및 복원 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset&#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
