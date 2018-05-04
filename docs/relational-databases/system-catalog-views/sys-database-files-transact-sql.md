---
title: sys.database_files (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/19/2016
ms.prod: ''
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_files
- sys.database_files_TSQL
- database_files
- database_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_files catalog view
ms.assetid: 0f5b0aac-c17d-4e99-b8f7-d04efc9edf44
caps.latest.revision: 61
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 47eda96728428cf7fc5cfdb5571808789534fe45
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabasefiles-transact-sql"></a>sys.database_files(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스 자체에 저장되어 있는 각 데이터베이스 파일당 한 개의 행을 포함합니다. 이 뷰는 데이터베이스별 뷰입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**file_id**|**int**|데이터베이스 내 파일의 ID입니다.|  
|**file_guid**|**uniqueidentifier**|파일에 대한 GUID입니다.<br /><br /> NULL = 데이터베이스가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드되었습니다.|  
|**type**|**tinyint**|파일 유형입니다.<br /><br /> 0 = 행([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드되었거나 에서 만들어진 전체 텍스트 카탈로그의 파일을 포함함)<br /><br /> 1 = 로그<br /><br /> 2 = FILESTREAM<br /><br /> 3 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 4 = 전체 텍스트([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전의 전체 텍스트 카탈로그. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드되었거나 에서 생성된 전체 텍스트 카탈로그는 파일 유형 0을 보고함)|  
|**type_desc**|**nvarchar(60)**|파일 유형에 대한 설명입니다.<br /><br /> ROWS([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드되었거나 에서 생성된 전체 텍스트 카탈로그의 파일을 포함함)<br /><br /> LOG<br /><br /> FILESTREAM<br /><br /> FULLTEXT([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전의 전체 텍스트 카탈로그)|  
|**data_space_id**|**int**|값은 0 이상일 수 있습니다. 값 0은 데이터베이스 로그 파일을 나타내고 0보다 큰 값은 이 데이터 파일이 저장되는 파일 그룹의 ID를 나타냅니다.|  
|**name**|**sysname**|데이터베이스에서 파일의 논리적 이름입니다.|  
|**physical_name**|**nvarchar(260)**|운영 체제 파일 이름입니다. 데이터베이스가 AlwaysOn으로 호스트 되는 경우 [읽기 가능한 보조 복제본](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md), **physical_name** 주 복제본 데이터베이스의 파일 위치를 나타냅니다. 읽기 가능한 보조 데이터베이스의 올바른 파일 위치에 대 한 쿼리 [sys.sysaltfiles](../../relational-databases/system-compatibility-views/sys-sysaltfiles-transact-sql.md)합니다.|  
|**상태**|**tinyint**|파일 상태입니다.<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY_PENDING<br /><br /> 4 = SUSPECT<br /><br /> 5 = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT|  
|**state_desc**|**nvarchar(60)**|파일 상태에 대한 설명입니다.<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> OFFLINE<br /><br /> DEFUNCT<br /><br /> 자세한 내용은 [파일 상태](../../relational-databases/databases/file-states.md)를 참조하세요.|  
|**size**|**int**|8KB 페이지 단위로 나타낸 파일의 현재 크기입니다.<br /><br /> 0 = 해당 사항 없음<br /><br /> 데이터베이스 스냅숏의 경우 size는 스냅숏이 파일에 대해 사용할 수 있는 최대 공간을 나타냅니다.<br /><br /> FILESTREAM 파일 그룹 컨테이너 크기는 현재 사용 된 컨테이너의 크기를 반영 합니다.|  
|**max_size**|**int**|8KB 페이지 단위로 나타낸 파일의 최대 크기입니다.<br /><br /> 0 = 증가를 허용하지 않습니다.<br /><br /> -1 = 디스크가 꽉 찰 때까지 파일이 증가합니다.<br /><br /> 268435456 = 로그 파일이 최대 2TB까지 증가합니다.<br /><br /> Max_size는 FILESTREAM 파일 그룹 컨테이너에 대 한 컨테이너의 최대 크기를 반영 합니다.<br /><br /> 참고 무제한 로그 파일 크기와 업그레이드 된 데이터베이스에 로그 파일의 최대 크기에 대 한-1을 보고 합니다.|  
|**growth**|**int**|0 = 파일 크기가 고정되어 증가하지 않습니다.<br /><br /> >0 = 파일이 자동으로 증가합니다.<br /><br /> is_percent_growth = 0인 경우 증분은 8KB 페이지 단위로 표시되며 64KB 단위로 반올림됩니다.<br /><br /> is_percent_growth = 1이면 증분은 정수 백분율로 표시됩니다.|  
|**is_media_read_only**|**bit**|1 = 파일이 읽기 전용 미디어에 있습니다.<br /><br /> 0 = 파일이 읽기/쓰기 미디어에 있습니다.|  
|**is_read_only**|**bit**|1 = 파일이 읽기 전용으로 표시되어 있습니다.<br /><br /> 0 = 파일이 읽기/쓰기로 표시되어 있습니다.|  
|**is_sparse**|**bit**|1 = 스파스 파일입니다.<br /><br /> 0 = 스파스 파일이 아닙니다.<br /><br /> 자세한 내용은 [데이터베이스 스냅숏 스파스 파일의 크기 보기&#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)를 참조하세요.|  
|**is_percent_growth**|**bit**|1 = 파일의 증가 단위가 백분율입니다.<br /><br /> 0 = 페이지 단위의 절대 증가 크기입니다.|  
|**is_name_reserved**|**bit**|1 = 삭제된 파일 이름(name 또는 physical_name)은 다음 로그 백업 후에만 다시 사용이 가능합니다. 데이터베이스에서 파일을 삭제할 때 논리적 이름은 다음 로그 백업까지 예약된 상태로 유지됩니다. 이 열은 전체 복구 모델 및 대량 로그 복구 모델에만 해당됩니다.|  
|**create_lsn**|**numeric(25,0)**|파일이 생성된 시점의 LSN(로그 시퀀스 번호)입니다.|  
|**drop_lsn**|**numeric(25,0)**|파일이 삭제된 시점의 LSN입니다.<br /><br /> 0 = 이 파일 이름을 다시 사용할 수 없습니다.|  
|**read_only_lsn**|**numeric(25,0)**|해당 파일이 포함된 파일 그룹이 읽기/쓰기에서 읽기 전용으로 변경된 시점(가장 최근 변경)의 LSN입니다.|  
|**read_write_lsn**|**numeric(25,0)**|해당 파일이 포함된 파일 그룹이 읽기 전용에서 읽기/쓰기로 변경된 시점(가장 최근 변경)의 LSN입니다.|  
|**differential_base_lsn**|**numeric(25,0)**|차등 백업에 대한 기본 LSN입니다. 이 LSN 이후에 변경된 데이터 익스텐트가 차등 백업에 포함됩니다.|  
|**differential_base_guid**|**uniqueidentifier**|차등 백업의 기반이 되는 기준 백업의 고유 식별자입니다.|  
|**differential_base_time**|**datetime**|differential_base_lsn에 해당하는 시간입니다.|  
|**redo_start_lsn**|**numeric(25,0)**|다음 롤포워드가 시작되어야 하는 시점의 LSN입니다.<br /><br /> state = RESTORING 또는 state = RECOVERY_PENDING이 아니면 NULL입니다.|  
|**redo_start_fork_guid**|**uniqueidentifier**|복구 분기 지점의 고유 식별자입니다. 복원된 다음 로그 백업의 first_fork_guid는 이 값과 일치해야 합니다. 파일의 현재 상태를 나타냅니다.|  
|**redo_target_lsn**|**numeric(25,0)**|이 파일에 대한 온라인 롤포워드를 중지할 수 있는 시점의 LSN입니다.<br /><br /> state = RESTORING 또는 state = RECOVERY_PENDING이 아니면 NULL입니다.|  
|**redo_target_fork_guid**|**uniqueidentifier**|파일을 복구할 수 있는 복구 분기 지점입니다. redo_target_lsn과 쌍을 이룹니다.|  
|**backup_lsn**|**numeric(25,0)**|파일의 가장 최근 데이터 또는 차등 백업의 LSN입니다.|  
  
> [!NOTE]  
>  대형 인덱스를 삭제하거나 다시 작성할 때 또는 대형 테이블을 삭제하거나 자를 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 트랜잭션이 커밋될 때까지 실제 페이지 할당 해제 및 관련 잠금을 연기합니다. 삭제 작업이 지연되어도 할당된 공간이 즉시 해제되지는 않습니다. 따라서 대형 인덱스를 삭제하거나 잘라낸 직후 sys.database_files에서 반환한 값은 실제 사용할 수 있는 디스크 공간과 다를 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  

## <a name="examples"></a>예  
다음 문은 이름, 파일 크기 및 각 데이터베이스 파일에 대 한 빈 공간의 크기를 반환합니다.

```
SELECT name, size/128.0 FileSizeInMB,
size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 
   AS EmptySpaceInMB
FROM sys.database_files;
```
사용 하는 경우 자세한 내용은 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 참조 [Azure SQL 데이터베이스 v 12에서 데이터베이스 크기 결정](https://blogs.msdn.microsoft.com/sqlcat/2016/09/21/determining-database-size-in-azure-sql-database-v12/) SQL 고객 자문 팀 블로그.
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [파일 상태](../../relational-databases/databases/file-states.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)   
 [sys.data_spaces & #40; Transact SQL & #41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
  
