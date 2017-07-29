---
title: "SQL Server에 JSON 문서 가져오기 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 1c842fde925e89901971a525c3e171ffce050269
ms.contentlocale: ko-kr
ms.lasthandoff: 06/23/2017

---
# <a name="import-json-documents-into-sql-server"></a>SQL Server에 JSON 문서 가져오기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

이 항목에서는 SQL Server로 JSON 파일 가져오기 하는 방법을 설명 합니다. 현재 파일에 저장 된 JSON 문서가 많이 있습니다. JSON 파일에서 정보를 기록 하는 응용 프로그램, 센서 등 JSON 파일에 저장 된 정보를 생성 합니다. 파일에 저장된 JSON 데이터를 읽고, 데이터를 SQL Server에 로드하여 분석할 수 있어야 합니다.

## <a name="import-a-json-document-into-a-single-column"></a>단일 열에 JSON 문서 가져오기
**OPENROWSET(BULK)**는 SQL Server에 해당 위치에 대한 읽기 권한이 있는 경우 로컬 드라이브 또는 네트워크에 있는 모든 파일에서 데이터를 읽을 수 있는 테이블 반환 함수입니다. 파일의 콘텐츠를 포함하는 단일 열로 된 테이블을 반환합니다. 구분 기호 등 OPENROWSET(BULK) 함수에서 사용할 수 있는 다양한 옵션이 있습니다. 하지만 가장 간단하게 파일의 전체 콘텐츠를 텍스트 값으로 로드할 수 있습니다. (이 단일 큰 값을 단일 문자 LOB(Large Object) 또는 SINGLE_CLOB이라고 합니다.) 

다음은 JSON 파일의 콘텐츠를 읽고 단일 값으로 사용자에게 반환하는 **OPENROWSET(BULK)** 함수의 예입니다.

```sql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

OPENJSON(BULK)이 파일의 콘텐츠를 읽고 `BulkColumn`에 반환합니다.

로드할 수도 있습니다는 파일의 내용을 지역 변수 또는 테이블에 다음 예제와 같이:

```sql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

JSON 파일의 콘텐츠를 로드 한 후 테이블에 JSON 텍스트를 저장할 수 있습니다.

## <a name="import-multiple-json-documents"></a>여러 개의 JSON 문서 가져오기
한 번에 파일 시스템에서 하나를 지역 변수에 JSON 파일의 집합을 로드할 수 같은 방법을 사용할 수 있습니다. 파일 이름을 `book<index>.json`이라고 가정합니다.
  
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
사용할 수도 있습니다 openrowset (bulk) 위에 설명 된 대로 SQL Server에 액세스할 수 있는 다른 파일 위치에서 JSON 파일을 읽을 수 있습니다. 예를 들어 Azure File Storage는 SMB 프로토콜을 지원합니다. 따라서 다음 절차에 따라 Azure File Storage 공유에 로컬 가상 드라이브를 매핑할 수 있습니다.
1.  Azure Portal 또는 Azure PowerShell을 사용하여 Azure File Storage에 파일 저장소 계정(예: `mystorage`), 파일 공유(예: `sharejson`) 및 폴더를 만듭니다.
2.  파일 저장소 공유에 일부 JSON 파일을 업로드합니다.
3.  포트 445를 허용하는 컴퓨터에서 Windows 방화벽에 아웃바운드 방화벽 규칙을 만듭니다. 인터넷 서비스 공급자가 이 포트를 차단할 수 있습니다. 다음 단계에서 DNS 오류(오류 53)가 발생하면 포트 445를 열지 않았거나 ISP가 이 포트를 차단하고 있는 것입니다.
4. Azure 파일 저장소 공유 로컬 드라이브로 탑재 (예를 들어 `T:`).

    명령 구문은 다음과 같습니다.

    ```dos
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    다음은 로컬 드라이브 문자를 할당 하는 예제 `T:` Azure 파일 저장소 공유에:

    ```dos
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    Azure Portal에서 설정의 키 섹션에서 저장소 계정 키 및 기본 또는 보조 저장소 계정 액세스 키를 찾을 수 있습니다.

5.  이제 액세스할 수 있습니다 JSON 파일이 Azure 파일 저장소 공유에서 매핑된 드라이브를 사용 하 여 다음 예제와 같이.

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

