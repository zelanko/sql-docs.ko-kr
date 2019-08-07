---
title: SQL Server용 ODBC 드라이버와 함께 상시 암호화 사용 | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: cc6deae9a2ddcb11675586ffd8777644aff00672
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702701"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>SQL Server용 ODBC 드라이버와 함께 상시 암호화 사용
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>적용 가능 대상

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>소개

이 문서에서는 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 또는 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) 및 [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)를 사용하여 ODBC 애플리케이션을 개발하는 방법을 설명합니다.

Always Encrypted를 사용하면 클라이언트 애플리케이션이 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. SQL Server용 ODBC 드라이버와 같은 상시 암호화 지원 드라이버는 클라이언트 애플리케이션의 중요한 데이터를 투명하게 암호화하고 암호 해독합니다. 이 드라이버는 중요 데이터베이스 열에 해당하는 쿼리 매개 변수를 자동으로 확인하고(Always Encrypted를 사용하여 보호) 데이터를 SQL Server 또는 Azure SQL Database로 전달하기 전에 이러한 매개 변수의 값을 암호화합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. *보안 Enclave를 사용한* Always Encrypted는 이 기능을 확장하여 데이터 기밀성을 유지하면서 중요한 데이터에 대해 보다 풍부한 기능을 사용하도록 설정합니다.

