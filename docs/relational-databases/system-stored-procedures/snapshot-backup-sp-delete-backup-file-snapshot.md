---
title: sp_delete_backup_file_snapshot (Transact-sql) | Microsoft Docs
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5afe5530-a404-4fa5-af3c-bc7c3ca43ce6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cf376712d51f542f6da5eaa8e89b53779eda0c07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67941832"
---
# <a name="sp_delete_backup_file_snapshot-transact-sql"></a>sp_delete_backup_file_snapshot (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정 된 데이터베이스에서 지정 된 백업 스냅숏을 삭제 합니다. 이 시스템 저장 프로시저를 사용 하 여 **sys. fn_db_backup_file_snapshots** 시스템 함수와 함께 분리 된 백업 스냅숏을 식별 하 고 삭제 합니다. 자세한 내용은 [Azure에서 데이터베이스 파일에 대한 파일-스냅샷 Backup](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N'<database_name>  
    , [ @snapshot_url = ] N'<snapshot_url>  
```  
  
## <a name="arguments"></a>인수  
 *[ @db_name =] database_name*  
 삭제할 스냅숏이 포함 된 데이터베이스의 이름으로, 유니코드 문자열로 제공 됩니다.  
  
 *[ @snapshot_url =] snapshot_url*  
 삭제할 스냅숏의 URL로, 유니코드 문자열로 제공 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY DATABASE 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [fn_db_backup_file_snapshots &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [Transact-sql&#41;sp_delete_backup &#40;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