Azure File Storage에 대한 자세한 내용은 [파일 저장소](https://azure.microsoft.com/en-us/services/storage/files/)를 참조하세요.

## <a name="import-json-documents-from-azure-blob-storage"></a>Azure Blob Storage에서 JSON 문서 가져오기

T-SQL BULK INSERT 명령을 또는 OPENROWSET 함수를 Azure Blob 저장소에서 Azure SQL 데이터베이스에 직접 파일을 로드할 수 있습니다.

다음 예제와 같이 외부 데이터 원본을 먼저 만듭니다.

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

자세한 내용 및 OPENROWSET을 사용 하는 예제에 대 한 참조 [파일을 Azure Blob 저장소에서 Azure SQL 데이터베이스로 로드](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/)합니다.

## <a name="parse-json-documents-into-rows-and-columns"></a>행과 열로 JSON 문서 구문 분석
단일 값으로 JSON 파일 전체를 읽는 대신 구문 분석 하 고 책 파일 및 행과 열에 해당 속성에서 반환 하는 것이 좋습니다. 다음 예제에서는 JSON 파일에서 사용 하 여 [이 사이트](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json) 책의 목록이 포함 됩니다.

### <a name="example-1"></a>예 1
가장 간단하게 파일에서 전체 목록을 로드할 수 있습니다. 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

### <a name="example-2"></a>예 2
OPENROWSET는 파일에서 단일 텍스트 값을 읽어 BulkColumn으로 반환하고 OPENJSON 함수에 전달합니다. OPENJSON은 BulkColumn 배열에 대 한 JSON 개체의 배열에서 반복 하 고 JSON으로 서식이 지정 된 각 행에 한 권의 책을 반환 합니다.

```json
{"id":"978-0641723445″, "cat":["book","hardcover"], "name":"The Lightning Thief", … 
{"id":"978-1423103349″, "cat":["book","paperback"], "name":"The Sea of Monsters", … 
{"id":"978-1857995879″, "cat":["book","paperback"], "name":"Sophie’s World : The Greek … 
{"id":"978-1933988177″, "cat":["book","paperback"], "name":"Lucene in Action, Second … 
```

### <a name="example-3"></a>예 3
OPENJSON 함수는 JSON 콘텐츠를 구문 분석하여 테이블 또는 결과 집합으로 변환할 수 있습니다. 다음 예제에서는 콘텐츠를 로드하고 로드된 JSON을 구문 분석하여 5개의 필드를 열로 반환합니다.

```sql
SELECT book.*
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
 WITH( id nvarchar(100), name nvarchar(100), price float,
 pages_i int, author nvarchar(100)) AS book
```

이 예제에서 OPENROWSET(BULK)는 파일 콘텐츠를 읽고 그 콘텐츠를 출력에 대해 정의된 스키마로 OPENJSON 함수에 전달합니다. OPENJSON은 열 이름을 사용하여 JSON 개체의 속성을 찾습니다. 예를 들어 `price` 속성은 `price` 열로 반환되고 float 데이터 형식으로 변환됩니다. 결과는 다음과 같습니다.

|Id|이름|price|pages_i|작성자
|---|---|---|---|---|
978-0641723445|번개 도둑|12.5|384|Rick Riordan| 
978-1423103349|몬스터 바다|6.49|304|Rick Riordan| 
978-1857995879|소피의 세계: 그리스 철학자|3.07|64|Jostein Gaarder| 
978-1933988177|루씬 인 액션(개정판)|30.5|475|Michael McCandless|
||||||

이제 사용자에게 이 테이블을 반환하거나 다른 테이블로 데이터를 로드할 수 있습니다.

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>기본 제공 SQL Server에서 JSON 지원에 대 한 자세한 정보  
특정 솔루션에 많이 사용 사례 및 권장 사항, 참조는 [기본 제공 JSON 지원에 대 한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) SQL Server와 Microsoft 프로그램 관리자 인 Jovan popovic의 Azure SQL 데이터베이스에 있습니다.
  
## <a name="see-also"></a>참고 항목
[OPENJSON을 사용하여 JSON 데이터를 행 및 열로 변환](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)


