---
title: BULK INSERT(Transact-SQL) | Microsoft Docs
description: BULK INSERT 문의 Transact-SQL 참조입니다.
ms.date: 02/21/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BULK_TSQL
- BULK_INSERT
- BULK_INSERT_TSQL
- BULK INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- tables [SQL Server], importing data into
- inserting files
- views [SQL Server], importing data into
- BULK INSERT statement
- views [SQL Server], exporting data from
- importing data, bulk import
- bulk importing [SQL Server], BULK INSERT statement
- file importing [SQL Server]
ms.assetid: be3984e1-5ab3-4226-a539-a9f58e1e01e2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 83ccbac5d01fca3e7ca237e0debedcd4c1ad9e83
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688809"
---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT(Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

데이터 파일을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자가 지정한 형식으로 데이터베이스 테이블이나 뷰로 가져옵니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
BULK INSERT
   { database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }
      FROM 'data_file'
     [ WITH
    (
   [ [ , ] BATCHSIZE = batch_size ]
   [ [ , ] CHECK_CONSTRAINTS ]
   [ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]
   [ [ , ] DATAFILETYPE =
      { 'char' | 'native'| 'widechar' | 'widenative' } ]
   [ [ , ] DATA_SOURCE = 'data_source_name' ]
   [ [ , ] ERRORFILE = 'file_name' ]
   [ [ , ] ERRORFILE_DATA_SOURCE = 'data_source_name' ]
   [ [ , ] FIRSTROW = first_row ]
   [ [ , ] FIRE_TRIGGERS ]
   [ [ , ] FORMATFILE_DATA_SOURCE = 'data_source_name' ]
   [ [ , ] KEEPIDENTITY ]
   [ [ , ] KEEPNULLS ]
   [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]
   [ [ , ] LASTROW = last_row ]
   [ [ , ] MAXERRORS = max_errors ]
   [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]
   [ [ , ] ROWS_PER_BATCH = rows_per_batch ]
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]
   [ [ , ] TABLOCK ]

   -- input file format options
   [ [ , ] FORMAT = 'CSV' ]
   [ [ , ] FIELDQUOTE = 'quote_characters']
   [ [ , ] FORMATFILE = 'format_file_path' ]
   [ [ , ] FIELDTERMINATOR = 'field_terminator' ]
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]
    )]
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

*database_name* 지정한 테이블 또는 뷰가 상주하는 데이터베이스 이름입니다. 지정하지 않으면 기본값은 현재 데이터베이스입니다.

*schema_name* 테이블 또는 뷰 스키마의 이름입니다. 대량 가져오기 작업을 수행하는 사용자의 기본 스키마가 지정한 테이블이나 뷰의 스키마인 경우에는 *schema_name*을 지정하지 않아도 됩니다. *schema*를 지정하지 않은 경우 대량 가져오기 작업을 수행하는 사용자의 기본 스키마가 지정된 테이블이나 뷰와 다르면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류 메시지를 반환하고 대량 가져오기 작업이 취소됩니다.

*table_name* 데이터를 대량으로 가져올 테이블 또는 뷰의 이름입니다. 모든 열이 동일한 기본 테이블을 참조하는 뷰만 사용할 수 있습니다. 뷰에 데이터를 로드하는 경우의 제한 사항에 대한 자세한 내용은 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)를 참조하세요.

**‘** _data_file_ **’** 지정한 테이블 또는 뷰로 가져올 데이터가 포함된 데이터 파일의 전체 경로입니다. BULK INSERT는 디스크 또는 Azure Blob Storage(예: 네트워크, 플로피 디스크, 하드 디스크 등)에서 데이터를 가져올 수 있습니다.

*data_file*은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행 중인 서버에서 유효한 경로를 지정해야 합니다. *data_file*이 원격 파일일 경우 UNC(Universal Naming Convention) 이름을 지정합니다. UNC 이름의 형식은 \\\\*Systemname*\\*ShareName*\\*Path*\\*FileName*입니다. 예를 들면 다음과 같습니다.

```sql
BULK INSERT Sales.Orders
FROM '\\SystemX\DiskZ\Sales\data\orders.dat';
```

