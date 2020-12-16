---
title: BULK INSERT 또는 OPENROWSET(BULK ...)을 사용하여 데이터를 SQL Server로 가져오기
description: 보안 고려 사항을 포함하여, Transact-SQL 문을 통해 파일에서 SQL Server 또는 Azure SQL Database 테이블로 데이터를 대량으로 가져오는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
author: markingmyname
ms.author: maghan
ms.date: 09/25/2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 4afac2fde54524d5440d33d8ff2bf4cdc9062521
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473974"
---
# <a name="use-bulk-insert-or-openrowsetbulk-to-import-data-to-sql-server"></a>BULK INSERT 또는 OPENROWSET(BULK ...)을 사용하여 데이터를 SQL Server로 가져오기

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 문서에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT 문 및 INSERT...SELECT * FROM OPENROWSET(BULK...) 문을 사용하여 데이터 파일의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database 테이블에 대량으로 가져오는 방법을 간략하게 설명합니다. BULK INSERT 및 OPENROWSET(BULK…)을 사용할 때와 이러한 방법을 사용하여 원격 데이터 원본에서 데이터를 대량으로 가져올 때의 보안 고려 사항에 대해서도 설명합니다.

> [!NOTE]
> BULK INSERT 또는 OPENROWSET(BULK…)을 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 가장을 처리하는 방법을 이해해야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "보안 고려 사항"을 참조하십시오.

## <a name="bulk-insert-statement"></a>BULK INSERT 문

BULK INSERT는 데이터 파일의 데이터를 테이블로 로드합니다. 이 기능은 **bcp** 명령의 **in** 옵션이 제공하는 기능과 유사하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 데이터 파일을 읽는다는 점이 다릅니다. BULK INSERT 구문에 대한 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.

## <a name="bulk-insert-examples"></a>BULK INSERT 예