자세한 내용은 [Always Encrypted (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 [Always Encrypted with Secure Enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조 하세요.

### <a name="prerequisites"></a>사전 요구 사항

데이터베이스에서 상시 암호화를 구성합니다. 상시 암호화를 구성하려면 상시 암호화 키를 프로비전하고 선택한 데이터베이스 열에 대한 암호화를 설정해야 합니다. 데이터베이스에 상시 암호화가 구성되지 않은 경우 [상시 암호화 시작](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)의 지침을 따르세요. 특히, 데이터베이스에 CMK(열 마스터 키), CEK(열 암호화 키) 및 해당 CEK를 사용하여 암호화된 열을 하나 이상 포함하는 테이블에 대한 메타데이터 정의가 포함되어 있어야 합니다.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>ODBC 애플리케이션에서 Always Encrypted 사용

매개 변수 암호화와 결과 집합의 암호화된 열 암호 해독을 둘 다 사용하는 가장 쉬운 방법은 `ColumnEncryption` 연결 문자열 키워드 값을 **Enabled**로 설정하는 것입니다. 다음은 상시 암호화를 사용하는 연결 문자열의 예제입니다.

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

DSN 구성에서 동일한 키와 값(연결 문자열 설정이 있으면 해당 설정으로 재정의됨)을 사용하거나, `SQL_COPT_SS_COLUMN_ENCRYPTION` 연결 전 특성을 통해 프로그래밍 방식으로 Always Encrypted를 사용하도록 설정할 수도 있습니다. 이런 방식으로 설정하면 연결 문자열 또는 DSN에서 설정된 값이 재정의됩니다.

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

연결에 사용하도록 설정한 후 개별 쿼리에 맞게 Always Encrypted의 동작을 조정할 수 있습니다. 자세한 내용은 아래 [Always Encrypted가 성능에 미치는 영향 제어](#controlling-the-performance-impact-of-always-encrypted)를 참조하세요.

Always Encrypted를 사용하도록 설정해도 암호화 또는 암호 해독에 실패할 수 있습니다. 다음 사항도 확인해야 합니다.

- 애플리케이션에는 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 데이터베이스 권한이 있으며 데이터베이스에서 상시 암호화 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 [데이터베이스 사용 권한](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)을 참조하세요.

- 애플리케이션은 쿼리된 암호화된 열의 CEK를 보호하는 CMK에 액세스할 수 있습니다. 이 기능은 CMK를 저장하는 키 저장소 공급자에 따라 달라집니다. 자세한 내용은 [열 마스터 키 저장소 작업](#working-with-column-master-key-stores)을 참조하세요.

### <a name="enabling-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted를 사용하도록 설정

17.4 버전부터 드라이버는 Secure Enclaves를 사용 하 여 Always Encrypted을 지원 합니다. SQL Server 2019 이상에 연결할 때 enclave를 사용 하도록 설정 하려면 `ColumnEncryption` DSN, 연결 문자열 또는 연결 특성을 enclave 유형 및 증명 프로토콜의 이름과 연결 된 증명 데이터를 쉼표로 구분 하 여 설정 합니다. 버전 17.4에서는로 `VBS-HGS`표시 되는 [가상화 기반 Security](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) enclave type 및 [Host 보호자 서비스](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server) 증명 프로토콜만 지원 됩니다 .이를 사용 하려면 증명 서버의 URL을 지정 합니다. 예를 들면 다음과 같습니다.

```
Driver=ODBC Driver 17 for SQL Server;Server=yourserver.yourdomain;Trusted_Connection=Yes;ColumnEncryption=VBS-HGS,http://attestationserver.yourdomain/Attestation
```

서버 및 증명 서비스가 올바르게 구성 되어 있고 원하는 열에 대해 enclave 사용 CMKs 및 CEKs를 사용 하는 경우에는 현재 내부 암호화와 같은 enclave을 사용 하는 쿼리를 실행할 수 있어야 합니다. Always Encrypted에서 제공 하는 기존 기능 자세한 내용은 [Configure Always Encrypted with secure enclaves](../../relational-databases/security/encryption/configure-always-encrypted-enclaves.md) 를 참조 하세요.


### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정

연결에 Always Encrypted을 사용 하도록 설정 하면 표준 ODBC Api를 사용할 수 있습니다. ODBC Api는 암호화 된 데이터베이스 열의 데이터를 검색 하거나 수정할 수 있습니다. 다음 설명서 항목은이 작업에 도움이 될 수 있습니다.

- [ODBC 샘플 코드](cpp-code-example-app-connect-access-sql-db.md)
- [ODBC 프로그래머 참조](../../odbc/reference/odbc-programmer-s-reference.md)

응용 프로그램에 필요한 데이터베이스 권한이 있어야 하 고 열 마스터 키에 액세스할 수 있어야 합니다. 그런 다음, 드라이버는 암호화 된 열을 대상으로 하는 모든 쿼리 매개 변수를 암호화 합니다. 또한이 드라이버는 암호화 된 열에서 검색 된 데이터의 암호를 해독 합니다. 드라이버는 소스 코드의 도움 없이 모든 암호화 및 암호 해독을 수행 합니다. 프로그램에는 열이 암호화 되지 않은 것 처럼 됩니다.

상시 암호화를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없는 경우 암호화된 열에서 데이터를 검색할 수 있습니다. 그러나 드라이버에서 암호 해독을 시도하지 않고, 애플리케이션이 암호화된 이진 데이터를 바이트 배열로 수신합니다.

아래 표에서는 상시 암호화 사용 여부에 따른 쿼리 동작을 요약합니다.

|쿼리 특성 | 상시 암호화가 설정되고 애플리케이션에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 애플리케이션에서 키 또는 키 메타데이터에 액세스할 수 없는 경우 | 상시 암호화를 사용하지 않는 경우|
|:---|:---|:---|:---|
| 암호화된 열을 대상으로 하는 매개 변수입니다. | 매개 변수 값이 투명하게 암호화됩니다. | Error | Error|
| 암호화된 열을 대상으로 하는 매개 변수 없이 암호화된 열에서 데이터를 검색합니다.| 암호화된 열의 결과가 투명하게 암호 해독됩니다. 애플리케이션이 일반 텍스트 열 값을 받습니다. | Error | 암호화된 열의 결과가 암호 해독되지 않습니다. 애플리케이션에서 암호화된 값을 바이트 배열로 수신합니다.

다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 예제에서는 다음 스키마가 있는 테이블을 가정합니다. SSN 및 BirthDate 열은 암호화되어 있습니다.

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

- 샘플 코드에는 암호화에 대한 내용이 없습니다. 드라이버에서 암호화된 열을 대상으로 하는 SSN 및 날짜 매개 변수의 값을 자동으로 검색하고 암호화합니다. 이렇게 하면 애플리케이션에 투명하게 암호화할 수 있습니다.

- 암호화된 열을 포함하여 데이터베이스 열에 삽입된 값은 바인딩된 매개 변수로 전달됩니다([SQLBindParameter Function](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx) 참조). 매개 변수를 사용하여 암호화되지 않은 열에 값을 전달하는 것은 선택 사항이지만(그러나 SQL 삽입을 방지할 수 있으므로 매우 권장됨) 암호화된 열을 대상으로 하는 값에 필요합니다. SSN 또는 BirthDate 열에 삽입된 값을 쿼리 문에 포함된 리터럴로 전달하면, 드라이버에서 쿼리의 리터럴을 암호화하거나 다른 방식으로 처리하지 않기 때문에 쿼리가 실패합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.

- SSN 열에 삽입된 매개 변수의 SQL 형식은 **char** SQL Server 데이터 형식(`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`)에 매핑되는 SQL_CHAR로 설정됩니다. 매개 변수 형식을 **nchar**에 매핑되는 SQL_WCHAR로 설정하면 Always Encrypted에서 암호화된 nchar 값을 암호화된 char 값으로 변환하는 서버 쪽 작업을 지원하지 않으므로 쿼리가 실패합니다. 데이터 형식 매핑에 대한 자세한 내용은 [ODBC 프로그래머 참조 - 부록 D: 데이터 형식](https://msdn.microsoft.com/library/ms713607.aspx)을 참조하세요.

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
> 암호화가 결정적 이거나 secure enclave가 사용 하도록 설정 된 경우에만 쿼리에서 암호화 된 열에 대 한 같음 비교를 수행할 수 있습니다. 자세한 내용은 [결정적 또는 임의 암호화 선택](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)을 참조하세요.

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

상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 지원되는 형식 변환의 자세한 목록은 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. 데이터 형식 변환 오류를 방지하려면 암호화된 열을 대상으로 하는 매개 변수와 함께 SQLBindParameter를 사용할 때 다음 사항에 유의해야 합니다.

- 매개 변수의 SQL 형식이 대상 열의 형식과 정확히 같거나, SQL 형식에 열 형식으로의 변환이 지원되어야 합니다.

- SQL Server 데이터 형식이 `decimal` 및 `numeric`인 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다.

- 대상 열을 수정하는 쿼리에서 SQL Server 데이터 형식이 `datetime2`, `datetimeoffset` 또는 `time`인 열을 대상으로 하는 매개 변수의 정밀도가 대상 열의 정밀도보다 크지 않아야 합니다.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류

암호화된 열을 대상으로 하는 값은 서버로 전송하기 전에 암호화해야 합니다. 암호화된 열의 일반 텍스트 값으로 삽입, 수정 또는 필터링하면 오류가 발생합니다. 이러한 오류를 방지하려면 다음을 확인합니다.

- Always Encrypted가 사용됩니다(DSN에서는 특정 연결의 `SQL_COPT_SS_COLUMN_ENCRYPTION` 연결 특성이나 특정 문의 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 문 특성을 설정하여 연결하기 전의 연결 문자열).

- SQLBindParameter를 사용하여 암호화된 열을 대상으로 하는 데이터를 전송합니다. 아래 예제에서는 리터럴을 SQLBindParameter에 인수로 전달하는 대신암호화된 열(SSN)에서 리터럴/상수로 잘못 필터링하는 쿼리를 보여 줍니다.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>SQLSetPos 및 SQLMoreResults를 사용하는 경우의 예방 조치

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API를 사용하면 애플리케이션이 SQLBindCol로 바인딩되고 이전에 행 데이터를 가져온 버퍼를 통해 결과 집합의 행을 업데이트할 수 있습니다. 암호화된 고정 길이 형식의 비대칭 패딩 동작으로 인해 행의 다른 열을 업데이트하는 동안 이러한 열의 데이터가 예기치 않게 변경될 수 있습니다. AE에서는 값이 버퍼 크기보다 작을 경우 고정 길이 문자 값이 패딩됩니다.

이 동작을 완화하려면 커서 기반 업데이트에 `SQLSetPos`를 사용하는 경우 `SQL_COLUMN_IGNORE` 플래그를 사용하여 `SQLBulkOperations`의 일부로 업데이트되지 않는 열을 무시합니다.  실제 (DB) 크기보다 ‘작은’ 버퍼에 바인딩된 열의 잘림을 방지하고 성능을 최적화하려면 애플리케이션에서 직접 수정되지 않는 열을 모두 무시해야 합니다.  자세한 내용은 [SQLSetPos 함수 참조](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx)를 참조하세요.

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults 및 SQLDescribeCol

애플리케이션 프로그램에서 [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx)을 호출하여 준비된 문의 열에 대한 메타데이터를 반환할 수 있습니다.  Always Encrypted를 사용하는 경우, `SQLMoreResults`를 호출한 *후에* `SQLDescribeCol`을 호출하면 [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)가 호출되어 암호화된 열에 대한 일반 텍스트 메타데이터가 올바르게 반환되지 않습니다. 이 문제를 방지하려면 준비된 문에서 `SQLDescribeCol`을 호출한 *후에* `SQLMoreResults`를 호출합니다.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

상시 암호화는 클라이언트 쪽 암호화 기술이므로 데이터베이스가 아닌 클라이언트 쪽에서 대부분의 성능 오버헤드가 발생합니다. 암호화 및 암호 해독 작업의 비용 외에 클라이언트 쪽 성능 오버헤드의 원인은 다음과 같습니다.

- 쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복

- 열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출

이 섹션에서는 SQL Server용 ODBC Driver의 기본 제공 성능 최적화와 위의 두 성능 요소의 영향을 제어할 수 있는 방법에 대해 설명합니다.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복 제어

연결에 대한 상시 암호화가 설정된 경우 기본적으로 드라이버는 각 매개 변수화된 쿼리에 대해 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)을 호출하고 매개 변수 값 없이 쿼리 문을 SQL Server에 전달합니다. 이 저장 프로시저는 쿼리 문을 분석하여 암호화해야 하는 매개 변수가 있는지 확인하고, 있을 경우 드라이버에서 매개 변수를 암호화할 수 있도록 각 매개 변수에 대한 암호화 관련 정보를 반환합니다. 위의 동작은 클라이언트 애플리케이션에 대한 높은 수준의 투명성을 보장합니다. 암호화된 열을 대상으로 하는 값이 매개 변수로 드라이버에 전달되는 한, 애플리케이션(및 애플리케이션 개발자)에서는 어떤 쿼리가 암호화된 열에 액세스하는지 유의하지 않아도 됩니다.

### <a name="per-statement-always-encrypted-behavior"></a>문 단위의 Always Encrypted 동작

매개 변수가 있는 쿼리에 대한 암호화 메타데이터를 검색할 때 성능에 미치는 영향을 제어하기 위해, 연결에서 Always Encrypted가 사용되는 경우 개별 쿼리에 대해 Always Encrypted 동작을 변경할 수 있습니다. 이렇게 하면 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리에 대해서만 `sys.sp_describe_parameter_encryption`가 호출되도록 할 수 있습니다. 단, 이 경우 암호화의 투명성이 저하될 수 있습니다. 데이터베이스에서 추가 열을 암호화하는 경우 스키마 변경에 맞게 애플리케이션 코드를 변경해야 할 수 있습니다.

Always Encrypted의 문 동작을 제어하려면 SQLSetStmtAttr을 호출하여 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 문 특성을 다음 값 중 하나로 설정합니다.

|값|설명|
|-|-|
|`SQL_CE_DISABLED` (0)|문에 대해 Always Encrypted를 사용할 수 없습니다.|
|`SQL_CE_RESULTSETONLY` (1)|암호 해독만 수행합니다. 결과 집합과 반환 값의 암호가 해독되고, 매개 변수는 암호화되지 않습니다.|
|`SQL_CE_ENABLED` (3) | Always Encrypted를 사용할 수 있고, 매개 변수와 결과에 모두 사용됩니다.|

Always Encrypted가 사용되는 연결에서 새로 만든 문 핸들은 기본적으로 SQL_CE_ENABLED로 설정됩니다. Always Encrypted가 사용되지 않는 연결에서 만든 문 핸들은 기본적으로 SQL_CE_DISABLED로 설정되며, 해당 핸들에서 Always Encrypted를 사용하도록 설정할 수 없습니다.

클라이언트 애플리케이션의 쿼리가 대부분 암호화된 열에 액세스하는 경우 다음 작업을 수행하는 것이 좋습니다.

- `ColumnEncryption` 연결 문자열 키워드를 `Enabled`로 설정합니다.

- 암호화된 열에 액세스하지 않는 문에서는 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특성을 `SQL_CE_DISABLED`로 설정합니다. 이렇게 하면 `sys.sp_describe_parameter_encryption`이 호출되지 않고, 결과 집합의 값 암호도 해독되지 않습니다.
    
- 암호화를 요구하는 매개 변수는 없지만 암호화된 열에서 데이터를 검색하는 문에서는 `SQL_SOPT_SS_COLUMN_ENCRYPTION` 특성을 `SQL_CE_RESULTSETONLY`로 설정합니다. 이렇게 하면 `sys.sp_describe_parameter_encryption` 및 매개 변수 암호화가 호출되지 않습니다. 암호화된 열을 포함하는 결과의 암호 해독은 계속됩니다.

## <a name="always-encrypted-security-settings"></a>Always Encrypted 보안 설정

### <a name="force-column-encryption"></a>열 암호화 강제 적용

매개 변수의 암호화를 적용하려면 SQLSetDescField 함수 호출을 통해 `SQL_CA_SS_FORCE_ENCRYPT` IPD(구현 매개 변수 설명자) 필드를 설정합니다. 값이 0이 아니면, 관련 매개 변수에 대해 반환된 암호화 메타데이터가 없을 경우 드라이버에서 오류가 반환됩니다.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

SQL Server가 매개 변수를 암호화하지 않아도 되는 것을 드라이버에 알리는 경우 매개 변수를 사용하는 쿼리는 실패합니다. 이렇게 하면 데이터 노출을 야기할 수 있는 잘못된 암호화 메타데이터를 클라이언트에게 제공하는 손상된 SQL Server를 포함하는 보안 공격에 대한 보호 기능이 강화됩니다.

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

열 암호화 키의 암호 해독을 위한 열 마스터 키 저장소 호출 수를 줄이기 위해 드라이버는 일반 텍스트 CEK를 메모리에 캐시합니다. CEK 캐시는 드라이버 전체에서 사용되며, 특정 연결과 관련이 없습니다. 데이터베이스 메타데이터에서 ECEK를 받은 후 드라이버는 먼저 캐시에 있는 암호화된 키 값에 해당하는 일반 텍스트 CEK를 찾으려고 합니다. 캐시에서 해당하는 일반 텍스트 CEK를 찾을 수 없는 경우에만 드라이버에서 CMK가 포함된 키 저장소를 호출합니다.

> [!NOTE]
> SQL Server용 ODBC 드라이버에서는 2시간 제한이 경과하면 캐시의 항목이 제거됩니다. 즉, 드라이버는 지정된 ECEK에 대해 애플리케이션 수명이나 2시간마다 중 더 짧은 시간에 한 번만 키 저장소에 연결합니다.

ODBC Driver 17.1 for SQL Server부터 CEK가 캐시에 유지되는 시간(초)을 지정하는 `SQL_COPT_SS_CEKCACHETTL` 연결 특성을 사용하여 CEK 캐시 시간 제한을 조정할 수 있습니다. 캐시의 전역 특성 때문에, 드라이버에 유효한 모든 연결 핸들에서 이 특성을 조정할 수 있습니다. 캐시 TTL을 줄이면 새 TTL을 초과하는 기존 CEK도 제거됩니다. 캐시 TTL이 0이면 CEK가 캐시되지 않습니다.

### <a name="trusted-key-paths"></a>신뢰할 수 있는 키 경로

ODBC Driver 17.1 for SQL Server부터 `SQL_COPT_SS_TRUSTEDCMKPATHS` 연결 특성을 사용하면 애플리케이션이 Always Encrypted 작업에서 키 경로로 식별된 지정한 CMK 목록만 사용하도록 요구할 수 있습니다. 기본적으로 이 특성은 NULL이므로, 드라이버가 모든 키 경로를 허용합니다. 이 기능을 사용하려면 허용된 키 경로를 나열하는, null로 구분되고 null로 종료된 와이드 문자열을 가리키도록 `SQL_COPT_SS_TRUSTEDCMKPATHS`를 설정합니다. 이 특성이 가리키는 메모리는 특성이 설정된 연결 핸들을 사용한 암호화 또는 암호 해독 작업 중에 유효한 상태로 유지되어야 합니다. 여기서 드라이버는 서버 메타데이터에 지정된 CMK 경로가 대/소문자를 구분하지 않고 이 목록에 있는지 확인합니다. CMK 경로가 목록에 없으면 작업이 실패합니다. 애플리케이션은 특성을 다시 설정하지 않고 이 특성이 가리키는 메모리의 내용을 변경하여 신뢰할 수 있는 CMK 목록을 변경할 수 있습니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업

데이터를 암호화하거나 암호를 해독하려면 드라이버가 대상 열에 대해 구성된 CEK를 가져와야 합니다. CEK는 데이터베이스 메타데이터에 암호화된 형태(ECEK)로 저장됩니다. 각 CEK를 암호화하는 데 사용된 해당 CMK가 있습니다. [데이터베이스 메타데이터](../../t-sql/statements/create-column-master-key-transact-sql.md)는 CMK 자체를 저장하는 것이 아니라 키 저장소의 이름 및 키 저장소에서 CMK를 찾는 데 사용할 수 있는 정보만 포함합니다.

ECEK의 일반 텍스트 값을 가져오기 위해 드라이버는 먼저 CEK와 해당 CMK에 대한 메타데이터를 가져온 다음, 이 정보를 사용하여 CMK가 포함된 키 저장소에 연결하고 ECEK의 암호를 해독하도록 요청합니다. 드라이버는 키 저장소 공급자를 사용하여 키 저장소와 통신합니다.

### <a name="built-in-keystore-providers"></a>기본 제공 키 저장소 공급자

ODBC Driver for SQL Server에는 다음과 같은 기본 제공 키 저장소 공급자가 포함되어 있습니다.

| 속성 | 설명 | 공급자 (메타데이터) 이름 |가용성|
|:---|:---|:---|:---|
|Azure Key Vault |Azure Key Vault에 CMK를 저장합니다. | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Windows 인증서 저장소|Windows 키 저장소에 CMK를 로컬로 저장합니다.| `MSSQL_CERTIFICATE_STORE`|Windows|

- 사용자 또는 DBA는 열 마스터 키 메타데이터에 구성된 공급자 이름이 정확하고 열 마스터 키 경로가 특정 공급자에 적합한 키 경로 형식을 준수해야 합니다. [CREATE COLUMN MASTER KEY(Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 실행할 때 적합한 공급자 이름 및 키 경로를 자동으로 생성하는 SQL Server Management Studio 등의 도구를 사용하여 키를 구성하는 것이 좋습니다.

- 애플리케이션에서 키 저장소의 키에 액세스할 수 있어야 합니다. 여기에는 키 저장소에 따라 애플리케이션 액세스를 키 및/또는 키 저장소에 부여하거나 기타 키 저장소 관련 구성 단계를 수행하는 작업이 포함될 수 있습니다. 예를 들어 Azure Key Vault에 액세스하려면 키 저장소에 올바른 자격 증명을 제공해야 합니다.

### <a name="using-the-azure-key-vault-provider"></a>Azure Key Vault 공급자 사용

AKV(Azure Key Vault)는 Always Encrypted에 대한 열 마스터 키를 저장 및 관리하는 편리한 옵션입니다(특히 애플리케이션이 Azure에서 호스트되는 경우). Linux, macOS 및 Windows의 ODBC Driver for SQL Server에는 Azure Key Vault용 기본 제공 열 마스터 키 저장소 공급자가 포함되어 있습니다. Always Encrypted에 대해 Azure Key Vault를 구성하는 방법에 대한 자세한 내용은 [Azure Key Vault - 단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [Key Vault 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/) 및 [Azure Key Vault에 열 마스터 키 만들기](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2)를 참조하세요.

> [!NOTE]
> ODBC 드라이버는 AKV 인증에 대 한 Active Directory Federation Services 지원 하지 않습니다. AKV에 Azure Active Directory 인증을 사용 하는 경우 Active Directory 구성에 페더레이션된 서비스가 포함 되 면 인증에 실패할 수 있습니다.
> Linux 및 macOS의 드라이버 버전 17.2 이상에서 이 공급자를 사용하려면 `libcurl`이 필요하지만, 다른 드라이버 관련 작업에서는 필요하지 않기 때문에 명시적 종속성은 아닙니다. `libcurl`에 관한 오류가 발생하는 경우 해당 패키지가 설치되었는지 확인하십시오.

드라이버에서 다음과 같은 자격 증명 유형을 사용하여 Azure Key Vault에 인증할 수 있습니다.

- 사용자 이름/암호 - 이 방법을 사용할 경우 자격 증명은 Azure Active Directory 사용자 이름 및 해당 암호입니다.

- 클라이언트 ID/비밀 - 이 방법을 사용할 경우 자격 증명은 애플리케이션 클라이언트 ID 및 애플리케이션 비밀입니다.

드라이버가 AKV에 저장된 CMK를 열 암호화에 사용할 수 있게 하려면 다음과 같은 연결 문자열 전용 키워드를 사용합니다.

|자격 증명 유형| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|사용자 이름/암호| `KeyVaultPassword`|사용자 계정 이름|암호|
|클라이언트 ID/비밀| `KeyVaultClientSecret`|클라이언트 ID|비밀|

#### <a name="example-connection-strings"></a>연결 문자열 예

다음 연결 문자열은 두 가지 자격 증명 유형을 사용하여 Azure Key Vault에 인증하는 방법을 보여 줍니다.

**클라이언트 ID/비밀**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**사용자 이름/암호**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

AKV를 CMK 스토리지에 사용하는 데 필요한 다른 ODBC 애플리케이션 변경 내용은 없습니다.

### <a name="using-the-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자 사용

Windows의 ODBC Driver for SQL Server에는 `MSSQL_CERTIFICATE_STORE`라는 Windows 인증서 저장소용 기본 제공 열 마스터 키 저장소 공급자가 포함되어 있습니다. macOS 또는 Linux에서는 이 공급자를 사용할 수 없습니다. 이 공급자를 사용하면 CMK가 클라이언트 머신에 로컬로 저장되며, 드라이버에서 CMK를 사용하는 데 필요한 애플리케이션의 추가 구성이 없습니다. 그러나 애플리케이션에서 인증서 및 저장소에 있는 해당 프라이빗 키에 액세스할 수 있어야 합니다. 자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted)을 참조하세요.

### <a name="using-custom-keystore-providers"></a>사용자 지정 키 저장소 공급자 사용

ODBC Driver for SQL Server는 CEKeystoreProvider 인터페이스를 사용하여 사용자 지정 타사 키 저장소 공급자도 지원합니다. 이 기능을 통해 애플리케이션에서 드라이버가 암호화된 열에 액세스하는 데 사용할 수 있도록 키 저장소 공급자를 로드, 쿼리 및 구성할 수 있습니다. 애플리케이션에서 SQL Server에 저장할 CEK를 암호화하고 ODBC를 사용하여 암호화된 열에 액세스하는 이상의 태스크를 수행하기 위해 키 저장소 공급자와 직접 상호 작용할 수도 있습니다. 자세한 내용은 [사용자 지정 키 저장소 공급자](../../connect/odbc/custom-keystore-providers.md)를 참조하세요.

두 개의 연결 특성이 사용자 지정 키 저장소 공급자와 상호 작용하는 데 사용됩니다. 반환할 수 있습니다.

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

첫 번째 특성은 키 저장소 공급자를 로드 및 열거하는 데 사용되고, 두 번째 특성은 애플리케이션과 공급자 간의 통신에 사용됩니다. 애플리케이션과 공급자 간의 상호 작용에 SQL Server와의 통신이 필요하지 않으므로 연결 설정 이전이나 이후, 언제든지 이러한 연결 특성을 사용할 수 있습니다. 그러나 드라이버가 아직 로드되지 않았으므로 연결 전에 이러한 특성을 설정하고 가져오면 드라이버 관리자에서 특성이 처리되지 않아 예상한 결과가 나오지 않을 수 있습니다.

#### <a name="loading-a-keystore-provider"></a>키 저장소 공급자 로드

`SQL_COPT_SS_CEKEYSTOREPROVIDER` 연결 특성을 설정하면 클라이언트 애플리케이션이 공급자 라이브러리를 로드할 수 있으므로, 라이브러리 안에 포함된 키 저장소 공급자를 사용할 수 있습니다.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`|[Input] 연결 핸들입니다. 유효한 연결 핸들이어야 하지만, 한 연결 핸들을 통해 로드된 공급자를 같은 프로세스의 다른 모든 연결 핸들에서 액세스할 수 있습니다.|
|`Attribute`|[Input] 설정할 특성으로, `SQL_COPT_SS_CEKEYSTOREPROVIDER` 상수입니다.|
|`ValuePtr`|[Input] 공급자 라이브러리의 파일 이름을 지정하는, null로 종료된 문자열에 대한 포인터입니다. SQLSetConnectAttrA의 경우 ANSI(멀티바이트) 문자열입니다. SQLSetConnectAttrW의 경우 유니코드(wchar_t) 문자열입니다.|
|`StringLength`|[Input] SQL_NTS 또는 ValuePtr 문자열의 길이입니다.|

드라이버는 플랫폼에서 정의된 동적 라이브러리 로드 메커니즘(Linux 및 macOS에서는 `dlopen()`, Windows에서는 `LoadLibrary()`)을 사용하여 ValuePtr 매개 변수로 식별된 라이브러리를 로드하고, 라이브러리에 정의된 모든 공급자를 드라이버에 알려진 공급자 목록에 추가합니다. 다음 오류가 발생할 수 있습니다.

| Error | 설명 |
|:--|:--|
|`CE203`|동적 라이브러리를 로드할 수 없습니다.|
|`CE203`|라이브러리에 “CEKeyStoreProvider” 내보낸 기호가 없습니다.|
|`CE203`|라이브러리에서 하나 이상의 공급자가 이미 로드되었습니다.|

`SQLSetConnectAttr`은 일반적인 오류 또는 성공 값을 반환하며, 표준 ODBC 진단 메커니즘을 통해 발생한 오류의 경우 추가 정보가 제공됩니다.

> [!NOTE]
> 애플리케이션 프로그래머는 사용자 지정 공급자가 로드된 후에 사용자 지정 공급자를 요구하는 쿼리가 연결을 통해 전송되도록 해야 합니다. 그렇게 하지 않으면 오류가 발생합니다.

| Error | 설명 |
|:--|:--|
|`CE200`|키 저장소 공급자 %1을(를) 찾을 수 없습니다. 해당하는 키 저장소 공급자 라이브러리가 로드되어 있는지 확인하세요.|

> [!NOTE]
> 키 저장소 공급자 구현자는 사용자 지정 공급자 이름에 `MSSQL`을 사용해서는 안 됩니다. 이 용어는 Microsoft에서만 사용하도록 예약되었으며, 향후 기본 제공 공급자와 충돌을 일으킬 수 있습니다. 사용자 지정 공급자 이름에 이 용어를 사용하면 ODBC 경고가 발생할 수 있습니다.

#### <a name="getting-the-list-of-loaded-providers"></a>로드된 공급자 목록 가져오기

이 연결 특성을 가져오면 클라이언트 애플리케이션에서 기본 제공 키 저장소 공급자를 포함하여 현재 드라이버에 로드된 키 저장소 공급자를 확인할 수 있습니다. 이 작업은 연결 이후에만 수행할 수 있습니다.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`|[Input] 연결 핸들입니다. 유효한 연결 핸들이어야 하지만, 한 연결 핸들을 통해 로드된 공급자를 같은 프로세스의 다른 모든 연결 핸들에서 액세스할 수 있습니다.|
|`Attribute`|[Input] 검색할 특성으로, `SQL_COPT_SS_CEKEYSTOREPROVIDER` 상수입니다.|
|`ValuePtr`|[Output] 다음에 로드되는 공급자 이름을 반환할 메모리에 대한 포인터입니다.|
|`BufferLength`|[Input] 버퍼 ValuePtr의 길이입니다.|
|`StringLengthPtr`|[Output] \*ValuePtr에 반환할 수 있는, null 종료 문자를 제외한 총 바이트 수를 반환할 버퍼에 대한 포인터입니다. ValuePtr이 null 포인터이면, 길이가 반환되지 않습니다. 특성 값이 문자열이고 반환할 수 있는 바이트 수가 BufferLength에서 null 종료 문자의 길이를 뺀 값보다 크면, \*ValuePtr의 데이터가 BufferLength에서 null 종료 문자의 길이를 뺀 값으로 잘리고 드라이버에서 null로 종료됩니다.|

전체 목록의 검색을 허용하기 위해 모든 Get 작업은 현재 공급자의 이름을 반환하고, 내부 카운터를 다음 값으로 증가합니다. 이 카운터가 목록의 끝에 도달하면 빈 문자열(“”)이 반환되고 카운터가 초기화됩니다. 그런 다음, 이후의 Get 작업이 목록의 처음부터 다시 진행됩니다.

### <a name="communicating-with-keystore-providers"></a>키 저장소 공급자와 통신

`SQL_COPT_SS_CEKEYSTOREDATA` 연결 특성을 사용하면 클라이언트 애플리케이션이 추가 매개 변수, 키 관련 자료 등을 구성하기 위해 로드된 키 저장소 공급자와 통신할 수 있습니다. 클라이언트 애플리케이션과 공급자 간의 통신은 이 연결 특성을 사용한 Get 및 Set 요청을 기반으로 하여 간단한 요청-응답 프로토콜을 따릅니다. 클라이언트 애플리케이션만 통신을 시작합니다.

> [!NOTE]
> CEKeyStoreProvider가 응답하는 ODBC 호출(SQLGet/SetConnectAttr)의 특성 때문에 ODBC 인터페이스는 연결 컨텍스트 확인 시에만 데이터 설정을 지원합니다.

애플리케이션은 CEKeystoreData 구조체를 사용하여 드라이버를 통해 키 저장소 공급자와 통신합니다.

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```

| 인수 | 설명 |
|:---|:---|
|`name`|[Input] Set에서 데이터가 전송되는 공급자 이름입니다. Get에서는 무시됩니다. null로 종료된 와이드 문자열입니다.|
|`dataSize`|[Input] 구조를 따르는 데이터 배열의 크기입니다.|
|`data`|[InOut] Set에서 공급자에게 전송할 데이터입니다. 임의의 데이터일 수 있으며, 드라이버에서 해석하려고 시도하지 않습니다. Get에서 공급자로부터 읽은 데이터를 받을 버퍼입니다.|

#### <a name="writing-data-to-a-provider"></a>공급자에 데이터 쓰기

`SQL_COPT_SS_CEKEYSTOREDATA` 특성을 사용하는 `SQLSetConnectAttr` 호출은 지정한 키 저장소 공급자에 데이터 “패킷”을 씁니다.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`| [Input] 연결 핸들입니다. 유효한 연결 핸들이어야 하지만, 한 연결 핸들을 통해 로드된 공급자를 같은 프로세스의 다른 모든 연결 핸들에서 액세스할 수 있습니다.|
|`Attribute`|[Input] 설정할 특성으로, `SQL_COPT_SS_CEKEYSTOREDATA` 상수입니다.|
|`ValuePtr`|[Input] CEKeystoreData 구조체에 대한 포인터입니다. 구조체의 이름 필드는 데이터의 대상 공급자를 식별합니다.|
|`StringLength`|[Input] SQL_IS_POINTER 상수입니다.|

[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)를 통해 자세한 오류 정보를 얻을 수 있습니다.

> [!NOTE]
> 공급자는 필요한 경우 연결 핸들을 사용하여 기록된 데이터를 특정 연결에 연관지을 수 있습니다. 이 기능은 연결별 구성을 구현하는 데 유용합니다. 연결 컨텍스트를 무시하고, 데이터 전송에 사용된 연결과 관계없이 데이터를 동일하게 처리할 수도 있습니다. 자세한 내용은 [컨텍스트 연결](../../connect/odbc/custom-keystore-providers.md#context-association)을 참조하세요.

#### <a name="reading-data-from-a-provider"></a>공급자에서 데이터 읽기

`SQL_COPT_SS_CEKEYSTOREDATA` 특성을 사용하는 `SQLGetConnectAttr` 호출은 ‘마지막으로 기록된’ 공급자로부터 데이터 “패킷”을 읽습니다.  데이터 패킷이 없으면 함수 시퀀스 오류가 발생합니다. 키 저장소 공급자 구현자는 타당한 경우 다른 부작용 없이 읽기 작업에 사용할 공급자를 선택하는 방법으로 0바이트의 “더미 쓰기”를 지원하는 것이 좋습니다.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 인수 | 설명 |
|:---|:---|
|`ConnectionHandle`|[Input] 연결 핸들입니다. 유효한 연결 핸들이어야 하지만, 한 연결 핸들을 통해 로드된 공급자를 같은 프로세스의 다른 모든 연결 핸들에서 액세스할 수 있습니다.|
|`Attribute`|[Input] 검색할 특성으로, `SQL_COPT_SS_CEKEYSTOREDATA` 상수입니다.|
|`ValuePtr`|[Output] 공급자에서 읽은 데이터가 배치되는 CEKeystoreData 구조체에 대한 포인터입니다.|
|`BufferLength`|[Input] SQL_IS_POINTER 상수입니다.|
|`StringLengthPtr`|[Output] BufferLength를 반환할 버퍼에 대한 포인터입니다. *ValuePtr이 null 포인터이면, 길이가 반환되지 않습니다.|

호출자는 CEKEYSTOREDATA 구조체를 따르는 충분한 길이의 버퍼가 기록되는 공급자에 대해 할당되도록 해야 합니다. 반환 시 해당 dataSize 필드가 공급자로부터 읽은 데이터의 실제 길이로 업데이트됩니다. [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)를 통해 자세한 오류 정보를 얻을 수 있습니다.

애플리케이션과 키 저장소 공급자 간에 전송되는 데이터의 형식과 관련해서 이 인터페이스의 추가 요구 사항은 없습니다. 각 공급자가 필요에 따라 고유한 프로토콜/데이터 형식을 정의할 수 있습니다.

고유한 키 저장소 공급자를 구현하는 예제는 [사용자 지정 키 저장소 공급자](../../connect/odbc/custom-keystore-providers.md)를 참조하세요.

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Always Encrypted를 사용할 때 ODBC 드라이버의 제한 사항

### <a name="asynchronous-operations"></a>비동기 작업
ODBC 드라이버에서 Always Encrypted와 [비동기 작업](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)을 함께 사용할 수는 있지만, Always Encrypted가 사용되는 경우 작업 성능이 저하됩니다. 문에 대한 암호화 메타데이터를 확인하기 위한 `sys.sp_describe_parameter_encryption` 호출은 다른 작업을 차단하며, 드라이버가 `SQL_STILL_EXECUTING`을 반환하기 전에 서버에서 메타데이터가 반환되기를 기다립니다.

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>SQLGetData를 사용하여 데이터 부분 검색
ODBC Driver 17 for SQL Server 이전에는 SQLGetData를 사용하여 암호화된 문자와 이진 열을 부분 검색할 수 없습니다. 전체 열의 데이터를 포함하는 충분한 길이의 버퍼를 사용하여 SQLGetData를 한 번만 호출할 수 있습니다.

### <a name="send-data-in-parts-with-sqlputdata"></a>SQLPutData를 사용하여 데이터 부분 전송
ODBC Driver 17.3 for SQL Server 이전에는 SQLPutData를 사용하여 삽입 또는 비교할 데이터를 부분 전송할 수 없습니다. 전체 데이터를 포함하는 버퍼를 사용하여 SQLPutData를 한 번만 호출할 수 있습니다. 암호화된 열에 긴 데이터를 삽입하려면 다음 섹션에서 설명하는 대량 복사 API를 입력 데이터 파일과 함께 사용합니다.

### <a name="encrypted-money-and-smallmoney"></a>암호화된 money 및 smallmoney
암호화된 **money** 또는 **smallmoney** 열은 해당 형식에 매핑되는 특정 ODBC 데이터 형식이 없어 피연산자 형식 충돌 오류가 발생하기 때문에 매개 변수에서 대상으로 지정할 수 없습니다.

## <a name="bulk-copy-of-encrypted-columns"></a>암호화된 열의 대량 복사

ODBC Driver 17 for SQL Server부터 Always Encrypted에서 [SQL 대량 복사 함수](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) 및 **bcp** 유틸리티 사용이 지원됩니다. 대량 복사(bcp_&#42;) API와 **bcp** 유틸리티를 사용하면 일반 텍스트(삽입 시 암호화되고 검색 시 암호 해독됨) 및 암호 텍스트(축자 전송됨)를 둘 다 삽입하고 검색할 수 있습니다.

- varbinary(max) 형식으로 암호 텍스트를 검색하려면(예: 다른 데이터베이스에 대량 로드하려는 경우), `ColumnEncryption` 옵션 없이 연결하거나 `Disabled`로 설정하고 BCP OUT 작업을 수행합니다.

- 일반 텍스트를 삽입 및 검색하고, 드라이버가 필요에 따라 암호화 및 암호 해독을 투명하게 수행하도록 하려면 `ColumnEncryption`을 `Enabled`로 설정하는 것으로 충분합니다. 그 밖의 BCP API 기능은 변경되지 않습니다.

- varbinary(max) 형식으로 암호 텍스트를 삽입하려면(예: 위에서 검색한 경우), `BCPMODIFYENCRYPTED` 옵션을 TRUE로 설정하고 BCP IN 작업을 수행합니다. 결과 데이터의 암호 해독이 가능하도록 대상 열의 CEK가 원래 암호 텍스트를 얻는 데 사용한 CEK와 같은지 확인합니다.

**bcp** 유틸리티를 사용하는 경우 `ColumnEncryption` 설정을 제어하려면 -D 옵션을 사용하고 원하는 값이 포함된 DSN을 지정합니다. 암호 텍스트를 삽입하려면 사용자의 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 설정이 사용되었는지 확인합니다.

다음 표에는 암호화된 열에서 작업하는 경우의 작업 요약이 나와 있습니다.

|`ColumnEncryption`|BCP 방향|설명|
|----------------|-------------|-----------|
|`Disabled`|OUT(클라이언트로)|암호 텍스트를 검색합니다. 관찰한 데이터 형식은 **varbinary(max)** 입니다.|
|`Enabled`|OUT(클라이언트로)|일반 텍스트를 검색합니다. 드라이버에서 열 데이터의 암호를 해독합니다.|
|`Disabled`|IN(서버로)|암호 텍스트를 삽입합니다. 암호 해독을 요구하지 않고 암호화된 데이터를 불투명하게 이동하는 데 사용됩니다. 사용자에 대해 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 옵션을 설정하지 않거나 연결 핸들에 대해 BCPMODIFYENCRYPTED를 설정하지 않으면, 작업이 실패합니다. 자세한 내용은 아래를 참조하세요.|
|`Enabled`|IN(서버로)|일반 텍스트를 삽입합니다. 드라이버에서 열 데이터를 암호화합니다.|

### <a name="the-bcpmodifyencrypted-option"></a>BCPMODIFYENCRYPTED 옵션

데이터 손상을 방지하기 위해 서버는 일반적으로 암호화된 열에 암호 텍스트를 직접 삽입하는 것을 허용하지 않으므로, 이러한 시도는 실패합니다. 그러나 BCP API를 사용하여 암호화된 데이터를 대량 로드하는 경우 `BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 옵션을 TRUE로 설정하면 암호 텍스트를 직접 삽입할 수 있으며, 사용자 계정에 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 옵션을 설정하는 것보다 암호화된 데이터의 손상 위험이 줄어듭니다. 단, 키가 데이터와 일치해야 합니다. 대량 삽입 후, 계속 사용하기 전에 삽입된 데이터에 대한 몇 가지 읽기 전용 검사를 수행하는 것이 좋습니다.

자세한 내용은 [상시 암호화로 보호되는 중요한 데이터 마이그레이션](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)을 참조하세요.

## <a name="always-encrypted-api-summary"></a>Always Encrypted API 요약

### <a name="connection-string-keywords"></a>연결 문자열 키워드

|속성|설명|  
|----------|-----------------|  
|`ColumnEncryption`|허용되는 값은 `Enabled`/`Disabled`입니다.<br>`Enabled` - 연결에 상시 암호화 기능을 사용하도록 설정합니다.<br>`Disabled` - 연결에 Always Encrypted 기능을 사용하지 않도록 설정합니다.<br>*유형*,*데이터* --(버전 17.4 이상)를 사용 하면 보안 enclave 및 증명 프로토콜 *유형*및 연결 된 증명 데이터 *데이터*를 사용 하 여 Always Encrypted 수 있습니다. <br><br>기본값은 `Disabled`입니다.|
|`KeyStoreAuthentication` | 유효한 값: `KeyVaultPassword`,`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | `KeyStoreAuthentication` = `KeyVaultPassword`이면, 이 값을 유효한 Azure Active Directory 사용자 계정 이름으로 설정합니다. <br>`KeyStoreAuthetication` = `KeyVaultClientSecret`이면, 이 값을 유효한 Azure Active Directory 애플리케이션 클라이언트 ID로 설정합니다. |
|`KeyStoreSecret` | `KeyStoreAuthentication` = `KeyVaultPassword`이면, 이 값을 해당 사용자 이름의 암호로 설정합니다. <br>`KeyStoreAuthentication` = `KeyVaultClientSecret`이면, 이 값을 유효한 Azure Active Directory 애플리케이션 클라이언트 ID와 관련된 애플리케이션 비밀로 설정합니다. |


### <a name="connection-attributes"></a>연결 특성

|속성|형식|설명|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|연결 전|`SQL_COLUMN_ENCRYPTION_DISABLE`(0) - Always Encrypted를 사용하지 않도록 설정합니다. <br>`SQL_COLUMN_ENCRYPTION_ENABLE`(1) - Always Encrypted를 사용하도록 설정합니다.<br> *형식*에 대 한 포인터,*데이터* 문자열--(버전 17.4 이상)에서 secure enclave를 사용 하도록 설정|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|연결 후|[Set] CEKeystoreProvider 로드 시도<br>[Get] CEKeystoreProvider 이름 반환|
|`SQL_COPT_SS_CEKEYSTOREDATA`|연결 후|[Set] CEKeystoreProvider에 데이터 쓰기<br>[Get] CEKeystoreProvider에서 데이터 읽기|
|`SQL_COPT_SS_CEKCACHETTL`|연결 후|[Set] CEK 캐시 TTL 설정<br>[Get] 현재 CEK 캐시 TTL 가져오기|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|연결 후|[Set] 신뢰할 수 있는 CMK 경로 포인터 설정<br>[Get] 신뢰할 수 있는 현재 CMK 경로 포인터 가져오기|

### <a name="statement-attributes"></a>문 특성

|속성|설명|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED`(0) - 문에 대해 Always Encrypted를 사용할 수 없습니다. <br>`SQL_CE_RESULTSETONLY`(1) - 암호 해독만 수행합니다. 결과 집합과 반환 값의 암호가 해독되고, 매개 변수는 암호화되지 않습니다. <br>`SQL_CE_ENABLED`(3) - Always Encrypted를 사용할 수 있고, 매개 변수와 결과에 모두 사용됩니다.|

### <a name="descriptor-fields"></a>설명자 필드

|IPD 필드|크기/형식|기본값|설명|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD(2바이트)|0|0(기본값)인 경우: 이 매개 변수의 암호화가 암호화 메타데이터의 사용 가능 여부에 따라 결정됩니다.<br><br>0이 아닌 경우: 이 매개 변수에 대한 암호화 메타데이터를 사용할 수 있으면 암호화됩니다. 암호화 메타데이터를 사용할 수 없으면 다음 오류가 발생하고 요청이 실패합니다. [CE300] [Microsoft][ODBC Driver 13 for SQL Server]매개 변수에 대해 필수 암호화가 지정되었지만 서버에서 제공된 암호화 메타데이터가 없습니다.|

### <a name="bcp_control-options"></a>bcp_control 옵션

|옵션 이름|기본값|설명|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|TRUE이면, varbinary(max) 값을 암호화된 열에 삽입할 수 있습니다. FALSE이면, 올바른 형식 및 암호화 메타데이터를 제공해야만 삽입할 수 있습니다.|

## <a name="see-also"></a>참고 항목

- [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [보안 enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)
- [상시 암호화 블로그](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

