---
title: Azure Blob Storage의 데이터에 대량 액세스 예제 | Microsoft 문서
ms.custom: ''
ms.date: 01/04/2017
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
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 29d54fc9c2643638ccbcb61691bbb12931c2b348
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64946264"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Azure Blob Storage의 데이터에 대량 액세스 예제
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

`BULK INSERT` 및 `OPENROWSET` 문은 Azure Blob Storage의 파일에 직접 액세스할 수 있습니다. 다음 예제에서는 `newinvoices`라는 스토리지 계정 및 `Week3`이라는 컨테이너에 저장된 `inv-2017-01-19.csv`라는 CSV(쉼표로 구분된 값) 파일의 데이터를 사용합니다. 서식 파일의 경로를 사용할 수 있지만 다음 예제에는 이러한 경로가 포함되어 있지 않습니다. 

SQL Server에서 Azure Blob Storage에 대량 액세스하려면 적어도 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1이 필요합니다.

> [!IMPORTANT]
>  Blob의 컨테이너 및 파일에 대한 모든 경로는 `CASE SENSITIVE`입니다. 정확하지 않은 경우 “대량 로드할 수 없습니다. 파일 "file.csv"가 없거나 파일 액세스 권한이 없습니다.” 같은 오류가 반환될 수 있습니다.
> "


## <a name="create-the-credential"></a>자격 증명 만들기   
   
아래 모든 예제에는 공유 액세스 서명을 참조하는 데이터베이스 범위 자격 증명이 필요합니다.   

> [!IMPORTANT]
>  외부 데이터 원본은 `SHARED ACCESS SIGNATURE` ID를 사용하는 데이터베이스 범위 자격 증명으로 만들어야 합니다. 스토리지 계정에 대한 공유 액세스 서명을 만들려면 Azure Portal에서 스토리지 계정 속성 페이지의 **공유 액세스 서명** 속성을 참조하세요. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요. 자격 증명에 대한 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.  
 
`SHARED ACCESS SIGNATURE`여야 하는 `IDENTITY`를 사용하여 데이터베이스 범위 자격 증명을 만듭니다. Azure Portal의 암호를 사용합니다. 예를 들어  

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```


## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Azure Blob Storage 위치를 참조하는 CSV 파일 데이터 액세스   
다음 예제에서는 Azure 스토리지 계정을 가리키는 `newinvoices`라는 외부 데이터 원본을 사용합니다.   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net', 
        CREDENTIAL = UploadInvoices  
    );
```   

그러면 `OPENROWSET` 문의 파일 설명에 컨테이너 이름 (`week3`)을 추가합니다. 파일 이름은 `inv-2017-01-19.csv`로 지정됩니다.
```sql     
SELECT * FROM OPENROWSET(
   BULK  'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
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
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3', 
        CREDENTIAL = UploadInvoices  
    );
```  
  
그러면 `OPENROWSET` 문의 파일 설명에 컨테이너 이름을 포함하지 않습니다.
```sql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   SINGLE_CLOB) AS DataFile;
```   

`BULK INSERT`를 사용하여 다음과 같이 파일 설명에 컨테이너 이름을 사용하지 않습니다. 

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV'); 
```

## <a name="see-also"></a>참고 항목   

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)   
[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)   
[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)   

