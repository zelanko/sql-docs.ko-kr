---
title: "9단원: 백업 세트 및 파일-스냅숏 백업 관리 | Microsoft 문서"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 766a0846-db15-4346-b814-4049039bcbfc
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2e16cd4312b50b700363be0dc85a67d2740a889
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-9-manage-backup-sets-and-file-snapshot-backups"></a>9단원: 백업 세트 및 파일-스냅숏 백업 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 단원에서는 [sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md) 시스템 저장 프로시저를 사용하여 백업 세트를 삭제합니다. 이 시스템 저장 프로시저는 이 백업 세트와 연결된 각 데이터베이스 파일에서 백업 파일 및 파일 스냅숏을 삭제합니다.  
  
> [!NOTE]  
> Azure Blob 컨테이너에서 백업 파일을 삭제하여 백업 세트를 삭제하려고 하면 백업 파일 자체만 삭제되고 연결된 파일 스냅숏은 유지됩니다. 이 시나리오에서는 [sys.fn_db_backup_file_snapshots&#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) 시스템 함수를 사용하여 분리된 파일 스냅숏의 URL을 확인하고 [sp_delete_backup_file_snapshot&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) 시스템 저장 프로시저를 사용하여 각 분리된 파일 스냅숏을 삭제합니다. 자세한 내용은  [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
파일-스냅숏 백업 세트를 삭제하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  새 쿼리 창을 열고 Azure 가상 컴퓨터에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스(또는 이 컨테이너에 대한 읽기 및 쓰기 권한이 있는 모든 SQL Server 2016 인스턴스)에 연결합니다.  
  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 연결된 파일 스냅숏과 함께 삭제할 로그 백업을 선택합니다. 1단원에서 지정한 컨테이너 및 저장소 계정 이름에 맞게 URL을 수정하고 로그 백업 파일 이름을 제공한 다음 이 스크립트를 실행합니다.  
  
    ```  
  
    sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-9164-20150726012420.bak';  
  
    ```  
  
4.  개체 탐색기에서 Azure Storage에 연결합니다.  
  
5.  컨테이너를 확장하고 1단원에서 만든 컨테이너를 확장한 다음 3단계에서 사용한 백업 파일이 이 컨테이너에 더 이상 표시되지 않는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![로그 백업 blob의 삭제를 보여 주는 Azure 컨테이너](../relational-databases/media/c0070b08-4667-4db5-aaff-987a404ec934.JPG "로그 백업 blob의 삭제를 보여 주는 Azure 컨테이너")  
  
6.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣은 다음 실행하여 두 개의 파일 스냅숏이 삭제되었는지 확인합니다.  
  
    ```  
  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![삭제된 2개 파일 스냅숏을 보여 주는 결과 창](../relational-databases/media/f3891361-dfb6-4f4d-a090-ebfeb977981e.JPG "삭제된 2개 파일 스냅숏을 보여 주는 결과 창")  
  
**자습서의 끝**  
  
## <a name="see-also"></a>참고 항목  
[Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sp_delete_backup&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots&#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
  

