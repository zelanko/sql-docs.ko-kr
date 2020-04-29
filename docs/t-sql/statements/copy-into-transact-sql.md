---
title: COPY INTO(Transact-SQL)(미리 보기)
titleSuffix: (SQL Data Warehouse) - SQL Server
description: 외부 스토리지 계정에서 로드하려면 Azure SQL Data Warehouse의 COPY 문을 사용합니다.
ms.date: 04/24/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COPY_TSQL
- COPY INTO
- COPY
- LOAD
dev_langs:
- TSQL
author: kevinvngo
ms.author: kevin
monikerRange: =sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: de9d629622c8f568383083c69dedf1224c85a8dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82153234"
---
# <a name="copy-transact-sql-preview"></a>COPY(Transact-SQL)(미리 보기)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

이 문서에서는 외부 스토리지 계정에서 로드하기 위해 Azure SQL Data Warehouse의 COPY 문을 사용하는 방법을 설명합니다. COPY 문은 SQL Data Warehouse에 대한 처리량이 높은 데이터 수집을 위한 가장 뛰어난 유연성을 제공합니다. 다음 기능에 COPY를 사용합니다.

- 권한이 낮은 사용자를 사용하여 데이터 웨어하우스에 대한 엄격한 제어 권한 없이 로드
- 추가 데이터베이스 개체를 만들 필요 없이 단일 T-SQL 문을 실행
- **구분 기호**(문자열, 필드, 행)**가** **문자열로 구분된 열 내에서 이스케이프**되는 경우 CSV 파일을 올바르게 구문 분석하고 로드
- SAS(공유 액세스 서명)를 사용하여 스토리지 계정 키를 노출하지 않고 보다 세부적인 사용 권한 모델을 지정
- ERRORFILE 위치(REJECTED_ROW_LOCATION)에 대해 다른 스토리지 계정을 사용
- 각 대상 열에 대한 기본값을 사용자 지정하고 원본 데이터 필드를 지정하여 특정 대상 열에 로드
- CSV 파일에 대한 사용자 지정 행 종결자 지정
- CSV 파일에 대한 SQL Server 날짜 형식 활용
- 스토리지 위치 경로에 와일드카드 및 여러 파일 지정

> [!NOTE]  
> COPY 문은 현재 공개 미리 보기로 제공됩니다.

## <a name="syntax"></a>구문  

```syntaxsql
COPY INTO [schema.]table_name
[(Column_list)] 
FROM ‘<external_location>’ [,...n]
WITH  
 ( 
 [FILE_TYPE = {'CSV' | 'PARQUET' | 'ORC'} ]
 [,FILE_FORMAT = EXTERNAL FILE FORMAT OBJECT ]  
 [,CREDENTIAL = (AZURE CREDENTIAL) ]
 [,ERRORFILE = '[http(s)://storageaccount/container]/errorfile_directory[/]] 
 [,ERRORFILE_CREDENTIAL = (AZURE CREDENTIAL) ]
 [,MAXERRORS = max_errors ] 
 [,COMPRESSION = { 'Gzip' | 'DefaultCodec'|’Snappy’}] 
 [,FIELDQUOTE = ‘string_delimiter’] 
 [,FIELDTERMINATOR =  ‘field_terminator’]  
 [,ROWTERMINATOR = ‘row_terminator’]
 [,FIRSTROW = first_row]
 [,DATEFORMAT = ‘date_format’] 
 [,ENCODING = {'UTF8'|'UTF16'}] 
 [,IDENTITY_INSERT = {‘ON’ | ‘OFF’}]
)
```

## <a name="arguments"></a>인수  

*schema_name*  
작업을 수행하는 사용자의 기본 스키마가 지정된 테이블의 스키마인 경우에는 선택 사항입니다. *schema*가 지정되지 않고 COPY 작업을 수행하는 사용자의 기본 스키마가 지정된 테이블과 다를 경우 COPY가 취소되고 오류 메시지가 반환됩니다.  

*table_name*  
데이터를 복사할 대상 테이블의 이름입니다. 대상 테이블은 임시 또는 영구 테이블일 수 있으며, 데이터베이스에 이미 있어야 합니다. 

