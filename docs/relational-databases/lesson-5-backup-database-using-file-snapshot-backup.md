---
title: "5단원: 파일-스냅숏 백업을 사용하여 데이터베이스 백업 | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b5e0888f00f34fc3d85f6727cc98903c66c2239
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-5-backup-database-using-file-snapshot-backup"></a>5단원: 파일-스냅숏 백업을 사용하여 데이터베이스 백업
이 단원에서는 Azure 스냅숏을 사용하여 거의 즉시 백업을 수행하기 위해 파일-스냅숏 백업을 사용하여 Azure 가상 컴퓨터에서 AdventureWorks2014 데이터베이스를 백업합니다. 파일-스냅숏 백업에 대한 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
파일-스냅숏 백업을 사용하여 AdventureWorks2014 데이터베이스를 백업하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  새 쿼리 창을 열고 Azure 가상 컴퓨터에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
3.  다음 TRANSACT-SQL 스크립트를 복사하여 쿼리 창에 붙여넣고 실행합니다. 이 쿼리 창을 닫지 마세요. 5단계에서 이 스크립트를 다시 실행합니다. 이 시스템 저장 프로시저를 사용하면 지정된 데이터베이스를 구성하는 각 파일에 대한 기존 파일 스냅숏 백업을 볼 수 있습니다. 이 데이터베이스에 대한 파일 스냅숏 백업이 없는 것을 확인할 수 있습니다.  
  
    ```  
  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
4.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 1단원에서 지정한 컨테이너 및 저장소 계정 이름에 맞게 URL을 수정한 다음 이 스크립트를 실행합니다. 이 백업이 얼마나 빨리 수행되는지 확인합니다.  
  
    ```  
  
    -- Backup the AdventureWorks2014 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Azure.bak'   
       WITH FILE_SNAPSHOT;  
  
    ```  
  
    ![각 데이터베이스 파일의 파일 스냅숏을 보여 주는 결과 창](../relational-databases/media/2a9320e0-067a-485a-8e0e-636660005e5c.JPG "각 데이터베이스 파일의 파일 스냅숏을 보여 주는 결과 창")  
  
5.  4단계의 스크립트가 성공적으로 실행되었는지 확인한 후 다음 스크립트를 다시 실행합니다. 4단계의 파일-스냅숏 백업 작업은 데이터와 로그 파일 둘 다의 파일-스냅숏을 생성했습니다.  
  
    ```  
  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![2개 스냅숏을 보여 주는 sys.fn_db_backup_file_snapshots 함수의 결과](../relational-databases/media/fca1436e-9607-4432-97ee-f66ac2f2108d.JPG "2개 스냅숏을 보여 주는 sys.fn_db_backup_file_snapshots 함수의 결과")  
  
6.  개체 탐색기에서 Azure 가상 컴퓨터의 SQL Server 2016 인스턴스에 있는 데이터베이스 노드를 확장하고 AdventureWorks2014 데이터베이스가 이 인스턴스로 복원되었는지 확인합니다(필요에 따라 노드 새로 고침).  
  
7.  개체 탐색기에서 Azure Storage에 연결합니다.  
  
8.  컨테이너를 확장하고 1단원에서 만든 컨테이너를 확장한 다음 위 4단계의 AdventureWorks2014_Azure.bak가 3단원의 백업 파일 및 4단원의 데이터베이스 파일과 함께 이 컨테이너에 표시되는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![파일 스냅숏 백업이 Azure 컨테이너에 나타남](../relational-databases/media/181bc970-4af7-4272-a9ae-4bef674f2e02.JPG "파일 스냅숏 백업이 Azure 컨테이너에 나타남")  
  
**다음 단원:**  
  
[6단원: 파일-스냅숏 백업을 사용하여 작업 및 백업 로그 생성](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
## <a name="see-also"></a>참고 항목  
[Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sys.fn_db_backup_file_snapshots&#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
  
  
  
