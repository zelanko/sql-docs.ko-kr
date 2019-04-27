---
title: '5단원: (선택 사항) TDE를 사용 하 여 데이터베이스 암호화 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0850fb7b6be85f8052781ca70f97477d5cb3e403
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743309"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>5단원: (선택 사항) TDE를 사용하여 데이터베이스 암호화
  선택적 단계로, 새로 만든 데이터베이스를 암호화할 수 있습니다. TDE(투명한 데이터 암호화)를 통해 데이터 및 로그 파일의 실시간 I/O 암호화 및 암호 해독을 수행합니다. 이러한 종류의 암호화에서는 DEK(데이터베이스 암호화 키)를 사용하며 이 키는 복구하는 동안 사용할 수 있도록 데이터베이스 부트 레코드에 저장됩니다. 자세한 내용은 [투명 한 데이터 암호화 &#40;TDE&#41; ](security/encryption/transparent-data-encryption.md) 하 고 [다른 SQL Server로 TDE 보호 데이터베이스 이동](security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
 이 단원에서는 다음 단계를 이미 완료했다고 가정합니다.  
  
-   Microsoft Azure Storage 계정이 있습니다.  
  
-   Microsoft Azure Storage 계정에서 컨테이너를 만들었습니다.  
  
-   읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들었습니다. SAS 키도 생성했습니다.  
  
-   원본 컴퓨터에서 SQL Server 자격 증명을 만들었습니다.  
  
-   4단원에서 설명한 단계를 수행하여 데이터베이스를 만들었습니다.  
  
 데이터베이스를 암호화하려면 다음 단계를 수행합니다.  
  
1.  원본 컴퓨터의 쿼리 창에서 다음 문을 수정하여 실행합니다.  
  
    ```  
  
    -- Create a master key and a server certificate   
    USE master   
    GO   
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01';   
    GO   
    CREATE CERTIFICATE MySQLCert WITH SUBJECT = 'SQL - Azure Storage Certification'   
    GO   
    -- Create a backup of the server certificate in the master database.   
    -- Store TDS certificates in the source machine locally.   
    BACKUP CERTIFICATE MySQLCert   
    TO FILE = 'C:\certs\MySQLCert.CER'   
    WITH PRIVATE KEY   
    (   
    FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
    ENCRYPTION BY PASSWORD = 'MySQLKey01'   
    );  
  
    ```  
  
2.  다음 단계를 수행하여 원본 컴퓨터에서 새 데이터베이스를 암호화합니다.  
  
    ```  
  
    -- Switch to the new database.   
    -- Create a database encryption key, that is protected by the server certificate in the master database.    
    -- Alter the new database to encrypt the database using TDE.   
    USE TestDB1;   
    GO   
    -- Encrypt your database   
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE MySQLCert   
    GO   
  
    ALTER DATABASE TestDB1   
    SET ENCRYPTION ON   
    GO  
  
    ```  
  
 데이터베이스의 암호화 상태와 연결된 데이터베이스 암호화 키를 알아보려면 다음 문을 실행합니다.  
  
```  
  
SELECT * FROM sys.dm_database_encryption_keys;   
GO  
  
```  
  
 이 단원에서 사용 된 자세한 내용은 TRANSACT-SQL 문을 참조 하세요 [CREATE DATABASE &#40;SQL Server TRANSACT-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)하십시오 [ALTER DATABASE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql), [CREATE MASTER KEY &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)에 [CREATE CERTIFICATE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql), 및 [sys.dm_database_ encryption_keys &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)합니다.  
  
 **다음 단원:**  
  
 [6단원: 원본에서 데이터베이스를 마이그레이션할 컴퓨터 온-프레미스를 대상 컴퓨터에 Windows Azure](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
