---
title: "대량 삽입 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BULK_TSQL
- BULK INSERT
- BULK_INSERT_TSQL
- BULK
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
caps.latest.revision: 153
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80b16fd446ff72c6a673a576d9a8deb9514be8b2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터 파일을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자가 지정한 형식으로 데이터베이스 테이블이나 뷰로 가져옵니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
BULK INSERT   
   [ database_name . [ schema_name ] . | schema_name . ] [ table_name | view_name ]   
      FROM 'data_file'   
     [ WITH   
    (   
   [ [ , ] BATCHSIZE = batch_size ]   
   [ [ , ] CHECK_CONSTRAINTS ]   
   [ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ [ , ] DATAFILETYPE =   
      { 'char' | 'native'| 'widechar' | 'widenative' } ]   
   [ [ , ] DATASOURCE = 'data_source_name' ]
   [ [ , ] ERRORFILE = 'file_name' ]
   [ [ , ] ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ [ , ] FIRSTROW = first_row ]   
   [ [ , ] FIRE_TRIGGERS ]   
   [ [ , ] FORMATFILE_DATASOURCE = 'data_source_name' ]
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
  
## <a name="arguments"></a>인수  
 *database_name*  
 지정한 테이블이나 뷰가 상주하는 데이터베이스 이름입니다. 지정하지 않으면 기본값은 현재 데이터베이스입니다.  
  
 *schema_name*  
 테이블 또는 뷰 스키마의 이름입니다. *schema_name* 경우 대량 가져오기 작업을 수행 하는 사용자에 대 한 기본 스키마가 지정 된 테이블 또는 뷰의 스키마는 선택 사항입니다. 경우 *스키마* 지정 하지 않으면이 고 대량 가져오기 작업을 수행 하는 사용자의 기본 스키마가 지정한 테이블이 나 뷰, 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 하는 오류 메시지와 대량 가져오기 작업이 취소 됩니다.  
  
 *table_name*  
 데이터를 대량으로 가져올 테이블 또는 뷰의 이름입니다. 모든 열이 동일한 기본 테이블을 참조하는 뷰만 사용할 수 있습니다. 뷰로 데이터를 로드에 대 한 제한에 대 한 자세한 내용은 참조 [insert&#40; Transact SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
 **'** *data_file* **'**  
 지정한 테이블이나 뷰로 가져올 데이터가 포함된 데이터 파일의 전체 경로입니다. BULK INSERT는 디스크(예: 네트워크, 플로피 디스크, 하드 디스크 등)에서 데이터를 가져올 수 있습니다.   
 
 *data_file* 에 서버에서 유효한 경로 지정 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 합니다. 경우 *data_file* 이 원격 파일, 범용 명명 규칙 (UNC) 이름을 지정 합니다. UNC 이름은 \\ \\ *Systemname*\\*ShareName*\\*경로* \\ *FileName*합니다. `\\SystemX\DiskZ\Sales\update.txt`)을 입력합니다.   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP1.1는 data_file Azure blob 저장소에 있을 수 있습니다.

**'** *data_source_name* **'**   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
명명 된 외부 데이터 원본에 가져올 파일의 Azure Blob 저장소 위치를 가리킵니다. 외부 데이터 원본을 사용 하 여 만들어야는 `TYPE = BLOB_STORAGE` 옵션에 추가 된 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. 자세한 내용은 참조 [외부 데이터 원본 만들기](../../t-sql/statements/create-external-data-source-transact-sql.md)합니다.    
  
 BATCHSIZE  **=**  *batch_size*  
 일괄 처리에 포함될 행 수를 지정합니다. 모든 일괄 처리는 하나의 트랜잭션으로 서버에 복사됩니다. 이 작업이 실패하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모든 일괄 처리에 대한 트랜잭션을 커밋하거나 롤백합니다. 기본적으로 지정된 데이터 파일의 모든 데이터는 하나의 일괄 처리입니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 CHECK_CONSTRAINTS  
 대량 가져오기 작업 중 대상 테이블 또는 뷰의 모든 제약 조건을 검사하도록 지정합니다. CHECK_CONSTRAINTS 옵션을 지정하지 않으면 모든 CHECK 및 FOREIGN KEY 제약 조건이 무시되고 작업 이후 테이블의 제약 조건은 트러스트될 수 없는 것으로 표시됩니다.  
  
> [!NOTE]  
>  UNIQUE 및 PRIMARY KEY 제약 조건은 항상 적용됩니다. NOT NULL 제약 조건으로 정의된 문자 열로 가져올 때 텍스트 파일에 값이 없으면 BULK INSERT는 공백 문자열을 삽입합니다.  
  
 특정 지점에서는 전체 테이블의 제약 조건을 확인해야 합니다. 대량 가져오기 작업을 수행하기 전에 테이블이 비어 있지 않으면 제약 조건의 유효성을 다시 검사하는 비용이 증분 데이터에 CHECK 제약 조건을 적용하는 비용을 초과할 수 있습니다.  
  
 입력 데이터에 제약 조건을 위반하는 행이 포함된 경우에는 제약 조건을 사용하지 않을 수 있습니다(기본 동작). CHECK 제약 조건을 사용하지 않으면 데이터를 가져온 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 잘못된 데이터를 제거할 수 있습니다.  
  
> [!NOTE]  
>  MAXERRORS 옵션은 제약 조건 확인에 적용되지 않습니다.  
  
 코드 페이지  **=**  { **'**ACP**'** | **'**OEM**'**  |  **'**RAW**'** | **'***code_page***'** }  
 데이터 파일에서 데이터의 코드 페이지를 지정합니다. 코드 페이지와 데이터를 포함 하는 경우에 관련 된 **char**, **varchar**, 또는 **텍스트** 보다 큰 문자 값을 갖는 열 **127** 이하의 보다 **32**합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)]각 열에 대 한 데이터 정렬 이름을 지정 하는 것을 권장 한 [서식 파일](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)합니다.  
  
