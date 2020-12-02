---
title: 전체 데이터베이스 백업 만들기 | Microsoft Docs
description: 이 문서에서는 SQL Server에서 SQL Server Management Studio, Transact-SQL 또는 PowerShell을 사용하여 전체 데이터베이스 백업을 만드는 방법을 보여 줍니다.
ms.custom: sqlfreshmay19
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: cawrites
ms.author: chadam
ms.openlocfilehash: e0c103fba0dae4f6e31d976c151b7c01c487f658
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129280"
---
# <a name="create-a-full-database-backup"></a>전체 데이터베이스 백업 만들기

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 PowerShell을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 전체 데이터베이스 백업을 만드는 방법을 설명합니다.

Azure Blob Storage 서비스로의 SQL Server 백업 방법에 대한 자세한 내용은 [Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 및 [URL로 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요.

## <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항

- 명시적 또는 암시적 트랜잭션에서는 `BACKUP` 문을 사용할 수 없습니다.
- 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 만든 백업은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없습니다.

백업 개념과 태스크의 개요를 보고 자세히 살펴보려면 계속하기 전에 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)를 참조하세요.

## <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항

- 데이터베이스가 커짐에 따라 전체 데이터베이스 백업은 마치는 데 시간이 오래 걸리고 스토리지 공간도 더 많이 필요하게 됩니다. 큰 데이터베이스의 경우 일련의 [차등 데이터베이스 백업](../../relational-databases/backup-restore/differential-backups-sql-server.md)으로 전체 데이터베이스 백업 보완을 고려합니다.
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 시스템 저장 프로시저를 사용하여 전체 데이터베이스 백업의 크기를 예측합니다.
- 기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 백업 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.

## <a name="security"></a><a name="Security"></a> 보안

데이터베이스 백업에서 **TRUSTWORTHY** 는 OFF로 설정되어 있습니다. **TRUSTWORTHY** 를 ON으로 설정하는 방법에 대한 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터는 **PASSWORD** 및 **MEDIAPASSWORD** 옵션은 백업을 만드는 데 더 이상 사용되지 않습니다. 암호를 사용하여 만든 백업은 계속 복원할 수 있습니다.

## <a name="permissions"></a><a name="Permissions"></a> 권한

`BACKUP DATABASE` 및 `BACKUP LOG` 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.

 백업 디바이스의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 디바이스를 읽고 쓸 수 있어야 하므로, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 실행에 사용되는 계정에 백업 디바이스에 대한 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 디바이스에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 따라서 백업 디바이스의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 물리적 리소스를 액세스하기 전까지는 발생하지 않습니다.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 백업 작업을 지정할 때 **스크립트** 단추를 클릭하고 스크립트 대상을 선택하여 해당되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 스크립트를 생성할 수 있습니다.

1. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음, **개체 탐색기** 에서 서버 트리를 확장합니다.

1. **데이터베이스** 를 확장하고 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.

1. 백업하려는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크** 를 가리킨 다음 **백업...** 을 클릭합니다.

1. **데이터베이스 백업** 대화 상자에서 선택한 데이터베이스가 드롭다운 목록에 표시됩니다(서버에 있는 다른 데이터베이스로 변경할 수 있음).

1. **백업 유형** 드롭다운 목록에서 원하는 백업 유형을 선택합니다. 기본값은 **Full** 입니다.

   > [!IMPORTANT]
   > 차등 또는 트랜잭션 로그 백업을 수행하려면 1개 이상의 전체 데이터베이스 백업을 수행해야 합니다.
   
1. **백업 구성 요소** 아래에서 **데이터베이스** 를 선택합니다.

1. **대상** 섹션에서 백업 파일의 기본 위치를 검토합니다(../mssql/data 폴더).

   다른 디바이스로 백업하려면 **백업 대상** 드롭다운 목록을 사용하여 선택 항목을 변경합니다. 백업 속도를 높이기 위해 백업 세트를 여러 파일에서 스트라이프하려면 **추가** 를 클릭하여 백업 개체 및/또는 대상을 더 추가합니다.
 
   백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거** 를 클릭합니다. 기존 백업 대상의 내용을 보려면 선택한 다음 **내용** 을 클릭합니다.

1. (옵션) **미디어 옵션** 및 **백업 옵션** 페이지에서 사용 가능한 다른 설정을 검토합니다.

   다양한 백업 옵션에 대한 자세한 정보는 [일반 페이지](back-up-database-general-page.md), [미디어 옵션 페이지](back-up-database-media-options-page.md) 및 [백업 옵션 페이지](back-up-database-backup-options-page.md)를 참조하세요.

1. **확인** 을 클릭하여 백업을 시작합니다.

1. 백업이 성공적으로 완료되면, **확인** 을 클릭하여 SQL Server Management Studio 대화 상자를 닫습니다.

### <a name="additional-information"></a>추가 정보

- 전체 데이터베이스 백업을 만든 후 [차등 데이터베이스 백업](create-a-differential-database-backup-sql-server.md) 또는 [트랜잭션 로그 백업](back-up-a-transaction-log-sql-server.md)을 만들 수 있습니다.

- (옵션) **복사 전용 백업** 확인란을 선택하여 복사 전용 백업을 만들 수 있습니다. *복사 전용 백업* 은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요. **서로 다른** 백업 유형에서는 복사 전용 백업을 사용할 수 없습니다.

- URL에 백업할 경우 **미디어 덮어쓰기** 옵션은 **미디어 옵션** 페이지에서 사용할 수 없습니다.

### <a name="examples"></a>예

다음 예제에서는 다음 Transact-SQL 코드를 사용하여 테스트 데이터베이스를 만듭니다.

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest
   (
      ID INT NOT NULL PRIMARY KEY,
      c1 VARCHAR(100) NOT NULL,
      dt1 DATETIME NOT NULL DEFAULT getdate()
   );
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

#### <a name="a-full-back-up-to-disk-to-default-location"></a>A. 기본 위치로 디스크 전체 백업

이 예제에서는 `SQLTestDB` 데이터베이스가 기본 백업 위치에서 디스크로 백업됩니다.

1. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음, **개체 탐색기** 에서 서버 트리를 확장합니다.

1. **데이터베이스** 를 확장하고 `SQLTestDB`를 마우스 오른쪽 단추로 클릭한 다음 **태스크** 를 가리키고 **백업...** 을 클릭합니다.

1. **확인** 을 클릭합니다.

1. 백업이 성공적으로 완료되면, **확인** 을 클릭하여 SQL Server Management Studio 대화 상자를 닫습니다.

![SQL 백업 만들기](media/quickstart-backup-restore-database/backup-db-ssms.png)

#### <a name="b-full-back-up-to-disk-to-non-default-location"></a>B. 기본이 아닌 위치로 디스크 전체 백업

이 예제에서는 `SQLTestDB` 데이터베이스가 선택한 위치의 디스크로 백업됩니다.

1. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음, **개체 탐색기** 에서 서버 트리를 확장합니다.

1. **데이터베이스** 를 확장하고 `SQLTestDB`를 마우스 오른쪽 단추로 클릭한 다음 **태스크** 를 가리키고 **백업...** 을 클릭합니다.

1. **대상** 섹션의 **일반** 페이지에 있는 **백업할 위치:** 드롭다운 목록에서 **디스크** 를 선택합니다.

1. 모든 기존 백업 파일이 제거될 때까지 **제거** 를 선택합니다.

1. **추가** 를 선택하면 **백업 대상 선택** 대화 상자가 열립니다.

1. **파일 이름** 텍스트 상자에 올바른 경로 및 파일 이름을 입력하고 **.bak** 를 확장명으로 사용하여 이 파일의 분류를 간소화합니다.

1. **확인** 을 클릭한 다음, **확인** 을 다시 클릭하여 백업을 시작합니다.

1. 백업이 성공적으로 완료되면, **확인** 을 클릭하여 SQL Server Management Studio 대화 상자를 닫습니다.

![DB 위치 변경](media/create-a-full-database-backup-sql-server/change-db-location.png)

#### <a name="c-create-an-encrypted-backup"></a>C. 암호화된 백업 만들기

이 예제에서는 `SQLTestDB` 데이터베이스가 기본 백업 위치로 암호화를 사용하여 백업됩니다.

1. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음, **개체 탐색기** 에서 서버 트리를 확장합니다.

1. **데이터베이스**, **시스템 데이터베이스** 를 차례로 확장하고 `master`를 마우스 오른쪽 단추로 클릭한 후 **새 쿼리** 를 클릭하여 `SQLTestDB` 데이터베이스에 연결된 쿼리 창을 엽니다.

1. 다음 명령을 실행하여 `master` 데이터베이스 안에 [**데이터베이스 마스터 키**](../../relational-databases/security/encryption/create-a-database-master-key.md) 및 [**인증서**](../../t-sql/statements/create-certificate-transact-sql.md)를 만듭니다.  

   ```sql
   -- Create the master key
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  

   -- If the master key already exists, open it in the same session that you create the certificate (see next step)
   OPEN MASTER KEY DECRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe'

   -- Create the certificate encrypted by the master key
   CREATE CERTIFICATE MyCertificate
   WITH SUBJECT = 'Backup Cert', EXPIRY_DATE = '20201031';  
   ```

1. **개체 탐색기** 의 **데이터베이스** 노드에서 `SQLTestDB`를 마우스 오른쪽 단추로 클릭한 다음, **작업** 을 가리키고 **백업...** 을 클릭합니다.

1. **미디어 옵션** 페이지의 **미디어 덮어쓰기** 섹션에서 **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기** 를 선택합니다.

1. **백업 옵션** 페이지의 **암호화** 섹션에서 **백업 암호화** 확인란을 선택합니다.

1. 알고리즘 드롭다운 목록에서 **AES 256** 을 선택합니다.

1. **인증서 또는 비대칭 키** 드롭다운 목록에서 `MyCertificate`를 선택합니다.

1. **확인** 을 선택합니다.

![암호화된 백업](media/create-a-full-database-backup-sql-server/encrypted-backup.png)

#### <a name="d-back-up-to-the-azure-blob-storage-service"></a>D. Azure Blob Storage 서비스에 백업

아래 예제에서는 Azure Blob Storage 서비스에 `SQLTestDB`의 전체 데이터베이스 백업을 수행합니다. 이 예제에서는 Blob 컨테이너가 있는 스토리지 계정이 이미 있다고 가정합니다. 이 예제에서는 공유 액세스 서명을 만듭니다. 컨테이너에 기존 공유 액세스 서명이 있으면 이 예제는 실패합니다.

스토리지 계정에 Azure Blob 컨테이너가 없는 경우 계속하기 전에 만듭니다. 자세한 내용은 [범용 스토리지 계정 만들기](/azure/storage/common/storage-quickstart-create-account?tabs=azure-portal) 및 [컨테이너 만들기](/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container)를 참조하세요.

1. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음, **개체 탐색기** 에서 서버 트리를 확장합니다.

1. **데이터베이스** 를 확장하고 `SQLTestDB`를 마우스 오른쪽 단추로 클릭한 다음 **태스크** 를 가리키고 **백업...** 을 클릭합니다.

1. **대상** 섹션의 **일반** 페이지에 있는 **백업할 위치:** 드롭다운 목록에서 **URL** 을 선택합니다.

1. **추가** 를 클릭하면 **백업 대상 선택** 대화 상자가 열립니다.

1. SQL Server Management Studio에서 사용하려는 Azure Storage 컨테이너를 이전에 등록한 경우 해당 컨테이너를 선택합니다. 그렇지 않으면 **새 컨테이너** 를 클릭하여 새 컨테이너를 등록합니다.

1. **Microsoft 구독에 연결** 대화 상자에서 계정에 로그인합니다.

1. **스토리지 계정 선택** 드롭다운 텍스트 상자에서 스토리지 계정을 선택합니다.

1. **Blob 컨테이너 선택** 드롭다운 텍스트 상자에서 Blob 컨테이너를 선택합니다.

1. **공유 액세스 정책 만료** 드롭다운 일정 상자에서 이 예제에서 만든 공유 액세스 정책의 만료 날짜를 선택합니다.

1. **자격 증명 만들기** 를 클릭하여 SQL Server Management Studio에서 공유 액세스 서명 및 자격 증명을 생성합니다.

1. **확인** 을 클릭하여 **Microsoft 구독에 연결** 대화 상자를 닫습니다.

1. **백업 파일** 텍스트 상자에서 백업 파일의 이름을 수정합니다(옵션).

1. **확인** 을 클릭하여 **백업 대상 선택** 대화 상자를 닫습니다.

1. **확인** 을 클릭하여 백업을 시작합니다.

1. 백업이 성공적으로 완료되면, **확인** 을 클릭하여 SQL Server Management Studio 대화 상자를 닫습니다.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용

`BACKUP DATABASE` 문을 실행하여 전체 데이터베이스 백업을 만듭니다. 이때 다음을 지정합니다.

- 백업할 데이터베이스의 이름
- 전체 데이터베이스 백업이 기록되는 백업 디바이스

전체 데이터베이스 백업의 기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 다음과 같습니다.

 BACKUP DATABASE *database* TO *backup_device* [ **,** ...*n* ] [ WITH *with_options* [ **,** ...*o* ] ] ;

|옵션|Description|
|------------|-----------------|
|*database*|백업할 데이터베이스입니다.|
|*backup_device* [ **,** ...*n* ]|백업 작업에 사용할 1-64개의 백업 디바이스 목록을 지정합니다. 물리적 백업 디바이스를 지정하거나, 이미 정의된 경우 해당 논리적 백업 디바이스를 지정할 수 있습니다. 물리적 백업 디바이스를 지정하려면 다음 DISK 또는 TAPE 옵션을 사용합니다.<br /><br /> { DISK &#124; TAPE } **=** _physical\_backup\_device\_name_<br /><br /> 자세한 내용은 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.|
|WITH *with_options* [ **,** ...*o* ]|필요에 따라 *o* 등과 같은 하나 이상의 추가 옵션을 지정합니다. 몇 가지 WITH의 기본 옵션에 대한 자세한 내용은 2단계를 참조하세요.|
|||

필요에 따라 한 개 이상의 **WITH** 옵션을 지정합니다. 몇 가지 기본적인 **WITH** 옵션은 이 페이지에 설명되어 있습니다. 모든 **WITH** 옵션에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.

기본 백업 세트 **WITH** 옵션

- **{ COMPRESSION | NO_COMPRESSION }** : [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상에서만 사용 가능. 이 백업에서 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md) 을 수행하고 서버 수준 기본값을 재정의할지 여부를 지정합니다.
- **ENCRYPTION (ALGORITHM, SERVER CERTIFICATE | ASYMMETRIC KEY)** : SQL Server 2014 이상에서만 사용할 암호화 알고리즘과 암호화 보안에 사용할 인증서 또는 비대칭 키를 지정합니다.
- **DESCRIPTION** **=** { **‘** _text_ **’**  |  **@** _text\_variable_ }: 백업 세트를 설명하는 자유 형식의 텍스트를 지정합니다. 문자열을 최대 255자까지 지정할 수 있습니다.
- **NAME = { *backup_set_name* |  **@** _backup\_set\_name\_var_ }** : 백업 세트의 이름을 지정합니다. 이름은 최대 128자까지 지정할 수 있습니다. NAME을 지정하지 않으면 공백이 됩니다.

기본적으로 `BACKUP`은 기존 백업 세트를 유지하면서 기존 미디어 세트에 백업을 추가합니다. 이것을 명시적으로 지정하려면 `NOINIT` 옵션을 사용합니다. 기존 백업 세트에 추가하는 방법은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.

또는 백업 미디어를 포맷하기 위해 **FORMAT** 옵션을 사용합니다.

 FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text\_variable_ } ]

 미디어를 처음 사용하거나 기존의 모든 데이터를 덮어쓰려고 하는 경우 **FORMAT** 절을 사용합니다. 필요에 따라 새 미디어에 미디어 이름과 설명을 지정합니다.

 > [!IMPORTANT]
 > `BACKUP` 문의 **FORMAT** 절을 사용하는 경우 백업 미디어에 이전에 저장된 백업이 모두 삭제되므로 각별히 주의해야 합니다.