**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 및 Azure SQL Database.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP1.1부터 data_file은 Azure Blob Storage에 있을 수 있습니다. 이 경우 **data_source_name** 옵션을 지정해야 합니다. 예제는 [Azure Blob Storage의 파일에서 데이터 가져오기](#f-importing-data-from-a-file-in-azure-blob-storage)를 참조하세요.

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

**‘** _data_source_name_ **’** 
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 및 Azure SQL Database.
가져올 파일의 Azure Blob Storage 위치를 가리키는 명명된 외부 데이터 원본입니다. 외부 데이터 원본은 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1에서 추가된 `TYPE = BLOB_STORAGE` 옵션을 사용하여 만들어야 합니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조하세요. 예제는 [Azure Blob Storage의 파일에서 데이터 가져오기](#f-importing-data-from-a-file-in-azure-blob-storage)를 참조하세요.

BATCHSIZE **=** _batch_size_ 일괄 처리의 행 수를 지정합니다. 모든 일괄 처리는 하나의 트랜잭션으로 서버에 복사됩니다. 이 작업이 실패하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모든 일괄 처리에 대한 트랜잭션을 커밋하거나 롤백합니다. 기본적으로 지정된 데이터 파일의 모든 데이터는 하나의 일괄 처리입니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.

CHECK_CONSTRAINTS 대량 가져오기 작업 중 대상 테이블 또는 뷰의 모든 제약 조건을 검사하도록 지정합니다. CHECK_CONSTRAINTS 옵션을 지정하지 않으면 모든 CHECK 및 FOREIGN KEY 제약 조건이 무시되고 작업 이후 테이블의 제약 조건은 트러스트될 수 없는 것으로 표시됩니다.

> [!NOTE]
> UNIQUE 및 PRIMARY KEY 제약 조건은 항상 적용됩니다. NOT NULL 제약 조건으로 정의된 문자 열로 가져올 때 텍스트 파일에 값이 없으면 BULK INSERT는 공백 문자열을 삽입합니다.

특정 지점에서는 전체 테이블의 제약 조건을 확인해야 합니다. 대량 가져오기 작업을 수행하기 전에 테이블이 비어 있지 않으면 제약 조건의 유효성을 다시 검사하는 비용이 증분 데이터에 CHECK 제약 조건을 적용하는 비용을 초과할 수 있습니다.

입력 데이터에 제약 조건을 위반하는 행이 포함된 경우에는 제약 조건을 사용하지 않을 수 있습니다(기본 동작). CHECK 제약 조건을 사용하지 않으면 데이터를 가져온 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 잘못된 데이터를 제거할 수 있습니다.

> [!NOTE]
> MAXERRORS 옵션은 제약 조건 확인에 적용되지 않습니다.

CODEPAGE **=** { **'** ACP **'** \| **'** OEM **'** \| **'** RAW **'** \| **'** _code_page_ **'** } 데이터 파일에 있는 데이터의 코드 페이지를 지정합니다. CODEPAGE는 문자 값이 **127**보다 크거나 **32**보다 작은 **char**, **varchar**또는 **text** 열이 데이터에 포함된 경우에만 적합합니다. 예제는 [코드 페이지 지정](#d-specifying-a-code-page)을 참조하세요.

> [!IMPORTANT]
> CODEPAGE는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]의 경우 Linux에서 지원되는 옵션이 아닙니다. [!INCLUDE[ssSQLv15_md](../../includes/sssqlv15-md.md)]의 경우 CODEPAGE에 대해 **'RAW'** 옵션만 허용됩니다.

> [!NOTE]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 [서식 파일](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)의 각 열에 대해 데이터 정렬 이름을 지정하는 것이 좋습니다.

|CODEPAGE 값|Description|
|--------------------|-----------------|
|ACP|**char**, **varchar** 또는 **text** 데이터 형식의 열은 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 코드 페이지(ISO 1252)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지로 변환됩니다.|
|OEM(기본값)|**char**, **varchar** 또는 **text** 데이터 형식의 열은 시스템 OEM 코드 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지로 변환됩니다.|
|RAW|다른 코드 페이지로의 변환이 이루어지지 않는 가장 빠른 옵션입니다.|
|*code_page*|특정 코드 페이지 번호(예: 850)입니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이전 버전은 코드 페이지 65001(UTF-8 인코딩)을 지원하지 않습니다.|
| &nbsp; | &nbsp; |

DATAFILETYPE **=** { **'char'** \| **'native'** \| **'widechar'** \| **'widenative'** } BULK INSERT에서 지정된 데이터 파일 형식 값을 사용하여 가져오기 작업을 수행하도록 지정합니다.

&nbsp;

|DATAFILETYPE 값|모든 데이터 표시 형식|
|------------------------|------------------------------|
|**char**(기본값)|문자 형식<br /><br /> 자세한 내용은 [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.|
|**native**|네이티브(데이터베이스) 데이터 형식. **bcp** 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 대량으로 가져와 원시 데이터 파일을 만듭니다.<br /><br /> 네이티브 값은 char 값을 대체하여 보다 뛰어난 성능을 제공합니다. 확장/DBCS(더블바이트 문자 집합) 문자가 포함되어 있지 않은 데이터 파일을 사용하여 여러 개의 SQL Server 인스턴스 간에 데이터를 대량 전송할 때는 네이티브 형식을 사용하는 것이 좋습니다.<br /><br /> 자세한 내용은 [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)를 참조하세요.|
|**widechar**|유니코드 문자<br /><br /> 자세한 내용은 [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.|
|**widenative**|**char**, **varchar** 및 **text** 열을 제외하고 데이터가 유니코드로 저장되는 원시(데이터베이스) 데이터 형식입니다. **bcp** 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 대량으로 가져와 **widenative** 데이터 파일을 만듭니다.<br /><br /> **widenative** 값은 **widechar** 값을 대체하여 보다 뛰어난 성능을 제공합니다. 데이터 파일에 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] 확장 문자가 포함되어 있으면 **widenative**를 지정하십시오.<br /><br /> 자세한 내용은 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)을 참조하세요.|
| &nbsp; | &nbsp; |

ERRORFILE **=’** _file_name_ **’** 서식 오류가 있어 OLE DB 행 집합으로 변환할 수 없는 행을 수집하는 데 사용되는 파일을 지정합니다. 이러한 행은 데이터 파일에서 "있는 그대로" 이 오류 파일에 복사됩니다.

오류 파일은 명령이 실행될 때 생성됩니다. 파일이 이미 있으면 오류가 발생합니다. 또한 확장명이 .ERROR.txt인 제어 파일이 생성됩니다. 이 파일은 오류 파일의 각 행을 참조하여 오류를 진단합니다. 오류를 해결하는 즉시 데이터를 로드할 수 있습니다.
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]부터 `error_file_path`는 Azure Blob Storage에 있을 수 있습니다.

‘errorfile_data_source_name’ **적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
가져오는 동안 발견된 오류를 포함할 오류 파일의 Azure Blob 스토리지 위치를 가리키는 명명된 외부 데이터 원본입니다. 외부 데이터 원본은 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1에서 추가된 `TYPE = BLOB_STORAGE` 옵션을 사용하여 만들어야 합니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조하세요.

FIRSTROW **=** _first_row_ 로드할 첫 번째 행의 번호를 지정합니다. 기본값은 지정한 데이터 파일의 첫 번째 행입니다. FIRSTROW는 1부터 시작합니다.

> [!NOTE]
> FIRSTROW 특성은 열 머리글을 건너뛰기 위해 제공된 것이 아닙니다. BULK INSERT 문에서는 머리글 건너뛰기가 지원되지 않습니다. 행을 건너뛰면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 필드 종결자만 확인하며 건너뛴 행의 필드에 있는 데이터의 유효성을 검사하지 않습니다.

FIRE_TRIGGERS 대량 가져오기 작업 중에 대상 테이블에서 정의된 삽입 트리거가 실행되도록 지정합니다. 트리거가 대상 테이블의 INSERT 작업에 대해 정의되면 완료된 모든 일괄 처리에 대해 발생합니다.

FIRE_TRIGGERS를 지정하지 않으면 삽입 트리거가 실행되지 않습니다.

FORMATFILE_DATA_SOURCE **=** 'data_source_name' **적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1.
가져온 파일의 스키마를 정의할 서식 파일의 Azure Blob Storage 위치를 가리키는 명명된 외부 데이터 원본입니다. 외부 데이터 원본은 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1에서 추가된 `TYPE = BLOB_STORAGE` 옵션을 사용하여 만들어야 합니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조하세요.

KEEPIDENTITY 가져온 데이터 파일의 ID 값이 ID 열에 사용되도록 지정합니다. KEEPIDENTITY를 지정하지 않는 경우 이 열의 ID 값을 확인하지만 가져오지는 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 테이블 생성 중에 지정된 초기값 및 증가값에 따라 고유한 값을 자동으로 할당합니다. 데이터 파일에 테이블이나 뷰의 ID 열 값이 포함되지 않은 경우 서식 파일을 사용하여 데이터를 가져올 때 테이블이나 뷰의 ID 열을 생략하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 해당 열에 고유한 값을 자동으로 할당합니다. 자세한 내용은 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)를 참조하세요.

