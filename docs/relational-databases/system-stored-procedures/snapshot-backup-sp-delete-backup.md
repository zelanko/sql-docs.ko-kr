---
title: sp_delete_backup (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2955570ee99eaa05d9a689ccbe62973af3208d80
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33241011"
---
# <a name="spdeletebackup-transact-sql"></a>sp_delete_backup (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스냅숏 백업 세트 지정된 된 데이터베이스를 구성 하는 백업 파일 및 모든 스냅숏을 삭제 합니다. 이 시스템 저장 프로시저는 스냅숏 백업 집합을 관리 하기 위한 권장 되는 유일한 방법입니다. 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>인수  
 *[ @backup_url =] backup_meta_file_url*  
 지정 된 백업 세트는 백업 파일 자체를 포함 하 여 구성 하는 모든 스냅숏 삭제, 삭제에 대 한 백업의 URL입니다.  
  
 *[ @db_name =] database_name*  
 삭제할 스냅숏을 포함 하는 데이터베이스의 이름입니다. 시스템 확인이 지정된 된 데이터베이스에 대 한 백업 URL 하 고 사용 하 여 백업 URL에서 제공 되는 제공 된 데이터베이스 이름이 표시 되는 경우 [sp_delete_backup_file_snapshot &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) 각 스냅숏을 삭제 하려면. 제공 된 데이터베이스 이름이 없는 경우이 데이터베이스 검사 수행 되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 지정된 된 데이터베이스에 대 한 ALTER 권한이 나 ALTER ANY DATABASE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.fn_db_backup_file_snapshots &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
