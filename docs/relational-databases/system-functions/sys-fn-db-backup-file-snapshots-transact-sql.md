---
title: sys. fn_db_backup_file_snapshots (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5159b72cb91cfdcf21129c6216cab4cf0e8d4dea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68120266"
---
# <a name="sysfn_db_backup_file_snapshots-transact-sql"></a>sys. fn_db_backup_file_snapshots (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  데이터베이스 파일에 연결 된 Azure 스냅숏을 반환 합니다. 지정 된 데이터베이스를 찾을 수 없거나 데이터베이스 파일이 Microsoft Azure Blob storage 서비스에 저장 되어 있지 않은 경우에는 행이 반환 되지 않습니다. 이 시스템 함수를 **sp_delete_backup_file_snapshot** 시스템 저장 프로시저와 함께 사용 하 여 분리 된 백업 스냅숏을 식별 하 고 삭제 합니다. 자세한 내용은 [Azure에서 데이터베이스 파일에 대한 파일-스냅샷 Backup](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>인수  
 *Database_name*  
 쿼리 중인 데이터베이스의 이름입니다. NULL 인 경우이 함수는 현재 데이터베이스 범위에서 실행 됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|file_id|**int**|데이터베이스의 파일 ID입니다. Null을 허용하지 않습니다.|  
|snapshot_time|**nvarchar(260)**|REST API에서 반환 하는 스냅숏의 타임 스탬프입니다. 스냅숏이 없으면 NULL을 반환 합니다.|  
|snapshot_url|**nvarchar(360)**|파일 스냅숏의 전체 URL입니다. 스냅숏이 없는 경우 NULL을 반환 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_backup_file_snapshot &#40;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