### <a name="examples"></a><a name="TsqlExample"></a> 예

다음 예제에서는 다음 Transact-SQL 코드를 사용하여 테스트 데이터베이스를 만듭니다.

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
   dt1 DATETIME NOT NULL DEFAULT GETDATE()
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

#### <a name="a-back-up-to-a-disk-device"></a>A. 디스크 디바이스에 백업

다음 예에서는 `SQLTestDB` 을 사용하여 새 미디어 세트를 만들어 `FORMAT` 데이터베이스 전체를 디스크에 백업합니다.

```sql
USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
TO DISK = 'c:\tmp\SQLTestDB.bak'
   WITH FORMAT,
      MEDIANAME = 'SQLServerBackups',
      NAME = 'Full Backup of SQLTestDB';
GO
```

#### <a name="b-back-up-to-a-tape-device"></a>B. 테이프 디바이스에 백업

 다음 예제에서는 이전 백업에 백업을 추가하여 `SQLTestDB` 데이터베이스 전체를 테이프에 백업합니다.

```sql
USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
   TO TAPE = '\\.\Tape0'
   WITH NOINIT,
      NAME = 'Full Backup of SQLTestDB';
GO
```

#### <a name="c-back-up-to-a-logical-tape-device"></a>C. 논리적 테이프 디바이스에 백업