|CODEPAGE 값|Description|  
|--------------------|-----------------|  
|ACP|열 **char**, **varchar**, 또는 **텍스트** 데이터 형식에서 변환 됩니다는 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] / [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 코드 페이지 (ISO 1252)에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지입니다.|  
|OEM(기본값)|열 **char**, **varchar**, 또는 **텍스트** 를 시스템 OEM 코드 페이지에서 데이터 형식 변환 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지입니다.|  
|RAW|다른 코드 페이지로의 변환이 이루어지지 않는 가장 빠른 옵션입니다.|  
|*code_page*|특정 코드 페이지 번호(예: 850)입니다.<br /><br /> **\*\*중요 한 \* \***  이전 버전을 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 코드 페이지 65001 (utf-8 인코딩)을 지원 하지 않습니다.|  
  
 DATAFILETYPE  **=**  { **'char'** | **'native'** | **'widechar'**  |  **'widenative'** }  
 BULK INSERT에서 지정된 데이터 파일 유형 값을 사용하여 가져오기 작업을 수행하도록 지정합니다.  
  
|DATAFILETYPE 값|모든 데이터 표시 형식|  
|------------------------|------------------------------|  
|**char** (기본값)|문자 형식<br /><br /> 자세한 내용은 [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.|  
|**네이티브**|네이티브(데이터베이스) 데이터 형식. 대량으로 데이터를 가져와 네이티브 데이터 파일을 만들 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하는 **bcp** 유틸리티입니다.<br /><br /> 네이티브 값은 char 값을 대체하여 보다 뛰어난 성능을 제공합니다.<br /><br /> 자세한 내용은 [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)를 참조하세요.|  
|**widechar**|유니코드 문자<br /><br /> 자세한 내용은 [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.|  
|**widenative**|네이티브 (데이터베이스) 데이터 형식을 제외 하 고 **char**, **varchar**, 및 **텍스트** 열, 데이터는 유니코드로 저장 합니다. 만들기는 **widenative** 데이터 파일에서 데이터 대량 가져오기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하는 **bcp** 유틸리티입니다.<br /><br /> **widenative** 값이 제공 하는 더 높은 성능 대신 **widechar**합니다. 데이터 파일에 포함 하는 경우 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] 확장 문자가 지정 **widenative**합니다.<br /><br /> 자세한 내용은 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)을 참조하세요.|  
  
  ERRORFILE **='***file_name***'**  
 형식 오류가 있어 OLE DB 행 집합으로 변환할 수 없는 행을 수집하는 데 사용되는 파일을 지정합니다. 이러한 행은 데이터 파일에서 "있는 그대로" 이 오류 파일에 복사됩니다.  
  
 오류 파일은 명령이 실행될 때 생성됩니다. 파일이 이미 있으면 오류가 발생합니다. 또한 확장명이 .ERROR.txt인 제어 파일이 생성됩니다. 이 파일은 오류 파일의 각 행을 참조하여 오류를 진단합니다. 오류를 해결하는 즉시 데이터를 로드할 수 있습니다.   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], `error_file_path` Azure blob 저장소에 있을 수 있습니다.

