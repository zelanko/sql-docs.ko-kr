---
title: Azure Blob 스토리지 데이터에 대한 대량 액세스
description: BULK INSERT 및 OPENROWSET을 사용하여 Azure Blob 스토리지 계정의 데이터에 액세스하는 Transact-SQL 예제입니다.
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], from Azure blob storage
- Azure blob storage, bulk import to SQL Server
- BULK INSERT, Azure blob storage
- OPENROWSET, Azure blob storage
ms.assetid: f7d85db3-7a93-400e-87af-f56247319ecd
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: de82e4c1b72355fa97e1d844be45d563a4161ed5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473994"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Azure Blob 스토리지 데이터에 대한 대량 액세스 예제

[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

`BULK INSERT` 및 `OPENROWSET` 문은 Azure Blob Storage의 파일에 직접 액세스할 수 있습니다. 다음 예제에서는 `newinvoices`라는 스토리지 계정 및 `Week3`이라는 컨테이너에 저장된 `inv-2017-01-19.csv`라는 CSV(쉼표로 구분된 값) 파일의 데이터를 사용합니다. 서식 파일의 경로를 사용할 수 있지만 다음 예제에는 이러한 경로가 포함되어 있지 않습니다.

SQL Server에서 Azure Blob Storage에 대량 액세스하려면 적어도 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1이 필요합니다.

> [!IMPORTANT]
> Blob의 컨테이너 및 파일에 대한 모든 경로는 `CASE SENSITIVE`입니다. 정확하지 않은 경우 “대량 로드할 수 없습니다. 파일 "file.csv"가 없거나 파일 액세스 권한이 없습니다.” 같은 오류가 반환될 수 있습니다.

## <a name="create-the-credential"></a>자격 증명 만들기

아래 모든 예제에는 공유 액세스 서명을 참조하는 데이터베이스 범위 자격 증명이 필요합니다.

> [!IMPORTANT]
> 외부 데이터 원본은 `SHARED ACCESS SIGNATURE` ID를 사용하는 데이터베이스 범위 자격 증명으로 만들어야 합니다. 스토리지 계정에 대한 공유 액세스 서명을 만들려면 Azure Portal에서 스토리지 계정 속성 페이지의 **공유 액세스 서명** 속성을 참조하세요. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요. 자격 증명에 대한 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.

`SHARED ACCESS SIGNATURE`여야 하는 `IDENTITY`를 사용하여 데이터베이스 범위 자격 증명을 만듭니다. BLOB 스토리지 계정에 대해 생성된 SAS 토큰을 사용합니다. SAS 토큰에 선행하는 `?`이(가) 없는지, 로드해야 하는 개체의 읽기 권한이 하나 이상인지 및 만료 기간(모든 날짜는 UTC 시간임)이 유효한지 확인하세요.

예를 들면 다음과 같습니다.

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'sv=2018-03-28&ss=b&srt=sco&sp=rwdlac&se=2019-08-31T02:25:19Z&st=2019-07-30T18:25:19Z&spr=https&sig=KS51p%2BVnfUtLjMZtUTW1siyuyd2nlx294tL0mnmFsOk%3D';
```

## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Azure Blob Storage 위치를 참조하는 CSV 파일 데이터 액세스

다음 예제에서는 Azure 스토리지 계정을 가리키는 `MyAzureInvoices`라는 외부 데이터 원본을 사용합니다.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net',
        CREDENTIAL = UploadInvoices
    );
```

그러면 `OPENROWSET` 문의 파일 설명에 컨테이너 이름 (`week3`)을 추가합니다. 파일 이름은 `inv-2017-01-19.csv`로 지정됩니다.

```sql
SELECT * FROM OPENROWSET(
   BULK 'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;   
```

`BULK INSERT`를 사용하여 다음과 같이 컨테이너 및 파일 설명을 사용합니다.

```sql
BULK INSERT Colors2
FROM 'week3/inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
      FORMAT = 'CSV');
```

## <a name="accessing-data-in-a-csv-file-referencing-a-container-in-an-azure-blob-storage-location"></a>Azure Blob Storage 위치의 컨테이너를 참조하는 CSV 파일 데이터 액세스

다음 예제에서는 Azure 스토리지 계정의 컨테이너(`week3`)를 가리키는 외부 데이터 원본을 사용합니다.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoicesContainer
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = UploadInvoices
    );
```

그러면 `OPENROWSET` 문의 파일 설명에 컨테이너 이름을 포함하지 않습니다.

```sql
SELECT * FROM OPENROWSET(
   BULK 'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;
```

`BULK INSERT`를 사용하여 다음과 같이 파일 설명에 컨테이너 이름을 사용하지 않습니다.

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV');
```

## <a name="see-also"></a>참고 항목

- [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)