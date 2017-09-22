---
title: Using Always Encrypted with the ODBC Driver 13.1 for SQL Server | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
caps.latest.revision: 3
ms.author: v-chojas
manager: jhubbard
author: MightyPen
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 2d0ac1f1a8e9a78539a2c7824f06d3ed3507c0b5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="using-always-encrypted-with-the-odbc-driver-131-for-sql-server"></a>Using Always Encrypted with the ODBC Driver 13.1 for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

이 문서를 사용 하 여 ODBC 응용 프로그램을 개발 하는 방법에 대해 설명 [상시 암호화 (데이터베이스 엔진)](/sql-docs/docs/relational-databases/security/encryption/always-encrypted-database-engine) 및 [for SQL Server ODBC Driver 13.1](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)합니다.

Always Encrypted를 사용하면 클라이언트 응용 프로그램이 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. ODBC Driver 13.1 for SQL Server에서는이를 위해 투명 하 게 암호화 하 고 클라이언트 응용 프로그램의 중요 한 데이터를 암호 해독과 같은 상시 암호화 드라이버를 지원 합니다. 이 드라이버는 중요 데이터베이스 열에 해당하는 쿼리 매개 변수를 자동으로 확인하고(Always Encrypted를 사용하여 보호) 데이터를 SQL Server 또는 Azure SQL Database로 전달하기 전에 이러한 매개 변수의 값을 암호화합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)](/sql-docs/docs/relational-databases/security/encryption/always-encrypted-database-engine)를 참조하세요.

### <a name="prerequisites"></a>필수 구성 요소

데이터베이스에서 상시 암호화를 구성합니다. 상시 암호화를 구성하려면 상시 암호화 키를 프로비전하고 선택한 데이터베이스 열에 대한 암호화를 설정해야 합니다. 데이터베이스에 상시 암호화가 구성되지 않은 경우 [상시 암호화 시작](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)의 지침을 따르세요. 특히, 데이터베이스 열 마스터 키 (CMK), 열 암호화 키 (CEK), 및 해당 CEK를 사용 하 여 암호화 하는 하나 이상의 열을 포함 하는 테이블에 대 한 메타 데이터 정의 포함 해야 합니다.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>ODBC 응용 프로그램에서 상시 암호화 설정

값을 설정 하 여이 매개 변수 암호화 및 암호화 하는 결과 집합 열 암호 해독 모두 활성화 하는 가장 쉬운 방법은 `ColumnEncryption` 연결 문자열 키워드를 **Enabled**합니다. 다음은 상시 암호화를 사용 하는 연결 문자열의 예입니다.

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

DSN 구성에서 동일한 키 및 값 (있는 경우 연결 문자열 설정으로 재정의 됩니다)를 사용 하 여 또는 프로그래밍 방식으로 암호화를 활성화할 수도 있습니다 항상는 `SQL_COPT_SS_COLUMN_ENCRYPTION` 사전 연결 특성입니다. 연결 문자열 또는 DSN에 설정 된 값을 재정의 이러한 방식으로 설정:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