다음 예에서는 테이프 드라이브에 대한 논리적 백업 디바이스를 만듭니다. 그런 다음, SQLTestDB 데이터베이스 전체를 이 디바이스에 백업합니다.

```sql
-- Create a logical backup device,
-- SQLTestDB_Bak_Tape, for tape device \\.\tape0.
USE master;
GO
EXEC sp_addumpdevice 'tape', 'SQLTestDB_Bak_Tape', '\\.\tape0'; USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
   TO SQLTestDB_Bak_Tape
   WITH FORMAT,
      MEDIANAME = 'SQLTestDB_Bak_Tape',
      MEDIADESCRIPTION = '\\.\tape0',
      NAME = 'Full Backup of SQLTestDB';
GO
```

## <a name="using-powershell"></a><a name="PowerShellProcedure"></a> PowerShell 사용

**Backup-SqlDatabase** cmdlet을 사용합니다. 전체 데이터베이스 백업임을 명시적으로 나타내기 위해 **-BackupAction** 매개 변수에 기본값인 **Database** 를 지정합니다. 전체 데이터베이스 백업의 경우 이 매개 변수는 선택 사항입니다.

> [!NOTE]
> 이러한 예제에는 SqlServer 모듈이 필요합니다. 이 모듈이 설치되어 있는지 확인하려면 `Get-Module -Name SqlServer`를 실행합니다. 이 모듈을 설치하려면 PowerShell의 관리자 세션에서 `Install-Module -Name SqlServer`를 실행합니다.
>
> 자세한 내용은 [SQL Server PowerShell Provider](../../powershell/sql-server-powershell-provider.md)을(를) 참조하세요.