- [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)
- [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)
- [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)
- [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
- [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)
- [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="openrowsetbulk-function"></a>OPENROWSET(BULK...) 함수

OPENROWSET 대량 행 집합 공급자는 OPENROWSET 함수를 호출하고 BULK 옵션을 지정하여 액세스합니다. OPENROWSET(BULK...) 함수를 사용하면 OLE DB 공급 기업을 통해 데이터 파일 등의 원격 데이터 원본에 연결하여 원격 데이터에 액세스할 수 있습니다.

데이터를 대량으로 가져오려면 INSERT 문 내의 SELECT...FROM 절에서 OPENROWSET(BULK...)를 호출합니다. 데이터 대량 가져오기의 기본 구문은 다음과 같습니다.

INSERT ... 선택 * OPENROWSET (BULK)에서

INSERT 문에서 사용하는 경우 OPENROWSET(BULK...)은 테이블 힌트를 지원합니다. 또한 TABLOCK과 같은 일반적인 테이블 힌트 외에도 BULK 절에는 다음과 같은 특수 테이블 힌트를 사용할 수 있습니다. IGNORE_CONSTRAINTS(CHECK 제약 조건만 무시), IGNORE_TRIGGERS, KEEPDEFAULTS 및 KEEPIDENTITY. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.

BULK 옵션의 추가 사용법에 대한 자세한 내용은 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)를 참조하세요.

## <a name="insertselect--from-openrowsetbulk-statements---examples"></a>INSERT...SELECT * FROM OPENROWSET(BULK...) 문 - 예제:

- [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)
- [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="security-considerations"></a>보안 고려 사항

사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 계정의 보안 프로필이 사용됩니다. SQL Server 인증을 사용하는 로그인은 데이터베이스 엔진 외부에서 인증될 수 없습니다. 따라서 BULK INSERT 명령이 SQL Server 인증을 사용하는 로그인에 의해 시작되면 데이터에 대한 연결이 SQL Server 프로세스 계정(SQL Server 데이터베이스 엔진 서비스에서 사용하는 계정)의 보안 컨텍스트를 사용하여 설정됩니다. 

원본 데이터를 성공적으로 읽으려면 SQL Server 데이터베이스 엔진에서 사용하는 계정에 원본 데이터에 대한 액세스 권한을 부여해야 합니다. 반면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 Windows 인증을 사용하여 로그온한 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 보안 프로필에 관계없이 해당 사용자 계정으로 액세스할 수 있는 파일만 읽을 수 있습니다.

예를 들어 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그온한 사용자가 있다고 가정합니다. 이 사용자가 BULK INSERT 또는 OPENROWSET을 사용하여 데이터 파일의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 가져오려면 사용자 계정에 해당 데이터 파일에 대한 읽기 액세스 권한이 있어야 합니다. 해당 데이터 파일에 대한 액세스 권한이 있는 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 해당 파일에 대한 액세스 권한이 없더라도 해당 파일의 데이터를 테이블로 가져올 수 있습니다. 이때 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 파일 액세스 권한을 부여할 필요가 없습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 인증된 Windows 사용자의 자격 증명을 전달하여 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있도록 구성될 수 있습니다. 이러한 작업을 *가장* 또는 *위임* 이라고 합니다. BULK INSERT 또는 OPENROWSET을 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용자 가장에 대한 보안을 처리하는 방법을 이해해야 합니다. 사용자 가장을 사용하면 데이터 파일을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 또는 사용자와는 다른 컴퓨터에 저장할 수 있습니다. 예를 들어 **Computer_A** 의 사용자에게 **Computer_B** 의 데이터 파일에 대한 액세스 권한이 있고 자격 증명의 위임이 적절하게 설정되어 있는 경우 해당 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer_C **에서 실행 중인** 인스턴스에 연결하고 **Computer_B** 의 데이터 파일에 액세스하여 해당 파일의 데이터를 **Computer_C** 의 테이블로 대량 가져올 수 있습니다.

## <a name="bulk-importing-to-sql-server-from-a-remote-data-file"></a>원격 데이터 파일에서 SQL Server로 대량 가져오기

BULK INSERT 또는 INSERT...SELECT \* FROM OPENROWSET(BULK...)를 사용하여 다른 컴퓨터에서 데이터를 대량으로 가져오려면 두 컴퓨터 간에 데이터 파일을 공유해야 합니다. 공유 데이터 파일을 지정하려면 **\\\\** _Servername_ **\\** _Sharename_ **\\** _Path_ **\\** _Filename_ 의 일반 형식으로 해당 UNC(범용 명명 규칙) 이름을 사용합니다. 또한 데이터 파일을 액세스하는 데 사용되는 계정에는 원격 디스크의 파일을 읽는 데 필요한 사용 권한이 있어야 합니다.

예를 들어 다음 `BULK INSERT` 문은 `SalesOrderDetail` 라는 데이터 파일의 데이터를 `AdventureWorks` 데이터베이스의 `newdata.txt`테이블로 대량 가져옵니다. 이 데이터 파일은 `\dailyorders` 시스템의 네트워크 공유 디렉터리 `salesforce` 에서 공유 폴더 `computer2`에 있습니다.

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';
```

> [!NOTE]
> 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 독립적으로 파일을 읽기 때문에 **bcp** 유틸리티에는 이러한 제한 사항이 적용되지 않습니다.

## <a name="bulk-importing-from-azure-blob-storage"></a>Azure Blob Storage에서 대량 가져오기

Azure Blob Storage에서 가져오는 경우 데이터가 퍼블릭(익명 액세스)이 아니면 [MASTER KEY](../../t-sql/statements/create-master-key-transact-sql.md)로 암호화된 SAS 키를 기준으로 [DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 만든 다음, BULK INSERT 명령에 사용할 [외부 데이터베이스 원본](../../t-sql/statements/create-external-data-source-transact-sql.md)을 만듭니다.

> [!NOTE]
> 명시적 트랜잭션을 사용하지 마세요. 그러면 4861 오류가 표시됩니다.

### <a name="using-bulk-insert"></a>BULK INSERT 사용

다음 예제에서는 BULK INSERT 명령을 사용하여 SAS 키를 만든 Azure Blob Storage 위치에 있는 csv 파일의 데이터를 로드하는 방법을 보여 줍니다. Azure Blob Storage 위치는 외부 데이터 원본으로 구성되었습니다. 이 경우, 사용자 데이터베이스의 마스터 키로 암호화된 공유 액세스 서명을 사용하는 데이터베이스 범위 자격 증명이 필요합니다.

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (DATA_SOURCE = 'MyAzureBlobStorage');
```

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.

### <a name="using-openrowset"></a>OPENROWSET 사용

다음 예제에서는 OPENROWSET 명령을 사용하여 SAS 키를 만든 Azure Blob Storage 위치에 있는 csv 파일의 데이터를 로드하는 방법을 보여 줍니다. Azure Blob Storage 위치는 외부 데이터 원본으로 구성되었습니다. 이 경우, 사용자 데이터베이스의 마스터 키로 암호화된 공유 액세스 서명을 사용하는 데이터베이스 범위 자격 증명이 필요합니다.

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

INSERT INTO achievements with (TABLOCK) (id, description)
SELECT * FROM OPENROWSET(
   BULK  'csv/achievements.csv',
   DATA_SOURCE = 'MyAzureBlobStorage',
   FORMAT ='CSV',
   FORMATFILE='csv/achievements-c.xml',
   FORMATFILE_DATA_SOURCE = 'MyAzureBlobStorage'
    ) AS DataFile;
```

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.

## <a name="see-also"></a>참고 항목

- [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [SELECT 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)
- [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)
- [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [bcp 유틸리티](../../tools/bcp-utility.md)
- [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