*(column_list)*  
데이터를 로드하기 위해 원본 데이터 필드를 대상 테이블 열로 매핑하는 데 사용되는 하나 이상의 열에 대한 선택적 목록입니다. *column_list*는 괄호로 묶고 쉼표로 구분해야 합니다. 열 목록은 다음과 같은 형식입니다.

[(Column_name [Default_value] [Field_number] [,...n])]

- *Column_name* - 대상 테이블에 있는 열의 이름입니다.
- *Default_value* - 입력 파일의 NULL 값을 대체할 기본값입니다. 기본값은 모든 파일 형식에 적용됩니다. COPY는 열이 열 목록에서 생략되거나 빈 입력 파일 필드가 있는 경우 입력 파일에서 NULL을 로드하려고 시도합니다.
- *Field_number* - 대상 열 이름에 매핑되는 입력 파일 필드 번호입니다.
- 필드 인덱싱은 1에서 시작합니다.

열 목록을 지정하지 않으면 COPY는 원본 및 대상 ordinality를 기준으로 열을 매핑합니다. 입력 필드 1은 대상 열 1로 이동하고, 필드 2는 열 2로 이동합니다.

*외부 위치*</br>
데이터가 포함된 파일이 준비되는 위치입니다. 현재 ADLS(Azure Data Lake Storage) Gen2 및 Azure Blob Storage가 지원됩니다.

- Blob Storage의 *외부 위치*: https://<account>.blob.core.windows.net/<container>/<path>
- ADLS Gen2의 *외부 위치*: https://<account>. dfs.core.windows.net/<container>/<path>

> [!NOTE]  
> Blob 엔드포인트는 ADLS Gen2에 사용할 수 있으며 이전 버전과의 호환성을 위해서만 사용됩니다. 최상의 성능을 위해 ADLS Gen2에 **dfs** 엔드포인트를 사용합니다.

- *계정* - 스토리지 계정 이름

- *컨테이너* - Blob 컨테이너 이름

- *경로* - 데이터의 폴더 또는 파일 경로입니다. 위치는 컨테이너에서 시작합니다. 폴더를 지정하면 COPY는 폴더와 모든 하위 폴더에서 모든 파일을 검색합니다. COPY는 숨겨진 폴더를 무시하고 경로에 명시적으로 지정되지 않은 경우 밑줄(_) 또는 마침표(.)로 시작하는 파일을 반환하지 않습니다. 와일드카드를 사용하여 경로를 지정하는 경우에도 이 동작은 동일합니다.

와일드카드 카드는 다음 경로에 포함될 수 있습니다.