> [!IMPORTANT]
> SQL Server Management Studio 내에서 PowerShell 창을 열어 SQL Server 설치에 연결하는 경우 SSMS의 자격 증명이 PowerShell과 SQL Server 인스턴스 간의 연결을 설정하는 데 자동으로 사용되므로 이 예제의 자격 증명 부분을 생략해도 됩니다.

### <a name="examples"></a>예

#### <a name="a-full-backup-local"></a>A. 전체 백업(로컬)

다음 예에서는 서버 인스턴스 `<myDatabase>` 의 기본 백업 위치에 `Computer\Instance`데이터베이스의 전체 데이터베이스 백업을 만듭니다. 선택 사항으로, 이 예제에서는 **-BackupAction Database** 를 지정합니다.

전체 구문 및 추가 예제는 [Backup-SqlDatabase](/powershell/module/sqlserver/backup-sqldatabase)를 참조하세요.

```powershell
$credential = Get-Credential

Backup-SqlDatabase -ServerInstance Computer[\Instance] -Database <myDatabase> -BackupAction Database -Credential $credential
```

#### <a name="b-full-backup-to-azure"></a>B. Azure에 전체 백업

다음 예제에서는 Azure Blob Storage 서비스로 `<myServer>` 인스턴스의 `<myDatabase>` 데이터베이스 전체 백업을 만듭니다. 읽기, 쓰기 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다. 저장된 액세스 정책에 연결된 공유 액세스 서명을 사용하여 SQL Server 자격 증명인 `https://<myStorageAccount>.blob.core.windows.net/<myContainer>`를 만들었습니다. PowerShell 명령은 **BackupFile** 매개 변수를 사용하여 위치(URL)와 백업 파일 이름을 지정합니다.

```powershell
$credential = Get-Credential
$container = 'https://<myStorageAccount>blob.core.windows.net/<myContainer>'
$fileName = '<myDatabase>.bak'
$server = '<myServer>'
$database = '<myDatabase>'
$backupFile = $container + '/' + $fileName

Backup-SqlDatabase -ServerInstance $server -Database $database -BackupFile $backupFile -Credential $credential
```

## <a name="related-tasks"></a><a name="RelatedTasks"></a> Related tasks

- [데이터베이스 백업(SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
- [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)
- [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
- [단순 복구 모델에서 데이터베이스 백업 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)
- [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)
- [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)
- [유지 관리 계획 마법사 사용](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)

## <a name="see-also"></a>참고 항목

- [SQL Server 백업 및 복원 작업 문제 해결](https://support.microsoft.com/kb/224071)
- [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)
- [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)
- [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)
- [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)
- [데이터베이스 백업&#40;일반 페이지&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)
- [데이터베이스 백업&#40;백업 옵션 페이지&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)
- [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)
- [전체 데이터베이스 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)