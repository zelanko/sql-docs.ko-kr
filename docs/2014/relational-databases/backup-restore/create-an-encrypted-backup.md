---
title: 암호화된 백업 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3959e998111d5fa45eee45b3d7de35501f86f794
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531847"
---
# <a name="create-an-encrypted-backup"></a>암호화된 백업 만들기
  이 항목에서는 Transact-SQL을 사용하여 암호화된 백업을 만드는 데 필요한 단계에 대해 설명합니다.  
  
## <a name="backup-to-disk-with-encryption"></a>암호화하여 디스크에 백업  
 **사전 요구 사항:**  
  
-   데이터베이스의 백업을 만드는 데 적합한 공간이 있는 로컬 디스크나 스토리지에 대한 액세스 권한  
  
-   master 데이터베이스의 데이터베이스 마스터 키 및 SQL Server 인스턴스에서 사용할 수 있는 인증서 또는 비대칭 키. 암호화 요구 사항과 사용 권한에 대한 자세한 내용은 [Backup Encryption](backup-encryption.md)를 참조하십시오.  
  
 다음 단계를 사용하여 로컬 디스크에 데이터베이스의 암호화된 백업을 만들 수 있습니다. 이 예에서는 MyTestDB라는 사용자 데이터베이스를 사용합니다.  
  
1.  **Master 데이터베이스의 데이터베이스 마스터 키를 만듭니다.** 데이터베이스에 저장되는 마스터 키의 복사본을 암호화하기 위한 암호를 선택합니다. 데이터베이스 엔진에 연결하고 새 쿼리 창을 시작한 다음 아래의 예를 복사하여 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **백업 인증서 만들기:** master 데이터베이스에 백업 인증서를 만듭니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **데이터베이스 백업:** 사용할 암호화 알고리즘과 인증서를 지정합니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
 EKM에 의해 보호되는 백업을 암호화하는 예제를 보려면 [Azure 키 자격 증명 모음을 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)를 참조하세요.  
  
### <a name="backup-to-windows-azure-storage-with-encryption"></a>암호화하여 Microsoft Azure Storage에 백업  
 **URL에 대한 SQL Server 백업** 옵션을 사용하여 Windows Azure 저장소에 백업을 만드는 경우 암호화 단계는 동일하지만 URL을 대상으로 사용하고 SQL 자격 증명을 사용하여 Windows Azure 저장소에 인증해야 합니다. 구성 하려는 경우 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 암호화 옵션을 사용 하 여 참조 [SQL Server Managed Backup to Windows Azure 설정](enable-sql-server-managed-backup-to-microsoft-azure.md) 고 [가용성그룹에대한SQLServerManagedBackuptoWindowsAzure설정](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md).  
  
 **사전 요구 사항:**  
  
-   Windows 스토리지 계정 및 컨테이너. 자세한 내용은 [1 단원: Windows Azure 저장소 개체 만들기](../../tutorials/lesson-1-create-windows-azure-storage-objects.md)합니다.  
  
-   master 데이터베이스의 데이터베이스 마스터 키 및 SQL Server 인스턴스에 대한 인증서 또는 비대칭 키. 암호화 요구 사항과 사용 권한에 대한 자세한 내용은 [Backup Encryption](backup-encryption.md)를 참조하십시오.  
  
1.  **SQL Server 자격 증명을 만듭니다.** SQL Server 자격 증명을 만들려면 데이터베이스 엔진에 연결, 새 쿼리 창을 열고 하 고 복사 하 고 다음 예제에서는 붙여넣고 클릭 **Execute**합니다.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **데이터베이스 마스터 키를 만듭니다.** 데이터베이스에 저장되는 마스터 키의 복사본을 암호화하기 위한 암호를 선택합니다. 데이터베이스 엔진에 연결하고 새 쿼리 창을 시작한 다음 아래의 예를 복사하여 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **백업 인증서 만들기:** master 데이터베이스에 백업 인증서를 만듭니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **데이터베이스 백업:** 사용할 암호화 알고리즘과 인증서를 지정합니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' - this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  
