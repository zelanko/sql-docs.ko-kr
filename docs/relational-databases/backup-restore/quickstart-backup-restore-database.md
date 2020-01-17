---
title: '빠른 시작: 데이터베이스 백업 및 복원'
titleSuffix: SQL Server
description: 이 빠른 시작에서는 온-프레미스에서 SQL Server 데이터베이스를 백업 및 복원하는 방법을 보여 줍니다.
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: backup-restore
ms.prod_service: backup-restore
ms.assetid: ''
ms.openlocfilehash: 97993d621de9b10d930feb2fc54f53bc83f00293
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258640"
---
# <a name="quickstart-backup-and-restore-a-sql-server-database-on-premises"></a>빠른 시작: 온-프레미스 SQL Server 데이터베이스 백업 및 복원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 새 데이터베이스를 만들고, 간단하게 백업한 다음, 복원합니다. 

자세한 방법은 [전체 데이터베이스 백업 만들기](create-a-full-database-backup-sql-server.md)와 [SSMS를 사용하여 백업 복원](restore-a-database-backup-using-ssms.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항
이 빠른 시작을 완료하려면 다음이 필요합니다. 

- [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads)
- [SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)

## <a name="create-a-test-database"></a>테스트 데이터베이스 만들기 

1. [SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)를 시작하고 SQL Server 인스턴스에 연결합니다.
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
 
## <a name="take-a-backup"></a>백업 만들기
데이터베이스의 백업을 만들려면 다음을 수행합니다. 

1. [SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)를 시작하고 SQL Server 인스턴스에 연결합니다.
1. **개체 탐색기**에서 **데이터베이스** 노드를 확장합니다.  
1. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업** 위에 마우스를 놓은 다음, **백업업...** 을 선택합니다. 
1. **대상** 아래에서 백업 경로가 올바른지 확인합니다. 이를 변경해야 할 경우 **제거**를 선택하여 기존 경로를 제거한 다음, 새 경로를 입력하여 **추가**합니다. 줄임표를 사용하여 특정 파일로 이동할 수 있습니다. 
1. 데이터베이스의 백업을 만들려면 **확인**을 선택합니다. 

![SQL 백업 만들기](media/quickstart-backup-restore-database/backup-db-ssms.png)

또는 다음 Transact-SQL 명령을 실행하여 데이터베이스를 백업할 수 있습니다. 

```sql
BACKUP DATABASE [SQLTestDB] 
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' 
WITH NOFORMAT, NOINIT,  
NAME = N'SQLTestDB-Full Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
GO
```


## <a name="restore-a-backup"></a>백업 복원
데이터베이스를 복원하려면 다음을 수행합니다. 

1. [SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)를 시작하고 SQL Server 인스턴스에 연결합니다.
1. **개체 탐색기**에서 **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭한 다음, **데이터베이스 복원...** 을 선택합니다.

    ![데이터베이스 복원](media/quickstart-backup-restore-database/restore-db-ssms1.png)

1. **디바이스:** 를 선택한 다음, 줄임표(...)를 선택하여 백업 파일을 찾습니다. 
1. **추가**를 선택하고 `.bak` 파일이 있는 위치로 이동합니다. `.bak` 파일을 선택한 다음, **확인**을 선택합니다. 
1. **확인**을 선택하여 **백업 디바이스 선택** 대화 상자를 닫습니다. 
1. 데이터베이스의 백업을 복원하려면 **확인**을 선택합니다. 

    ![데이터베이스 복원](media/quickstart-backup-restore-database/restore-db-ssms2.png)

또는 다음 Transact-SQL 스크립트를 실행하여 데이터베이스를 복원할 수 있습니다.

```sql
USE [master]
RESTORE DATABASE [SQLTestDB] 
FROM DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO
```

### <a name="clean-up-resources"></a>리소스 정리
다음 Transact-SQL 명령을 실행하여 만든 데이터베이스와 MSDB 데이터베이스의 백업 기록을 함께 제거합니다.

```sql
EXEC msdb.dbo.sp_delete_database_backuphistory @database_name = N'SQLTestDB'
GO

USE [master]
DROP DATABASE [SQLTestDB]
GO
```

## <a name="see-more"></a>자세히 보기
[백업 및 복원 개요](back-up-and-restore-of-sql-server-databases.md)
[URL에 백업](sql-server-backup-to-url.md)
[전체 백업 만들기](create-a-full-database-backup-sql-server.md)
[데이터베이스 백업 복원](restore-a-database-backup-using-ssms.md)