ID 값의 보관에 대한 자세한 내용은 [데이터를 대량으로 가져올 때 ID 값 보관 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)를 참조하세요.

KEEPNULLS 대량 가져오기 작업 시 삽입된 열에 기본값을 지정하는 대신 빈 열에 Null 값을 유지하도록 지정합니다. 자세한 내용은 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)을 참조하세요.

KILOBYTES_PER_BATCH **=** _kilobytes_per_batch_ 일괄 처리당 데이터의 근사치 크기(KB)를 *kilobytes_per_batch*로 지정합니다. 기본적으로 KILOBYTES_PER_BATCH는 알 수 없습니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.

LASTROW **=** _last_row_ 로드할 마지막 행의 번호를 지정합니다. 기본값은 0이며 지정한 데이터 파일의 마지막 행을 가리킵니다.

MAXERRORS **=** _max_errors_ 대량 가져오기 작업을 취소하기 전에 데이터에서 허용되는 최대 구문 오류 수를 지정합니다. 대량 가져오기 작업으로 가져올 수 없는 각 행은 무시되고 하나의 오류로 계산됩니다. *max_errors*를 지정하지 않으면 기본값은 10입니다.

> [!NOTE]
> MAX_ERRORS 옵션은 제약 조건 확인이나 **money** 및 **bigint** 데이터 형식 변환에 적용되지 않습니다.

