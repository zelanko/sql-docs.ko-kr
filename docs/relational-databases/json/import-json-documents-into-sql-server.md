---
title: SQL Server에 JSON 문서 가져오기 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
caps.latest.revision: 5
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 726b1d8bf70204912f9ebbf4c2352dcc0dc55fc7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="import-json-documents-into-sql-server"></a>SQL Server에 JSON 문서 가져오기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

이 항목에서는 SQL Server에 JSON 파일을 가져오는 방법을 설명합니다. 현재 많은 JSON 문서가 파일로 저장됩니다. JSON 파일의 응용 프로그램 로그 정보, JSON 파일에 저장된 센서 생성 정보 등을 예로 들 수 있습니다. 파일에 저장된 JSON 데이터를 읽고, 데이터를 SQL Server에 로드하여 분석할 수 있어야 합니다.

## <a name="import-a-json-document-into-a-single-column"></a>단일 열에 JSON 문서 가져오기
**OPENROWSET(BULK)** 는 SQL Server에 해당 위치에 대한 읽기 권한이 있는 경우 로컬 드라이브 또는 네트워크에 있는 모든 파일에서 데이터를 읽을 수 있는 테이블 반환 함수입니다. 파일의 콘텐츠를 포함하는 단일 열로 된 테이블을 반환합니다. 구분 기호 등 OPENROWSET(BULK) 함수에서 사용할 수 있는 다양한 옵션이 있습니다. 하지만 가장 간단하게 파일의 전체 콘텐츠를 텍스트 값으로 로드할 수 있습니다. (이 단일 큰 값을 단일 문자 LOB(Large Object) 또는 SINGLE_CLOB이라고 합니다.) 

다음은 JSON 파일의 콘텐츠를 읽고 단일 값으로 사용자에게 반환하는 **OPENROWSET(BULK)** 함수의 예입니다.

```sql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

OPENJSON(BULK)이 파일의 콘텐츠를 읽고 `BulkColumn`에 반환합니다.

다음 예제에서처럼 파일의 콘텐츠를 지역 변수 또는 테이블로 로드할 수도 있습니다.

```sql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

JSON 파일의 콘텐츠를 로드한 후 JSON 텍스트를 테이블에 저장할 수 있습니다.

## <a name="import-multiple-json-documents"></a>여러 개의 JSON 문서 가져오기
같은 방법을 사용하여 파일 시스템에서 JSON 파일 집합을 지역 변수로 한 번에 하나씩 로드할 수 있습니다. 파일 이름을 `book<index>.json`이라고 가정합니다.
  
```sql
DECLARE @i INT = 1
DECLARE @json AS NVARCHAR(MAX)

WHILE(@i < 10)
BEGIN
    SET @file = 'C:\JSON\Books\book' + cast(@i AS VARCHAR(5)) + '.json';
    SELECT @json = BulkColumn FROM OPENROWSET (BULK (@file), SINGLE_CLOB) AS j
    SELECT * FROM OPENJSON(@json) AS json
    -- Optionally, save the JSON text in a table.
    SET @i = @i + 1 ;
END
```

## <a name="import-json-documents-from-azure-file-storage"></a>Azure File Storage에서 JSON 문서 가져오기
위에서 설명한 대로 OPENROWSET(BULK)을 사용하여 SQL Server가 액세스할 수 있는 파일 위치에서 JSON 파일을 읽을 수도 있습니다. 예를 들어 Azure File Storage는 SMB 프로토콜을 지원합니다. 따라서 다음 절차에 따라 Azure File Storage 공유에 로컬 가상 드라이브를 매핑할 수 있습니다.
1.  Azure Portal 또는 Azure PowerShell을 사용하여 Azure File Storage에 파일 저장소 계정(예: `mystorage`), 파일 공유(예: `sharejson`) 및 폴더를 만듭니다.
2.  파일 저장소 공유에 일부 JSON 파일을 업로드합니다.
3.  포트 445를 허용하는 컴퓨터에서 Windows 방화벽에 아웃바운드 방화벽 규칙을 만듭니다. 인터넷 서비스 공급자가 이 포트를 차단할 수 있습니다. 다음 단계에서 DNS 오류(오류 53)가 발생하면 포트 445를 열지 않았거나 ISP가 이 포트를 차단하고 있는 것입니다.
4. Azure File Storage 공유를 로컬 드라이브(예: `T:`)로 탑재합니다.

    명령 구문은 다음과 같습니다.

    ```dos
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    다음은 Azure File Storage 공유에 로컬 드라이브 문자 `T:`를 할당하는 예제입니다.

    ```dos
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    Azure Portal에서 설정의 키 섹션에서 저장소 계정 키 및 기본 또는 보조 저장소 계정 액세스 키를 찾을 수 있습니다.

