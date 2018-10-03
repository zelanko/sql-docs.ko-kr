---
title: sp_delete_backup_file_snapshot (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 66099ab0821bcccf399b353207c09b9571130736
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718661"
---
# <a name="spdeletebackupfilesnapshot-transact-sql"></a>sp_delete_backup_file_snapshot (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정된 된 데이터베이스에서 지정한 백업 스냅숏을 삭제합니다. 이 시스템 저장 프로시저와 함께에서 사용 합니다 **sys.fn_db_backup_file_snapshots** 분리 된 백업 스냅숏 시스템 함수를 식별 하 고 삭제 합니다. 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N’<database_name>  
    , [ @snapshot_url = ] N’<snapshot_url>  
```  
  
## <a name="arguments"></a>인수  
 *[ @db_name =] database_name*  
 삭제, 유니코드 문자열로 지정 된 스냅숏이 포함 된 데이터베이스의 이름입니다.  
  
 *[ @snapshot_url =] snapshot_url*  
 스냅숏의 삭제할를 유니코드 문자열로 지정 된 URL입니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY DATABASE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.fn_db_backup_file_snapshots &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
