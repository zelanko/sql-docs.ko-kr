---
title: '빠른 시작: Azure Blob Storage 서비스로 백업 및 복원'
description: '빠른 시작: Azure Blob Storage 서비스에서 백업을 작성하고 복원하는 방법을 알아봅니다. Azure Blob 컨테이너를 만들고 백업을 작성한 후 복원합니다.'
ms.custom: seo-dt-2019
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: quickstart
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
ms.openlocfilehash: 332fde643d285b20c0bd772918f8c9cf1bf578f2
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864960"
---
# <a name="quickstart-sql-backup-and-restore-to-azure-blob-storage-service"></a>빠른 시작: Azure Blob Storage 서비스로 SQL 백업 및 복원
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md](../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
이 빠른 시작은 Azure Blob Storage 서비스에서 백업을 작성하고 복원하는 방법을 이해하도록 도와줍니다.  이 문서에서는 Azure Blob 컨테이너를 만들고 blob 서비스에 백업을 쓴 다음 복원을 수행하는 방법을 설명합니다.
  
## <a name="prerequisites"></a>필수 구성 요소  
이 빠른 시작을 완료하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 개념과 T-SQL 구문에 대해 잘 알고 있어야 합니다.  Azure Storage 계정, SQL Server Management Studio(SSMS), 그리고 SQL Server 또는 Azure SQL Managed Instance를 실행하는 서버에 대한 액세스 권한이 필요합니다. 또한 BACKUP 및 RESTORE 명령을 실행하는 데 사용하는 계정은 **모든 자격 증명 변경** 권한이 있는 **db_backup operator** 데이터베이스 역할에 있어야 합니다. 

- 체험 [Azure 계정](https://azure.microsoft.com/offers/ms-azr-0044p/)을 받습니다.
- [Azure Storage 계정](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal)을 만듭니다.
- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치하거나 [Azure SQL 가상 머신](/azure/sql-database/sql-database-managed-instance-configure-vm) 또는 [지점 및 사이트 간](/azure/sql-database/sql-database-managed-instance-configure-p2s) 연결을 통해 설정된 연결을 사용하여 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance-get-started)를 배포합니다.
- 사용자 계정에 [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) 역할을 할당하고 [모든 자격 증명 변경](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql) 권한을 부여합니다. 

## <a name="create-azure-blob-container"></a>Azure Blob 컨테이너 만들기
컨테이너는 Blob 집합의 그룹화를 제공합니다. 모든 Blob은 컨테이너에 있어야 합니다. 스토리지 계정은 개수에 제한 없이 컨테이너를 포함할 수 있지만 적어도 하나는 포함해야 합니다. 한 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다. 

컨테이너를 만들려면 다음 단계를 수행합니다.

1. Azure Portal을 엽니다. 
1. 스토리지 계정으로 이동합니다. 
1. 스토리지 계정을 선택하고 **Blob Services**로 스크롤합니다.
1. **Blobs**을 선택하고 **+ 컨테이너**를 선택하여 새 컨테이너를 추가합니다. 
1. 컨테이너의 이름을 입력하고 지정한 컨테이너 이름을 기록해 둡니다. 이 정보는 이 빠른 시작의 뒷부분에 나오는 T-SQL 문의 URL(백업 파일 경로)에 사용됩니다. 
1. **확인**을 선택합니다. 
    
    ![새 컨테이너](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)

  > [!NOTE]
  > 공용 컨테이너를 만들도록 선택한 경우에도 SQL Server 백업 및 복원에 스토리지 계정 인증이 필요합니다. 또한 REST API를 사용하여 프로그래밍 방식으로 컨테이너를 만들 수도 있습니다. 자세한 내용은 [컨테이너 만들기](https://docs.microsoft.com/rest/api/storageservices/Create-Container)를 참조하세요.

## <a name="create-a-test-database"></a>테스트 데이터베이스 만들기 
이 단계에서는 SSMS(SQL Server Management Studio)를 사용하여 테스트 데이터베이스를 만듭니다. 

1. [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)를 시작하고 SQL Server 인스턴스에 연결합니다.
1. **새 쿼리** 창을 엽니다. 
1. 다음 T-SQL(Transact-SQL) 코드를 실행하여 테스트 데이터베이스를 만듭니다. **개체 탐색기**에서 **데이터베이스** 노드를 새로 고쳐 새 데이터베이스를 확인합니다. SQL Managed Instance에서 새로 만든 데이터베이스는 자동으로 TDE를 사용하도록 설정되므로 계속하려면 사용하지 않도록 설정해야 합니다. 

```sql
USE [master]
GO

-- Create database
CREATE DATABASE [SQLTestDB]
GO

-- Create table in database
USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO

-- Populate table 
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

-- Disable TDE for newly-created databases on SQL Managed Instance 
USE [SQLTestDB];
GO
ALTER DATABASE [SQLTestDB] SET ENCRYPTION OFF;
GO
```

## <a name="create-credential"></a>자격 증명 만들기

다음 단계를 따라 SQL Server Management Studio의 GUI를 사용하여 자격 증명을 만듭니다. 또는 [프로그래밍 방식](tutorial-use-azure-blob-storage-service-with-sql-server-2016.md#2---create-a-sql-server-credential-using-a-shared-access-signature)으로 자격 증명을 만들 수 있습니다. 

1. [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)의 **개체 탐색기**에서 **데이터베이스** 노드를 확장합니다.
1. 새 `SQLTestDB` 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업**을 가리킨 다음 **백업...** 을 선택하여 **데이터베이스 백업** 마법사를 시작합니다. 
1. **백업할 위치** 대상 드롭다운에서 **URL**을 선택하고 **추가**를 선택하여 **백업 대상 선택** 대화 상자를 시작합니다. 

   ![URL로 백업](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/back-up-to-url.png)

1. **백업 대상 선택** 대화 상자에서 **새 컨테이너**를 선택하여 **Microsoft 구독에 연결** 창을 시작합니다. 

   ![백업 대상](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-backup-destination.png)

1. **로그인...** 을 선택하고 로그인 프로세스를 진행하여 Azure Portal에 로그인합니다. 
1. 드롭다운에서 **구독**을 선택합니다. 
1. 드롭다운 목록에서 **스토리지 계정**을 선택합니다. 
1. 드롭다운에서 이전에 만든 컨테이너를 선택합니다. 
1. **자격 증명 만들기**를 선택하여 *SAS(공유 액세스 서명)* 를 생성합니다.  **복원에 필요하므로 이 값을 저장합니다.**

   ![자격 증명 만들기](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/create-credential.png)

1. **확인**을 클릭하여 **Microsoft 구독에 연결** 창을 닫습니다. 그러면 **백업 대상 선택** 대화 상자에서 *Azure Storage 컨테이너* 값이 채워집니다. **확인**을 선택하여 선택된 스토리지 컨테이너를 선택하고 대화 상자를 닫습니다. 
1. 이 시점에서 다음 섹션의 4단계로 건너뛰고 데이터베이스 백업을 수행하거나, Transact-SQL을 사용하여 데이터베이스를 백업하려면 **데이터베이스 백업** 마법사를 닫을 수 있습니다. 


## <a name="back-up-database"></a>데이터베이스 백업
이 단계에서는 SQL Server Management Studio의 GUI 또는 T-SQL(Transact-SQL)을 사용하여 Azure Blob Storage 계정에 `SQLTestDB` 데이터베이스를 백업합니다. 

# <a name="ssms"></a>[SSMS](#tab/SSMS)

1. **데이터베이스 백업** 마법사가 아직 열려 있지 않은 경우 [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)의 **개체 탐색기**에서 **데이터베이스** 노드를 확장합니다.
1. 새 `SQLTestDB` 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업**을 가리킨 다음 **백업...** 을 선택하여 **데이터베이스 백업** 마법사를 시작합니다. 
1. **백업할 위치** 드롭다운에서 **URL**을 선택하고 **추가**를 선택하여 **백업 대상 선택** 대화 상자를 시작합니다. 

   ![URL로 백업](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/back-up-to-url.png)

1. **Azure Storage 컨테이너** 드롭다운에서 이전 단계에서 만든 컨테이너를 선택합니다. 

   ![Azure 스토리지 컨테이너](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/azure-storage-container.png)

1. **데이터베이스 백업** 마법사에서 **확인**을 선택하여 데이터베이스를 백업합니다. 
1. 데이터베이스가 성공적으로 백업되면 **확인**을 선택하여 모든 백업 관련 창을 닫습니다. 

   > [!TIP]
   > **데이터베이스 백업** 마법사의 상단에서 **스크립트**를 선택하여 이 명령의 Transact-SQL을 스크립팅할 수 있습니다. ![스크립트 명령](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/script-backup-command.png)


# <a name="transact-sql"></a>[Transact-SQL](#tab/tsql)

다음 명령을 실행하여 Transact-SQL로 데이터베이스를 백업합니다. 


```sql
USE [master]

BACKUP DATABASE [SQLTestDB] 
TO  URL = N'https://msftutorialstorage.blob.core.windows.net/sql-backup/sqltestdb_backup_2020_01_01_000001.bak' 
WITH  COPY_ONLY, CHECKSUM
GO
```

---

## <a name="delete-database"></a>데이터베이스 삭제
이 단계에서는 복원을 수행하기 전에 데이터베이스를 삭제합니다. 이 단계는 이 자습서의 목적으로만 필요하고 일반 데이터베이스 관리 절차에서 사용될 가능성은 낮습니다. 이 단계를 건너뛸 수는 있지만, 관리되는 인스턴스에서 복원하는 동안 데이터베이스 이름을 변경하거나, 데이터베이스를 온-프레미스로 성공적으로 복원하려면 복원 명령 `WITH REPLACE`를 실행해야 합니다. 

# <a name="ssms"></a>[SSMS](#tab/SSMS)

1. **개체 탐색기**에서 **데이터베이스** 노드를 확장하고 `SQLTestDB` 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 삭제를 선택하여 **개체 삭제** 마법사를 시작합니다. 
1. 관리되는 인스턴스의 경우, **확인**을 선택하여 데이터베이스를 삭제합니다. 온-프레미스의 경우, **기존 연결 닫기** 옆의 확인란을 선택하고 **확인**을 선택하여 데이터베이스를 삭제합니다. 

# <a name="transact-sql"></a>[Transact-SQL](#tab/tsql)

다음 Transact-SQL 명령을 실행하여 데이터베이스를 삭제합니다.

```sql
USE [master]
GO
DROP DATABASE [SQLTestDB]
GO

-- If connections currently exist on-premises, you'll need to set the database into single user mode first
USE [master]
GO
ALTER DATABASE [SQLTestDB] SET  SINGLE_USER WITH ROLLBACK IMMEDIATE
GO
USE [master]
GO
DROP DATABASE [SQLTestDB]
GO
```

---


## <a name="restore-database"></a>대화 상자의 
이 단계에서는 SQL Server Management Studio의 GUI 또는 Transact-SQL을 사용하여 데이터베이스를 복원합니다. 

# <a name="ssms"></a>[SSMS](#tab/SSMS)

1. SQL Server Management Studio의 **개체 탐색기**에서 **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원**을 선택합니다. 
1. **디바이스**를 선택한 다음, 줄임표(...)를 선택하여 디바이스를 선택합니다. 

   ![디바이스 복원 선택](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-restore-device.png)

1. **백업 미디어 유형** 드롭다운에서 **URL**을 선택하고 **추가**를 선택하여 디바이스를 추가합니다. 

   ![백업 디바이스 추가](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/add-backup-device.png)

1. 드롭다운에서 컨테이너를 선택하고 자격 증명을 만들 때 저장한 SAS(공유 액세스 서명)를 붙여넣습니다. 

   ![백업 대상](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/restore-from-container.png)

1. **확인**을 선택하여 백업 파일 위치를 선택합니다. 
1. **컨테이너**를 확장하고 백업 파일이 있는 컨테이너를 선택합니다. 
1. 복원할 백업 파일을 선택하고 **확인**을 선택합니다. 파일이 표시되지 않는 경우 잘못된 SAS 키를 사용한 것일 수 있습니다. 이전과 동일한 단계에 따라 SAS 키를 다시 생성하여 컨테이너에 추가할 수 있습니다. 

   ![파일 복원 선택](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/select-restore-file.png)

1. **확인**을 선택하여 **백업 디바이스 선택** 대화 상자를 닫습니다. 
1. **확인**을 선택하여 데이터베이스를 복원합니다. 

# <a name="transact-sql"></a>[Transact-SQL](#tab/tsql)

Azure Blob Storage에서 온-프레미스 데이터베이스를 복원하려면 다음 Transact-SQL 명령을 사용자 자체 스토리지 계정을 사용하도록 수정하고 새 쿼리 창에서 실행합니다. 

```sql
USE [master]
RESTORE DATABASE [SQLTestDB] FROM 
URL = N'https://msftutorialstorage.blob.core.windows.net/sql-backup/sqltestdb_backup_2020_01_01_000001.bak'
```

---


## <a name="see-also"></a>참고 항목 
다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업에 Azure Blob Storage 서비스를 사용할 때 개념 및 모범 사례를 이해하기 위한 권장 참조 항목입니다.  
  
-   [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [URL에 SQL Server 백업 모범 사례 및 문제 해결](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
