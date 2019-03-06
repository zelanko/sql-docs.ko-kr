---
title: SQL Server용 ODBC 드라이버와 함께 상시 암호화 사용 | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: dd6037cbc40c9cf422c38827d5c96115db33db73
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56956064"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>SQL Server용 ODBC 드라이버와 함께 상시 암호화 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>적용 가능 대상

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>소개

이 문서를 사용 하 여 ODBC 응용 프로그램을 개발 하는 방법에 대해 설명 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 하며 [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)합니다.

Always Encrypted를 사용하면 클라이언트 애플리케이션이 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. SQL Server용 ODBC 드라이버와 같은 상시 암호화 지원 드라이버는 클라이언트 애플리케이션의 중요한 데이터를 투명하게 암호화하고 암호 해독합니다. 이 드라이버는 중요 데이터베이스 열에 해당하는 쿼리 매개 변수를 자동으로 확인하고(Always Encrypted를 사용하여 보호) 데이터를 SQL Server 또는 Azure SQL Database로 전달하기 전에 이러한 매개 변수의 값을 암호화합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요.

### <a name="prerequisites"></a>사전 요구 사항

데이터베이스에서 상시 암호화를 구성합니다. 상시 암호화를 구성하려면 상시 암호화 키를 프로비전하고 선택한 데이터베이스 열에 대한 암호화를 설정해야 합니다. 데이터베이스에 상시 암호화가 구성되지 않은 경우 [상시 암호화 시작](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)의 지침을 따르세요. 특히, 데이터베이스를 열 마스터 키 (CMK), 열 암호화 키 (CEK), 및 해당 CEK를 사용 하 여 암호화 하는 하나 이상의 열을 포함 하는 테이블에 대 한 메타 데이터 정의 포함 해야 합니다.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>ODBC 응용 프로그램에서 상시 암호화를 사용 하도록 설정

값을 설정 된 경우 매개 변수 암호화 및 암호화 하는 결과 집합 열 암호 해독 모두를 사용 하도록 설정 하는 가장 쉬운 방법은 합니다 `ColumnEncryption` 연결 문자열 키워드 **사용**합니다. 다음은 상시 암호화를 사용하는 연결 문자열의 예제입니다.

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

DSN 구성에서 동일한 키 및 값 (있는 경우 연결 문자열 설정으로 재정의 됩니다)를 사용 하 여 또는 프로그래밍 방식으로 사용 하 여 암호화를 활성화할 수도 있습니다 항상를 `SQL_COPT_SS_COLUMN_ENCRYPTION` 사전 연결 특성입니다. 연결 문자열 또는 DSN에 설정 된 값을 재정의 이러한 방식으로 설정:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

