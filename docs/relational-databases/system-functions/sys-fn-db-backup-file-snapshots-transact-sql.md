---
title: sys.fn_db_backup_file_snapshots (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7845ef36347d9131ed6991674b4e09b23ee34155
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670437"
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  데이터베이스 파일을 사용 하 여 연결 된 Azure 스냅숏을 반환 합니다. 지정 된 데이터베이스가 없는 경우 또는 데이터베이스 파일이 Microsoft Azure Blob 저장소 서비스에 저장 되지 않은 경우에 아무 행도 반환 됩니다. 와 함께에서이 시스템 함수를 사용 합니다 **sys.sp_delete_backup_file_snapshot** 시스템 저장 프로시저를 식별 하 여 분리 된 백업 스냅숏을 삭제 합니다. 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>인수  
 *Database_name*  
 쿼리 중인 데이터베이스의 이름입니다. NULL 인 경우이 함수는 현재 데이터베이스 범위에서 실행 됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|file_id|**int**|데이터베이스에 대 한 파일 ID입니다. Null을 허용하지 않습니다.|  
|snapshot_time|**nvarchar(260)**|REST API를 그대로 스냅숏의 타임 스탬프를 반환 합니다. 스냅숏이 없습니다 있으면 NULL을 반환 합니다.|  
|snapshot_url|**nvarchar(360)**|파일 스냅숏 전체 URL입니다. 경우 스냅숏이 없으면 NULL을 반환 존재 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_delete_backup_file_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
