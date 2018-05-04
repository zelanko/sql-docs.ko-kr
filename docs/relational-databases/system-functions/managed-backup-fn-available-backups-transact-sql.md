---
title: managed_backup.fn_available_backups (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_available_backups
- smart_admin.fn_available_backups_TSQL
- fn_available_backups_TSQL
- fn_available_backups
dev_langs:
- TSQL
helpviewer_keywords:
- fn_available_backups
- smart_admin.fn_available_backups
ms.assetid: 7aa84474-16e5-49bd-a703-c8d1408ef107
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a9e9a6b608d4380c7836059fd5bbf305a4937d77
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="managedbackupfnavailablebackups-transact-sql"></a>managed_backup.fn_available_backups (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스에 대해 사용 가능한 백업 파일의 행 수가 0, 1 또는 그 이상인 테이블을 반환합니다. 반환된 백업 파일은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]에서 생성된 백업입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.fn_available_backups ([@database_name = ] 'database name')  
```  
  
##  <a name="Arguments"></a> 인수  
 @database_name  
 데이터베이스의 이름입니다. @database_name 은 nvarchar (512).  
  
## <a name="table-returned"></a>반환된 테이블  
 테이블에 (database_guid, backup_start_date 및 first_lsn, backup_type)에 대한 고유 클러스터형 제약 조건이 포함됩니다.   
데이터베이스가 삭제된 다음 다시 생성된 경우에는 모든 데이터베이스에 대한 백업 집합이 반환됩니다. 출력은 각 데이터베이스를 고유하게 식별하는 database_guid 순서로 지정됩니다.   
LSN에 로그 체인이 끊어졌음을 의미하는 간격이 있으면 테이블에 누락된 각 LSN 세그먼트에 대한 특수 행이 포함됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|Backup_path|NVARCHAR(260) COLLATE Latin1_General_CI_AS_KS_WS|백업 파일의 URL입니다.|  
|backup_type|NVARCHAR(6)|데이터베이스 백업의 경우 'DB', 로그 백업의 경우 'LOG'|  
|expiration_date|DATETIME|이 파일이 삭제될 날짜입니다. 지정된 보존 기간 내에 특정 시점으로 데이터베이스를 복구할 수 있는 기능을 기반으로 설정됩니다.|  
|database_guid|UNIQUEIDENTIFIER|지정된 데이터베이스에 대한 GUID 값입니다.  데이터베이스를 고유하게 식별하는 GUID입니다.|  
|first_lsn|NUMERIC(25, 0)|백업 세트에서 첫 번째 또는 가장 오래된 로그 레코드의 로그 시퀀스 번호입니다. NULL일 수 있습니다.|  
|last_lsn|NUMERIC(25, 0)|백업 세트 다음에 오는 로그 레코드의 로그 시퀀스 번호입니다. NULL일 수 있습니다.|  
|backup_start_date|DATETIME|백업 작업이 시작된 날짜와 시간입니다.|  
|backup_finish_date|NVARCHAR(128)|백업 작업이 완료된 날짜와 시간입니다.|  
|machine_name|NVARCHAR(128)|SQL Server 인스턴스가 설치되었고 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 실행 중인 컴퓨터의 이름입니다.|  
|last_recovery_fork_id|UNIQUEIDENTIFIER|복구 분기 끝 지점의 식별 번호입니다.|  
|first_recovery_fork_id|UNIQUEIDENTIFIER|복구 분기 시작 지점의 ID입니다. 데이터 백업의 경우 first_recovery_fork_guid는 last_recovery_fork_guid와 같습니다.|  
|fork_point_lsn|NUMERIC(25, 0)|first_recovery_fork_id가 last_recovery_fork_id와 동일하지 않으면 분기 지점의 로그 시퀀스 번호입니다. 그렇지 않은 경우 이 값은 NULL입니다.|  
|availability_group_guid|UNIQUEIDENTIFIER|데이터베이스가 Always On 데이터베이스를 가용성 그룹의 GUID입니다. 그렇지 않은 경우 이 값은 NULL입니다.|  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패).  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 필요한 **선택** 이 함수에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 'MyDB' 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 통해 백업된 사용 가능한 모든 백업을 보여줍니다.  
  
```  
SELECT *   
FROM managed_backup.fn_available_backups ('MyDB')  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft Azure에 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)   
 [Microsoft Azure에 저장된 백업에서 복원](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