ORDER ( { *column* [ ASC | DESC ] } [ **,** ... *n* ] ) 데이터 파일의 데이터를 정렬하는 방법을 지정합니다. 가져올 데이터를 테이블의 클러스터형 인덱스(있는 경우)에 따라 정렬하면 대량 가져오기 성능이 향상됩니다. 데이터 파일을 클러스터형 인덱스 키와 다른 순서로 정렬하거나 테이블에 클러스터형 인덱스가 없으면 ORDER 절이 무시됩니다. 지정한 열 이름은 대상 테이블에서 올바른 열 이름이어야 합니다. 기본적으로 대량 삽입 작업은 데이터 파일이 정렬되지 않았음을 전제로 합니다. 대량 가져오기 작업을 최적화하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 가져온 데이터가 정렬되어 있는지도 확인합니다.

*n* 복수 열을 지정할 수 있음을 나타내는 자리 표시자입니다.

ROWS_PER_BATCH **=** _rows_per_batch_ 데이터 파일에 있는 대략적인 데이터 행 수를 나타냅니다.

기본적으로 데이터 파일의 모든 데이터는 단일 트랜잭션으로 서버에 전송되며 일괄 처리의 행 수는 쿼리 최적화 프로그램에 알려지지 않습니다. ROWS_PER_BATCH를 0보다 큰 값으로 지정하면 서버에서 이 값을 사용하여 대량 가져오기 작업을 최적화합니다. ROWS_PER_BATCH에 지정된 값은 실제 행 수와 대략적으로 동일해야 합니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.

TABLOCK 대량 가져오기 작업이 진행되는 동안 테이블 수준 잠금을 획득하도록 지정합니다. 테이블에 인덱스가 없고 TABLOCK이 지정되어 있으면 여러 클라이언트가 동시에 테이블을 로드할 수 있습니다. 기본적으로 잠금 동작은 **table lock on bulk load**테이블 옵션에 의해 결정됩니다. 대량 가져오기 작업이 진행되는 동안에만 잠금을 보유하면 테이블에 대한 잠금 경합이 줄어들고 이 경우 성능이 크게 향상됩니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.

columnstore 인덱스의 경우. 내부적으로 여러 개의 행 집합으로 나뉘기 때문에 잠금 동작은 다릅니다. 각 스레드가 행 집합에 대해 X 잠금을 수행하여 데이터를 각 행 집합에 배타적으로 로드하므로 동시 데이터 로드 세션에서 병렬 데이터 로드가 가능합니다. TABLOCK 옵션을 사용하면 스레드가 테이블에 대해 X 잠금을 수행하여(기존 행 집합에 대한 BU 잠금과 달리) 다른 동시 스레드가 동시에 데이터를 로드하지 못하게 합니다.

### <a name="input-file-format-options"></a>입력 파일 형식 옵션

