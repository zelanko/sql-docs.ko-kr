---
title: "8단원: 로그 백업에서 새 데이터베이스로 복원 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 281259fb737bbc41885a61e62a4fcc83b3001119
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-8-restore-as-new-database-from-log-backup"></a>8단원: 로그 백업에서 새 데이터베이스로 복원
이 단원에서는 파일-스냅숏 트랜잭션 로그 백업에서 AdventureWorks2014 데이터베이스를 새 데이터베이스로 복원합니다.  
  
이 시나리오에서는 비즈니스 분석 및 보고를 위해 다른 가상 컴퓨터의 SQL Server 인스턴스로 복원을 수행합니다. 다른 가상 컴퓨터의 다른 인스턴스로 복원할 경우 이 목적을 위한 큰 전용 가상 컴퓨터에 작업이 오프로드되므로 트랜잭션 시스템의 리소스를 사용할 필요가 없습니다.  
  
트랜잭션 로그 백업에서 파일-스냅숏 백업을 사용한 복원은 매우 빠르며, 기존의 스트리밍 백업보다 훨씬 더 빠릅니다. 기존의 스트리밍 백업의 경우 전체 데이터베이스 백업, 차등 백업 및 일부 또는 전체 트랜잭션 로그 백업(또는 새로운 전체 데이터베이스 백업)을 사용해야 합니다. 그러나 파일-스냅숏 로그 백업의 경우 가장 최근 로그 백업(또는 다른 로그 백업이나 두 로그 백업 시간 사이의 지점으로 특정 시점 복원을 위한 두 개의 인접한 로그 백업)만 있으면 됩니다. 즉, 각 파일-스냅숏 로그 백업이 각 데이터베이스 파일(각 데이터 파일 및 로그 파일)의 파일 스냅숏을 만들기 때문에 하나의 로그 파일-스냅숏 백업 세트만 있으면 됩니다.  
  
파일 스냅숏 백업을 사용하여 트랜잭션 로그 백업에서 새 데이터베이스로 데이터베이스를 복원하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  새 쿼리 창을 열고 Azure 가상 컴퓨터에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
    > [!NOTE]  
    > 이전 단원에 사용한 것과 다른 Azure 가상 컴퓨터인 경우 [2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)의 단계를 수행한 상태여야 합니다. 다른 컨테이너로 복원하려면 새 컨테이너에 대해 [1단원: Azure 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명 만들기](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md) 및 [2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md) 의 단계를 따르세요.  
  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 사용할 로그 백업 파일을 선택합니다. 1단원에서 지정한 컨테이너 및 저장소 계정 이름에 맞게 URL을 수정하고 로그 백업 파일 이름을 제공한 다음 이 스크립트를 실행합니다.  
  
    ```  
  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2014_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE  
  
    ```  
  
4.  출력을 검토하여 복원이 성공했는지 확인합니다.  
  
5.  개체 탐색기에서 Azure Storage에 연결합니다.  
  
6.  컨테이너를 확장하고, 1단원에서 만든 컨테이너를 확장한 다음(필요한 경우 새로 고침) 새 데이터 및 로그 파일이 이전 단원의 Blob과 함께 컨테이너에 나타나는지 확인합니다.  
  
    ![새 데이터베이스에 대한 데이터 및 로그 파일을 보여 주는 Azure 컨테이너](../relational-databases/media/e9705083-86bc-4309-a0bf-92c15f174c0a.JPG "새 데이터베이스에 대한 데이터 및 로그 파일을 보여 주는 Azure 컨테이너")  
  
[9단원: 백업 세트 및 파일-스냅숏 백업 관리](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)  
  
  
  

