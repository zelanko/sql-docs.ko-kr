---
title: '빠른 시작: Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원 | Microsoft 문서'
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dcc749166f7c86575a84f41e12b452275ff3649c
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402983"
---
# <a name="quickstart-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>빠른 시작: Azure Blob Storage Service로 SQL Server 백업 및 복원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 빠른 시작은 Azure Blob Storage 서비스에서 백업을 작성하고 복원하는 방법을 이해하도록 도와줍니다.  이 빠른 시작에서는 Azure Blob 컨테이너, 스토리지 계정에 액세스하기 위한 자격 증명을 만들고, Blob Service에 백업을 작성한 후 간단한 복원을 수행하는 방법을 설명합니다.
  
### <a name="prerequisites"></a>사전 요구 사항  
이 빠른 시작을 완료하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 개념과 T-SQL 구문에 대해 잘 알고 있어야 합니다. 이 빠른 시작을 사용하려면 Azure Storage 계정, SSMS(SQL Server Management Studio), SQL Server를 실행하는 서버에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다. 또한 BACKUP 및 RESTORE 명령을 실행하는 데 사용하는 계정은 **모든 자격 증명 변경** 권한이 있는 **db_backup operator** 데이터베이스 역할에 있어야 합니다. 

- 체험 [Azure 계정](https://azure.microsoft.com/offers/ms-azr-0044p/)을 받습니다.
- [Azure Storage 계정](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal)을 만듭니다.
- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
- 사용자 계정에 [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) 역할을 할당하고 [모든 자격 증명 변경](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql) 권한을 부여합니다. 


## <a name="create-azure-blob-container"></a>Azure Blob 컨테이너 만들기
컨테이너에서는 그룹화된 blob 집합을 제공합니다. 모든 blob는 컨테이너에 있어야 합니다. 계정에는 개수에 제한 없이 컨테이너를 포함할 수 있지만 적어도 하나 이상 포함해야 합니다. 컨테이너에는 개수에 제한 없이 blob를 저장할 수 있습니다. 

컨테이너를 만들려면 다음 단계를 수행합니다.

1. Azure Portal을 엽니다. 
1. 스토리지 계정으로 이동합니다. 
   1. 스토리지 계정을 선택하고 **Blob Services**로 스크롤합니다.
   1. **Blob**을 선택하고 +**컨테이너**를 선택하여 새 컨테이너를 추가합니다. 
   1. 컨테이너의 이름을 입력하고 지정한 컨테이너 이름을 기록해 둡니다. 이 정보는 이 빠른 시작의 뒷부분에 나오는 T-SQL 문의 URL(백업 파일 경로)에 사용됩니다. 
   1. **확인**을 선택합니다. 
    
    ![새 컨테이너](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)


  >[!NOTE]
  >공용 컨테이너를 만들도록 선택한 경우에도 SQL Server 백업 및 복원에 스토리지 계정 인증이 필요합니다. 또한 REST API를 사용하여 프로그래밍 방식으로 컨테이너를 만들 수도 있습니다. 자세한 내용은 [컨테이너 만들기](https://docs.microsoft.com/rest/api/storageservices/Create-Container)를 참조하세요.

## <a name="create-a-test-database"></a>테스트 데이터베이스 만들기 

1. [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)를 시작하고 SQL Server 인스턴스에 연결합니다.
1. **새 쿼리** 창을 엽니다. 
1. 다음 T-SQL(Transact-SQL) 코드를 실행하여 테스트 데이터베이스를 만듭니다. **개체 탐색기**에서 **데이터베이스** 노드를 새로 고쳐 새 데이터베이스를 확인합니다. 

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```


## <a name="create-a-sql-server-credential"></a>SQL Server 자격 증명 만들기
SQL Server 자격 증명은 SQL Server 외부의 리소스에 연결하는 데 필요한 인증 정보를 저장하는 데 사용되는 개체입니다. 여기에서는 SQL Server 백업 및 복원 프로세스에서 자격 증명을 사용하여 Microsoft Azure Blob Storage 서비스의 인증을 받습니다. 자격 증명에는 스토리지 계정 이름과 스토리지 계정 **액세스 키** 값이 저장됩니다. 만든 자격 증명은 BACKUP/RESTORE 문을 실행할 때 WITH CREDENTIAL 옵션에 지정해야 합니다. 자격 증명에 대한 자세한 내용은 [자격 증명](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/credentials-database-engine)을 참조하세요. 

  >[!IMPORTANT]
  >아래에 설명된 SQL Server 자격 증명을 만들기 위한 요구 사항은 SQL Server 백업 프로세스([URL에 대한 SQL Server 백업](backup-restore/sql-server-backup-to-url.md)및 [Microsoft Azure에 대한 SQL Server Managed Backup](backup-restore/sql-server-managed-backup-to-microsoft-azure.md))와 관련되어 있습니다. SQL Server는 Azure Storage에 액세스하여 백업을 쓰거나 읽을 때 스토리지 계정 이름 및 액세스 키 정보를 사용합니다.

### <a name="access-keys"></a>액세스 키
Azure Portal을 열어 둔 상태로, 자격 증명을 만드는 데 필요한 액세스 키를 저장합니다. 

1. Azure Portal의 **스토리지 계정**으로 이동합니다. 
1. **설정**으로 스크롤하고 **액세스 키**를 선택합니다. 
1. 이 빠른 시작의 뒷부분에서 사용하게 되므로 이 키와 연결 문자열을 모두 저장합니다. 

   ![액세스 키](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/access-keys.png)

### <a name="create-a-sql-server-credential"></a>SQL Server 자격 증명 만들기
저장된 액세스 키를 사용하고, 다음 단계에 따라 SQL Server 자격 증명을 만듭니다. 

1. SQL Server Management Studio를 사용하여 SQL Server에 연결합니다. 
1. **SQLTestDB** 데이터베이스를 선택하고 **새 쿼리** 창을 엽니다. 
1. 다음 예제를 복사하여 쿼리 창에 붙여넣고 필요한 대로 수정한 후 실행합니다. 

   ```sql
   CREATE CREDENTIAL mycredential   
   WITH IDENTITY= 'msftutorialstorage', -- this is the name of the storage account you specified when creating a storage account   
   SECRET = '<storage account access key>' -- this should be either the Primary or Secondary Access Key for the storage account 
   ```

1. 자격 증명을 만들기 위한 문을 실행합니다. 

## <a name="back-up-database-to-the-windows-azure-blob-storage-service"></a>Microsoft Azure Blob Storage 서비스로 데이터베이스 백업
이 섹션에서는 T-SQL 문을 사용하여 Microsoft Azure Blob Storage 서비스에 대한 전체 데이터베이스 백업을 수행합니다. 

1. SQL Server Management Studio를 사용하여 SQL Server에 연결합니다. 
1. **SQLTestDB** 데이터베이스를 선택하고 **새 쿼리** 창을 엽니다. 
1. 다음 예제를 복사하여 쿼리 창에 붙여넣고 필요한 대로 수정합니다. 

     ```sql
     BACKUP DATABASE [SQLTestDB] 
     TO URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/SQLTestDB.bak' 
     /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/ 
     WITH CREDENTIAL = 'mycredential';
     /* name of the credential you created in the previous step */ 
     GO
     ```

1. SQLTestDB 데이터베이스를 URL에 백업하는 명령문을 실행합니다. 

 
## <a name="restore-database-from-windows-azure-blob-storage-service"></a>Microsoft Azure Blob Storage 서비스에서 데이터베이스 복원
이 섹션에서는 T-SQL 문을 사용하여 전체 데이터베이스 백업을 복원합니다. 

1. SQL Server Management Studio를 사용하여 SQL Server에 연결합니다. 
1. **새 쿼리** 창을 엽니다. 
1. 다음 예제를 복사하여 쿼리 창에 붙여넣고 필요한 대로 수정합니다. 

 ```sql
 RESTORE DATABASE [SQLTestDB] 
 FROM URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/SQLTestDB.bak' 
 WITH CREDENTIAL = 'mycredential',
 STATS = 5 -- use this to see monitor the progress
 GO
 ``` 

## <a name="see-also"></a>관련 항목: 
다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업에 Azure Blob Storage 서비스를 사용할 때 개념 및 모범 사례를 이해하기 위한 권장 참조 항목입니다.  
  
-   [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