FORMAT **=** ‘CSV’ **적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[RFC 4180](https://tools.ietf.org/html/rfc4180) 표준을 준수하는 쉼표로 구분된 값 파일을 지정합니다.

```sql
BULK INSERT Sales.Orders
FROM '\\SystemX\DiskZ\Sales\data\orders.csv'
WITH ( FORMAT='CSV');
```

FIELDQUOTE **=** ‘field_quote’ **적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
CSV 파일에 따옴표 문자로 사용될 문자를 지정합니다. 지정하지 않으면 [RFC 4180](https://tools.ietf.org/html/rfc4180) 표준에 정의한 대로 따옴표 문자(")가 따옴표 문자로 사용됩니다.

FORMATFILE **=** ‘_format_file_path_’ 서식 파일의 전체 경로를 지정합니다. 서식 파일이란 동일한 테이블이나 뷰에서 **bcp** 유틸리티를 사용하여 생성된 저장 응답을 포함하는 데이터 파일을 말합니다. 다음과 같은 경우에 서식 파일이 사용됩니다.

- 데이터 파일의 열이 테이블 또는 뷰보다 많거나 적을 경우
- 열 순서가 다를 경우
- 열 구분 기호가 다를 경우
- 데이터 서식에 기타 변경 내용이 있을 경우. 일반적으로 서식 파일은 **bcp** 유틸리티를 사용하여 만들고 필요에 따라 텍스트 편집기로 수정합니다. 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md) 및 [서식 파일 만들기](../../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요.

**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 및 Azure SQL Database.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 format_file_path는 Azure Blob Storage에 있을 수 있습니다.

FIELDTERMINATOR **=’** _field_terminator_ **’** **char** 및 **widechar** 데이터 파일에 사용할 필드 종결자를 지정합니다. 기본 필드 종결자는 \t(탭 문자)입니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.

ROWTERMINATOR **=’** _row_terminator_ **’** **char** 및 **widechar** 데이터 파일에 사용할 행 종결자를 지정합니다. 기본 행 종결자는 **\r\n**(줄 바꿈 문자)입니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.

## <a name="compatibility"></a>호환성

BULK INSERT는 파일에서 읽은 데이터에 엄격한 데이터 유효성 검사 및 데이터 검사를 강제로 실행합니다. 이로 인해 기존 스크립트가 잘못된 데이터에서 실행되면 오류가 발생할 수 있습니다. 예를 들어 BULK INSERT는 다음을 확인합니다.

- **float** 또는 **real** 데이터 형식의 원시 표시가 유효한지 여부
- 유니코드 데이터의 길이가 짝수 바이트인지 여부

## <a name="data-types"></a>데이터 형식

### <a name="string-to-decimal-data-type-conversions"></a>String 데이터 형식에서 Decimal 데이터 형식으로의 변환

BULK INSERT에 사용되는 String 데이터 형식에서 Decimal 데이터 형식으로의 변환은 [!INCLUDE[tsql](../../includes/tsql-md.md)] [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수와 동일한 규칙을 따르며 과학적 표기법을 사용하는 숫자 값을 나타내는 문자열을 거부합니다. 따라서 BULK INSERT는 이러한 문자열을 잘못된 값으로 처리하고 변환 오류를 보고합니다.

이 동작을 해결하려면 서식 파일을 사용하여 과학적 표기법 **float** 데이터를 Decimal 열로 대량 가져옵니다. 서식 파일에서 명시적으로 열을 **real** 또는 **float** 데이터로 설명합니다. 두 데이터 형식에 대한 자세한 내용은 [float 및 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)을 참조하십시오.

> [!NOTE]
> 서식 파일은 **실수** 데이터를 **SQLFLT4** 데이터 형식으로, **부동** 데이터를 **SQLFLT8** 데이터 형식으로 나타냅니다. XML이 아닌 서식 파일에 대한 자세한 내용은 [bcp를 사용하여 파일 스토리지 형식 지정 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)를 참조하세요.

#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>과학적 표기법을 사용하는 숫자 값 가져오기 예

이 예에서는 다음 테이블을 사용합니다.

```sql
CREATE TABLE t_float(c1 FLOAT, c2 DECIMAL (5,4));
```

 사용자가 `t_float` 테이블로 데이터를 대량 가져오려고 합니다. 데이터 파일 C:\t_float-c.dat에는 과학적 표기법 **float** 데이터가 들어 있습니다. 예를 들면 다음과 같습니다.

```input
8.0000000000000002E-28.0000000000000002E-2
```

그러나 두 번째 열 `t_float`에서 `c2` 데이터 형식을 사용하므로 BULK INSERT는 이 데이터를 직접 `decimal`으로 가져올 수 없습니다. 따라서 서식 파일이 필요합니다. 서식 파일은 열 `c2`의 과학적 표기법 **float** 데이터를 Decimal 형식으로 매핑해야 합니다.

다음 서식 파일은 `SQLFLT8` 데이터 형식을 사용하여 두 번째 데이터 필드를 두 번째 열로 매핑합니다.

```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<RECORD>
<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/>
<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/> </RECORD> <ROW>
<COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/>
<COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/> </ROW> </BCPFORMAT>
```

이 서식 파일(`C:\t_floatformat-c-xml.xml`)을 사용하여 테스트 데이터를 테스트 테이블로 가져오려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.

```sql
BULK INSERT bulktest..t_float
FROM 'C:\t_float-c.dat' WITH (FORMATFILE='C:\t_floatformat-c-xml.xml');
```

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

### <a name="data-types-for-bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML 문서 대량 내보내기 또는 가져오기를 위한 데이터 형식

SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다.

|데이터 형식|영향|
|---------------|------------|
|SQLCHAR 또는 SQLVARCHAR|데이터를 클라이언트 코드 페이지나 데이터 정렬에 포함된 코드 페이지로 보냅니다. 결과는 서식 파일을 지정하지 않고 DATAFILETYPE **='char'** 를 지정하는 것과 같습니다.|
|SQLNCHAR 또는 SQLNVARCHAR|데이터를 유니코드로 보냅니다. 결과는 서식 파일을 지정하지 않고 DATAFILETYPE **= 'widechar'** 를 지정하는 것과 같습니다.|
|SQLBINARY 또는 SQLVARYBIN|데이터를 변환하지 않고 보냅니다.|
| &nbsp; | &nbsp; |

## <a name="general-remarks"></a>일반적인 주의 사항

BULK INSERT 문과 INSERT 문을 비교하면 다음과 같습니다. SELECT \* FROM OPENROWSET(BULK...) 문 및 **bcp** 명령은 [데이터 대량 가져오기 및 내보내기 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)를 참조하세요.

대량 가져오기를 위한 데이터 준비에 대한 자세한 내용은 [대량 내보내기 또는 가져오기를 위한 데이터 준비 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)를 참조하세요.

BULK INSERT 문은 데이터를 테이블 또는 뷰로 가져올 사용자 정의 트랜잭션 내에서 실행할 수 있습니다. 필요에 따라 대량 데이터 가져오기를 위한 여러 일치 항목을 사용하려면 트랜잭션에서 BULK INSERT 문 내에 BATCHSIZE 절을 지정할 수 있습니다. 여러 일괄 처리 트랜잭션이 롤백되는 경우에는 트랜잭션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 보낸 모든 일괄 처리가 롤백됩니다.

## <a name="interoperability"></a>상호 운용성

### <a name="importing-data-from-a-csv-file"></a>CSV 파일에서 데이터 가져오기

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 BULK INSERT는 Azure SQL Database처럼 CSV 형식을 지원합니다.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 전의 CSV(쉼표로 구분된 값) 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 가져오기 작업에서 지원되지 않습니다. 그러나 경우에 따라 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 대량으로 가져오기 위한 데이터 파일로 CSV(쉼표로 구분된 값) 파일이 사용될 수 있습니다. CSV 데이터 파일에서 데이터 가져오기의 요구 사항에 대한 자세한 내용은 [대량 내보내기 또는 가져오기를 위한 데이터 준비 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)를 참조하세요.

## <a name="logging-behavior"></a>로깅 동작

 SQL Server로 대량 가져오기에서 수행된 행 삽입 작업이 트랜잭션 로그에 로그되는 경우에 대한 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 필수 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요. 최소 로깅은 Azure SQL Database에서 지원되지 않습니다.

## <a name="restrictions"></a><a name="Limitations"></a> 제한 사항

서식 파일을 BULK INSERT와 함께 사용하면 최대 1024개의 필드만 지정할 수 있습니다. 이는 테이블에 허용된 최대 열 수와 동일합니다. 1024개가 넘는 필드를 포함하는 데이터 파일의 BULK INSERT와 함께 서식 파일을 사용하면 BULK INSERT에서 4822 오류가 발생합니다. [bcp 유틸리티](../../tools/bcp-utility.md)에는 이러한 제한이 없으므로, 1024개가 넘는 필드를 포함하는 데이터 파일의 경우 서식 파일 없이 BULK INSERT를 사용하거나 **bcp** 명령을 사용합니다.

## <a name="performance-considerations"></a>성능 고려 사항

단일 일괄 처리에서 플러시될 페이지 수가 내부 임계값을 초과하면 버퍼 풀의 전체 검색이 일괄 처리를 커밋할 때 플러시할 페이지를 식별할 수 있습니다. 이 전체 검색으로 대량 가져오기 성능이 저하될 수 있습니다. 대용량 버퍼 풀이 느린 I/O 하위 시스템과 결합할 때 내부 임계값이 초과될 수 있습니다. 대규모 컴퓨터에서 버퍼 오버플로를 방지하려면 대량 최적화를 제거하는 TABLOCK 힌트를 사용하지 않거나 대량 최적화를 유지하는 보다 작은 크기의 일괄 처리를 사용합니다.

각 컴퓨터는 서로 다르므로, 데이터 로드로 다양한 일괄 처리 크기를 테스트하여 가장 적합한 크기를 찾는 것이 좋습니다.

대량 데이터를 가져오는 경우, 가져오기 전에 Azure SQL Database로 데이터베이스 또는 인스턴스의 성능 수준을 일시적으로 높이는 것이 좋습니다.

## <a name="security"></a>보안

### <a name="security-account-delegation-impersonation"></a>보안 계정 위임(가장)

사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 계정의 보안 프로필이 사용됩니다. SQL Server 인증을 사용하는 로그인은 데이터베이스 엔진 외부에서 인증될 수 없습니다. 따라서 BULK INSERT 명령이 SQL Server 인증을 사용하는 로그인에 의해 시작되면 데이터에 대한 연결이 SQL Server 프로세스 계정(SQL Server 데이터베이스 엔진 서비스에서 사용하는 계정)의 보안 컨텍스트를 사용하여 설정됩니다. 원본 데이터를 성공적으로 읽으려면 SQL Server 데이터베이스 엔진에서 사용하는 계정에 원본 데이터에 대한 액세스 권한을 부여해야 합니다. 반면에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 Windows 인증을 사용하여 로그온한 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 보안 프로필에 관계없이 해당 사용자 계정으로 액세스할 수 있는 파일만 읽을 수 있습니다.

**sqlcmd** 또는 **osql**을 사용하는 BULK INSERT 문을 실행하는 경우 한 컴퓨터에서 두 번째 컴퓨터의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 데이터를 삽입하고 UNC 경로를 사용하여 세 번째 컴퓨터에서 *data_file*을 지정하면 4861 오류가 발생할 수 있습니다.

이러한 오류를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 계정의 보안 프로필을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정하거나 보안 계정 위임을 사용하도록 Windows를 구성하십시오. 위임용으로 사용자 계정이 트러스트될 수 있도록 설정하는 방법은 Windows 도움말을 참조하십시오.

이에 대한 자세한 내용 및 BULK INSERT를 사용하기 위한 기타 보안 고려 사항에 대한 자세한 내용은 [Import Bulk Data by Using BULK INSERT 또는 OPENROWSET을 사용하여 대량 데이터 가져오기 &#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)를 참조하세요.

Azure Blob Storage에서 가져오는 경우 데이터가 퍼블릭(익명 액세스)이 아니면 [MASTER KEY](create-master-key-transact-sql.md)로 암호화된 SAS 키를 기준으로 [DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 만든 다음, BULK INSERT 명령에 사용할 [외부 데이터베이스 원본](../../t-sql/statements/create-external-data-source-transact-sql.md)을 만듭니다. 예제는 [Azure Blob Storage의 파일에서 데이터 가져오기](#f-importing-data-from-a-file-in-azure-blob-storage)를 참조하세요.

### <a name="permissions"></a>사용 권한

INSERT 및 ADMINISTER BULK OPERATIONS 권한이 필요합니다. Azure SQL Database에서는 INSERT 및 ADMINISTER DATABASE BULK OPERATIONS 권한이 필요합니다. SQL Server on Linux에 대해서는 ADMINISTER BULK OPERATIONS 권한 또는 bulkadmin 역할이 지원되지 않습니다. `sysadmin`만 SQL Server on Linux에 대한 대량 삽입을 수행할 수 있습니다. 

또한 다음 중 하나 이상이 적용되는 경우에는 ALTER TABLE 권한이 필요합니다.

- 제약 조건이 있으며 CHECK_CONSTRAINTS 옵션을 지정하지 않았습니다.

   > [!NOTE]
   > 기본적으로 제약 조건은 사용되지 않습니다. 명시적으로 제약 조건을 확인하려면 CHECK_CONSTRAINTS 옵션을 사용하십시오.

- 트리거가 있으며 FIRE_TRIGGER 옵션을 지정하지 않았습니다.

   > [!NOTE]
   > 기본적으로 트리거는 실행되지 않습니다. 명시적으로 트리거를 발생시키려면 FIRE_TRIGGER 옵션을 사용하십시오.

- KEEPIDENTITY 옵션을 사용하여 데이터 파일에서 ID 값을 가져올 수 있습니다.

## <a name="examples"></a>예제

### <a name="a-using-pipes-to-import-data-from-a-file"></a>A. 파이프를 사용하여 파일에서 데이터 가져오기

다음 예에서는 필드 종결자로 파이프(`AdventureWorks2012.Sales.SalesOrderDetail`)를 사용하고 행 종결자로 `|`을 사용하여 지정한 데이터 파일에서 `|\n` 테이블로 주문 세부 정보를 가져옵니다.

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM 'f:\orders\lineitem.tbl'
   WITH
      (  
         FIELDTERMINATOR =' |'
         , ROWTERMINATOR =' |\n'
      );
```

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

### <a name="b-using-the-fire_triggers-argument"></a>B. FIRE_TRIGGERS 인수 사용

다음 예에서는 `FIRE_TRIGGERS` 인수를 지정합니다.

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM 'f:\orders\lineitem.tbl'
   WITH
     (
         FIELDTERMINATOR =' |'
         , ROWTERMINATOR = ':\n'
         , FIRE_TRIGGERS
      );
```

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

### <a name="c-using-line-feed-as-a-row-terminator"></a>C. 행 종결자로 줄 바꿈 사용

 다음 예에서는 UNIX 출력 같은 행 종결자로 줄 바꿈을 사용하는 파일을 가져옵니다.

```sql
DECLARE @bulk_cmd VARCHAR(1000);
SET @bulk_cmd = 'BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
FROM ''<drive>:\<path>\<filename>''
WITH (ROWTERMINATOR = '''+CHAR(10)+''')';
EXEC(@bulk_cmd);
```

> [!NOTE]
> Microsoft Windows에서 텍스트 파일을 처리하는 방법으로 인해 **(\n**은 **\r\n)** 으로 자동으로 바뀝니다.

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

### <a name="d-specifying-a-code-page"></a>D. 코드 페이지 지정

다음 예에서는 코드 페이지를 지정하는 방법을 보여 줍니다.

```sql
BULK INSERT MyTable
FROM 'D:\data.csv'
WITH
( CODEPAGE = '65001'
   , DATAFILETYPE = 'char'
   , FIELDTERMINATOR = ','
);
```

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

### <a name="e-importing-data-from-a-csv-file"></a>E. CSV 파일에서 데이터 가져오기

다음 예제는 헤더(첫 행)를 건너뛰고 `;`를 필드 종결자로, `0x0a`를 행 종결자로 사용하여 CSV 파일을 지정하는 방법을 보여 줍니다.

```sql
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'
      , FIRSTROW=2
      , FIELDQUOTE = '\'
      , FIELDTERMINATOR = ';'
      , ROWTERMINATOR = '0x0a');
```

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>F. Azure Blob Storage의 파일에서 데이터 가져오기

다음 예제에서는 SAS 키를 만든 Azure Blob Storage 위치에 있는 csv 파일에서 데이터를 로드하는 방법을 보여 줍니다. Azure Blob Storage 위치는 외부 데이터 원본으로 구성되었습니다. 이 경우, 사용자 데이터베이스의 마스터 키로 암호화된 공유 액세스 서명을 사용하는 데이터베이스 범위 자격 증명이 필요합니다.

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
스토리지 계정에 액세스하는 또 다른 방법은 [관리 ID](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)를 사용하는 것입니다. [1~3단계](https://docs.microsoft.com/azure/sql-database/sql-database-vnet-service-endpoint-rule-overview?toc=/azure/sql-data-warehouse/toc.json&bc=/azure/sql-data-warehouse/breadcrumb/toc.json#steps)를 수행하여 관리 ID를 통해 스토리지에 액세스하도록 SQL Database를 구성하면 됩니다. 그런 다음, 코드 샘플을 아래와 같이 구현할 수 있습니다.
```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Change to using Managed Identity instead of SAS key 
CREATE DATABASE SCOPED CREDENTIAL msi_cred WITH IDENTITY = 'Managed Identity';
GO
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/curriculum'
          , CREDENTIAL= msi_cred --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (DATA_SOURCE = 'MyAzureBlobStorage');
```

> [!IMPORTANT]
> Azure SQL Database는 Azure Blob Storage에서 읽기만 지원합니다.

### <a name="g-importing-data-from-a-file-in-azure-blob-storage-and-specifying-an-error-file"></a>G. Azure Blob Storage의 파일에서 데이터 가져오기 및 오류 파일 지정

다음 예제에서는 외부 데이터 원본으로 구성되고 오류 파일을 지정하는 Azure Blob Storage 위치의 csv 파일에서 데이터를 로드하는 방법을 보여줍니다. 이를 위해 공유 액세스 서명을 사용하는 데이터베이스 범위 자격 증명이 필요합니다. Azure SQL Database에서 실행되는 경우 ERRORFILE 옵션에는 ERRORFILE_DATA_SOURCE가 함께 사용되어야 하지만 사용 권한 오류로 인해 가져오기에 실패할 수 있습니다. ERRORFILE에 지정된 파일이 컨테이너에 존재하지 않아야 합니다.

```sql
BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (
         DATA_SOURCE = 'MyAzureInvoices'
         , FORMAT = 'CSV'
         , ERRORFILE = 'MyErrorFile'
         , ERRORFILE_DATA_SOURCE = 'MyAzureInvoices');
```

자격 증명 및 외부 데이터 원본의 구성을 포함하여 전체 `BULK INSERT` 예제는 [Azure Blob Storage의 데이터에 대한 대량 액세스 예제](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)를 참조하세요.

### <a name="additional-examples"></a>추가 예

 다른 `BULK INSERT` 예제는 다음 토픽에 제공됩니다.

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

## <a name="see-also"></a>참고 항목

- [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [bcp 유틸리티](../../tools/bcp-utility.md)
- [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
- [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)
- [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)
- [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)