5.  이제 다음 예제에서처럼 매핑된 드라이브를 사용하여 Azure File Storage 공유에서 JSON 파일에 액세스할 수 있습니다.

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

Azure File Storage에 대한 자세한 내용은 [파일 저장소](https://azure.microsoft.com/services/storage/files/)를 참조하세요.

## <a name="import-json-documents-from-azure-blob-storage"></a>Azure Blob Storage에서 JSON 문서 가져오기

T-SQL BULK INSERT 명령 또는 OPENROWSET 함수를 사용하여 Azure Blob Storage에서 Azure SQL Database로 직접 파일을 로드할 수 있습니다.

먼저 다음 예제와 같이 외부 데이터 원본을 만듭니다.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
 WITH ( TYPE = BLOB_STORAGE,
        LOCATION = 'https://myazureblobstorage.blob.core.windows.net',
        CREDENTIAL= MyAzureBlobStorageCredential);
```

그런 다음 DATA_SOURCE 옵션을 사용하여 BULK INSERT 명령을 실행합니다.

```sql
BULK INSERT Product
FROM 'data/product.dat'
WITH ( DATA_SOURCE = 'MyAzureBlobStorage');
```

자세한 내용 및 OPENROWSET 사용 예제는 [Loading files from Azure Blob Storage into Azure SQL Database](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/)(Azure Blob Storage에서 Azure SQL Database로 파일 로드)를 참조하세요.

## <a name="parse-json-documents-into-rows-and-columns"></a>행과 열로 JSON 문서 구문 분석
단일 값으로 전체 JSON 파일을 읽지 않고 파일을 구문 분석하여 파일의 책과 해당 속성을 행과 열에 반환할 수 있습니다. 다음 예제에서는 [이 사이트](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json)에서 책 목록이 포함된 JSON 파일을 사용합니다.

### <a name="example-1"></a>예 1
가장 간단하게 파일에서 전체 목록을 로드할 수 있습니다. 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

### <a name="example-2"></a>예제 2
OPENROWSET는 파일에서 단일 텍스트 값을 읽어 BulkColumn으로 반환하고 OPENJSON 함수에 전달합니다. OPENJSON은 BulkColumn 배열에서 JSON 개체의 배열을 반복하고 각 행에 JSON으로 형식이 지정된 한 권의 책을 반환합니다.

```json
{"id":"978-0641723445", "cat":["book","hardcover"], "name":"The Lightning Thief", … }
{"id":"978-1423103349", "cat":["book","paperback"], "name":"The Sea of Monsters", … }
{"id":"978-1857995879", "cat":["book","paperback"], "name":"Sophie’s World : The Greek", … } 
{"id":"978-1933988177", "cat":["book","paperback"], "name":"Lucene in Action, Second", … }
```

### <a name="example-3"></a>예제 3
OPENJSON 함수는 JSON 콘텐츠를 구문 분석하여 테이블 또는 결과 집합으로 변환할 수 있습니다. 다음 예제에서는 콘텐츠를 로드하고 로드된 JSON을 구문 분석하여 5개의 필드를 열로 반환합니다.

```sql
SELECT book.*
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
 WITH( id nvarchar(100), name nvarchar(100), price float,
 pages_i int, author nvarchar(100)) AS book
```

이 예제에서 OPENROWSET(BULK)는 파일 콘텐츠를 읽고 그 콘텐츠를 출력에 대해 정의된 스키마로 OPENJSON 함수에 전달합니다. OPENJSON은 열 이름을 사용하여 JSON 개체의 속성을 찾습니다. 예를 들어 `price` 속성은 `price` 열로 반환되고 float 데이터 형식으로 변환됩니다. 결과는 다음과 같습니다.

|Id|속성|price|pages_i|작성자
|---|---|---|---|---|
978-0641723445|번개 도둑|12.5|384|Rick Riordan| 
978-1423103349|몬스터 바다|6.49|304|Rick Riordan| 
978-1857995879|소피의 세계: 그리스 철학자|3.07|64|Jostein Gaarder| 
978-1933988177|루씬 인 액션(개정판)|30.5|475|Michael McCandless|
||||||

이제 사용자에게 이 테이블을 반환하거나 다른 테이블로 데이터를 로드할 수 있습니다.

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-blog-posts"></a>Microsoft 블로그 게시물  
  
특정 솔루션, 사용 사례 및 권장 사항은 SQL Server 및 Azure SQL Database의 기본 제공 JSON 지원에 대한 [블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>참고 항목
[OPENJSON을 사용하여 JSON 데이터를 행 및 열로 변환](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)

