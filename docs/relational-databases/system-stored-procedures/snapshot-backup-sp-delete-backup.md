---
title: sp_delete_backup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 49eb0906a9a5af1fec2abfeec3ef58845b605e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67941829"
---
# <a name="sp_delete_backup-transact-sql"></a>sp_delete_backup (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정 된 데이터베이스에서 스냅숏 백업 집합을 구성 하는 모든 스냅숏과 백업 파일을 삭제 합니다. 이 시스템 저장 프로시저는 스냅숏 백업 집합을 관리 하는 유일한 권장 방법입니다. 자세한 내용은 [Azure에서 데이터베이스 파일에 대한 파일-스냅샷 Backup](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>인수  
 *[ @backup_url =] backup_meta_file_url*  
 삭제할 백업의 URL로, 백업 파일 자체를 포함 하 여 지정 된 백업 집합을 구성 하는 모든 스냅숏을 삭제 합니다.  
  
 *[ @db_name =] database_name*  
 삭제할 스냅숏이 포함 된 데이터베이스의 이름입니다. 데이터베이스 이름을 제공 하는 경우 시스템은 제공 된 백업 URL이 지정 된 데이터베이스에 대 한 백업 URL 인지 확인 하 고 [sp_delete_backup_file_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) 를 사용 하 여 각 스냅숏을 삭제 합니다. 데이터베이스 이름을 제공 하지 않으면이 데이터베이스 검사는 수행 되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY DATABASE 권한 또는 지정 된 데이터베이스에 대 한 ALTER 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [fn_db_backup_file_snapshots &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [Transact-sql&#41;sp_delete_backup_file_snapshot &#40;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
