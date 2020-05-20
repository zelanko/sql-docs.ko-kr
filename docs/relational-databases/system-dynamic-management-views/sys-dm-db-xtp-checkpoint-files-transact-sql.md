---
title: sys. dm_db_xtp_checkpoint_files (Transact-sql) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3db08ac05d88bcea9f6b138ab08a48fd61a675fd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830848"
---
# <a name="sysdm_db_xtp_checkpoint_files-transact-sql"></a>sys.dm_db_xtp_checkpoint_files(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  파일 크기, 물리적 위치 및 트랜잭션 ID를 포함하여 검사점 파일에 대한 정보를 표시합니다.  
  
> **참고:** 닫히지 않은 현재 검사점의 경우의 상태 열은 `ys.dm_db_xtp_checkpoint_files` 새 파일에 대해 생성 중입니다. 마지막 검사점 이후 트랜잭션 로그 증가가 충분 하거나 명령을 실행 하는 경우 `CHECKPOINT` ([검사점 &#40;transact-sql&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)) 검사점이 자동으로 닫힙니다.  
  
 메모리 최적화 파일 그룹은 내부적으로 추가 전용 파일을 사용 하 여 메모리 내 테이블에 삽입 된 행과 삭제 된 행을 저장 합니다. 두 가지 유형의 파일이 있으며, 데이터 파일에는 삽입 된 행이 포함 되 고 델타 파일에는 삭제 된 행에 대 한 참조가 포함 됩니다. 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]는 최신 버전과 상당히 다르며 [SQL Server 2014](#bkmk_2014)의 항목에서 더 자세히 설명 합니다.  
  
 자세한 내용은 [메모리 액세스에 최적화 된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)를 참조 하세요.  
  
##  <a name="sssql15-and-later"></a><a name="bkmk_2016"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]이상  
 다음 표에서는부터의 열에 대해 설명 합니다 `sys.dm_db_xtp_checkpoint_files` **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** .  
  
|열 이름|형식|설명|  
|-----------------|----------|-----------------|  
|container_id|**int**|데이터 또는 델타 파일이 속한 컨테이너(sys.database_files에서 FILESTREAM 형식의 파일로 표현됨)의 ID입니다. [Database_files &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)를 사용 하 여 file_id와 조인 합니다.|  
|container_guid|**uniqueidentifier**|루트, 데이터 또는 델타 파일이 속한 컨테이너의 GUID입니다. Database_files 테이블의 file_guid와 조인 합니다.|  
|checkpoint_file_id|**uniqueidentifier**|검사점 파일의 GUID입니다.|  
|relative_file_path|**nvarchar(256)**|매핑되는 컨테이너를 기준으로 하는 파일의 경로입니다.|  
|file_type|**smallint**|-1 (무료)<br /><br /> 데이터 파일의 경우 0입니다.<br /><br /> 델타 파일의 경우 1입니다.<br /><br /> 2 (루트 파일의 경우)<br /><br /> 대량 데이터 파일의 경우 3|  
|file_type_desc|**nvarchar(60)**|FREE-무료로 유지 되는 모든 파일을 할당할 수 있습니다. 사용 가능한 파일의 크기는 시스템의 예상 수요에 따라 달라질 수 있습니다. 최대 크기는 1GB입니다.<br /><br /> 데이터 데이터 파일에는 메모리 최적화 테이블에 삽입 된 행이 포함 됩니다.<br /><br /> 델타 델타 파일은 삭제 된 데이터 파일의 행에 대 한 참조를 포함 합니다.<br /><br /> 루트 루트 파일에는 메모리 최적화 및 고유 하 게 컴파일된 개체에 대 한 시스템 메타 데이터가 포함 됩니다.<br /><br /> 대량 데이터-대량 데이터 파일에는 (n) varchar (max) 및 varbinary (max) 열에 삽입 된 값과 메모리 최적화 테이블에 있는 columnstore 인덱스의 일부인 열 세그먼트가 포함 됩니다.|  
|internal_storage_slot|**int**|내부 스토리지 배열에 있는 파일의 인덱스입니다. ROOT의 경우 NULL이 고, 그렇지 않으면 1입니다.|  
|checkpoint_pair_file_id|**uniqueidentifier**|해당 데이터 또는 델타 파일. ROOT의 경우 NULL입니다.|  
|file_size_in_bytes|**bigint**|디스크에 있는 파일의 크기입니다.|  
|file_size_used_in_bytes|**bigint**|계속 채워지고 있는 검사점 파일 쌍의 경우 다음 검사점 이후 이 열이 업데이트됩니다.|  
|logical_row_count|**bigint**|데이터의 경우 삽입 된 행의 수입니다.<br /><br /> 델타의 경우 drop table의 회계 후 삭제 된 행 수입니다.<br /><br /> Root의 경우 NULL입니다.|  
|state|**smallint**|0-사전 생성<br /><br /> 1-생성 중<br /><br /> 2 - ACTIVE<br /><br /> 3-대상 병합<br /><br /> 8-로그 잘림 대기 중|  
|state_desc|**nvarchar(60)**|미리 만듦-트랜잭션이 실행 될 때 새 파일을 할당 하는 대기를 최소화 하거나 제거 하기 위해 많은 검사점 파일이 미리 할당 됩니다. 이러한 미리 생성 된 파일은 워크 로드의 예상 요구 사항에 따라 크기가 다를 수 있지만 데이터는 포함 되지 않습니다. 이는 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 데이터베이스의 저장소 오버 헤드입니다.<br /><br /> 생성 중-이러한 검사점 파일은 생성 중 이며,이는 데이터베이스에서 생성 된 로그 레코드를 기준으로 채워지고 아직 검사점의 일부가 아니라는 것을 의미 합니다.<br /><br /> 활성-이전에 닫힌 검사점에서 삽입/삭제 된 행을 포함 합니다. 여기에는 데이터베이스를 다시 시작할 때 트랜잭션 로그의 활성 부분을 적용 하기 전에 메모리로 읽어 온 테이블의 내용이 포함 됩니다. 이러한 검사점 파일의 크기는 메모리 최적화 테이블의 메모리 내 크기의 약 2 배입니다 (병합 작업이 트랜잭션 워크 로드를 유지 하는 경우).<br /><br /> Merge TARGET-병합 작업의 대상-이러한 검사점 파일은 병합 정책에 의해 식별 된 원본 파일의 통합 데이터 행을 저장 합니다. 병합이 설치되면 MERGE TARGET이 ACTIVE 상태로 전환됩니다.<br /><br /> 로그 잘림 대기 중-병합이 설치 되 고 병합 대상 CFP가 지 속성 검사점의 일부인 경우 병합 원본 검사점 파일이이 상태로 전환 됩니다. 이 상태의 파일은 메모리 최적화 테이블이 포함 된 데이터베이스의 운영 정확성을 위해 필요 합니다.  예를 들어 이전 시점으로 돌아가기 위해 영구 검사점에서 복구할 수 있습니다.|  
|lower_bound_tsn|**bigint**|파일의 트랜잭션 하한값입니다. 상태가 (1, 3)에 없는 경우 null입니다.|  
|upper_bound_tsn|**bigint**|파일에 있는 트랜잭션의 상한입니다. 상태가 (1, 3)에 없는 경우 null입니다.|  
|begin_checkpoint_id|**bigint**|시작 검사점의 ID입니다.|  
|end_checkpoint_id|**bigint**|최종 검사점의 ID입니다.|  
|last_updated_checkpoint_id|**bigint**|이 파일을 업데이트 한 마지막 검사점의 ID입니다.|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar(60)**|0 => UNENCRTPTED<br /><br /> 1 = 키 1로 암호화 된><br /><br /> 2 = 키 2로 암호화 된>. 활성 파일에 대해서만 유효 합니다.|  
  
##  <a name="sssql14"></a><a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 다음 표에서는의 열에 대해 설명 합니다 `sys.dm_db_xtp_checkpoint_files` **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** .  
  
|열 이름|형식|설명|  
|-----------------|----------|-----------------|  
|container_id|**int**|데이터 또는 델타 파일이 속한 컨테이너(sys.database_files에서 FILESTREAM 형식의 파일로 표현됨)의 ID입니다. [Database_files &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)를 사용 하 여 file_id와 조인 합니다.|  
|container_guid|**uniqueidentifier**|데이터 또는 델타 파일이 속한 컨테이너의 GUID입니다.|  
|checkpoint_file_id|**GUID**|데이터 또는 델타 파일의 ID입니다.|  
|relative_file_path|**nvarchar(256)**|컨테이너 위치에 상대적인 데이터 또는 델타 파일의 경로입니다.|  
|file_type|**tinyint**|데이터 파일의 경우 0이고,<br /><br /> 델타 파일의 경우 1입니다.<br /><br /> 상태 열이 7로 설정된 경우 NULL입니다.|  
|file_type_desc|**nvarchar(60)**|파일의 형식: DATA_FILE, DELTA_FILE, 상태 열이 7로 설정 된 경우 NULL입니다.|  
|internal_storage_slot|**int**|내부 스토리지 배열에 있는 파일의 인덱스입니다. 상태 열이 2 또는 3이 아닌 경우 NULL입니다.|  
|checkpoint_pair_file_id|**uniqueidentifier**|해당하는 데이터 또는 델타 파일입니다.|  
|file_size_in_bytes|**bigint**|사용되는 파일의 크기입니다. 상태 열이 5, 6 또는 7로 설정된 경우 NULL입니다.|  
|file_size_used_in_bytes|**bigint**|사용되는 파일의 사용된 크기입니다. 상태 열이 5, 6 또는 7로 설정된 경우 NULL입니다.<br /><br /> 계속 채워지고 있는 검사점 파일 쌍의 경우 다음 검사점 이후 이 열이 업데이트됩니다.|  
|inserted_row_count|**bigint**|데이터 파일의 행 수입니다.|  
|deleted_row_count|**bigint**|델타 파일의 삭제된 행 수입니다.|  
|drop_table_deleted_row_count|**bigint**|테이블 삭제의 영향을 받는 데이터 파일의 행 수입니다. 상태 열이 1인 경우 데이터 파일에 적용됩니다.<br /><br /> 삭제된 테이블에서 삭제된 행 수를 표시합니다. 삭제된 테이블에서 행의 메모리 가비지 수집이 완료되고 검사점이 확인된 후 drop_table_deleted_row_count 통계가 컴파일됩니다. 테이블 삭제 통계가 이 열에 적용되기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하는 경우 통계가 복구의 일부로 업데이트됩니다. 복구 프로세스는 삭제된 테이블에서 행을 로드하지 않습니다. 삭제된 테이블의 통계는 로드 단계에서 컴파일되고 복구가 완료되면 이 열에서 보고됩니다.|  
|state|**int**|0-사전 생성<br /><br /> 1-생성 중<br /><br /> 2 - ACTIVE<br /><br /> 3-대상 병합<br /><br /> 4-병합 된 원본<br /><br /> 5-BACKUP/HA에 필요<br /><br /> 6-삭제 표시로 전환<br /><br /> 7-삭제 표시|  
|state_desc|**nvarchar(60)**|미리 만듦-트랜잭션이 실행 될 때 새 파일을 할당 하는 대기를 최소화 하거나 제거 하기 위해 CFPs (검사점 파일 쌍) 라고도 하는 작은 데이터 및 델타 파일 쌍 집합이 미리 할당 된 상태로 유지 됩니다. 전체 크기는 128MB의 데이터 파일 크기와 8MB의 델타 파일 크기를 포함하지만 데이터를 포함하지 않습니다. CFP 수는 최소값이 8개인 논리 프로세서 또는 스케줄러의 수(코어당 1개, 최대값 없음)로 계산됩니다. 메모리 최적화 테이블이 있는 데이터베이스의 고정된 스토리지 오버헤드입니다.<br /><br /> 생성 중-마지막 검사점 이후에 새로 삽입 되거나 삭제 될 수 있는 데이터 행을 저장 하는 CFPs 집합에 있습니다.<br /><br /> ACTIVE - 이전의 닫힌 검사점에서 삽입된 행과 삭제된 행이 포함됩니다. 이러한 CFP에는 데이터베이스를 다시 시작할 때 트랜잭션 로그의 활성 부분을 적용하기 전에 필요한 모든 삽입된 행과 삭제된 행이 포함됩니다. 이러한 CFP의 크기는 병합 작업이 트랜잭션 작업과 동시에 이루어지는 경우 메모리 최적화 테이블에 대한 메모리 내 크기의 두 배 정도입니다.<br /><br /> MERGE TARGET-CFP는 병합 정책에 의해 식별 된 CFP의 통합 데이터 행을 저장 합니다. 병합이 설치되면 MERGE TARGET이 ACTIVE 상태로 전환됩니다.<br /><br /> 병합 된 원본-병합 작업이 설치 되 면 원본 CFPs가 병합 된 원본으로 표시 됩니다. 병합 정책 평가기가 여러 병합을 식별할 수 있지만 CFP는 하나의 병합 작업에만 참여할 수 있습니다.<br /><br /> BACKUP/HA에 필요 합니다. 병합이 설치 되 고 병합 대상 CFP가 지 속성 검사점의 일부인 경우 병합 원본 Cfp가이 상태로 전환 됩니다. 이 상태의 CFP는 메모리 최적화 테이블이 포함된 데이터베이스의 정확한 작업을 위해 필요합니다.  예를 들어 이전 시점으로 돌아가기 위해 영구 검사점에서 복구할 수 있습니다. 로그 잘림 지점이 트랜잭션 범위를 벗어나는 경우 가비지 수집에 대해 CFP를 표시할 수 있습니다.<br /><br /> 삭제 표식으로 전환-이러한 CFPs는 메모리 내 OLTP 엔진에서 필요 하지 않으며 가비지 수집 될 수 있습니다. 이 상태는 이러한 CFP가 백그라운드 스레드에서 다음 상태인 TOMBSTONE으로 전환되기를 기다리고 있음을 나타냅니다.<br /><br /> 삭제 표식-이러한 CFPs는 filestream 가비지 수집기에 의해 가비지 수집 될 때까지 대기 합니다. ([sp_filestream_force_garbage_collection &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|파일에 포함된 트랜잭션의 하한입니다. 상태 열이 2, 3 또는 4가 아닌 경우 Null입니다.|  
|upper_bound_tsn|**bigint**|파일에 포함된 트랜잭션의 상한입니다. 상태 열이 2, 3 또는 4가 아닌 경우 Null입니다.|  
|last_backup_page_count|**int**|마지막 백업에서 결정되는 논리 페이지 수입니다. 상태 열이 2, 3, 4 또는 5로 설정된 경우 적용됩니다. 페이지 수를 알 수 없으면 NULL입니다.|  
|delta_watermark_tsn|**int**|이 델타 파일에 쓴 마지막 검사점의 트랜잭션입니다. 델타 파일에 대한 워터마크입니다.|  
|last_checkpoint_recovery_lsn|**nvarchar (23)**|여전히 파일이 필요한 마지막 검사점의 복구 로그 시퀀스 번호입니다.|  
|tombstone_operation_lsn|**nvarchar (23)**|tombstone_operation_lsn이 로그 잘림 로그 시퀀스 번호보다 작으면 파일이 삭제됩니다.|  
|logical_deletion_log_block_id|**bigint**|5 상태에만 적용됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="use-cases"></a>사용 사례  
 다음과 같이 메모리 내 OLTP에 사용 되는 저장소를 예상할 수 있습니다.  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
상태 및 파일 형식별 저장소 사용률에 대 한 분석을 보려면 다음 쿼리를 실행 합니다.
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>참고 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
