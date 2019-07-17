---
title: sys.master_files (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_files
- master_files_TSQL
- sys.master_files_TSQL
- master_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_files catalog view
ms.assetid: 803b22f2-0016-436b-a561-ce6f023d6b6a
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 679a048a40c990c5c86c0c5a24f4f1c53fb9e0b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102387"
---
# <a name="sysmasterfiles-transact-sql"></a>sys.master_files(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  master로 저장된 데이터베이스의 각 파일당 한 개의 행을 포함합니다. 시스템 차원의 단일 뷰입니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|database_id|**int**|이 파일을 적용할 데이터베이스의 ID입니다. masterdatabase_id은 항상 1입니다.|  
|file_id|**int**|데이터베이스 내 파일의 ID입니다. 주 file_id는 항상 1입니다.|  
|file_guid|**uniqueidentifier**|파일의 고유 식별자입니다.<br /><br /> NULL = 데이터베이스가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드되었습니다.|  
|type|**tinyint**|파일 유형입니다.<br /><br /> 0 = 행<br /><br /> 1 = 로그<br /><br /> 2 = FILESTREAM<br /><br /> 3 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 4 = 전체 텍스트([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전의 전체 텍스트 카탈로그. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상으로 업그레이드되었거나 여기서 만들어진 전체 텍스트 카탈로그는 파일 유형 0을 보고함)|  
|type_desc|**nvarchar(60)**|파일 유형에 대한 설명입니다.<br /><br /> ROWS<br /><br /> LOG<br /><br /> FILESTREAM<br /><br /> FULLTEXT([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전의 전체 텍스트 카탈로그)|  
|data_space_id|**int**|이 파일이 속한 데이터 공간의 ID입니다. 데이터 공간은 파일 그룹입니다.<br /><br /> 0 = 로그 파일|  
|name|**sysname**|데이터베이스에서 파일의 논리적 이름입니다.|  
|physical_name|**nvarchar(260)**|운영 체제 파일 이름입니다.|  
|state|**tinyint**|파일 상태입니다.<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY_PENDING<br /><br /> 4 = SUSPECT<br /><br /> 5 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT|  
|state_desc|**nvarchar(60)**|파일 상태에 대한 설명입니다.<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> OFFLINE<br /><br /> DEFUNCT<br /><br /> 자세한 내용은 [파일 상태](../../relational-databases/databases/file-states.md)를 참조하세요.|  
|크기|**int**|8KB 페이지 단위로 나타낸 파일의 현재 크기입니다. 데이터베이스 스냅샷의 경우 size는 스냅샷이 파일에 대해 사용할 수 있는 최대 공간을 나타냅니다.<br /><br /> 참고: 이 필드는 FILESTREAM 컨테이너에 대해 0으로 채워집니다. 쿼리는 *sys.database_files* 카탈로그 뷰를 FILESTREAM 컨테이너의 실제 크기입니다.|  
|max_size|**int**|8KB 페이지 단위로 나타낸 파일의 최대 크기입니다.<br /><br /> 0 = 증가를 허용하지 않습니다.<br /><br /> -1 = 디스크가 꽉 찰 때까지 파일이 증가합니다.<br /><br /> 268435456 = 로그 파일이 최대 2TB까지 증가합니다.<br /><br /> 참고: 무제한 로그 파일 크기를 사용 하 여 업그레이드 된 데이터베이스에 로그 파일의 최대 크기에 대 한-1을 보고 합니다.|  
|증가|**int**|0 = 파일 크기가 고정되어 증가하지 않습니다.<br /><br /> > 0 = 파일이 자동으로 증가 합니다.<br /><br /> is_percent_growth = 0일 경우 증분은 8KB 페이지 단위로 표시되며 64KB 단위로 반올림됩니다.<br /><br /> is_percent_growth = 1이면 증분은 정수 백분율로 표시됩니다.|  
|is_media_read_onlyF|**bit**|1 = 파일이 읽기 전용 미디어에 있습니다.<br /><br /> 0 = 파일이 읽기/쓰기 미디어에 있습니다.|  
|is_read_only|**bit**|1 = 파일이 읽기 전용으로 표시되어 있습니다.<br /><br /> 0 = 파일이 읽기/쓰기로 표시되어 있습니다.|  
|is_sparse|**bit**|1 = 스파스 파일입니다.<br /><br /> 0 = 스파스 파일이 아닙니다.<br /><br /> 자세한 내용은 [데이터베이스 스냅숏 스파스 파일의 크기 보기&#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)를 참조하세요.|  
|is_percent_growth|**bit**|1 = 파일의 증가 단위가 백분율입니다.<br /><br /> 0 = 페이지 단위의 절대 증가 크기입니다.|  
|is_name_reserved|**bit**|1 = 삭제된 파일 이름을 다시 사용할 수 있습니다. 이름(name 또는 physical_name)을 새 파일 이름에 다시 사용하기 전에 로그 백업을 수행해야 합니다.<br /><br /> 0 = 파일 이름을 다시 사용할 수 없습니다.|  
|create_lsn|**numeric(25,0)**|파일이 생성된 시점의 LSN(로그 시퀀스 번호)입니다.|  
|drop_lsn|**numeric(25,0)**|파일이 삭제된 시점의 LSN입니다.|  
|read_only_lsn|**numeric(25,0)**|해당 파일이 포함된 파일 그룹이 읽기/쓰기에서 읽기 전용으로 변경된 시점(가장 최근 변경)의 LSN입니다.|  
|read_write_lsn|**numeric(25,0)**|해당 파일이 포함된 파일 그룹이 읽기 전용에서 읽기/쓰기로 변경된 시점(가장 최근 변경)의 LSN입니다.|  
|differential_base_lsn|**numeric(25,0)**|차등 백업에 대한 기본 LSN입니다. 이 LSN 이후에 변경된 데이터 익스텐트가 차등 백업에 포함됩니다.|  
|differential_base_guid|**uniqueidentifier**|차등 백업의 기반이 되는 기준 백업의 고유 식별자입니다.|  
|differential_base_time|**datetime**|differential_base_lsn에 해당하는 시간입니다.|  
|redo_start_lsn|**numeric(25,0)**|다음 롤포워드가 시작되어야 하는 시점의 LSN입니다.<br /><br /> state = RESTORING 또는 state = RECOVERY_PENDING이 아니면 NULL입니다.|  
|redo_start_fork_guid|**uniqueidentifier**|복구 분기 지점의 고유 식별자입니다. 복원된 다음 로그 백업의 first_fork_guid는 이 값과 일치해야 합니다. 컨테이너의 현재 상태를 나타냅니다.|  
|redo_target_lsn|**numeric(25,0)**|이 파일에 대한 온라인 롤포워드를 중지할 수 있는 시점의 LSN입니다.<br /><br /> state = RESTORING 또는 state = RECOVERY_PENDING이 아니면 NULL입니다.|  
|redo_target_fork_guid|**uniqueidentifier**|컨테이너를 복구할 수 있는 복구 분기 지점입니다. redo_target_lsn과 쌍을 이룹니다.|  
|backup_lsn|**numeric(25,0)**|파일의 가장 최근 데이터 또는 차등 백업의 LSN입니다.|  
|credential_id|**int**|합니다 `credential_id` 에서 `sys.credentials` 파일을 저장 하는 데 사용 합니다. 예를 들어, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 가상 컴퓨터 및 데이터베이스에서 실행 되 고 파일은 Azure blob 저장소에 저장, 자격 증명 저장소 위치에 대 한 액세스 자격 증명으로 구성 됩니다.|  
  
> [!NOTE]  
>  대형 인덱스를 삭제하거나 다시 작성할 때 또는 대형 테이블을 삭제하거나 자를 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 트랜잭션이 커밋될 때까지 실제 페이지 할당 해제 및 관련 잠금을 연기합니다. 삭제 작업이 지연되어도 할당된 공간이 즉시 해제되지는 않습니다. 따라서 큰 개체를 삭제하거나 자른 직후 sys.master_files가 반환한 값은 실제 사용 가능한 디스크 공간과 다를 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 해당 행을 보는 데 필요한 최소 권한은 CREATE DATABASE, ALTER ANY DATABASE 또는 VIEW ANY DEFINITION입니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [파일 상태](../../relational-databases/databases/file-states.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