연결에 사용 하도록 설정 하면 개별 쿼리에 대해 상시 암호화의 동작을 조정할 수 있습니다. 참조 [성능 영향의 Always Encrypted 제어](#controlling-the-performance-impact-of-always-encrypted) 아래 자세한 내용은 합니다.

암호화 또는 해독 성공 하기에 충분 하지 않습니다 상시 암호화 사용 있는지 확인 해야 합니다.

- 애플리케이션에는 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 데이터베이스 권한이 있으며 데이터베이스에서 상시 암호화 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 참조 하세요 [데이터베이스 사용 권한](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)합니다.

- 응용 프로그램 쿼리 암호화 된 열에 대 한 Cek를 보호 하는 CMK를 액세스할 수 있습니다. 이 CMK를 저장 하는 키 저장소 공급자에 따라 달라 집니다. 참조 [열 마스터 키 저장소를 사용 하 여 작업](#working-with-column-master-key-stores) 자세한 내용은 합니다.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정

연결에 Always Encrypted를 사용 하면 표준 ODBC Api를 사용할 수 있습니다 (참조 [ODBC 샘플 코드](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) 하거나 [ODBC 프로그래머 참조](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) 암호화 된 데이터베이스 열에 데이터를 검색 하거나 수정 합니다. 데이터베이스 사용 권한 및 열 마스터 키에 액세스할 수, 드라이버는 암호화 된 열을 대상에 투명 하 게 작동 하는 암호화 된 열에서 검색 데이터를 해독 하는 모든 쿼리 매개 변수를 암호화 하는 응용 프로그램에 필요한 것으로 가정 합니다 열 암호화 되지 않은 것 처럼 응용 프로그램입니다.

상시 암호화를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없는 경우 암호화된 열에서 데이터를 검색할 수 있습니다. 그러나 드라이버에서 모든 암호 해독을 시도 하지 않습니다 하 고 응용 프로그램 (바이트 배열)로 암호화 된 이진 데이터를 받게 됩니다.

아래 표에서는 상시 암호화 사용 여부에 따른 쿼리 동작을 요약합니다.

|쿼리 특성 | 상시 암호화가 설정되고 애플리케이션에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 애플리케이션에서 키 또는 키 메타데이터에 액세스할 수 없는 경우 | 상시 암호화를 사용하지 않는 경우|
|:---|:---|:---|:---|
| 암호화 된 열을 대상으로 하는 매개 변수입니다. | 매개 변수 값이 투명하게 암호화됩니다. | Error | Error|
| 암호화된 열을 대상으로 하는 매개 변수 없이 암호화된 열에서 데이터를 검색합니다.| 암호화된 열의 결과가 투명하게 암호 해독됩니다. 응용 프로그램 일반 텍스트 열 값을 받습니다. | Error | 암호화된 열의 결과가 암호 해독되지 않습니다. 애플리케이션에서 암호화된 값을 바이트 배열로 수신합니다.

다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 예제에서는 다음 스키마를 사용 하 여 테이블을 가정합니다. SSN 및 BirthDate 열은 암호화되어 있습니다.

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

- 샘플 코드에는 암호화에 대한 내용이 없습니다. 드라이버는 자동으로 검색 하 고 암호화 된 열을 대상의 SSN 및 날짜 매개 변수의 값을 암호화 합니다. 이렇게 하면 애플리케이션에 투명하게 암호화할 수 있습니다.

- 암호화된 열을 포함하여 데이터베이스 열에 삽입된 값은 바인딩된 매개 변수로 전달됩니다([SQLBindParameter Function](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx) 참조). 매개 변수를 사용하여 암호화되지 않은 열에 값을 전달하는 것은 선택 사항이지만(그러나 SQL 삽입을 방지할 수 있으므로 매우 권장됨) 암호화된 열을 대상으로 하는 값에 필요합니다. SSN 또는 BirthDate 열에 삽입 된 값 쿼리 문에 포함 된 리터럴로 전달 하는 경우 드라이버는 암호화 하거나, 쿼리에서 리터럴을 처리 하려고 시도 하지 않습니다 때문에 쿼리가 실패 합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.

- SSN 열에 삽입 하는 매개 변수의 SQL 형식에 매핑되는 SQL_CHAR로 되어는 **char** SQL Server 데이터 형식 (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). 매개 변수의 형식에 매핑되는 SQL_WCHAR 설정 되었는지 여부 **nchar**, 상시 암호화에서는 암호화 된 char 값을 암호화 된 nchar 값에서 서버 쪽 변환을 지원 하지 않으므로 쿼리가 실패 합니다. 참조 [ODBC 프로그래머 참조-부록 d: 데이터 형식](https://msdn.microsoft.com/library/ms713607.aspx) 데이터 형식 매핑에 대 한 정보에 대 한 합니다.

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

#### <a name="plaintext-data-retrieval-example"></a>일반 텍스트 데이터 검색 예제

다음 예제에서는 암호화된 값을 기준으로 데이터를 필터링하고 암호화된 열에서 일반 텍스트 데이터를 검색하는 방법을 보여 줍니다. 다음에 유의하세요.

- 해당 드라이버가 서버로 전달하기 전에 투명하게 암호화할 수 있도록 SQLBindParameter 매개 변수를 사용하여 SSN 열에서 필터링하기 위해 WHERE 절에 사용되는 값을 전달해야 합니다.

- 이 드라이버는 SSN 및 BirthDate 열에서 검색한 데이터의 암호를 투명하게 해독하므로 프로그램에서 인쇄한 모든 값은 일반 텍스트로 표시됩니다.

> [!NOTE]
> 쿼리는 결정적 암호화 하는 경우에 암호화 된 열에서 같음 비교를 수행할 수 있습니다. 자세한 내용은 [결정적 또는 임의 암호화 선택](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)을 참조하세요.

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

#### <a name="ciphertext-data-retrieval-example"></a>암호 텍스트 데이터 검색 예제

상시 암호화를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예제에서는 암호화된 열에서 암호화된 이진 데이터를 검색하는 방법을 보여 줍니다. 다음에 유의하세요.

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

이 섹션에서는 ODBC 애플리케이션에서 암호화된 열을 쿼리할 때 발생하는 일반적인 오류 범주와 이를 방지하는 방법을 설명합니다.

##### <a name="unsupported-data-type-conversion-errors"></a>지원되지 않는 데이터 형식 변환 오류

상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 지원되는 형식 변환의 자세한 목록은 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. 데이터 형식 변환 오류를 방지 하려면 SQLBindParameter 암호화 된 열을 대상으로 하는 매개 변수를 사용 하 여 사용 하는 경우 다음 사항을 관찰 해야 있는지 확인 합니다.

- 매개 변수의 SQL 형식을 동일 하거나 대상 열의 형식과 동일 하거나 열의 형식 변환이 SQL 유형에 서 지원 합니다.

- SQL Server 데이터 형식이 `decimal` 및 `numeric`인 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다.

- 대상 열을 수정하는 쿼리에서 SQL Server 데이터 형식이 `datetime2`, `datetimeoffset` 또는 `time`인 열을 대상으로 하는 매개 변수의 정밀도가 대상 열의 정밀도보다 크지 않아야 합니다.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류

암호화 된 열을 대상으로 하는 모든 값을 서버로 전송 되기 전에 암호화 해야 합니다. 암호화된 열의 일반 텍스트 값으로 삽입, 수정 또는 필터링하면 오류가 발생합니다. 이러한 오류를 방지하려면 다음을 확인합니다.

- 상시 암호화가 설정 (DSN, 연결 문자열에서에서 설정 하 여 이전 연결 된 `SQL_COPT_SS_COLUMN_ENCRYPTION` 특정 연결에 대 한 연결 특성 또는 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특정 문에 대 한 문 특성).

- SQLBindParameter를 사용하여 암호화된 열을 대상으로 하는 데이터를 전송합니다. 아래 예제에서는 리터럴을 SQLBindParameter에 인수로 전달하는 대신암호화된 열(SSN)에서 리터럴/상수로 잘못 필터링하는 쿼리를 보여 줍니다.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>SQLSetPos 및 SQLMoreResults를 사용 하는 경우 주의 사항

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API SQLBindCol를 사용 하 여 바인딩된 하 고 데이터 행에 이전에 가져온 버퍼를 사용 하 여 결과 집합의 행을 업데이트 하려면 응용 프로그램을 수 있습니다. 암호화 된 고정 길이 형식 비대칭 패딩 동작으로 인해 예기치 않게 행의 다른 열에 업데이트를 수행 하는 동안 이러한 열의 데이터를 변경 하는 것이 같습니다. 값은 버퍼 크기 보다 작은 경우 AE를 사용 하 여 고정된 길이 문자 값이 패딩 됩니다.

이 문제를 완화 하려면 사용 합니다 `SQL_COLUMN_IGNORE` 의 일부로 업데이트 되는 열을 무시 하도록 플래그 `SQLBulkOperations` 사용 하는 경우 `SQLSetPos` 커서에 대 한 업데이트를 기반 합니다.  응용 프로그램에 의해 직접 수정 하지는 않은 모든 열을 무시할지, 성능에 대 한 버퍼에 바인딩된 열의 잘림을 방지 하려면 둘 다 *작은* 실제 (DB) 크기 보다 합니다. 자세한 내용은 [SQLSetPos 함수 참조](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx)합니다.

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

응용 프로그램에서 호출할 수 있습니다 [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) 준비 된 문에서 열에 대 한 메타 데이터를 반환 합니다.  상시 암호화를 사용 하는 경우 호출 `SQLMoreResults` *하기 전에* 호출 `SQLDescribeCol` 사용 하면 [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 호출 되는 반환 하지 않는 올바르게 일반 텍스트 암호화 된 열에 대 한 메타 데이터입니다. 이 문제를 방지 하려면 호출 `SQLDescribeCol` 준비 된 문에서 *하기 전에* 호출 `SQLMoreResults`합니다.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

상시 암호화는 클라이언트 쪽 암호화 기술이므로 데이터베이스가 아닌 클라이언트 쪽에서 대부분의 성능 오버헤드가 발생합니다. 암호화 및 암호 해독 작업의 비용 외에 클라이언트 쪽 성능 오버헤드의 원인은 다음과 같습니다.

- 쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복

- 열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출

이 섹션에서는 SQL Server용 ODBC Driver의 기본 제공 성능 최적화와 위의 두 성능 요소의 영향을 제어할 수 있는 방법에 대해 설명합니다.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복 제어

연결에 대한 상시 암호화가 설정된 경우 기본적으로 드라이버는 각 매개 변수화된 쿼리에 대해 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)을 호출하고 매개 변수 값 없이 쿼리 문을 SQL Server에 전달합니다. 이 저장된 프로시저 매개 변수를 암호화 해야 하 고 그렇다면 알아 쿼리 문을 분석 하 여, 드라이버를 암호화할 수 있도록 각 매개 변수에 대해 암호화 관련 정보를 반환 합니다. 위의 동작은 클라이언트 응용 프로그램에 대 한 투명도 수준의: 응용 프로그램 (및 응용 프로그램 개발자)에 암호화 된 열을 대상으로 하는 값이 전달 되는 있다면 어떤 쿼리가 암호화 된 열 액세스 알아야 할 필요 하지 않습니다 매개 변수에서 드라이버입니다.

### <a name="per-statement-always-encrypted-behavior"></a>문 별 동작을 상시 암호화

매개 변수가 있는 쿼리에 대 한 암호화 메타 데이터 검색의 성능 영향을 제어 하려면 연결에서 사용할 수 있는 경우 개별 쿼리에 대해 Always Encrypted 동작을 변경할 수 있습니다. 이 이렇게 하면 확실히는 `sys.sp_describe_parameter_encryption` 있는 쿼리에 있는 매개 변수 대상이 암호화 된 열에 대해서만 호출 됩니다. 단, 이 경우 암호화의 투명성이 저하될 수 있습니다. 데이터베이스에서 추가 열을 암호화하는 경우 스키마 변경에 맞게 애플리케이션 코드를 변경해야 할 수 있습니다.

문의 Always Encrypted 동작을 제어 하려면 호출을 설정 하는 SQLSetStmtAttr는 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 문 특성을 다음 값 중 하나:

|값|설명|
|-|-|
|`SQL_CE_DISABLED` (0)|암호화 된 문에 대 한 항상 사용할 수 없음|
|`SQL_CE_RESULTSETONLY` (1)|암호 해독에만 합니다. 결과 집합 및 반환 값은 암호를 해독 하 고 매개 변수는 암호화 되지 않습니다.|
|`SQL_CE_ENABLED` (3) | 암호화가 사용 되 고 매개 변수 및 결과에 사용 되는 항상|

상시 암호화와 연결에서 만든 새 문 핸들 SQL_CE_ENABLED 기본값으로 사용할 수 있습니다. 이 사용 하 여 연결에서 만든 비활성화 SQL_CE_DISABLED 기본값으로 (및에 Always Encrypted를 사용 하도록 설정할 수 없는.)

클라이언트 응용 프로그램의 쿼리 대부분이 암호화 된 열에 액세스 하는 경우 다음이 권장 됩니다.

- `ColumnEncryption` 연결 문자열 키워드를 `Enabled`로 설정합니다.

- 설정 합니다 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특성을 `SQL_CE_DISABLED` 문에서 암호화 된 모든 열을 액세스 하지 않습니다. 두 호출 없게 `sys.sp_describe_parameter_encryption` 결과에 값을 해독 하려고 뿐만 아니라 설정 합니다.
    
- 설정 된 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특성을 `SQL_CE_RESULTSETONLY` 에서 암호화를 요구 하는 모든 매개 변수가 없지만 암호화 된 열에서 데이터를 검색 하는 문입니다. 이렇게 하면 호출 `sys.sp_describe_parameter_encryption` 및 매개 변수 암호화 합니다. 암호화 된 열을 포함 하는 결과를 해독할 계속 됩니다.

## <a name="always-encrypted-security-settings"></a>상시 암호화 보안 설정

### <a name="force-column-encryption"></a>열 암호화

매개 변수의 암호화를 적용 하려면 설정의 `SQL_CA_SS_FORCE_ENCRYPT` SQLSetDescField 함수 호출을 통해 IPD (구현 매개 변수 설명자) 필드입니다. 0이 아닌 값 하면 드라이버 관련 매개 변수 암호화 메타 데이터가 반환 될 때 오류를 반환 합니다.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

SQL Server가 매개 변수를 암호화하지 않아도 되는 것을 드라이버에 알리는 경우 매개 변수를 사용하는 쿼리는 실패합니다. 이렇게 하면 데이터 노출을 야기할 수 있는 잘못된 암호화 메타데이터를 클라이언트에게 제공하는 손상된 SQL Server를 포함하는 보안 공격에 대한 보호 기능이 강화됩니다.

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

열 암호화 키의 암호를 해독 하는 열 마스터 키 저장소에 대 한 호출의 수를 줄이려면 드라이버 메모리에 일반 텍스트 Cek를 캐시 합니다. CEK 캐시 드라이버 전역적 이며 하나의 연결을 사용 하 여 연결 되지 않습니다. 데이터베이스 메타 데이터에서 여 ECEK를 받은 후 드라이버는 먼저 일반 텍스트 CEK에 해당 하는 캐시에 있는 암호화 된 키 값을 찾으려고 합니다. 드라이버는 해당 일반 텍스트 CEK 캐시에서 찾을 수 없는 경우에 CMK를 포함 하는 키 저장소를 호출 합니다.

> [!NOTE]
> SQL Server 용 ODBC 드라이버에서 두 시간의 시간 초과 이후 캐시에서 항목 제거 됩니다. 즉, 또는 2 시간 마다 응용 프로그램의 수명 동안 한 번만 키 저장소를 연결 하는 드라이버는 지정 된 ECEK에 대 한 더 작은 합니다.

SQL Server 용 ODBC 드라이버 17.1부터, CEK 캐시 시간 제한을 조정할 수는 `SQL_COPT_SS_CEKCACHETTL` CEK 캐시에 남아 있는 시간 (초) 수를 지정 하는 연결 특성입니다. 캐시의 전역 특성상 드라이버에 대 한 유효한 연결 핸들에서이 특성을 조정할 수 있습니다. 때 TTL를 줄이면 새 TTL을 초과 하는 기존 Cek 캐시 제거 됩니다. 0 인 경우에 없는 Cek 캐시 됩니다.

### <a name="trusted-key-paths"></a>신뢰할 수 있는 키 경로

SQL Server 용 ODBC 드라이버 17.1로 시작 된 `SQL_COPT_SS_TRUSTEDCMKPATHS` 연결 특성을 사용 하면 응용 프로그램을 사용 해야 하는 Always Encrypted 작업만 cmk를 키가 경로 의해 식별 된 지정된 된 목록입니다. 기본적으로이 특성이 NULL 이며이 드라이버에서 모든 키 경로 허용 한다는 것을 의미 합니다. 이 기능을 사용 하려면 설정 `SQL_COPT_SS_TRUSTEDCMKPATHS` 허용 된 키 경로 나열 하는 null 구분 되어 null로 끝나는 와이드 문자 문자열을 가리키도록 합니다. 이 특성에 의해 가리키는 메모리 유효한 상태로 유지 되어야 서버 메타 데이터에 지정 된 대로 CMK 경로 인지 대이 드라이버는 확인 하는 기반이 있는 설정은---연결 핸들을 사용 하 여 암호화 또는 암호 해독 작업 중 목록입니다. CMK 경로 목록에 없는 경우 작업이 실패 합니다. 응용 프로그램 특성을 다시 설정 하지 않고 신뢰할 수 있는 Cmk 목록을 변경 하려면이 특성이 가리키는 메모리의 내용을 변경할 수 있습니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업

를 암호화 하거나 데이터를 해독 하려면 드라이버를 대상 열에 대해 구성 된 CEK를 입수해 야 합니다. Cek는 데이터베이스 메타 데이터에 암호화 된 형식 (ECEKs)에 저장 됩니다. 각 CEK 암호화에 사용 된 해당 CMK에 있습니다. [데이터베이스 메타 데이터](../../t-sql/statements/create-column-master-key-transact-sql.md) 자체 CMK를 저장 하지 않는 키 저장소 CMK를 찾는 데 사용할 수 있는 정보와 키 저장소의 이름을 포함 합니다.

ECEK의 일반 텍스트 값을 가져오려면, 드라이버 먼저 CEK와 CMK는 해당 하는 방법에 대 한 메타 데이터를 가져오고이 정보를 사용 하 여 CMK를 포함 하는 키 저장소에 문의 하 고 암호 해독 된 ECEK에 요청 합니다. 드라이버는 키 저장소 공급자를 사용 하 여 키 저장소와 통신 합니다.

### <a name="built-in-keystore-providers"></a>기본 제공 키 저장소 공급자

SQL Server 용 ODBC 드라이버는 다음과 같은 기본 제공 키 저장소 공급자를 사용 하 여 제공 됩니다.

| 속성 | 설명 | (메타 데이터) 공급자 이름 |가용성|
|:---|:---|:---|:---|
|Azure Key Vault |Azure Key Vault에 저장소 Cmk | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Windows 인증서 저장소|Windows 키 저장소에 Cmk를 로컬로 저장| `MSSQL_CERTIFICATE_STORE`|Windows|

- 사용자 또는 DBA는 열 마스터 키 메타데이터에 구성된 공급자 이름이 정확하고 열 마스터 키 경로가 특정 공급자에 적합한 키 경로 형식을 준수해야 합니다. [CREATE COLUMN MASTER KEY(Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 실행할 때 적합한 공급자 이름 및 키 경로를 자동으로 생성하는 SQL Server Management Studio 등의 도구를 사용하여 키를 구성하는 것이 좋습니다.

- 애플리케이션에서 키 저장소의 키에 액세스할 수 있어야 합니다. 여기에는 키 저장소에 따라 애플리케이션 액세스를 키 및/또는 키 저장소에 부여하거나 기타 키 저장소 관련 구성 단계를 수행하는 작업이 포함될 수 있습니다. 예를 들어, Azure Key Vault에 액세스 하려면 키 저장소에 올바른 자격 증명을 제공 합니다.

### <a name="using-the-azure-key-vault-provider"></a>Azure Key Vault 공급자 사용

Azure 주요 자격 증명 모음은 상시 암호화에 대한 열 마스터 키를 저장 및 관리하는 편리한 옵션입니다(특히 애플리케이션이 Azure에서 호스트되는 경우). Linux, macOS 및 Windows의 SQL Server 용 ODBC 드라이버는 Azure Key Vault에 대 한 기본 제공 열 마스터 키 저장소 공급자를 포함합니다. 참조 [Azure Key Vault-단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)를 [Key Vault를 사용 하 여 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), 및 [Azure Key Vault에 열 마스터 키 만들기](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) Azure 키를 구성 하는 방법은 자격 증명 모음 Always Encrypted에 대 한 합니다.

> [!NOTE]
> Linux 및 macOS, 드라이버 버전 17.2 이상 `libcurl` 이 공급자를 사용 하는 데 필요한 아닌 명시적 종속성 있으므로 드라이버를 사용 하 여 다른 작업은 필요 하지 않습니다. 오류가 발생 하는 경우와 관련 하 여 `libcurl`, 설치 되어 있는지 확인 합니다.

드라이버가 다음 자격 증명 형식을 사용 하 여 Azure Key Vault에 인증을 지원 합니다.

- 사용자 이름/암호-이 메서드를 사용 하 여 자격 증명이 Azure Active Directory 사용자 및 해당 암호의 이름입니다.

- 클라이언트 I d/비밀-이 메서드를 사용 하 여 자격 증명은 응용 프로그램 클라이언트 ID 및 응용 프로그램 비밀입니다.

- 관리 서비스 Id-이 메서드를 사용 하 여 자격 증명이 시스템 할당 id 또는 사용자 할당 id입니다. 사용자 할당 id에 대해 UID 사용자 id의 개체 ID로 설정 됩니다.

열 암호화에 대 한 AKV에 저장 된 Cmk를 사용 하는 드라이버를 허용 하려면 다음 연결 문자열 전용 키워드를 사용 합니다.

|자격 증명 유형| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|사용자 이름/암호| `KeyVaultPassword`|사용자 계정 이름|암호|
|클라이언트 I d/비밀| `KeyVaultClientSecret`|클라이언트 ID|비밀|

#### <a name="example-connection-strings"></a>연결 문자열 예

다음 연결 문자열에는 두 가지 자격 증명 형식을 사용 하 여 Azure Key Vault에 인증 하는 방법을 보여 줍니다.

**ClientID/비밀**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**사용자 이름/암호**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

다른 ODBC 응용 프로그램은 변경 하지는 CMK 저장소 AKV를 사용 해야 합니다.

### <a name="using-the-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자 사용

라는 Windows 인증서 저장소에 대 한 기본 제공 열 마스터 키 저장소 공급자를 포함 하는 Windows의 SQL Server 용 ODBC 드라이버 `MSSQL_CERTIFICATE_STORE`합니다. (이 공급자는 macOS 또는 Linux에서 사용할 수 있습니다.) 이 공급자를 사용 하 여 CMK 클라이언트 컴퓨터에 로컬로 저장 되어 이며 응용 프로그램에서 추가 구성 없이 드라이버와 함께 사용 하는 데 필요한 합니다. 그러나 응용 프로그램 저장소에 인증서 및 개인 키에 액세스할 수 있어야 합니다. 자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted)을 참조하세요.

### <a name="using-custom-keystore-providers"></a>사용자 지정 키 저장소 공급자 사용

ODBC Driver for SQL Server는 또한 CEKeystoreProvider 인터페이스를 사용 하 여 사용자 지정 타사 키 저장소 공급자를 지원 합니다. 이 쿼리를 로드 하 고 암호화 된 열에 액세스 하려면 드라이버에서 사용 될 수 있도록 키 저장소 공급자를 구성 하려면 응용 프로그램을 수 있습니다. 응용 프로그램 저장소 SQL Server에 대 한 Cek를 암호화 하 고 ODBC 사용 하 여 암호화 된 열에 액세스 하는 이상의 작업을 수행 하기 위해 키 저장소 공급자와 직접 상호 작용할 수 있습니다. 자세한 내용은 [사용자 지정 키 저장소 공급자](../../connect/odbc/custom-keystore-providers.md)합니다.

두 연결 특성은 사용자 지정 키 저장소 공급자와 상호 작용 하는 데 사용 됩니다. 반환할 수 있습니다.

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

전자는를 로드 하 고 두 번째 응용 프로그램 공급자 통신이 가능 하도록 하는 동안 로드 된 키 저장소 공급자를 열거 합니다. 이전 또는 이후 응용 프로그램 공급자 상호 작용은 SQL Server와의 통신을 포함 하지 않는 연결을 설정한 후 언제 든 지 이러한 연결 특성을 사용할 수 있습니다. 그러나 드라이버 아직 로드 되었으므로, 설정 및 연결 하기 전에 이러한 특성을 가져오는 드라이버 관리자에 의해 처리 하면 및 예상된 결과 얻을 수 없는 합니다.

#### <a name="loading-a-keystore-provider"></a>키 저장소 공급자를 로드합니다.

설정 된 `SQL_COPT_SS_CEKEYSTOREPROVIDER` 연결 특성을 사용 하면 클라이언트 응용 프로그램이 그 안에 포함 된 키 저장소 공급자를 사용할 수 있도록 공급자 라이브러리를 로드 합니다.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`|[입력] 연결 핸들입니다. 올바른 연결 핸들을 해야 되지만 하나의 연결 핸들을 통해 로드할 공급자 동일한 프로세스에서 다른 액세스할 수 있습니다.|
|`Attribute`|[입력] 설정할 특성입니다:는 `SQL_COPT_SS_CEKEYSTOREPROVIDER` 상수입니다.|
|`ValuePtr`|[입력] 공급자 라이브러리의 파일 이름을 지정 하는 null로 끝나는 문자열에 대 한 포인터입니다. SQLSetConnectAttrA, ANSI (멀티 바이트) 문자열입니다. SQLSetConnectAttrW, 유니코드 (wchar_t) 문자열입니다.|
|`StringLength`|[입력] SQL_NTS ValuePtr 문자열의 길이입니다.|

드라이버 로드 메커니즘 플랫폼 정의 동적 라이브러리를 사용 하 여 ValuePtr 매개 변수로 식별 된 라이브러리를 로드 하려고 합니다. (`dlopen()` Linux 및 macOS에서 `LoadLibrary()` Windows에서), 여기 목록에 정의 된 모든 공급자를 추가 합니다. 드라이버에 알려진 공급자입니다. 다음 오류가 발생할 수 있습니다.

| Error | 설명 |
|:--|:--|
|`CE203`|동적 라이브러리를 로드할 수 없습니다.|
|`CE203`|라이브러리의 "CEKeyStoreProvider" 내보낸 기호를 찾을 수 없습니다.|
|`CE203`|라이브러리에서 하나 이상의 공급자는 이미 로드 됩니다.|

`SQLSetConnectAttr` 표준 ODBC 진단 메커니즘을 통해 발생 한 오류에 사용할 수 있는 일반적인 오류 또는 성공 값 및 추가 정보는를 반환.

> [!NOTE]
> 응용 프로그램 프로그래머는 것을 요구 하는 모든 쿼리는 모든 연결을 통해 전송 되기 전에 모든 사용자 지정 공급자 로드 되었는지 확인 해야 합니다. 그렇게 하지 않으면 오류가 발생합니다.

| Error | 설명 |
|:--|:--|
|`CE200`|키 저장소 공급자 %1 찾을 수 없습니다. 적절 한 키 저장소 공급자 라이브러리가 로드 되었는지 확인 합니다.|

> [!NOTE]
> 키 저장소 공급자 구현자의 사용을 피해 야 `MSSQL` 해당 사용자 지정 공급자의 이름입니다. 이 용어는 Microsoft 용도로 단독으로 예약 되며 향후 기본 제공 공급자를 사용 하 여 충돌을 일으킬 수 있습니다. 사용자 지정 공급자의 이름을이 용어를 사용 하 여 ODBC 경고를 발생할 수 있습니다.

#### <a name="getting-the-list-of-loaded-providers"></a>로드 된 공급자 목록 가져오기

이 연결 특성을 가져오는 등 빌드된. 드라이버에 현재 로드 된 키 저장소 공급자를 확인 하려면 클라이언트 응용 프로그램을 수 있습니다. 이 연결 되 면만 수행할 수 있습니다.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`|[입력] 연결 핸들입니다. 올바른 연결 핸들을 해야 되지만 하나의 연결 핸들을 통해 로드할 공급자 동일한 프로세스에서 다른 액세스할 수 있습니다.|
|`Attribute`|[입력] 검색할 특성:는 `SQL_COPT_SS_CEKEYSTOREPROVIDER` 상수입니다.|
|`ValuePtr`|[출력] 다음 로드 공급자 이름을 반환 하는 메모리에 대 한 포인터입니다.|
|`BufferLength`|[입력] ValuePtr 버퍼의 길이입니다.|
|`StringLengthPtr`|[출력] (Null 종료 문자를 제외한) 바이트의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \*ValuePtr 합니다. ValuePtr null 포인터 이면 길이가 반환 됩니다. 특성 값은 문자열 및 반환에 사용할 수 있는 바이트 수가 BufferLength null 종료의 길이 뺀 값 보다 크면 경우 문자 데이터를 \*ValuePtr 잘립니다 BufferLength의 길이 뺀 값을 null 종결 문자 및 드라이버에 의해 null로 종결 됩니다.|

전체 목록을 검색을 허용 하려면 모든 가져오기 작업 현재 공급자의 이름을 반환 하 고는 내부 카운터를 증가 시킵니다. 이 카운터의 목록에서 빈 문자열의 끝에 도달 하면 ("")가 반환 되 고 카운터 다시 설정 됩니다. 연속 된 Get 작업 한 다음 목록의 처음부터 다시 진행합니다.

### <a name="communicating-with-keystore-providers"></a>키 저장소 공급자와의 통신

`SQL_COPT_SS_CEKEYSTOREDATA` 연결 특성을 사용 하면 클라이언트 응용 프로그램 키 자료 등의 추가 매개 변수를 구성 하는 데 로드 키 저장소 공급자와 통신 합니다. 클라이언트 응용 프로그램 및 공급자 간 통신에서 Get에 따라 간단한 요청-응답 프로토콜을 따르며 집합이 연결 특성을 사용 하 여 요청 합니다. 통신은 클라이언트 응용 프로그램에 의해서만 시작 됩니다.

> [!NOTE]
> ODBC의 특성상 (SQLGet/SetConnectAttr) CEKeyStoreProvider의 대응 되는 연결 컨텍스트의 해상도로 데이터를 설정 하 여 ODBC 인터페이스만 지원 호출 합니다.

응용 프로그램 CEKeystoreData 구조를 통해 드라이버를 통해 키 저장소 공급자와 통신합니다.

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```

| 인수 | 설명 |
|:---|:---|
|`name`|[입력] 공급자의 이름 집합으로 데이터 전송 됩니다. 가져오기 시 무시 됩니다. Null로 종료 되는 와이드 문자 문자열입니다.|
|`dataSize`|[입력] 구조를 다음 데이터 배열 크기입니다.|
|`data`|[InOut] 시 집합, 데이터를 공급자에 게 보낼 수 있습니다. 임의의 데이터를 수 있습니다. 드라이버를 해석 하지를 수 있습니다. Get으로 공급자에서 데이터를 받을 버퍼를 읽습니다.|

#### <a name="writing-data-to-a-provider"></a>공급자에 데이터 쓰기

A `SQLSetConnectAttr` 를 사용 하 여 호출 된 `SQL_COPT_SS_CEKEYSTOREDATA` 특성 지정된 키 저장소 공급자에 게 데이터 "패킷을"를 씁니다.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`| [입력] 연결 핸들입니다. 올바른 연결 핸들을 해야 되지만 하나의 연결 핸들을 통해 로드할 공급자 동일한 프로세스에서 다른 액세스할 수 있습니다.|
|`Attribute`|[입력] 설정할 특성입니다:는 `SQL_COPT_SS_CEKEYSTOREDATA` 상수입니다.|
|`ValuePtr`|[입력] CEKeystoreData 구조에 대 한 포인터입니다. 구조체의 이름 필드는 데이터를 위한 공급자를 식별 합니다.|
|`StringLength`|[입력] SQL_IS_POINTER 상수|

통해 자세한 추가 오류 정보를 얻을 수 있습니다 [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)합니다.

> [!NOTE]
> 하면 필요한 경우 공급자 특정 연결에 기록된 된 데이터에 연결할 연결 핸들을 사용할 수입니다. 연결당 구성을 구현 하는 것에 대 한 유용 합니다. 또한 연결 컨텍스트를 무시 하 고 데이터를 보내는 데 연결에 관계 없이 동일 하 게 데이터 처리 될 수 있습니다. 참조 [컨텍스트 연결](../../connect/odbc/custom-keystore-providers.md#context-association) 자세한 내용은 합니다.

#### <a name="reading-data-from-a-provider"></a>공급자에서 데이터 읽기

에 대 한 호출 `SQLGetConnectAttr` 를 사용 하는 `SQL_COPT_SS_CEKEYSTOREDATA` 특성 "패킷을"에서 데이터를 읽고 *는 마지막 기록-간* 공급자. 발생 한 경우 none, 함수 시퀀스 오류를 발생 합니다. 키 저장소 공급자 구현자는 "더미 쓰기" 작업을 수행 하는 것이 경우 다른 부작용 없이 읽기 작업에 대 한 공급자를 선택 하는 방법으로 0 바이트의 수입니다.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`|[입력] 연결 핸들입니다. 올바른 연결 핸들을 해야 되지만 하나의 연결 핸들을 통해 로드할 공급자 동일한 프로세스에서 다른 액세스할 수 있습니다.|
|`Attribute`|[입력] 검색할 특성:는 `SQL_COPT_SS_CEKEYSTOREDATA` 상수입니다.|
|`ValuePtr`|[출력] 공급자에서 읽는 데이터가 위치한 CEKeystoreData 구조에 대 한 포인터입니다.|
|`BufferLength`|[입력] SQL_IS_POINTER 상수|
|`StringLengthPtr`|[출력] BufferLength 반환할 버퍼에 대 한 포인터입니다. 경우 * ValuePtr null 포인터 이면 길이가 반환 됩니다.|

호출자에 게 CEKEYSTOREDATA 구조를 다음 충분 한 길이의 버퍼에 쓸 공급자에 대 한 할당 되는 확인 해야 합니다. 반환 될 때 해당 dataSize 필드는 공급자에서 읽은 데이터의 실제 길이 사용 하 여 업데이트 됩니다. 통해 자세한 추가 오류 정보를 얻을 수 있습니다 [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)합니다.

이 인터페이스는 응용 프로그램 및 키 저장소 공급자 간에 전송 되는 데이터의 형식에 추가 요구 사항이 없습니다를 배치 합니다. 각 공급자에는 해당 요구 사항에 따라 자체 프로토콜/데이터 형식을 정의할 수 있습니다.

사용자 고유의 키 저장소 공급자를 구현 하는 예제를 참조 하세요. [사용자 지정 키 저장소 공급자](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>상시 암호화를 사용 하는 경우 ODBC 드라이버의 제한 사항

### <a name="asynchronous-operations"></a>비동기 작업
ODBC 드라이버를 사용할 수는 있지만 [비동기 작업](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md) Always Encrypted 기능으로 성능에 미치는 영향에 있는지 작업 Always Encrypted가 설정 된 경우. 에 대 한 호출 `sys.sp_describe_parameter_encryption` 명령문을 차단 하 고 서버에서 반환 하기 전에 메타 데이터 반환을 기다려야 하면 드라이버에 대 한 암호화 메타 데이터를 확인 하려면 `SQL_STILL_EXECUTING`합니다.

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>SQLGetData 사용 하 여 파트의 데이터를 검색 합니다.
SQL Server 용 ODBC 드라이버 17 암호화 전에 SQLGetData 사용 하 여 파트의 문자 및 이진 열을 검색할 수 없습니다. SQLGetData 한 번만 호출 전체 열의 데이터를 포함 하도록 충분 한 길이의 버퍼를 사용 하 여 만들 수 있습니다.

### <a name="send-data-in-parts-with-sqlputdata"></a>SQLPutData 사용 하 여 파트의 데이터 전송
SQL Server 용 ODBC 드라이버 17.3, 전에 SQLPutData 사용 하 여 파트의 삽입 또는 비교에 대 한 데이터를 보낼 수 없습니다. 전체 데이터를 포함 하는 버퍼를 사용 하 여 SQLPutData 한 번만 호출을 만들 수 있습니다. 암호화 된 열에 long 데이터를 삽입, 입력된 데이터 파일을 사용 하 여 다음 섹션에 설명 된 대량 복사 API를 사용 합니다.

### <a name="encrypted-money-and-smallmoney"></a>암호화 된 money 및 smallmoney
암호화 **money** 하거나 **smallmoney** 매개 변수에서 열을 대상으로 지정할 수 없습니다, ODBC 데이터 형식 피연산자 유형 충돌 오류가 발생 하는 해당 형식에 매핑되는 특정 이상 있기 때문입니다.

## <a name="bulk-copy-of-encrypted-columns"></a>암호화 된 열에 대량 복사

사용 합니다 [SQL 대량 복사 함수](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) 하며 **bcp** 유틸리티는 ODBC 드라이버 17 이후 상시 암호화로 SQL Server에 대 한 지원 됩니다. 일반 텍스트 (에서 암호화 된 삽입 및에서 해독 된 검색) 및 암호 텍스트 (정확 하 게 전송) 삽입할 수 및 대량 복사를 사용 하 여 검색 (bcp_&#42;) Api와 **bcp** 유틸리티입니다.

- Varbinary (max) 형식 (예: 대량 로드를 위한 다른 데이터베이스로) 암호 텍스트를 검색 하지 않고 연결을 합니다 `ColumnEncryption` 옵션 (설정 또는 `Disabled`) BCP OUT 작업을 수행 하 고 합니다.

- 삽입 및 일반 텍스트를 가져오고, 드라이버 암호화 및 암호 해독에 필요한 설정으로 투명 하 게 수행할 수 있도록 `ColumnEncryption` 에 `Enabled` 부족 합니다. 그렇지 않으면 BCP API의 기능 변경 되지 않습니다.

- Varbinary (max) 형식 (예: 위의 검색) 암호 텍스트를 삽입, 설정 하는 `BCPMODIFYENCRYPTED` true 옵션 및 BCP IN 작업을 수행 합니다. 결과 데이터를 해독할 수에 대 한 순서 대로 있는지 확인 대상 열의 CEK 암호화 텍스트를 원래 가져온 것과 동일 합니다.

사용 하는 경우는 **bcp** 유틸리티: 컨트롤에는 `ColumnEncryption` 설정,-D 옵션을 사용 하 고 원하는 값이 포함 된 DSN을 지정 합니다. 암호 텍스트를 삽입 하려면 다음을 확인 합니다 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 사용자의 설정이 사용 됩니다.

다음 표에서 요약이 작업 중 암호화 된 열에서 작동 하는 경우:

|`ColumnEncryption`|BCP 방향입니다.|설명|
|----------------|-------------|-----------|
|`Disabled`|(클라이언트)로 나가기|암호 텍스트를 검색합니다. 관찰 된 데이터 형식이 **varbinary (max)** 합니다.|
|`Enabled`|(클라이언트)로 나가기|일반 텍스트를 검색합니다. 드라이버는 열 데이터를 해독 됩니다.|
|`Disabled`|IN (서버로)|암호 텍스트를 삽입합니다. 이 것 불투명 하 게 요구 하지 않고 암호화 된 데이터를 이동 하는 것에 대 한 암호를 해독할 수입니다. 작업이 실패 하는 경우는 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 옵션이 사용자에 대해 설정 되어 있지 않거나 BCPMODIFYENCRYPTED 연결 핸들에 대해 설정 되지 않았습니다. 자세한 내용은 아래를 참조하세요.|
|`Enabled`|IN (서버로)|일반 텍스트를 삽입합니다. 드라이버는 열 데이터를 암호화 합니다.|

### <a name="the-bcpmodifyencrypted-option"></a>BCPMODIFYENCRYPTED 옵션

데이터 손상을 방지 하기 위해 서버 일반적으로 않습니다을 허용 하지 않고 암호 텍스트를 암호화 된 열을 직접 삽입 따라서 하려고 시도 하면 실패 합니다. 그러나 설정, BCP API를 사용 하 여 암호화 된 데이터의 대량 로드에 대 한 합니다 `BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 옵션을 true로 ciphertext를 직접 삽입에 사용 하면 설정을 통해 암호화 된 데이터 손상의 위험을 줄이고는 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 사용자 계정에 대 한 옵션입니다. 그럼에도 불구 하 고 키에는 데이터와 일치 해야 합니다 및 대량 삽입 후 더 이상 사용 하기 전에 삽입된 된 데이터의 몇 가지 읽기 전용 검사를 수행 하는 것이 좋습니다.

자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.

## <a name="always-encrypted-api-summary"></a>Always Encrypted API 요약

### <a name="connection-string-keywords"></a>연결 문자열 키워드

|속성|설명|  
|----------|-----------------|  
|`ColumnEncryption`|허용 되는 값은 `Enabled` / `Disabled`합니다.<br>`Enabled` - 연결에 상시 암호화 기능을 사용하도록 설정합니다.<br>`Disabled` - 연결에 Always Encrypted 기능을 사용하지 않도록 설정합니다. <br><br>기본값은 `Disabled`입니다.|  
|`KeyStoreAuthentication` | 유효한 값: `KeyVaultPassword`,`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | 때 `KeyStoreAuthentication`  =  `KeyVaultPassword`, 유효한 Azure Active Directory 사용자 계정 이름으로이 값을 설정 합니다. <br>때 `KeyStoreAuthetication`  =  `KeyVaultClientSecret` 이 값을 유효한 Azure Active Directory 응용 프로그램 클라이언트 ID 설정 |
|`KeyStoreSecret` | 때 `KeyStoreAuthentication`  =  `KeyVaultPassword` 이 값을 해당 사용자 이름의 암호를 설정 합니다. <br>때 `KeyStoreAuthentication`  =  `KeyVaultClientSecret` 이 값을 유효한 Azure Active Directory 응용 프로그램 클라이언트 ID와 연결 된 응용 프로그램 암호 설정 |


### <a name="connection-attributes"></a>연결 특성

|속성|형식|설명|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|사전에 연결|`SQL_COLUMN_ENCRYPTION_DISABLE` (0)-상시 암호화 사용 안 함 <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1)--상시 암호화 사용|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|연결 후|[설정] CEKeystoreProvider 로드 하려고 합니다.<br>[가져오기] CEKeystoreProvider 이름을 반환 합니다.|
|`SQL_COPT_SS_CEKEYSTOREDATA`|연결 후|[설정] CEKeystoreProvider에 데이터 쓰기<br>[가져오기] CEKeystoreProvider에서 데이터 읽기|
|`SQL_COPT_SS_CEKCACHETTL`|연결 후|[설정] CEK 캐시 TTL 설정<br>[가져오기] 현재 CEK 캐시 TTL 가져오기|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|연결 후|[설정] 신뢰할 수 있는 CMK 경로 포인터를 설정 합니다.<br>[가져오기] 현재 신뢰할 수 있는 CMK 경로 포인터를 가져옵니다.|

### <a name="statement-attributes"></a>문 특성

|속성|설명|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0)-문에 대 한 always Encrypted 사용 하지 않도록 설정 <br>`SQL_CE_RESULTSETONLY` (1)--암호 해독에만 합니다. 결과 집합 및 반환 값은 암호를 해독 하 고 매개 변수는 암호화 되지 않습니다. <br>`SQL_CE_ENABLED` (3)-always Encrypted가 사용 되 고 매개 변수 및 결과 대 한 사용|

### <a name="descriptor-fields"></a>설명자 필드

|IPD 필드|크기/유형|기본값|설명|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 바이트)|0|때 0 (기본값):이 매개 변수를 암호화 하는 결정 암호화 메타 데이터의 가용성에 따라 결정 됩니다.<br><br>0이 아닌 경우: 암호화 된 암호화 메타 데이터를이 매개 변수에 대해 사용할 수 있는 경우. 오류 [CE300]와 함께 요청이 실패 하는 고, 그렇지 [Microsoft] [ODBC Driver 13 for SQL Server] 필수 암호화 매개 변수에 대해 지정 되었지만 서버에서 제공 된 암호화 메타 데이터가 없습니다.|

### <a name="bcpcontrol-options"></a>bcp_control 옵션

|옵션 이름|기본값|설명|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|TRUE 인 경우에 varbinary (max) 값을을 암호화 된 열에 삽입할 수 있습니다. FALSE 인 경우 올바른 형식 및 암호화 메타 데이터를 제공 하지 않으면 삽입을 방지 합니다.|

## <a name="see-also"></a>참고 항목

- [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [상시 암호화 블로그](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