' errorfile_data_source_name'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
명명 된 외부 데이터 소스는 가져오기 중 발견 된 오류가 포함 될 오류 파일의 Azure Blob 저장소 위치를 가리킵니다. 외부 데이터 원본을 사용 하 여 만들어야는 `TYPE = BLOB_STORAGE` 옵션에 추가 된 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. 자세한 내용은 참조 [외부 데이터 원본 만들기](../../t-sql/statements/create-external-data-source-transact-sql.md)합니다.
 
 FIRSTROW  **=**  *first_row*  
 로드할 첫 번째 행의 번호를 지정합니다. 기본값은 지정한 데이터 파일의 첫 번째 행입니다. FIRSTROW는 1부터 시작합니다.  
  
> [!NOTE]  
>  FIRSTROW 특성은 열 머리글을 건너뛰기 위해 제공된 것이 아닙니다. BULK INSERT 문에서는 머리글 건너뛰기가 지원되지 않습니다. 행을 건너뛰면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 필드 종결자만 확인하며 건너뛴 행의 필드에 있는 데이터의 유효성을 검사하지 않습니다.  
  
 FIRE_TRIGGERS  
 대량 가져오기 작업 중에 대상 테이블에서 정의된 삽입 트리거가 실행되도록 지정합니다. 트리거가 대상 테이블의 INSERT 작업에 대해 정의되면 완료된 모든 일괄 처리에 대해 발생합니다.  
  
 FIRE_TRIGGERS를 지정하지 않으면 삽입 트리거가 실행되지 않습니다.  

FORMATFILE_DATASOURCE  **=**  'data_source_name'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1.   
명명 된 외부 데이터 소스는 가져온된 데이터의 스키마를 정의 하는 서식 파일의 Azure Blob 저장소 위치를 가리킵니다. 외부 데이터 원본을 사용 하 여 만들어야는 `TYPE = BLOB_STORAGE` 옵션에 추가 된 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. 자세한 내용은 참조 [외부 데이터 원본 만들기](../../t-sql/statements/create-external-data-source-transact-sql.md)합니다.
  
 KEEPIDENTITY  
 가져온 데이터 파일의 ID 값이 ID 열에 사용되도록 지정합니다. KEEPIDENTITY를 지정하지 않는 경우 이 열의 ID 값을 확인하지만 가져오지는 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 테이블 생성 중에 지정된 초기값 및 증가값에 따라 고유한 값을 자동으로 할당합니다. 데이터 파일에 테이블이나 뷰의 ID 열 값이 포함되지 않은 경우 서식 파일을 사용하여 데이터를 가져올 때 테이블이나 뷰의 ID 열을 생략하도록 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 해당 열에 고유한 값을 자동으로 할당합니다. 자세한 내용은 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)를 참조하세요.  
  
 자세한 내용은 유지에 대 한 식별 값 참조 [유지 Identity 값 데이터 대량 가져오기 &#40; SQL Server &#41; ](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 KEEPNULLS  
 대량 가져오기 작업 시 삽입된 열에 기본값이 지정되지 않도록 하고, 빈 열이 Null 값을 보유하도록 지정합니다. 자세한 내용은 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)을 참조하세요.  
  
 KILOBYTES_PER_BATCH  **=**  *kilobytes_per_batch*  
 크기 (KB)로 일괄 처리당 데이터의 대략적인 수를 지정 *kilobytes_per_batch*합니다. 기본적으로 KILOBYTES_PER_BATCH는 알 수 없습니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 LASTROW**=***last_row*  
 로드할 마지막 행의 번호를 지정합니다. 기본값은 0이며 지정한 데이터 파일의 마지막 행을 가리킵니다.  
  
 MAXERRORS  **=**  *max_errors*  
 대량 가져오기 작업을 취소하기 전에 데이터에서 허용되는 최대 구문 오류 수를 지정합니다. 대량 가져오기 작업으로 가져올 수 없는 각 행은 무시되고 하나의 오류로 계산됩니다. 경우 *max_errors* 를 지정 하지 않으면 기본값은 10입니다.  
  