연결에 사용할 수 있는 경우 개별 쿼리에 대해 상시 암호화의 동작을 조정할 수 있습니다. 참조 [의 성능 영향의 항상 암호화 제어](#controlling-the-performance-impact-of-always-encrypted) 아래에 대 한 자세한 내용은 합니다.

상시 암호화 사용 암호화 나 암호 해독을 위해;에 충분 하지 않습니다 또한 있는지 확인 해야 합니다.

- 응용 프로그램에는 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 데이터베이스 권한이 있으며 데이터베이스에서 상시 암호화 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 참조 [데이터베이스 사용 권한](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)합니다.

- 응용 프로그램에서 쿼리 된 암호화 된 열에 대 한 Cek를 보호 하는 CMK를 액세스할 수 있습니다. 이 CMK를 저장 하는 키 저장소 공급자에 따라 달라 집니다. 참조 [열 마스터 키 저장소 작업](#working-with-column-master-key-stores) 자세한 정보에 대 한 합니다.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정

연결에 항상 암호화를 사용 하는 후 표준 ODBC Api를 사용할 수 있습니다 (참조 [ODBC 샘플 코드](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) 또는 [ODBC Programmer's Reference](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx))를 검색 하거나 암호화 된 데이터베이스 열에서 데이터를 수정 합니다. 데이터베이스 권한 및 열 마스터 키에 액세스할 수, 드라이버에서 암호화 된 열을 대상 데이터 및 암호 해독에 투명 하 게 작동 하는 암호화 된 열에서 검색 된 모든 쿼리 매개 변수를 암호화 하는 응용 프로그램에 필요한 가정은 열 암호화 되지 않은 경우 처럼 응용 프로그램입니다.

항상 암호화를 사용 하지 않는 경우에 암호화 된 열을 대상 매개 변수가 있는 쿼리 실패 합니다. 쿼리에 암호화 된 열을 대상으로 하는 매개 변수 없이으로 암호화 된 열에서 데이터를 검색할 수 계속 합니다. 그러나, 드라이버는 모든 암호 해독을 시도 하지 않습니다 및 응용 프로그램 (바이트 배열)로 암호화 된 이진 데이터를 받게 됩니다.

다음 표에서 상시 암호화가 사용 여부에 따른 쿼리 동작을 요약 되어 있습니다.

|쿼리 특성 | 상시 암호화가 설정되고 응용 프로그램에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 응용 프로그램에서 키 또는 키 메타데이터에 액세스할 수 없는 경우 | 상시 암호화를 사용하지 않는 경우|
|:---|:---|:---|:---|
| 암호화 된 열을 대상으로 하는 매개 변수입니다. | 매개 변수 값이 투명하게 암호화됩니다. | 오류 | 오류|
| 암호화 된 열을 대상으로 하는 매개 변수 없이 암호화 된 열에서 데이터를 검색 합니다.| 암호화된 열의 결과가 투명하게 암호 해독됩니다. 응용 프로그램에는 일반 텍스트 열 값을 받습니다. | 오류 | 암호화된 열의 결과가 암호 해독되지 않습니다. 응용 프로그램으로 바이트 배열을 암호화 된 값을 받습니다.

다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 예제에서는 다음 스키마를 가진 테이블을 가정합니다. SSN 및 BirthDate 열은 암호화되어 있습니다.

```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>데이터 삽입 예제

이 예제에서는 Patients 테이블에 행을 삽입합니다. 다음에 유의하세요.

- 샘플 코드에는 암호화에 대한 내용이 없습니다. 드라이버는 자동으로 검색 하 고는 암호화 된 열을 대상 SSN 및 날짜 매개 변수의 값을 암호화 합니다. 이렇게 하면 응용 프로그램에 투명하게 암호화할 수 있습니다.

- 데이터베이스 열을 포함 하는 암호화 된 열에 삽입 된 값이 바인딩된 매개 변수로 전달 됩니다 (참조 [SQLBindParameter 함수](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). 동안 매개 변수를 사용 하 여는 (하지만 권장 SQL 주입 공격을 방지할 수 있으므로) 암호화 되지 않은 열에 값을 보낼 때 선택 사항, 암호화 된 열을 대상으로 하는 값에 필요 합니다. SSN 또는 BirthDate 열에 삽입 된 값이 쿼리 문에 포함 된 리터럴로 전달 된, 드라이버는 암호화 또는 쿼리에서 리터럴을 처리 하려고 시도 하지 않습니다 때문에 쿼리가 실패 합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.

- SSN 열에 삽입 하는 매개 변수의 SQL 형식에 매핑되는 SQL_CHAR로 설정 되어는 **char** SQL Server 데이터 형식 (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). 매개 변수의 형식에 매핑되는 SQL_WCHAR로 설정 된 경우 **nchar**, 상시 암호화에서는 암호화 된 nchar 값에서 암호화 된 char 값으로 서버 쪽의 변환을 지원 하지 않으므로 쿼리가 실패 합니다. 참조 [ODBC 프로그래머 참조-부록 d: 데이터 형식](https://msdn.microsoft.com/library/ms713607.aspx) 데이터 형식 매핑에 대 한 정보에 대 한 합니다.

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>일반 텍스트 데이터 검색 예

다음 예제에서는 암호화된 값을 기준으로 데이터를 필터링하고 암호화된 열에서 일반 텍스트 데이터를 검색하는 방법을 보여 줍니다. 다음에 유의하세요.

- 전달할 SQLBindParameter를 사용 하 여 드라이버 암호화할 수 있도록 투명 하 게 해당 서버에 보내기 전에 필요한 SSN 열에서 필터링 할 WHERE 절에 사용 되는 값입니다.

- 드라이버 SSN 및 BirthDate 열에서 검색 한 데이터를 투명 하 게 해독 하므로 프로그램에서 인쇄 하는 모든 값 일반 텍스트로 됩니다.

> [!NOTE]
> 결정적 암호화는 경우에 쿼리에서 암호화 된 열에서 같음 비교를 수행할 수 있습니다. 자세한 내용은 참조 [선택 하면 결정적 또는 임의 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)합니다.

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>암호 텍스트 데이터 검색 예

상시 암호화를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예제에서는 암호화 된 열에서 암호화 된 이진 데이터를 검색 하는 방법을 보여 줍니다. 다음에 유의하세요.

- 연결 문자열에서는 상시 암호화를 사용하지 않으므로 쿼리에서 SSN 및 BirthDate의 암호화된 값을 바이트 배열로 반환합니다(프로그램에서 값을 문자열로 변환).
- 암호화된 열을 대상으로 하는 매개 변수가 없으면 상시 암호화를 사용하지 않고 암호화된 열에서 데이터를 검색하는 쿼리에 매개 변수가 있을 수 있습니다. 위의 쿼리는 LastName을 기준으로 필터링되며 데이터베이스에서 암호화되지 않습니다. 쿼리가 SSN 또는 BirthDate를 기준으로 필터링되면 쿼리가 실패합니다.


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>암호화된 열 쿼리 시 일반적인 문제 방지

이 섹션에서는 ODBC 응용 프로그램 및 방지 하는 방법에 대 한 몇 가지 지침에서 암호화 된 열을 쿼리할 때 일반적인 오류 범주를 설명 합니다.

##### <a name="unsupported-data-type-conversion-errors"></a>지원되지 않는 데이터 형식 변환 오류

상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 참조 [상시 암호화 (데이터베이스 엔진)](/sql-docs/docs/relational-databases/security/encryption/always-encrypted-database-engine) 자세한 목록은 지원 되는 형식 변환에 대 한 합니다. 데이터 형식 변환 오류를 방지 하려면 SQLBindParameter 암호화 된 열을 대상으로 하는 매개 변수와 함께 사용 하는 경우 다음 사항을 관찰 해야 있는지를 확인 합니다.

- 매개 변수의 SQL 형식을 하거나 정확히 대상 열의 형식과 동일 되었거나 열 형식으로 변환 하는 SQL 형식에서 사용할 수 있습니다.

- 전체 자릿수와 소수 자릿수의 열을 대상으로 하는 매개 변수는 `decimal` 및 `numeric` SQL Server 데이터 형식 전체 자릿수와 소수 대상 열에 대 한 구성으로 동일 합니다.

- 열을 대상으로 하는 매개 변수의 전체 자릿수 `datetime2`, `datetimeoffset`, 또는 `time` SQL Server 데이터 형식의 대상 열을 수정 하는 쿼리에서 대상 열에 대 한 전체 자릿수 보다 큽니다.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류

암호화 된 열을 대상으로 하는 모든 값은 서버에 전송 되기 전에 암호화 해야 합니다. 시도를 삽입, 수정 또는 암호화 된 열에서 일반 텍스트 값으로 필터링 하면 오류가 발생 합니다. 이러한 오류를 방지 하려면 사항을 확인 합니다.

- 암호화가 설정 되는 항상 (DSN, 연결 문자열에서에서 설정 하 여 연결 하기 전에 `SQL_COPT_SS_COLUMN_ENCRYPTION` 특정 연결에 대 한 연결 특성 또는 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특정 문에 대 한 문 특성).

- SQLBindParameter를 사용 하 여 암호화 된 열을 대상으로 하는 데이터를 보내려고 합니다. 다음 예제에서는 기준으로 잘못 필터링 암호화 된 열 (SSN)에서 리터럴/상수 SQLBindParameter에 리터럴을 인수로 전달 하는 대신 하는 쿼리를 보여 줍니다.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>SQLSetPos 및 SQLMoreResults를 사용할 때 예방 조치

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API를 통해 SQLBindCol으로 바인딩된 하 고 이전에 인출 된 데이터가 어떤 행에 버퍼를 사용 하 여 결과 집합의 행을 업데이트할 응용 프로그램입니다. 암호화 된 고정 길이 형식 비대칭 패딩 동작으로 인해 예기치 않게 행의 다른 열에 업데이트를 수행 하는 동안 이러한 열의 데이터를 변경 하는 것이 같습니다. 값은 버퍼 크기 보다 작으면 AE와 고정된 길이 문자 값이 채워집니다 됩니다.

이 문제를 줄이기 위해 사용 하 여는 `SQL_COLUMN_IGNORE` 플래그의 일환으로 업데이트 되지 않는 열을 무시 하도록 `SQLBulkOperations` 사용 하는 경우 및 `SQLSetPos` 커서에 대 한 업데이트를 기반으로 합니다.  응용 프로그램에 의해 직접 수정 되지 되는 모든 열을 무시할지, 성능을 고 버퍼에 바인딩되는 열 잘림을 방지 하기 위해 모두 *더 작은* 실제 (DB) 크기 보다 합니다. 자세한 내용은 참조 [SQLSetPos 함수 참조](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx)합니다.

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

응용 프로그램 호출 [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) 준비 된 문에서 열에 대 한 메타 데이터를 반환할 수 있습니다.  상시 암호화를 사용 하는 경우 호출 `SQLMoreResults` *전에* 호출 `SQLDescribeCol` 하면 [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 호출 되도록 제대로 반환 하지 않는 일반 텍스트 암호화 된 열에 대 한 메타 데이터입니다. 이 문제를 방지 하려면 호출 `SQLDescribeCol` 에 준비 된 문을 *전에* 호출 `SQLMoreResults`합니다.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

상시 암호화는 클라이언트 쪽 암호화 기술 이므로 데이터베이스에는 없는 클라이언트 쪽에서 대부분의 성능 오버 헤드가 발견 됩니다. 암호화 및 해독 작업의 비용 외에 클라이언트 쪽 성능 오버 헤드가 다른 원본 설정은:

- 쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복

- 열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출

이 섹션에서는 SQL Server와는 위의 두 성능 요소 영향을 제어 하는 방법에 대 한 ODBC Driver 13.1에서 기본 제공 성능 최적화를 설명 합니다.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>메타 데이터를 검색할 쿼리 매개 변수에 대 한 왕복 횟수를 제어 합니다.

상시 암호화를 연결에 사용 하는 경우 ODBC Driver 13.1 기본적으로 SQL Server가에 대 한 호출 [sys.sp_describe_parameter_encryption](/sql-docs/docs/relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql) 각 매개 변수가 있는 쿼리에 대 한 매개 변수 (없이 쿼리 문을 전달 SQL Server로 값). 이 저장된 프로시저 매개 변수를 암호화 해야 하는 경우 그리고 있다면 확인 하려면 쿼리 문을 분석 하 여, 드라이버를 암호화할 수 있도록 각 매개 변수에 대해 암호화 관련 정보를 반환 합니다. 위의 동작은 클라이언트 응용 프로그램에는 투명도 대 한 높은 수준의 보장: 응용 프로그램 (및 응용 프로그램 개발자)에 암호화 된 열을 대상으로 값이 전달 된으로 어떤 쿼리가 암호화 된 열 액세스 주의 해야 할 필요 하지 않습니다 매개 변수에서 드라이버입니다.

### <a name="per-statement-always-encrypted-behavior"></a>문 별 동작을 항상 암호화

매개 변수가 있는 쿼리에 대 한 암호화 메타 데이터 검색의 성능 영향을 제어 하려면 연결에서 사용할 수 있는 경우 개별 쿼리에 대 한 상시 암호화 동작을 변경할 수 있습니다. 이러한 방식으로 확인할 수 `sys.sp_describe_parameter_encryption` 있는 쿼리에 암호화 된 열을 대상으로 하는 매개 변수가 대해서만 호출 됩니다. 단, 이러한 작업을 통해 암호화의 투명성이 저하: 데이터베이스의 추가 열을 암호화 하는 경우 스키마 변경에 맞게 응용 프로그램의 코드를 변경 해야 할 수 있습니다.

문의 상시 암호화 동작을 제어 하려면 호출 SQLSetStmtAttr 설정 하 여 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 매개 변수 특성을 다음 값 중 하나:

|값|Description|
|-|-|
|`SQL_CE_DISABLED` (0)|암호화 된 문에 대해 항상 사용할 수 없음|
|`SQL_CE_RESULTSETONLY` (1)|만 암호 해독 합니다. 결과 집합 및 반환 값을 해독 되 고 매개 변수는 암호화 되지 않습니다.|
|`SQL_CE_ENABLED` (3) | 암호화 사용 되 고 매개 변수 및 결과에 사용 되는 항상|

상시 암호화와 연결에서 만든 새 문 핸들 SQL_CE_ENABLED 기본값으로 사용할 수 있습니다. 그와 연결에서 만든 해제 SQL_CE_DISABLED 기본값 (및에 항상 암호화를 사용 불가능.)

대부분의 클라이언트 응용 프로그램의 쿼리에 암호화 된 열에 액세스 하는 경우 다음 것이 좋습니다.

- 설정의 `ColumnEncryption` 연결 문자열 키워드를 `Enabled`합니다.

- 설정의 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특성을 `SQL_CE_DISABLED` 에 암호화 된 모든 열에 액세스 하지 않는 하는 문입니다. 이 두 호출 모두 비활성화 됩니다 `sys.sp_describe_parameter_encryption` 결과에서 값을 해독 하려고 뿐만 아니라 설정 합니다.
    
- 설정의 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특성을 `SQL_CE_RESULTSETONLY` 에 암호화를 요구 하는 매개 변수가 없지만 암호화 된 열에서 데이터를 검색 하는 문입니다. 호출 없게 `sys.sp_describe_parameter_encryption` 및 매개 변수 암호화 합니다. 암호 해독할 암호화 된 열을 포함 하는 결과 계속 됩니다.

## <a name="always-encrypted-security-settings"></a>항상 암호화 보안 설정

### <a name="force-column-encryption"></a>강제 열 암호화

매개 변수의 암호화를 적용 하려면 설정의 `SQL_CA_SS_FORCE_ENCRYPT` SQLSetDescField 함수에 대 한 호출을 통해 매개 변수 IPD (구현 설명자) 필드입니다. 0이 아닌 값에는 드라이버 관련된 매개 변수에 대 한 암호화 메타 데이터를 반환 하는 경우 오류를 반환 하도록 하면 됩니다.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

SQL Server 매개 변수는 암호화 하지 않아도 되는 드라이버, 메시지가 표시 되 면 해당 매개 변수를 사용 하 여 쿼리가 실패 합니다. 손상 된 SQL server가 데이터 노출을 야기할 수 있는 클라이언트에 잘못 된 암호화 메타 데이터를 제공 하는 보안 공격에 대해 추가적인 보호를 제공 합니다.

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

열 암호화 키를 해독 하는 열 마스터 키 저장소에 대 한 호출의 수를 줄이려면 드라이버 메모리에 일반 텍스트 Cek를 캐시 합니다. ECEK에서 데이터베이스 메타 데이터를 받은 후 드라이버는 먼저 일반 텍스트 CEK에 해당 하는 캐시에 사용할 수 있는 암호화 된 키 값을 찾으려고 시도 합니다. 드라이버는 CMK를 캐시에 해당 일반 텍스트 CEK를 찾을 수 없는 경우에 포함 하는 키 저장소를 호출 합니다.

> [!NOTE]
> SQL Server 용 ODBC Driver 13.1, 캐시의 항목은 두 시간의 시간 초과 이후 제거 됩니다. 즉, 주어진된 ECEK에 대 한 드라이버 또는 2 시간 마다 응용 프로그램의 수명 동안 키 저장소를 한 번만 연결 더 작은 쪽입니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업

데이터를 암호화 하거나 해독, 드라이버는 대상 열에 대해 구성 된 CEK를 가져올 해야 합니다. Cek는 데이터베이스 메타 데이터에 암호화 된 형식 (ECEKs)에 저장 됩니다. 각 CEK를 암호화 하기 위해 사용 된 해당 CMK에 있습니다. [데이터베이스 메타 데이터](../../t-sql/statements/create-column-master-key-transact-sql.md) 자체; CMK를 저장 하지 않는 키 저장소 CMK를 찾는 데 사용할 수 있는 정보와 키 저장소의 이름을 포함 합니다.

ECEK의 일반 텍스트 값을 가져오려면 드라이버 먼저 CEK 및 해당 해당 CMK를 둘 다에 대 한 메타 데이터를 가져오고이 정보를 사용 하 여 CMK를 포함 하는 키 저장소에 게 문의를 하 고는 ECEK 암호 해독 하도록 요청 합니다. 드라이버는 키 저장소 공급자를 사용 하 여 키 저장소와 통신 합니다.

### <a name="built-in-keystore-providers"></a>기본 제공 키 저장소 공급자

ODBC Driver 13.1 for SQL Server는 다음 기본 제공 키 저장소 공급자와 함께 제공 됩니다.

| 이름 | Description | 공급자 (메타 데이터) 이름 |가용성|
|:---|:---|:---|:---|
|Azure Key Vault |저장소 Cmk를 Azure 키 자격 증명 모음 | `AZURE_KEY_VAULT` |Windows, Linux, macOS|
|Windows 인증서 저장소|Windows 키 저장소에 Cmk를 로컬로 저장| `MSSQL_CERTIFICATE_STORE`|Windows|

- 사용자 (또는 DBA)는 열 마스터 키 메타 데이터에 구성 된 공급자 이름이 올바른지와 열 마스터 키 경로 지정 된 공급자에 대 한 키 경로 형식을 준수 되도록 해야 합니다. [CREATE COLUMN MASTER KEY(Transact-SQL)](/sql-docs/docs/t-sql/statements/create-column-master-key-transact-sql) 문을 실행할 때 적합한 공급자 이름 및 키 경로를 자동으로 생성하는 SQL Server Management Studio 등의 도구를 사용하여 키를 구성하는 것이 좋습니다.

- 응용 프로그램 키 저장소에 키에 액세스할 수 있는지 확인 해야 합니다. 여기에 키 및/또는 키 저장소에 따라 키 저장소에 대 한 응용 프로그램 액세스 권한을 부여 하거나 다른 키 저장소 관련 구성 단계를 수행 포함 될 수 있습니다. 예를 들어 Azure 키 자격 증명 모음에 액세스 하려면 키 저장소에 올바른 자격 증명을 제공 합니다.

### <a name="using-the-azure-key-vault-provider"></a>Azure 키 자격 증명 모음 공급자 사용

Azure 주요 자격 증명 모음은 상시 암호화에 대한 열 마스터 키를 저장 및 관리하는 편리한 옵션입니다(특히 응용 프로그램이 Azure에서 호스트되는 경우). ODBC Driver 13.1 for SQL Server, Linux, macOS 등 및 Windows에는 Azure 키 자격 증명 모음에 대 한 기본 제공 열 마스터 키 저장소 공급자를 포함합니다. 참조 [Azure 키 자격 증명 모음 – 단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [키 자격 증명 모음 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), 및 [Azure 키 자격 증명 모음에 열 마스터 키 만들기](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) Azure 키를 구성 하는 방법에 대 한 자세한 내용은 자격 증명 모음 항상 암호화 합니다.

드라이버는 다음과 같은 자격 증명을 사용 하 여 Azure 키 자격 증명 모음에 인증을 지원 합니다.

- 사용자 이름/암호-이 방법에서는 자격 증명이 Azure Active Directory 사용자 및 암호의 이름이 있습니다.

- 클라이언트 ID/암호-이 방법을 자격 증명은 응용 프로그램 클라이언트 ID 및 응용 프로그램 암호입니다.

열 암호화에 대 한 AKV에 저장 하는 Cmk를 사용 하는 드라이버를 허용 하려면 다음 연결 문자열 전용 키워드를 사용 합니다.

|자격 증명 유형| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|사용자 이름/암호| `KeyVaultPassword`|사용자 계정 이름|암호|
|클라이언트 ID/암호| `KeyVaultClientSecret`|클라이언트 ID|암호|

#### <a name="example-connection-strings"></a>연결 문자열 예

다음 연결 문자열에는 두 가지 자격 증명 유형이 Azure 키 자격 증명 모음에 인증 하는 방법을 보여 줍니다.

**ClientID/암호**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**사용자 이름/암호**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

다른 ODBC 응용 프로그램은 변경 하지 AKV CMK 저장소에 사용 해야 합니다.

### <a name="using-the-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자를 사용 하 여

라는 Windows 인증서 저장소에 대 한 기본 제공 열 마스터 키 저장소 공급자를 포함 하는 Windows에서 SQL Server에 대 한 ODBC Driver 13.1 `MSSQL_CERTIFICATE_STORE`합니다. (이 공급자에서 사용할 수 없으면 macOS 또는 Linux.) 이 공급자와 클라이언트 컴퓨터에 CMK를 로컬로 저장 되며 응용 프로그램에서 추가 구성 없이 드라이버와 함께 사용할 필요가 있습니다. 그러나 응용 프로그램 저장소에 인증서와 해당 개인 키에 액세스할 수 있어야 합니다. 참조 [만들기 열 마스터 키 및 저장 (상시 암호화)](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted) 자세한 정보에 대 한 합니다.

### <a name="using-custom-keystore-providers"></a>사용자 지정 키 저장소 공급자를 사용 하 여

또한 SQL Server 용 ODBC Driver 13.1 CEKeystoreProvider 인터페이스를 사용 하 여 공급 업체의 사용자 지정 키 저장소 공급자를 지원 합니다. 이 응용 프로그램을, 쿼리를 로드 하 고 암호화 된 열을 액세스 하는 드라이버에서 사용 될 수 있도록 키 저장소 공급자를 구성할 수 있습니다. 응용 프로그램 저장소 SQL Server에 대 한 Cek를 암호화 하 고 odbc; 암호화 된 열에 액세스 하는 다음 작업을 수행 하려면 키 저장소 공급자와도 직접 상호 작용할 수 있습니다. 자세한 내용은 참조 [사용자 지정 키 저장소 공급자](../../connect/odbc/custom-keystore-providers.md)합니다.

두 개의 연결 특성은 사용자 지정 키 저장소 공급자와 상호 작용 하는 데 사용 됩니다. 반환할 수 있습니다.

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

전자는 로드 하 고 후자의 응용 프로그램 공급자 통신할 수 있도록 하는 동안 로드 된 키 저장소 공급자를 열거 하는 데 사용 됩니다. 이전 또는 이후 응용 프로그램 공급자 상호 작용을 SQL Server와의 통신을 포함 하지 않는 한 연결을 설정한 후 언제 든 지 이러한 연결 특성을 사용할 수 있습니다. 그러나 드라이버 아직 로드 되지 않았으므로, 설정 및 연결 하기 전에 이러한 특성을 가져오는 드라이버 관리자에서 처리 하 고 예상된 결과 생성 하지 않을 수 있습니다.

#### <a name="loading-a-keystore-provider"></a>Keystore 공급자를 로드합니다.

설정의 `SQL_COPT_SS_CEKEYSTOREPROVIDER` 연결 특성을 사용 하면 클라이언트 응용 프로그램에서 그 안에 포함 된 키 저장소 공급자를 사용할 수 있도록 하는 공급자 라이브러리를 로드 합니다.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 인수 | Description |
|:---|:---|
|`ConnectionHandle`|[입력] 연결 핸들입니다. 유효한 연결 핸들을 해야 하나의 연결 핸들을 통해 로드 된 공급자는 동일한 프로세스에서 다른에서 액세스할 수 있지만 합니다.|
|`Attribute`|[입력] 설정할 특성:는 `SQL_COPT_SS_CEKEYSTOREPROVIDER` 상수입니다.|
|`ValuePtr`|[입력] Null로 끝나는 문자열에 공급자 라이브러리의 파일 이름을 지정 하는 포인터입니다. SQLSetConnectAttrA, ANSI (멀티 바이트) 문자열입니다. SQLSetConnectAttrW, (wchar_t) 유니코드 문자열입니다.|
|`StringLength`|[입력] ValuePtr 문자열 또는 SQL_NTS의 길이입니다.|

드라이버 로드 메커니즘 플랫폼 정의 동적 라이브러리를 사용 하 여 ValuePtr 매개 변수로 식별 된 라이브러리를 로드 하려고 시도 (`dlopen()` Linux와 macOS 등에서 `LoadLibrary()` Windows에서), 그 안에 목록에 정의 된 모든 공급자를 추가 합니다. 드라이버에 알려진 공급자입니다. 다음과 같은 오류가 발생할 수 있습니다.

| 오류 | Description |
|:--|:--|
|`CE203`|동적 라이브러리를 로드할 수 없습니다.|
|`CE203`|라이브러리에 내보낸 "CEKeyStoreProvider" 기호를 찾지 못했습니다.|
|`CE203`|라이브러리에 하나 이상의 공급자가 이미 로드 됩니다.|

`SQLSetConnectAttr`표준 ODBC 진단 메커니즘을 통해 발생 한 모든 오류에 사용할 수는 일반적인 오류 또는 성공 값을 추가 정보를 반환 합니다.

> [!NOTE]
> 응용 프로그램 프로그래머는 것을 요구 하는 모든 쿼리는 모든 연결을 통해 전송 되기 전에 사용자 지정 공급자 로드 되었는지 확인 해야 합니다. 이렇게 하지 않으면 오류가 발생 합니다.

| 오류 | Description |
|:--|:--|
|`CE200`|Keystore 공급자 %1 찾을 수 없습니다. 적절 한 키 저장소 공급자 라이브러리 로드 되었는지 확인 합니다.|

> [!NOTE]
> Keystore 공급자 구현자의 사용 하지 않아야 `MSSQL` 해당 사용자 지정 공급자의 이름입니다. 이 용어는 단독으로 Microsoft에 사용 되도록 예약 이며 이후 기본 제공 공급자와 충돌할 수 있습니다. 사용자 지정 공급자의 이름을이 용어를 사용 하 여 ODBC 경고가 발생할 수 있습니다.

#### <a name="getting-the-list-of-loaded-providers"></a>로드 된 공급자 목록 가져오기

(포함에 기본 제공 합니다.) 드라이버에 현재 로드 된 키 저장소 공급자를 확인 하는 클라이언트 응용 프로그램을 사용 하면이 연결 특성 가져오기 연결한 후 에서만 수행할 수 있습니다.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 인수 | Description |
|:---|:---|
|`ConnectionHandle`|[입력] 연결 핸들입니다. 유효한 연결 핸들을 해야 하나의 연결 핸들을 통해 로드 된 공급자는 동일한 프로세스에서 다른에서 액세스할 수 있지만 합니다.|
|`Attribute`|[입력] 검색할 특성:는 `SQL_COPT_SS_CEKEYSTOREPROVIDER` 상수입니다.|
|`ValuePtr`|[출력] 다음 로드 된 공급자 이름을 반환 하는 메모리에 대 한 포인터입니다.|
|`BufferLength`|[입력] ValuePtr 버퍼의 길이입니다.|
|`StringLengthPtr`|[출력] 바이트 (null 종결 문자 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \*ValuePtr 합니다. ValuePtr null 포인터 이면 길이가 반환 됩니다. 특성 값은 문자열 및 반환할 수 있는 바이트 수 BufferLength null 종료의 길이 뺀 값 보다 크면 경우 문자 데이터에 \*ValuePtr 잘립니다 BufferLength의 길이 만큼 뺀 길이로 null 종결 문자는 드라이버에서 null로 종결 되 고 있습니다.|

전체 목록을 검색을 허용 하려면 모든 가져오기 작업 현재 공급자의 이름을 반환 하 고는 내부 카운터를 증가 합니다. 이 카운터는 빈 문자열 목록의 끝에 도달 하면 ("")가 반환 되 고 카운터 다시 설정 됩니다. Get 작업을 연속 된 다음 목록의 시작 부분에서 다시 진행합니다.

### <a name="communicating-with-keystore-providers"></a>키 저장소 공급자와의 통신

`SQL_COPT_SS_CEKEYSTOREDATA` 연결 특성을 사용 하면 클라이언트 응용 프로그램에서 키 자료 등의 추가 매개 변수를 구성 하기 위한 로드 된 키 저장소 공급자와 통신 합니다. 클라이언트 응용 프로그램 및 공급자 간의 통신은 Get에 따라 간단한 요청-응답 프로토콜을 따르며 집합이 연결 특성을 사용 하 여 요청 합니다. 통신은 클라이언트 응용 프로그램에만 시작 됩니다.

> [!NOTE]
> ODBC의 특성으로 인해 연결 컨텍스트의 해상도로 데이터를 설정 하 여 ODBC 인터페이스만 지원 CEKeyStoreProvider의 응답 (SQLGet/SetConnectAttr)를 호출 합니다.

응용 프로그램 CEKeystoreData 구조를 통해 드라이버를 통해 키 저장소 공급자와 통신합니다.

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| 인수 | Description |
|:---|:---|
|`name`|[입력] 집합, 공급자의 이름에 데이터 전송 됩니다. Get 시 무시 됩니다. Null로 끝나는, 와이드 문자 문자열입니다.|
|`dataSize`|[입력] 구조를 다음 데이터 배열의 크기입니다.|
|`data`|[InOut] 집합, 데이터를 공급자에 게 보낼 수에 있습니다. 임의의 데이터; 수 있습니다. 드라이버에는를 해석 하려고 하지 않으므로 합니다. Get, 시 데이터를 받기 위한 버퍼 공급자에서 읽은입니다.|

#### <a name="writing-data-to-a-provider"></a>공급자에 데이터 쓰기

A `SQLSetConnectAttr` 사용 하 여 호출 된 `SQL_COPT_SS_CEKEYSTOREDATA` 특성 지정 된 키 저장소 공급자를 데이터 "패킷을"를 씁니다.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 인수 | Description |
|:---|:---|
|`ConnectionHandle`| [입력] 연결 핸들입니다. 유효한 연결 핸들을 해야 하나의 연결 핸들을 통해 로드 된 공급자는 동일한 프로세스에서 다른에서 액세스할 수 있지만 합니다.|
|`Attribute`|[입력] 설정할 특성:는 `SQL_COPT_SS_CEKEYSTOREDATA` 상수입니다.|
|`ValuePtr`|[입력] CEKeystoreData 구조에 대 한 포인터입니다. 이름 필드는 구조체의 데이터가 의도 한 공급자를 식별 합니다.|
|`StringLength`|[입력] SQL_IS_POINTER 상수|

통해 자세한 추가 오류 정보를 얻을 수 있습니다 [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)합니다.

> [!NOTE]
> 공급자 이므로 필요한 경우 기록된 된 데이터는 특정 연결에 연결 하려면 연결 핸들을 사용할 수 있습니다. 이 연결 구성을 구현 하는 데 유용 합니다. 또한 연결 컨텍스트를 무시 고 해당 데이터를 데이터를 보내는 데 사용 하는 연결에 관계 없이 동일 하 게 처리 될 수 있습니다. 참조 [컨텍스트 연결](../../connect/odbc/custom-keystore-providers.md#context-association) 자세한 정보에 대 한 합니다.

#### <a name="reading-data-from-a-provider"></a>공급자에서 데이터 읽기

에 대 한 호출 `SQLGetConnectAttr` 를 사용 하는 `SQL_COPT_SS_CEKEYSTOREDATA` 특성 "패킷을"에서 데이터를 읽고 *는 마지막 작성-대상* 공급자입니다. 발생 한 경우 none는 함수 시퀀스 오류 발생 합니다. 키 저장소 공급자 구현 자가 "더미 쓰기 를" 작업을 수행 하는 경우 다른 부작용이 발생 하지 않고 읽기 작업에 대 한 공급자를 선택 하는 방법으로 0 바이트를 지원 해야 합니다.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 인수 | Description |
|:---|:---|
|`ConnectionHandle`|[입력] 연결 핸들입니다. 유효한 연결 핸들을 해야 하나의 연결 핸들을 통해 로드 된 공급자는 동일한 프로세스에서 다른에서 액세스할 수 있지만 합니다.|
|`Attribute`|[입력] 검색할 특성:는 `SQL_COPT_SS_CEKEYSTOREDATA` 상수입니다.|
|`ValuePtr`|[출력] 공급자에서 읽은 데이터를 배치 되는 CEKeystoreData 구조에 대 한 포인터입니다.|
|`BufferLength`|[입력] SQL_IS_POINTER 상수|
|`StringLengthPtr`|[출력] BufferLength 반환할 버퍼에 대 한 포인터입니다. 하는 경우 * ValuePtr이 null 포인터 이면 길이가 반환 됩니다.|

호출자가 CEKEYSTOREDATA 구조를 다음 충분 한 길이의 버퍼에 쓸 공급자에 대 한 할당 되는 확인 해야 합니다. 반환 되 면 해당 dataSize 필드가 공급자에서 읽은 데이터의 실제 길이 함께 업데이트 됩니다. 통해 자세한 추가 오류 정보를 얻을 수 있습니다 [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)합니다.

이 인터페이스는 추가 요구 사항이 없습니다 응용 프로그램과 keystore 공급자 간에 전송 되는 데이터의 형식에 배치 합니다. 각 공급자는 필요에 따라 자체 프로토콜/데이터 형식을 정의할 수 있습니다.

키 저장소 공급자를 구현 하는의 예제를 보려면 [사용자 지정 키 저장소 공급자](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>상시 암호화를 사용 하는 경우 ODBC 드라이버의 제한 사항

### <a name="bulk-copy-function-usage"></a>대량 복사 함수 사용
사용은 [SQL 대량 복사 함수](/sql-docs/docs/relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc) 상시 암호화로 ODBC 드라이버를 사용 하는 경우 지원 되지 않습니다. SQL 대량 복사 함수와 함께 사용 되는 암호화 된 열에서 없습니다 투명 한 암호화/암호 해독이 발생 합니다.

### <a name="asynchronous-operations"></a>비동기 작업
ODBC 드라이버는 사용을 허용 하는 동안 [비동기 작업](/sql-docs/docs/relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel) 상시 암호화,이 생깁니다 성능에 영향 되는 작업에 항상 암호화를 사용 하도록 설정 합니다. 에 대 한 호출 `sys.sp_describe_parameter_encryption` 명령문을 차단 하 고 반환 하기 전에 메타 데이터를 반환 하는 서버에 대해 기다려야 하면 드라이버에 대 한 암호화 메타 데이터를 확인 하려면 `SQL_STILL_EXECUTING`합니다.

## <a name="always-encrypted-api-summary"></a>상시 암호화 API 요약

### <a name="connection-string-keywords"></a>연결 문자열 키워드

|이름|Description|  
|----------|-----------------|  
|`ColumnEncryption`|사용 가능한 값은 `Enabled` / `Disabled`합니다.<br>`Enabled`-연결에 대해 항상 암호화 기능을 사용 하도록 설정 합니다.<br>`Disabled`-연결에 대해 항상 암호화 기능을 사용 하지 않도록 설정 합니다. <br><br>기본값은 `Disabled`입니다.|  
|`KeyStoreAuthentication` | 유효한 값: `KeyVaultPassword`,`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | 때 `KeyStoreAuthentication`  =  `KeyVaultPassword`, 유효한 Azure Active Directory 사용자 계정 이름으로이 값을 설정 합니다. <br>때 `KeyStoreAuthetication`  =  `KeyVaultClientSecret` 유효한 Azure Active Directory 응용 프로그램 클라이언트 ID를이 값을 설정 합니다. |
|`KeyStoreSecret` | 때 `KeyStoreAuthentication`  =  `KeyVaultPassword` 이 값을 해당 사용자 이름의 암호를 설정 합니다. <br>때 `KeyStoreAuthentication`  =  `KeyVaultClientSecret` 이 값을 유효한 Azure Active Directory 응용 프로그램 클라이언트 ID와 연결 된 응용 프로그램 암호 설정|

### <a name="connection-attributes"></a>연결 특성

|이름|유형|Description|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|연결 전|`SQL_COLUMN_ENCRYPTION_DISABLE`(0)-상시 암호화 사용 안 함 <br>`SQL_COLUMN_ENCRYPTION_ENABLE`(1)--상시 암호화 사용|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|연결 후|[설정] CEKeystoreProvider 로드 하려고 합니다.<br>[가져오기] CEKeystoreProvider 이름 반환|
|`SQL_COPT_SS_CEKEYSTOREDATA`|연결 후|[설정] 데이터를 CEKeystoreProvider 기록<br>[가져오기] CEKeystoreProvider에서 데이터 읽기|

### <a name="statement-attributes"></a>문 특성

|이름|Description|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED`(0)-문에 대 한 상시 암호화 사용 하지 않도록 설정 <br>`SQL_CE_RESULTSETONLY`(1)--만 암호 해독 합니다. 결과 집합 및 반환 값을 해독 되 고 매개 변수는 암호화 되지 않습니다. <br>`SQL_CE_ENABLED`(3)-항상 암호화 됨을 활성화 하 고 매개 변수 및 결과 모두 사용|

### <a name="descriptor-fields"></a>설명자 필드

|IPD 필드|크기/유형|기본값|Description|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 바이트)|0|때 0 (기본값):이 매개 변수를 암호화 하는 결정 암호화 메타 데이터의 가용성에 따라 결정 됩니다.<br><br>0이 아닌 경우:이 매개 변수에 대해 사용할 수 있는 암호화 메타 데이터의 경우 암호화 합니다. 그렇지 않으면 요청은 실패 하며 오류 [CE300] [Microsoft] [ODBC Driver 13 for SQL Server] 필수 암호화 매개 변수에 대해 지정 되었지만 암호화 메타 데이터는 서버에서 제공 합니다.|

## <a name="see-also"></a>관련 항목:

- [상시 암호화(데이터베이스 엔진)](/sql-docs/docs/relational-databases/security/encryption/always-encrypted-database-engine)
- [상시 암호화 블로그](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)


