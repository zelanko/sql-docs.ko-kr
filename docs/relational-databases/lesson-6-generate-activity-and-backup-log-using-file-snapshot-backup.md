---
title: '6단원: 파일-스냅숏 백업을 사용하여 작업 및 백업 로그 생성 | Microsoft 문서'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 282f88a0b41749a4e38d73285a794e357155d9d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup"></a>6단원: 파일-스냅숏 백업을 사용하여 작업 및 백업 로그 생성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 단원에서는 AdventureWorks2014 데이터베이스에 작업을 생성하고 파일-스냅숏 백업을 사용하여 정기적으로 트랜잭션 로그 백업을 만듭니다. 파일 스냅숏 백업 사용 방법에 대한 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
AdventureWorks2014 데이터베이스에 작업을 생성하고 파일-스냅숏 백업을 사용하여 정기적으로 트랜잭션 로그 백업을 만들려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  두 개의 새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 각각 연결합니다.  
  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창의 하나에 붙여넣은 다음 실행합니다. 4단계에서 새 행을 추가하기 전에는 Production.Location 테이블에 14개의 행이 있습니다.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
4.  다음 Transact-SQL 스크립트 두 개를 복사하여 두 개의 개별 쿼리 창에 붙여넣습니다. 1단원에서 지정한 컨테이너 및 저장소 계정 이름에 맞게 URL을 수정한 다음 개별 쿼리 창에서 두 스크립트를 동시에 실행합니다. 두 스크립트를 완료하는 데 약 7분 정도 걸립니다.  
  
    ```  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2014.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
    ```  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2014.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2014 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  첫 번째 스크립트의 출력을 검토하여 최종 행 개수가 29,939개인 것을 확인합니다.  
  
    ![행 개수 29,939가 표시됨](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "행 개수 29,939가 표시됨")  
  
6.  두 번째 스크립트의 출력을 검토하여 BACKUP LOG 문을 실행할 때마다 두 개의 새 파일 스냅숏이 생성되는 것을 확인합니다.로그 파일의 파일 스냅숏 하나와 데이터 파일의 파일 스냅숏 하나 등 총 두 개의 파일 스냅숏이 각 데이터베이스 파일마다 생성됩니다. 두 번째 스크립트가 완료되면 각 데이터베이스 파일마다 8개씩, 총 16개의 파일 스냅샷이 있습니다. BACKUP DATABASE 문에서 하나가 생성되고 BACKUP LOG 문을 실행할 때마다 하나가 생성되었습니다.  
  
    ![로그 백업이 수행된 경우 데이터와 로그 파일의 파일 스냅숏을 보여 주는 결과 창](../relational-databases/media/acd213b8-895e-425c-bd72-2bf10e65a5ba.JPG "로그 백업이 수행된 경우 데이터와 로그 파일의 파일 스냅숏을 보여 주는 결과 창")  
  
    ![4개의 파일 스냅숏이 표시됨](../relational-databases/media/e7eff77d-85b9-4e52-abd8-e49952c8118a.JPG "4개의 파일 스냅숏이 표시됨")  
  
    ![총 16개 파일 스냅숏을 보여 주는 결과 창](../relational-databases/media/c3ddff17-a83c-4bf0-a670-a38834f9c922.JPG "총 16개 파일 스냅숏을 보여 주는 결과 창")  
  
7.  개체 탐색기에서 Azure Storage에 연결합니다.  
  
8.  컨테이너를 확장하고, 1단원에서 만든 컨테이너를 확장한 다음 새 백업 파일 7개가 이전 단원의 Blob과 함께 나타나는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![7개 로그 백업 blob을 보여 주는 Azure 컨테이너](../relational-databases/media/cfa5a326-87a2-4202-9a04-38bf577d2d0b.JPG "7개 로그 백업 blob을 보여 주는 Azure 컨테이너")  
  
**다음 단원:**  
  
[7단원: 데이터베이스를 특정 시점으로 복원](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
  