> [!NOTE]  
>  MAX_ERRORS 옵션에는 제약 조건 확인 이나 변환에 적용 되지 않습니다 **money** 및 **bigint** 데이터 형식입니다.  
  
 순서 ({ *열* [ASC | DESC]} [ **,**... *n* ] )  
 데이터 파일의 데이터 정렬 방법을 지정합니다. 가져올 데이터를 테이블의 클러스터형 인덱스(있는 경우)에 따라 정렬하면 대량 가져오기 성능이 향상됩니다. 데이터 파일을 클러스터형 인덱스 키와 다른 순서로 정렬하거나 테이블에 클러스터형 인덱스가 없으면 ORDER 절이 무시됩니다. 지정한 열 이름은 대상 테이블에서 올바른 열 이름이어야 합니다. 기본적으로 대량 삽입 작업은 데이터 파일이 정렬되지 않았음을 전제로 합니다. 대량 가져오기 작업을 최적화하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 가져온 데이터가 정렬되어 있는지도 확인합니다.  
  
 *n*  
 복수 열을 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
 ROWS_PER_BATCH  **=**  *rows_per_batch*  
 데이터 파일에 있는 대략적인 데이터 행 수를 나타냅니다.  
  
 기본적으로 데이터 파일의 모든 데이터는 단일 트랜잭션으로 서버에 전송되며 일괄 처리의 행 수는 쿼리 최적화 프로그램에 알려지지 않습니다. ROWS_PER_BATCH를 0보다 큰 값으로 지정하면 서버에서 이 값을 사용하여 대량 가져오기 작업을 최적화합니다. ROWS_PER_BATCH에 지정된 값은 실제 행 수와 대략적으로 동일해야 합니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 
 TABLOCK  
 대량 가져오기 작업이 진행되는 동안 테이블 수준 잠금을 획득하도록 지정합니다. 테이블에 인덱스가 없고 TABLOCK이 지정되어 있으면 여러 클라이언트가 동시에 테이블을 로드할 수 있습니다. 기본적으로 잠금 동작은 **table lock on bulk load**테이블 옵션에 의해 결정됩니다. 대량 가져오기 작업이 진행되는 동안에만 잠금을 보유하면 테이블에 대한 잠금 경합이 줄어들고 이 경우 성능이 크게 향상됩니다. 성능 고려 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 Columnstore 인덱스. 내부적으로 여러 행 집합으로 구분 하기 때문에 잠금 동작 차이가 있습니다.  각 스레드는 동시 데이터 로드 세션을 갖는 병렬 데이터 로드를 허용 하는 행 집합에 X 잠금을 수행 하 여 각 행 집합에 단독으로 데이터를 로드 합니다. TABLOCK 옵션을 사용할 다른 동시 스레드를 동시에 데이터 로드 수행 되지 것입니다 (달리 기존의 행 집합에 대 한 BU 잠금) 테이블에 대해 X 잠금을 수행 하는 스레드를 발생 합니다.  

### <a name="input-file-format-options"></a>입력된 파일 형식 옵션입니다.
  
