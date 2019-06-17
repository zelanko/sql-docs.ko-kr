---
title: '9단원: Windows Azure Storage에서 데이터베이스 복원 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 41fbe4cefb6a759befd8b96ded8487ff54b0a1c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090653"
---
# <a name="lesson-9-restore-a-database-from-windows-azure-storage"></a>9단원: Microsoft Azure Storage에서 데이터베이스 복원
  이 단원에서는 Microsoft Azure Storage의 데이터베이스 백업 파일을 온-프레미스나 Microsoft Azure의 가상 머신에 있는 데이터베이스에 복원하는 방법을 배웁니다. 이 단원을 수행하기 위해 4, 5, 6, 7, 8단원을 완료할 필요는 없습니다.  
  
 이 단원에서는 다음 단계를 이미 완료했다고 가정합니다.  
  
-   원본 컴퓨터에서 데이터베이스를 만들었습니다.  
  
-   (.Bak) 데이터베이스의 백업에서에서 만든 Windows Azure Storage를 사용 하 여 합니다 [Windows Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 기능입니다. 이 단계에서는 또 다른 SQL Server 자격 증명을 만들어야 합니다. 이 자격 증명은 저장소 계정 키를 사용합니다.  
  
-   Microsoft Azure Storage 계정이 있습니다.  
  
-   Microsoft Azure Storage 계정에서 컨테이너를 만들었습니다.  
  
-   읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들었습니다. SAS 키도 생성했습니다.  
  
-   컴퓨터에서 Microsoft Azure Storage 통합 기능에 대한 SQL Server 자격 증명을 만들었습니다. 이 자격 증명에는 SAS(공유 액세스 서명) 키가 필요합니다.  
  
 Microsoft Azure Storage에서 데이터베이스를 복원하려면 다음 단계를 수행합니다.  
  
1.  SQL Server Management Studio를 시작합니다. 기본 인스턴스에 연결합니다.  
  
2.  클릭 **새 쿼리** 표준 도구 모음입니다.  
  
3.  다음 전체 스크립트를 복사하여 쿼리 창에 붙여 넣습니다. 필요에 따라 스크립트를 수정 합니다.  
  
     **참고:** `RESTORE` 문을 실행하여 Microsoft Azure Storage의 데이터베이스 백업(.bak)을 다른 컴퓨터의 데이터베이스 인스턴스에 복원합니다.  
  
    ```sql  
  
    USE master   
    GO   
    -- Create a new database to be backed up.   
    CREATE DATABASE TestDbRestoreFrom;   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    SELECT * from dbo.Table1;   
    GO   
    -- Create a credential to be used by SQL Server Backup and Restore with Windows Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Windows Azure Storage.   
    BACKUP DATABASE TestDBRestoreFrom    
    TO URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
          WITH CREDENTIAL = 'BackupCredential'    
         ,COMPRESSION   
         ,STATS = 5;   
    GO    
    -- Create a Shared Access Signature credential   
    CREATE CREDENTIAL [https://teststorageaccnt.blob.core.windows.net/testrestorefrom]   
    WITH IDENTITY='SHARED ACCESS SIGNATURE',   
    SECRET = 'sv=2012-02-12&sr=c&si=policy_resfrom&sig=EhVpzLUXjG4ThAMLmVhrnoiCt8IfmD3BsuYiMawGzxc%3D'   
    GO   
    USE master;   
    GO   
    RESTORE DATABASE TestDBRestoreFrom    
    FROM URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
    WITH    
    CREDENTIAL = 'BackupCredential',    
    REPLACE,   
    MOVE 'TestDBRestoreFrom' TO 'C:\Backup\TestDBRestoreFrom.mdf',     
    MOVE 'TestDBRestoreFrom_log' TO 'C:\Backup\TestDBRestoreFrom_log.ldf';   
    GO  
  
    ```  
  
 **자습서의 끝: Windows Azure Storage 서비스에서 SQL Server 데이터 파일**  
  
  