- 와일드카드 경로 이름 일치는 대/소문자를 구분합니다.
- 백슬래시 문자(\\)를 사용하여 와일드카드를 이스케이프할 수 있습니다.
- 와일드카드 확장은 재귀적으로 적용됩니다. 예를 들어 Customer1의 하위 디렉터리를 포함하여 Customer1 아래의 모든 CSV 파일은 다음 예제에서 로드됩니다. ‘Account/Container/Customer1/*.csv’

> [!NOTE]  
> 최상의 성능을 위해 더 많은 수의 파일로 확장되는 와일드카드를 지정하지 마세요. 가능하면 와일드카드를 지정하는 대신 여러 파일 위치를 나열합니다.

여러 파일 위치는 다음과 같이 쉼표로 구분된 목록을 통해 동일한 스토리지 계정 및 컨테이너에서만 지정할 수 있습니다.

- ‘ https://<account>.blob.core.windows.net/<container>/<path>’, ‘ https://<account>.blob.core.windows.net/<container>/<path>’…

*FILE_TYPE = { ‘CSV’ | ‘PARQUET’ | ‘ORC’ }*</br>
*FILE_TYPE*은 외부 데이터의 형식을 지정합니다.

- CSV: [RFC 4180](https://tools.ietf.org/html/rfc4180) 표준을 준수하는 쉼표로 구분된 값 파일을 지정합니다.
- PARQUET: Parquet 형식을 지정합니다.
- ORC: ORC(최적화된 행 열 형식) 형식을 지정합니다.

>[!NOTE]  
> Polybase의 '구분된 텍스트' 파일 형식은 FIELDTERMINATOR 매개 변수를 통해 기본 쉼표 구분 기호를 구성할 수 있는 ‘CSV’ 파일 형식으로 대체됩니다. 

*FILE_FORMAT = external_file_format_name*</br>
*FILE_FORMAT*은 Parquet 및 ORC 파일에만 적용되면 외부 데이터에 대한 파일 형식과 압축 방법을 저장하는 외부 파일 형식 개체의 이름을 지정합니다. 외부 파일 형식을 만들려면 [CREATE EXTERNAL FILE FORMAT](create-external-file-format-transact-sql.md?view=azure-sqldw-latest)을 사용합니다.

*CREDENTIAL (IDENTITY = ‘’, SECRET = ‘’)*</br>
*자격 증명*은 외부 스토리지 계정에 액세스하기 위한 인증 메커니즘을 지정합니다. 인증 방법은 다음과 같습니다.

|                          |                CSV                |              Parquet              |                ORC                |
| :----------------------: | :-------------------------------: | :-------------------------------: | :-------------------------------: |
|  **Azure Blob 스토리지**  | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD |              SAS/KEY              |              SAS/KEY              |
| **Azure Data Lake Gen2** | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD | SAS/MSI/SERVICE PRINCIPAL/KEY/AAD |

AAD 또는 퍼블릭 스토리지 계정을 사용하여 인증할 때는 자격 증명을 지정할 필요가 없습니다. 

- SAS(공유 액세스 서명)를 사용하여 인증 *IDENTITY: ‘공유 액세스 서명’의 값이 있는 상수*
  *SECRET: [‘공유 액세스 서명’](/azure/storage/common/storage-sas-overview)은 ‘스토리지 계정의 리소스에 대한 위임된 액세스 권한을 제공합니다.’*  
  필요한 최소 권한: 읽기 및 목록

- [*서비스 사용자*](/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store#create-a-credential)로 인증

  *IDENTITY: <ClientID>@<OAuth_2.0_Token_EndPoint>* 
  *SECRET: AAD 애플리케이션 서비스 주체 키* 필요한 최소 RBAC 역할: Storage Blob 데이터 기여자, Storage Blob 데이터 기여자, Storage Blob 데이터 소유자 또는 Storage Blob 데이터 reader

  > [!NOTE]  
  > OAuth 2.0 토큰 엔드포인트 **V1** 사용

- Storage 계정 키를 사용하여 인증 *IDENTITY: ‘Storage 계정 키’의 값이 있는 상수*
  *SECRET: 스토리지 계정 키*
  
- [관리 ID](/azure/sql-data-warehouse/load-data-from-azure-blob-storage-using-polybase#authenticate-using-managed-identities-to-load-optional)(VNet 서비스 엔드포인트)를 사용하여 인증 *IDENTITY: ‘관리 ID’의 값이 있는 상수* 필요한 최소 RBAC 역할: Storage Blob 데이터 기여자, Storage Blob 데이터 소유자 또는 AAD 등록 SQL Database 서버용 Storage Blob 데이터 reader 
  
- AAD 사용자 *자격 증명이 필요하지 않음*으로 인증이 필요한 최소 RBAC 역할: Storage Blob 데이터 기여자, Storage Blob 데이터 소유자 또는 AAD 사용자용 Storage Blob 데이터 reader

*ERRORFILE = 디렉터리 위치*</br>
*ERRORFILE*는 CSV에만 적용됩니다. 거부된 행과 해당 오류 파일을 작성해야 하는 COPY 문 내의 디렉터리를 지정합니다. 스토리지 계정의 전체 경로를 지정하거나 컨테이너와 관련된 경로를 지정할 수 있습니다. 지정된 경로가 존재하지 않으면 사용자를 대신하여 경로를 만듭니다. "_rejectedrows"라는 이름의 하위 디렉터리가 생성됩니다. "_ " 문자는 위치 매개 변수에 명시적으로 명명되지 않는 한, 다른 데이터 처리를 위해 디렉터리를 이스케이프합니다. 

이 디렉터리 내에는 로드 제출 시간을 기준으로 YearMonthDay -HourMinuteSecond 형식에 따라 생성된 폴더가 있습니다(예: 20180330-173205). 이 폴더에는 queryID, distributionID 및 파일 guid가 각각 사전에 추가된 이유(오류) 파일과 데이터(행) 파일의 두 가지 유형의 파일이 작성됩니다. data와 reason은 별도의 파일에 있으므로 해당 파일에는 일치하는 접두사가 있습니다.

ERRORFILE에 정의된 스토리지 계정의 전체 경로가 있는 경우 ERRORFILE_CREDENTIAL이 해당 스토리지에 연결하는 데 사용됩니다. 그렇지 않으면 자격 증명에 대해 언급된 값이 사용됩니다.

*ERRORFILE_CREDENTIAL = (IDENTITY= ‘’, SECRET = ‘’)*</br>
*ERRORFILE_CREDENTIAL*은 CSV 파일에만 적용됩니다. 지원되는 데이터 원본 및 인증 방법은 다음과 같습니다.

- Azure Blob Storage - SAS/SERVICE PRINCIPAL/KEY/AAD
- Azure Data Lake Gen2 -   SAS/MSI/SERVICE PRINCIPAL/KEY/AAD
  
- SAS(공유 액세스 서명)를 사용하여 인증
  - *IDENTITY: ‘공유 액세스 서명’의 값이 있는 상수*
  - *SECRET:* [‘공유 액세스 서명’](/azure/storage/common/storage-sas-overview)은 ‘스토리지 계정의 리소스에 대한 위임된 액세스 권한을 제공합니다.’  
  - 필요한 최소 권한: 읽기, 나열, 쓰기, 만들기, 삭제
  
- [*서비스 사용자*](/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store#create-a-credential)로 인증
  - *IDENTITY: <ClientID>@<OAuth_2.0_Token_EndPoint>*
  - *SECRET: AAD 애플리케이션 서비스 주체 키*
  - 필요한 최소 RBAC 역할: Storage Blob 데이터 기여자 또는 Storage Blob 데이터 소유자
  
> [!NOTE]  
> OAuth 2.0 토큰 엔드포인트 **V1** 사용

- Storage 계정 키를 사용하여 인증
  - *IDENTITY: ‘Storage 계정 키’의 값이 있는 상수*
  - *SECRET: 스토리지 계정 키*
  
- [관리 ID](/azure/sql-data-warehouse/load-data-from-azure-blob-storage-using-polybase#authenticate-using-managed-identities-to-load-optional)(VNet 서비스 엔드포인트)를 사용하여 인증
  - *IDENTITY: ‘관리 ID’ 값이 있는 상수*
  - 필요한 최소 RBAC 역할: Storage Blob 데이터 기여자 또는 AAD 등록 SQL Database 서버용 Storage Blob 데이터 소유자
  
- AAD 사용자로 인증
  - *자격 증명이 필요하지 않음*
  - 필요한 최소 RBAC 역할: Storage Blob 데이터 기여자 또는 AAD 사용자용 Storage Blob 데이터 소유자

> [!NOTE]  
> ERRORFILE에 동일한 스토리지 계정을 사용하고 컨테이너 루트에 상대적인 ERRORFILE 경로를 지정하는 경우 ERROR_CREDENTIAL을 지정할 필요가 없습니다.

*MAXERRORS = max_errors*</br>
*MAXERRORS*는 COPY 작업이 취소되기 전에 로드에서 허용되는 최대 거부 행 수를 지정합니다. COPY 작업으로 가져올 수 없는 각 행은 무시되고 하나의 오류로 계산됩니다. max_errors를 지정하지 않으면 기본값은 0입니다.

*COMPRESSION = { 'DefaultCodec '| ’Snappy’ | ‘GZIP’ | ‘NONE’}*</br>
*COMPRESSION*은 선택 사항이며 외부 데이터에 대한 데이터 압축 메서드를 지정합니다.

- CSV에서 GZIP 지원
- Parquet은 GZIP 및 Snappy를 지원합니다.
- ORC는 DefaultCodec 및 Snappy를 지원합니다.
- Zlib는 ORC의 기본 압축입니다.

COPY 명령은 이 매개 변수가 지정되지 않은 경우 파일 확장명에 따라 압축 유형을 자동으로 검색합니다.

- .gz  - **GZIP**
- .snappy – **Snappy**
- .deflate - **DefaultCodec**(Parquet 및 ORC만 해당)

 *FIELDQUOTE = 'field_quote'*</br>
*FIELDQUOTE*는 CSV에 적용되며 CSV 파일에서 따옴표 문자(문자열 구분 기호)로 사용될 단일 문자를 지정합니다. 지정하지 않으면 RFC 4180 표준에 정의한 대로 따옴표 문자(")가 따옴표 문자로 사용됩니다. 확장 ASCII 및 멀티바이트 문자는 FIELDQUOTE의 UTF-8에 지원되지 않습니다.

> [!NOTE]  
> FIELDQUOTE 문자는 이중 FIELDQUOTE(구분 기호)가 있는 문자열 열에서 이스케이프됩니다. 

*FIELDTERMINATOR = 'field_terminator’*</br>
*FIELDTERMINATOR* CSV에만 적용됩니다. CSV 파일에서 사용될 필드 종결자를 지정합니다. 16진수 표기법을 사용하여 필드 종결자를 지정할 수 있습니다. 필드 종결자는 여러 문자일 수 있습니다. 기본 필드 종결자는 (,)입니다. 확장 ASCII 및 멀티바이트 문자는 FIELDTERMINATOR의 UTF-8에 지원되지 않습니다.

ROW TERMINATOR = 'row_terminator'</br>
*ROW TERMINATOR* CSV에만 적용됩니다. CSV 파일에서 사용될 행 종결자를 지정합니다. 16진수 표기법을 사용하여 행 종결자를 지정할 수 있습니다. 행 종결자는 여러 문자일 수 있습니다. 기본적으로 행 종결자는 \r\n입니다. 

COPY 명령은 \n(줄 바꿈)을 지정할 때 \r 문자를 접두사하여 \r\n을 생성합니다. \n 문자만 지정하려면 16진수 표기법(0x0A)을 사용합니다. 다중 문자 행 종결자를 16진수로 지정할 때 각 문자 사이에 0x를 지정하지 마세요.

확장 ASCII 및 멀티바이트 문자는 ROW TERMINATOR의 UTF-8에 지원되지 않습니다.

*FIRSTROW  = First_row_int*</br>
*FIRSTROW*는 CSV에 적용되며 COPY 명령의 모든 파일에서 먼저 읽을 행 번호를 지정합니다. 값은 1부터 시작되며 이것이 기본값입니다. 값이 2로 설정되면 데이터를 로드할 때 모든 파일의 첫 행(헤더 행)을 건너뜁니다. 행 종결자의 존재에 따라 행을 건너뜁니다.

*DATEFORMAT = { ‘mdy’ | ‘dmy’ | ‘ymd’ | ‘ydm’ | ‘myd’ | ‘dym’ }*</br>
DATEFORMAT은 CSV에만 적용되며 SQL Server 날짜 형식에 대한 날짜 매핑의 날짜 형식을 지정합니다. 모든 Transact-SQL 날짜/시간 데이터 형식 및 함수에 대한 개요는 [날짜/시간 데이터 형식 및 함수(Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md?view=sql-server-ver15)를 참조하세요. COPY 명령 내의 DATEFORMAT은 [세션 수준에서 구성된 DATEFORMAT](set-dateformat-transact-sql.md?view=sql-server-ver15)보다 우선합니다.

*ENCODING = ‘UTF8’ | ‘UTF16’*</br>
*ENCODING*은 CSV에만 적용됩니다. 기본값은 UTF8입니다. COPY 명령으로 로드된 파일의 데이터 인코딩 표준을 지정합니다. 

*IDENTITY_INSERT = ‘ON’ | ‘OFF’*</br>
IDENTITY_INSERT는 가져온 데이터 파일의 ID 값 또는 값을 ID 열에 사용할지 여부를 지정합니다. IDENTITY_INSERT가 OFF(기본값)이면 이 열의 ID 값은 확인되지만 가져오지는 않습니다. SQL DW는 테이블 생성 중에 지정된 시드 및 증분 값을 기준으로 고유 값을 자동으로 할당합니다. COPY 명령을 사용하여 다음 동작을 기록합니다.

- IDENTITY_INSERT가 OFF이고 테이블에 ID 열이 있는 경우
  - 입력 필드를 ID 열에 매핑하지 않는 열 목록을 지정해야 합니다.
- IDENTITY_INSERT가 ON이고 테이블에 ID 열이 있는 경우
  - 열 목록이 전달되면 입력 필드를 ID 열에 매핑해야 합니다.
- 열 목록의 IDENTITY COLUMN에 대한 기본값은 지원되지 않습니다.
- IDENTITY_INSERT는 한 번에 하나의 테이블에 대해서만 설정할 수 있습니다.

### <a name="permissions"></a>사용 권한  

복사 명령을 실행하는 사용자는 다음 권한을 가지고 있어야 합니다. 

- [ADMINISTER DATABASE BULK OPERATIONS](grant-database-permissions-transact-sql.md?view=azure-sqldw-latest#remarks)
- [INSERT ](grant-database-permissions-transact-sql.md?view=azure-sqldw-latest#remarks)

INSERT 및 ADMINISTER BULK OPERATIONS 권한이 필요합니다. Azure SQL Data Warehouse에서는 INSERT 및 ADMINISTER DATABASE BULK OPERATIONS 권한이 필요합니다.

## <a name="examples"></a>예  

### <a name="a-load-from-a-public-storage-account"></a>A. 퍼블릭 스토리지 계정에서 로드

다음 예제는 퍼블릭 스토리지 계정에서 데이터를 로드하는 COPY 명령의 가장 간단한 형태입니다. 이 예제에서 COPY 문의 기본값은 줄 항목 csv 파일의 형식과 일치합니다.

```sql
COPY INTO dbo.[lineitem] FROM 'https://unsecureaccount.blob.core.windows.net/customerdatasets/folder1/lineitem.csv'
```

COPY 명령의 기본값은 다음과 같습니다.

- DATEFORMAT = Session DATEFORMAT 

- MAXERRORS = 0

- 압축 기본값은 압축되지 않음

- FIELDQUOTE = “” 

- FIELDTERMINATOR = “,” 

- ROWTERMINATOR = ‘\n'

> [!IMPORTANT]
> COPY는 내부적으로 ‘\n’을 ‘\r\n’으로 처리합니다. 자세한 내용은 ROWTERMINATOR 섹션을 참조하세요.

- FIRSTROW = 1

- ENCODING = ‘UTF8’

- FILE_TYPE = ‘CSV’

- IDENTITY_INSERT = ‘OFF’

### <a name="b-load-authenticating-via-share-access-signature-sas"></a>B. SAS(공유 액세스 서명)를 통한 로드 인증

다음 예제에서는 UNIX 출력과 같은 행 종결자로 줄 바꿈을 사용하는 파일을 로드합니다. 이 예제에서는 SAS 키를 사용하여 Azure Blob 스토리지에 대해서도 인증합니다.

```sql
COPY INTO test_1
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/'
WITH (
    FILE_TYPE = 'CSV',
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>'),
    --CREDENTIAL should look something like this:
    --CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='?sv=2018-03-28&ss=bfqt&srt=sco&sp=rl&st=2016-10-17T20%3A14%3A55Z&se=2021-10-18T20%3A19%3A00Z&sig=IEoOdmeYnE9%2FKiJDSHFSYsz4AkNa%2F%2BTx61FuQ%2FfKHefqoBE%3D'),
    FIELDQUOTE = '"',
    FIELDTERMINATOR=';',
    ROWTERMINATOR='0X0A',
    ENCODING = 'UTF8',
    DATEFORMAT = 'ymd',
    MAXERRORS = 10,
    ERRORFILE = '/errorsfolder/',--path starting from the storage container
    IDENTITY_INSERT = 'ON'
)
```

### <a name="c-load-with-a-column-list-with-default-values-authenticating-via-storage-account-key"></a>C. 스토리지 계정 키를 통해 인증되는 기본값이 있는 열 목록으로 로드

이 예제에서는 기본값을 사용하여 열 목록을 지정하는 파일을 로드합니다. 

```sql
--Note when specifying the column list, input field numbers start from 1
COPY INTO test_1 (Col_one default 'myStringDefault' 1, Col_two default 1 3)
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/'
WITH (
    FILE_TYPE = 'CSV',
    CREDENTIAL=(IDENTITY= 'Storage Account Key', SECRET='<Your_Account_Key>'),
    --CREDENTIAL should look something like this:
    --CREDENTIAL=(IDENTITY= 'Storage Account Key', SECRET='x6RWv4It5F2msnjelv3H4DA80n0PQW0daPdw43jM0nyetx4c6CpDkdj3986DX5AHFMIf/YN4y6kkCnU8lb+Wx0Pj+6MDw=='),
    FIELDQUOTE = '"',
    FIELDTERMINATOR=',',
    ROWTERMINATOR='0x0A',
    ENCODING = 'UTF8',
    FIRSTROW = 2
)
```

### <a name="d-load-parquet-or-orc-using-existing-file-format-object"></a>D. 기존 파일 형식 개체를 사용하여 Parquet 또는 ORC 로드

 이 예제에서는 와일드카드를 사용하여 폴더 아래에 있는 모든 parquet 파일을 로드합니다. 

```sql
COPY INTO test_parquet
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/*.parquet'
WITH (
    FILE_FORMAT = myFileFormat
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>')
)
```

### <a name="e-load-specifying-wild-cards-and-multiple-files"></a>E. 와일드카드 및 여러 파일을 지정하여 로드

```sql
COPY INTO t1
FROM 
'https://myaccount.blob.core.windows.net/myblobcontainer/folder0/*.txt', 
    'https://myaccount.blob.core.windows.net/myblobcontainer/folder1'
WITH ( 
    FILE_TYPE = 'CSV'
    CREDENTIAL=(IDENTITY= '<client_id>@<OAuth_2.0_Token_EndPoint>',SECRET='<key>'),
    FIELDTERMINATOR = '|'
)
```

## <a name="faq"></a>FAQ

### <a name="what-is-the-performance-of-the-copy-command-compared-to-polybase"></a>PolyBase 대비 COPY 명령의 성능은 어떤가요?
COPY 명령은 워크로드에 따라 성능이 향상됩니다. 퍼블릭 미리 보기 중에 최상의 로드 성능을 얻으려면 CSV를 로드할 때 입력을 여러 개의 파일로 분할하는 것이 좋습니다. 미리 보기 기간 동안 Microsoft 팀과 성능 결과를 공유하세요! sqldwcopypreview@service.microsoft.com

### <a name="what-is-the-file-splitting-guidance-for-the-copy-command-loading-csv-files"></a>CSV 파일을 로드하는 COPY 명령의 파일 분할 지침은 무엇인가요?
파일 수에 대한 지침은 아래 표에 나와 있습니다. 권장 파일 수에 도달하면 파일이 클수록 성능이 향상됩니다. 간단한 파일 분할 환경을 보려면 다음 [설명서](https://techcommunity.microsoft.com/t5/azure-synapse-analytics/how-to-maximize-copy-load-throughput-with-file-splits/ba-p/1314474)를 참조하세요. 

| **DWU** | **#Files** |
| :-----: | :--------: |
|   100   |     60     |
|   200   |     60     |
|   300   |     60     |
|   400   |     60     |
|   500   |     60     |
|  1,000  |    120     |
|  1,500  |    180     |
|  2,000  |    240     |
|  2,500  |    300     |
|  3,000  |    360     |
|  5,000  |    600     |
|  6,000  |    720     |
|  7,500  |    900     |
| 10000  |    1200    |
| 15,000  |    1800    |
| 30,000  |    3600    |


### <a name="what-is-the-file-splitting-guidance-for-the-copy-command-loading-parquet-or-orc-files"></a>Parquet 또는 ORC 파일을 로드하는 COPY 명령의 파일 분할 지침은 무엇인가요?
Parquet 및 ORC 파일은 COPY 명령이 자동으로 분할하기 때문에 파일을 분할할 필요가 없습니다. 최상의 성능을 얻으려면 Azure Storage 계정의 Parquet 및 ORC 파일이 256MB 이상이어야 합니다. 

### <a name="when-will-the-copy-command-be-generally-available"></a>COPY 명령은 언제 출시되나요?
COPY 명령은 올해(2020년) 말에 출시될 예정입니다. 

### <a name="are-there-any-known-issues-with-the-copy-command"></a>COPY 명령에 알려진 문제가 있나요?

- (n)varchar(max)와 같은 LOB 지원은 COPY 문에서 사용할 수 없습니다. 이 기능은 내년 초에 제공될 예정입니다.

피드백이나 문제가 있으면 배포 목록(sqldwcopypreview@service.microsoft.com)으로 보내주세요.

## <a name="see-also"></a>참고 항목  

 [SQL Data Warehouse를 사용하여 개요 로드](/azure/sql-data-warehouse/design-elt-data-loading)