형식  **=**  'CSV'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
쉼표로 구분 된 값 파일에 규정 지정는 [RFC 4180](https://tools.ietf.org/html/rfc4180) 표준입니다.

FIELDQUOTE  **=**  'field_quote'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
CSV 파일의 따옴표 문자로 사용 될 문자를 지정 합니다. 에 정의 된 대로 인용 문자 (") 따옴표 문자로 사용될지를 지정 하지는 [RFC 4180](https://tools.ietf.org/html/rfc4180) 표준입니다.
  
 FORMATFILE **='***format_file_path***'**  
 서식 파일의 전체 경로를 지정합니다. 사용 하 여 생성 된 저장된 응답을 포함 하는 데이터 파일을 설명 하는 서식 파일의 **bcp** 유틸리티에서 동일한 테이블 또는 뷰. 다음과 같은 경우에 서식 파일이 사용됩니다.  
  
-   데이터 파일의 열이 테이블 또는 뷰보다 많거나 적을 경우  
  
-   열 순서가 다를 경우  
  
-   열 구분 기호가 다를 경우  
  
-   데이터 서식에 기타 변경 내용이 있을 경우. 서식 파일은 일반적으로 사용 하 여 생성 된 **bcp** 유틸리티 및 필요에 따라 텍스트 편집기로 수정 합니다. 자세한 내용은 [bcp Utility](../../tools/bcp-utility.md)를 참조하세요.  

**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1는 format_file_path Azure blob 저장소에 있을 수 있습니다.

 FIELDTERMINATOR **='***field_terminator***'**  
 에 사용할 필드 종결자 지정 **char** 및 **widechar** 데이터 파일. 기본 필드 종결자는 \t(탭 문자)입니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  

 ROWTERMINATOR **='***row_terminator***'**  
 에 사용할 행 종결자 지정 **char** 및 **widechar** 데이터 파일. 기본 행 종결자는 **\r\n** (줄 바꿈 문자)입니다.  자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  

  
## <a name="compatibility"></a>호환성  
 BULK INSERT는 파일에서 읽은 데이터에 엄격한 데이터 유효성 검사 및 데이터 검사를 강제로 실행합니다. 이로 인해 기존 스크립트가 잘못된 데이터에서 실행되면 오류가 발생할 수 있습니다. 예를 들어 BULK INSERT는 다음을 확인합니다.  
  
-   네이티브 표시가 **float** 또는 **실제** 데이터 형식을 사용할 수 있습니다.  
  
-   유니코드 데이터의 길이가 짝수 바이트인지 여부  
  
## <a name="data-types"></a>데이터 형식  
  
### <a name="string-to-decimal-data-type-conversions"></a>String 데이터 형식에서 Decimal 데이터 형식으로의 변환  
 BULK INSERT에 사용 되는 문자열에서 decimal 데이터 형식 변환이 동일한 규칙을 따르며는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [변환](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수 과학적 표기법을 사용 하는 숫자 값을 나타내는 문자열을 거부 합니다. 따라서 BULK INSERT는 이러한 문자열을 잘못된 값으로 처리하고 변환 오류를 보고합니다.  
  
 이 문제를 해결 하려면 사용 하 여 서식 파일을 대량 가져오기 과학적 표기법 **float** 10 진수 열에 데이터를 합니다. 서식 파일에서 열을 명시적으로 설명 **실제** 또는 **float** 데이터입니다. 이러한 데이터 형식에 대 한 자세한 내용은 참조 하십시오. [float 및 real &#40; Transact SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
> [!NOTE]  
>  서식 파일을 나타내며 **실제** 으로 데이터는 **SQLFLT4** 데이터 형식 및 **float** 으로 데이터는 **SQLFLT8** 데이터 형식입니다. 비 XML 서식 파일에 대 한 정보를 참조 하세요. [bcp &#40;를 사용 하 여 파일 저장 유형 지정 SQL Server &#41; ](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>과학적 표기법을 사용하는 숫자 값 가져오기 예  
 이 예에서는 다음 테이블을 사용합니다.  
  
```  
CREATE TABLE t_float(c1 float, c2 decimal (5,4));  
```  
  
 사용자가 `t_float` 테이블로 데이터를 대량 가져오려고 합니다. 과학적 표기법을 포함 하는 데이터 파일 C:\t_float-c.dat에 **float** 데이터; 예:  
  
```  
8.0000000000000002E-28.0000000000000002E-2  
```  
  
 그러나 두 번째 열 `t_float`에서 `c2` 데이터 형식을 사용하므로 BULK INSERT는 이 데이터를 직접 `decimal`으로 가져올 수 없습니다. 따라서 서식 파일이 필요합니다. 서식 파일은 과학적 표기법 매핑해야 **float** 데이터를 decimal 형식 열의 `c2`합니다.  
  
 다음 서식 파일은 `SQLFLT8` 데이터 형식을 사용하여 두 번째 데이터 필드를 두 번째 열로 매핑합니다.  
  
 ```
 <?xml version="1.0"?> 
 <BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
 <RECORD> 
 <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/> 
 <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/>  </RECORD>  <ROW> 
 <COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/> 
 <COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/>  </ROW> </BCPFORMAT> 
 ```
  
 이 서식 파일(`C:\t_floatformat-c-xml.xml`)을 사용하여 테스트 데이터를 테스트 테이블로 가져오려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
```  
BULK INSERT bulktest..t_float  
FROM 'C:\t_float-c.dat' WITH (FORMATFILE='C:\t_floatformat-c-xml.xml');  
GO  
```  
  
### <a name="data-types-for-bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML 문서 대량 내보내기 또는 가져오기를 위한 데이터 형식  
 SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다.  
  
|데이터 형식|영향|  
|---------------|------------|  
|SQLCHAR 또는 SQLVARCHAR|데이터를 클라이언트 코드 페이지나 데이터 정렬에 포함된 코드 페이지로 보냅니다. 효과 DATAFILETYPE을 지정 하는 것과 같습니다 **'char' =** 서식 파일을 지정 하지 않고 있습니다.|  
|SQLNCHAR 또는 SQLNVARCHAR|데이터를 유니코드로 보냅니다. 효과 DATAFILETYPE을 지정 하는 것과 같습니다 **= 'widechar'** 서식 파일을 지정 하지 않고 있습니다.|  
|SQLBINARY 또는 SQLVARYBIN|데이터를 변환하지 않고 보냅니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 BULK INSERT 문, INSERT ... 선택 \* 에서 openrowset (bulk) 문 및 **bcp** 명령에서 참조 [대량 가져오기 및 데이터의 내보내기 &#40; SQL Server &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 대량 가져오기를 위한 데이터 준비 하는 방법에 대 한 정보를 참조 하세요. [대량 내보내기 또는 가져오기 &#40;에 대 한 데이터 준비 SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 BULK INSERT 문은 데이터를 테이블 또는 뷰로 가져올 사용자 정의 트랜잭션 내에서 실행할 수 있습니다. 필요에 따라 대량 데이터 가져오기를 위한 여러 일치 항목을 사용하려면 트랜잭션에서 BULK INSERT 문 내에 BATCHSIZE 절을 지정할 수 있습니다. 여러 일괄 처리 트랜잭션이 롤백되는 경우에는 트랜잭션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 보낸 모든 일괄 처리가 롤백됩니다.  
  
## <a name="interoperability"></a>상호 운용성  
  
### <a name="importing-data-from-a-csv-file"></a>CSV 파일에서 데이터 가져오기  
부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, BULK INSERT는 CSV 형식을 지원 합니다.  
하기 전에 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 쉼표로 구분 된 값 (CSV) 파일에서 지원 되지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 가져오기 작업입니다. 그러나 경우에 따라 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 대량으로 가져오기 위한 데이터 파일로 CSV(쉼표로 구분된 값) 파일이 사용될 수 있습니다. CSV 데이터 파일에서 데이터를 가져오기 위한 요구 사항에 대 한 정보를 참조 하세요. [대량 내보내기 또는 가져오기 &#40;에 대 한 데이터 준비 SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
## <a name="logging-behavior"></a>로깅 동작  
 대량 가져오기로 수행된 행 삽입 작업이 트랜잭션 로그에 기록되는 경우에 대한 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 선행 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.  
  
##  <a name="Limitations"></a> 제한 사항  
 서식 파일을 BULK INSERT와 함께 사용하면 최대 1024개의 필드만 지정할 수 있습니다. 이는 테이블에 허용된 최대 열 수와 동일합니다. 1024개가 넘는 필드를 포함하는 데이터 파일과 함께 BULK INSERT를 사용하면 BULK INSERT에서 4822 오류를 생성합니다. [bcp 유틸리티](../../tools/bcp-utility.md) 이러한 제한이, 따라서 1024 개가 넘는 필드를 포함 하는 데이터 파일을 사용 하지 않습니다는 **bcp** 명령입니다.  
  
## <a name="performance-considerations"></a>성능 고려 사항  
 단일 일괄 처리에서 플러시될 페이지 수가 내부 임계값을 초과하면 버퍼 풀의 전체 검색이 일괄 처리를 커밋할 때 플러시할 페이지를 식별할 수 있습니다. 이 전체 검색으로 대량 가져오기 성능이 저하될 수 있습니다. 대용량 버퍼 풀이 느린 I/O 하위 시스템과 결합할 때 내부 임계값이 초과될 수 있습니다. 대규모 컴퓨터에서 버퍼 오버플로를 방지하려면 대량 최적화를 제거하는 TABLOCK 힌트를 사용하지 않거나 대량 최적화를 유지하는 보다 작은 크기의 일괄 처리를 사용합니다.  
  
 각 컴퓨터는 서로 다르므로, 데이터 로드로 다양한 일괄 처리 크기를 테스트하여 가장 적합한 크기를 찾는 것이 좋습니다.  
  
## <a name="security"></a>보안  
  
### <a name="security-account-delegation-impersonation"></a>보안 계정 위임(가장)  
 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 계정의 보안 프로필이 사용됩니다. SQL Server 인증을 사용하는 로그인은 데이터베이스 엔진 외부에서 인증될 수 없습니다. 따라서 BULK INSERT 명령이 SQL Server 인증을 사용하는 로그인에 의해 시작되면 데이터에 대한 연결이 SQL Server 프로세스 계정(SQL Server 데이터베이스 엔진 서비스에서 사용하는 계정)의 보안 컨텍스트를 사용하여 설정됩니다. 원본 데이터를 성공적으로 읽으려면 SQL Server 데이터베이스 엔진에서 사용하는 계정에 원본 데이터에 대한 액세스 권한을 부여해야 합니다. 반면에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 Windows 인증을 사용하여 로그온한 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 보안 프로필에 관계없이 해당 사용자 계정으로 액세스할 수 있는 파일만 읽을 수 있습니다.  
  
 사용 하 여 BULK INSERT 문을 실행할 때 **sqlcmd** 또는 **osql**, 한 컴퓨터에서 데이터를 삽입 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 두 번째 컴퓨터에 지정 하는 *data_file* UNC 경로 사용 하 여 세 번째 컴퓨터에서 4861 오류가 나타날 수 있습니다.  
  
 이 오류를 해결 하려면 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 하 고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 보안 프로필을 사용 하는 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스, 계정 또는 보안 계정 위임을 사용 하도록 설정 하는 기간을 구성 합니다. 위임용으로 사용자 계정이 트러스트될 수 있도록 설정하는 방법은 Windows 도움말을 참조하십시오.  
  
 이 및 BULK INSERT를 사용 하기 위한 기타 보안 고려 사항에 대 한 자세한 내용은 참조 [를 사용 하 여 BULK INSERT 또는 openrowset&#40; 하 여 데이터 대량 가져오기 대량... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Permissions  
 INSERT 및 ADMINISTER BULK OPERATIONS 권한이 필요합니다. 또한 다음 중 하나 이상이 적용되는 경우에는 ALTER TABLE 권한이 필요합니다.  
  
-   제약 조건이 있으며 CHECK_CONSTRAINTS 옵션을 지정하지 않았습니다.  
  
    > [!NOTE]  
    >  기본적으로 제약 조건은 사용되지 않습니다. 명시적으로 제약 조건을 확인하려면 CHECK_CONSTRAINTS 옵션을 사용하십시오.  
  
-   트리거가 있으며 FIRE_TRIGGER 옵션을 지정하지 않았습니다.  
  
    > [!NOTE]  
    >  기본적으로 트리거는 실행되지 않습니다. 명시적으로 트리거를 발생시키려면 FIRE_TRIGGER 옵션을 사용하십시오.  
  
-   KEEPIDENTITY 옵션을 사용하여 데이터 파일에서 ID 값을 가져올 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-pipes-to-import-data-from-a-file"></a>1. 파이프를 사용하여 파일에서 데이터 가져오기  
 다음 예에서는 필드 종결자로 파이프(`AdventureWorks2012.Sales.SalesOrderDetail`)를 사용하고 행 종결자로 `|`을 사용하여 지정한 데이터 파일에서 `|\n` 테이블로 주문 세부 정보를 가져옵니다.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH   
      (  
         FIELDTERMINATOR =' |',  
         ROWTERMINATOR =' |\n'  
      );  
```  
  
### <a name="b-using-the-firetriggers-argument"></a>2. FIRE_TRIGGERS 인수 사용  
 다음 예에서는 `FIRE_TRIGGERS` 인수를 지정합니다.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH  
     (  
        FIELDTERMINATOR =' |',  
        ROWTERMINATOR = ':\n',  
        FIRE_TRIGGERS  
      );  
```  
  
### <a name="c-using-line-feed-as-a-row-terminator"></a>3. 행 종결자로 줄 바꿈 사용  
 다음 예에서는 UNIX 출력 같은 행 종결자로 줄 바꿈을 사용하는 파일을 가져옵니다.  
  
```  
DECLARE @bulk_cmd varchar(1000);  
SET @bulk_cmd = 'BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
FROM ''<drive>:\<path>\<filename>''   
WITH (ROWTERMINATOR = '''+CHAR(10)+''')';  
EXEC(@bulk_cmd);  
```  
  
> [!NOTE]  
>  Microsoft Windows에서는 텍스트 파일을 처리 하는 방법으로 인해 **(\n** 으로 자동으로 바뀝니다 **\r\n)**합니다.  
  
### <a name="d-specifying-a-code-page"></a>4. 코드 페이지 지정  
 다음 예제에서는 코드 페이지를 지정 하는 방법을 보여 줍니다.  
  
```  
BULK INSERT MyTable  
FROM 'D:\data.csv'  
WITH  
( CODEPAGE = '65001',  
    DATAFILETYPE = 'char',  
    FIELDTERMINATOR = ','  
);  
```  
### <a name="e-importing-data-from-a-csv-file"></a>5. CSV 파일에서 데이터 가져오기   
다음 예제에서는 CSV 파일을 지정 하는 방법을 보여 줍니다.   
```
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'); 
```

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>6. Azure blob 저장소에 파일에서 데이터 가져오기   
다음 예제에서는 외부 데이터 원본으로 구성 된 Azure blob 저장소 위치에 있는 csv 파일에서 데이터를 로드 하는 방법을 보여 줍니다. 이 공유 액세스 서명을 사용 하 여 데이터베이스 범위 자격 증명이 필요 합니다.    

```tsql
BULK INSERT Sales.Invoices
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
     FORMAT = 'CSV'); 
```

에 대 한 완료 `BULK INSERT` 자격 증명 및 외부 데이터 원본을 구성 하는 등 예제 참조 [예의 대량 데이터에에서 액세스를 Azure Blob 저장소](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)합니다.
  
### <a name="additional-examples"></a>추가 예  
 다른 `BULK INSERT` 예는 다음 항목에서 제공 됩니다.  
  
-   [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [가져오거나 데이터 &#40; 내보내기 위한 서식 파일 SQL Server &#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [대량 내보내기 또는 가져오기 &#40;에 대 한 데이터를 준비 합니다. SQL Server &#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [sp_tableoption &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  

