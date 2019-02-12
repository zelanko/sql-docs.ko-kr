---
title: SQL Server용 PHP 드라이버와 함께 Always Encrypted 사용 | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: 5c82c32922712b377fd732b6745b1761e9f32a82
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55890004"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>SQL Server용 PHP 드라이버와 함께 Always Encrypted 사용
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>적용 가능 대상
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>소개

이 문서를 사용 하 여 PHP 응용 프로그램을 개발 하는 방법에 대해 설명 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 하며 [SQL Server 용 PHP 드라이버](../../connect/php/Microsoft-php-driver-for-sql-server.md)합니다.

Always Encrypted를 사용하면 클라이언트 애플리케이션이 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. ODBC Driver for SQL Server와 같은 Always Encrypted 사용 드라이버는 클라이언트 애플리케이션의 중요한 데이터를 투명하게 암호화하고 암호 해독합니다. 이 드라이버는 중요 데이터베이스 열에 해당하는 쿼리 매개 변수를 자동으로 확인하고(Always Encrypted를 사용하여 보호) 데이터를 SQL Server 또는 Azure SQL Database로 전달하기 전에 이러한 매개 변수의 값을 암호화합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. SQL Server 용 PHP 드라이버는 ODBC Driver for SQL Server 중요 한 데이터 암호화를 활용 합니다.

## <a name="prerequisites"></a>사전 요구 사항

 -   데이터베이스에서 상시 암호화를 구성합니다. 이 구성에는 Always Encrypted 키 프로비전 및 선택한 데이터베이스 열에 대한 암호화 설정이 포함됩니다. 데이터베이스에 상시 암호화가 구성되지 않은 경우 [상시 암호화 시작](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)의 지침을 따르세요. 특히, 데이터베이스를 열 마스터 키 (CMK), 열 암호화 키 (CEK), 및 해당 CEK를 사용 하 여 암호화 하는 하나 이상의 열을 포함 하는 테이블에 대 한 메타 데이터 정의 포함 해야 합니다.
 -   ODBC Driver for SQL Server 버전 17 이상이 개발 컴퓨터에 설치 되어 있는지 확인 합니다. 자세한 내용은 참조 하세요 [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)합니다.

## <a name="enabling-always-encrypted-in-a-php-application"></a>PHP 응용 프로그램에서 상시 암호화를 사용 하도록 설정

암호화된 열을 대상으로 하는 매개 변수 암호화를 설정하고 쿼리 결과의 암호를 해독하기에 가장 쉬운 방법은 `ColumnEncryption` 연결 문자열 키워드 값을 `Enabled`로 설정하는 것입니다. 다음은 예제는 SQLSRV 및 PDO_SQLSRV 드라이버에서 상시 암호화를 사용 하도록 설정 합니다.

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

암호화 또는 암호 해독을 성공 하는 데 적합 하지 않은 상시 암호화 사용 있는지 확인 해야 합니다.
 -   애플리케이션에는 VIEW ANY COLUMN MASTER KEY DEFINITION 및 VIEW ANY COLUMN ENCRYPTION KEY DEFINITION 데이터베이스 권한이 있으며 데이터베이스에서 Always Encrypted 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 참조 하세요 [Database 권한이](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)합니다.
 -   응용 프로그램 쿼리 암호화 된 열에 대 한 Cek를 보호 하는 CMK를 액세스할 수 있습니다. 이 요구 사항은 CMK를 저장 하는 키 저장소 공급자에 따라 달라 집니다. 자세한 내용은 [열 마스터 키 저장소를 사용 하 여 작업](#working-with-column-master-key-stores)합니다.

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정

연결에 Always Encrypted를 사용 하면 표준 SQLSRV Api를 사용할 수 있습니다 (참조 [SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)) 또는 PDO_SQLSRV Api (참조 [PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)) 데이터를 검색 또는 수정 암호화 된 데이터베이스 열에 있습니다. 응용 프로그램에 필요한 데이터베이스 권한이 있고 열 마스터 키에 액세스할 수 가정 하 고, 드라이버 암호화 된 열을 대상에 투명 하 게 작동 하는 암호화 된 열에서 검색 데이터를 해독 하는 쿼리 매개 변수를 암호화 합니다 열 암호화 되지 않은 것 처럼 응용 프로그램입니다.

Always Encrypted를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없는 경우 암호화된 열에서 데이터를 검색할 수 있습니다. 그러나 드라이버는 모든 암호 해독을 시도 하지 않습니다 하 고 응용 프로그램 (바이트 배열)로 암호화 된 이진 데이터를 받습니다.

다음 표에서는 Always Encrypted 사용 여부에 따른 쿼리 동작을 요약합니다.

|쿼리 특성|상시 암호화가 설정되고 애플리케이션에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 애플리케이션에서 키 또는 키 메타데이터에 액세스할 수 없는 경우|상시 암호화를 사용하지 않는 경우|
|---|---|---|---|
|암호화 된 열을 대상으로 하는 매개 변수입니다.|매개 변수 값이 투명하게 암호화됩니다.|Error|Error|
|암호화된 열을 대상으로 하는 매개 변수 없이 암호화된 열에서 데이터를 검색합니다.|암호화된 열의 결과가 투명하게 암호 해독됩니다. 응용 프로그램 일반 텍스트 열 값을 받습니다. |Error|암호화된 열의 결과가 암호 해독되지 않습니다. 애플리케이션에서 암호화된 값을 바이트 배열로 수신합니다.|
 
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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>데이터 삽입 예제

다음 예제에서는 환자 테이블을 사용 하 여 행 삽입을 SQLSRV 및 PDO_SQLSRV 드라이버를 사용 하는 방법을 보여 줍니다. 다음 사항을 note 합니다.
 -   샘플 코드에는 암호화에 대한 내용이 없습니다. 드라이버는 자동으로 검색 하 고 암호화 된 열을 대상의 SSN 및 BirthDate 매개 변수의 값을 암호화 합니다. 이 메커니즘을 통해 애플리케이션에 투명하게 암호화할 수 있습니다.
 -   암호화된 열을 포함하여 데이터베이스 열에 삽입된 값은 바인딩된 매개 변수로 전달됩니다. 매개 변수를 사용하여 암호화되지 않은 열에 값을 전달하는 것은 선택 사항이지만(그러나 SQL 삽입을 방지할 수 있으므로 매우 권장됨) 암호화된 열을 대상으로 하는 값에 필요합니다. SSN 또는 BirthDate 열에 삽입 된 값 쿼리 문에 포함 된 리터럴로 전달 하는 경우 드라이버는 암호화 하거나, 쿼리에서 리터럴을 처리 하려고 시도 하지 않습니다 때문에 쿼리가 실패 합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.
 -   바인딩 매개 변수를 사용 하 여 값을 삽입할 때 동일한 데이터 형식의 대상 열 또는 대상 열의 데이터 형식으로 변환 된 지원 되는 SQL 형식 데이터베이스에 전달 되어야 합니다. 상시 암호화는 몇 가지 형식 변환을 지원 하기 때문에이 요구 사항은 (세부 정보를 참조 하세요 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). 두 가지 PHP 드라이버를 SQLSRV 및 PDO_SQLSRV, 각 사용자가 SQL 형식의 값을 확인할 수 있도록 하는 메커니즘에 있습니다. 따라서 사용자는 SQL 형식을 명시적으로 제공할 필요가 없습니다.
  -   SQLSRV 드라이버를 사용자에 두 가지 옵션이 있습니다.
   -   PHP 드라이버를 확인 하 고 올바른 SQL 유형 설정에 의존 합니다. 이 경우 사용자를 사용 해야만 `sqlsrv_prepare` 및 `sqlsrv_execute` 매개 변수가 있는 쿼리를 실행 합니다.
   -   SQL 형식을 명시적으로 설정 합니다.
  -   PDO_SQLSRV 드라이버에 대 한 사용자가 없습니다 매개 변수의 SQL 형식을 명시적으로 설정 하는 옵션. PDO_SQLSRV 드라이버에는 자동으로 매개 변수를 바인딩할 때 SQL 형식을 결정 하는 사용자 수 있습니다.
 -   SQL 형식을 결정 하도록 드라이버에 대 한 몇 가지 제한 사항이 적용 됩니다.
  -   SQLSRV 드라이버
   -   사용자가 암호화 된 열에 대 한 SQL 유형을 확인 하는 드라이버, 사용자를 사용 해야만 `sqlsrv_prepare` 고 `sqlsrv_execute`입니다.
   -   경우 `sqlsrv_query` 는 기본 사용자는 모든 매개 변수의 SQL 형식을 지정 합니다. 문자열 형식에 대 한 문자열 길이 및 전체 자릿수 및 소수 10 진수 형식에 대 한 지정된 된 SQL 형식이 포함 해야 합니다.
  -   PDO_SQLSRV 드라이버
   -   문 특성 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 매개 변수가 있는 쿼리에서 지원 되지 않습니다.
   -   문 특성 `PDO::ATTR_EMULATE_PREPARES` 매개 변수가 있는 쿼리에서 지원 되지 않습니다.
   
SQLSRV 드라이버 및 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

SQLSRV 드라이버 및 [sqlsrv_query](../../connect/php/sqlsrv-query.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

PDO_SQLSRV 드라이버 및 [pdo:: prepare](../../connect/php/pdo-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>일반 텍스트 데이터 검색 예제

다음 예제에서는 SQLSRV 및 PDO_SQLSRV 드라이버를 사용 하 여 암호화 된 열에서 일반 텍스트 데이터를 검색 하 고 암호화 된 값에 따라 데이터 필터링을 보여 줍니다. 다음 사항을 note 합니다.
 -   해당 드라이버가 서버로 전달하기 전에 투명하게 암호화할 수 있도록 바인딩 매개 변수를 사용하여 SSN 열에서 필터링하기 위해 WHERE 절에 사용되는 값을 전달해야 합니다.
 -   바인딩된 매개 변수를 사용 하 여 쿼리를 실행할 때 SQLSRV 드라이버를 사용 하는 경우 명시적으로 사용자 SQL 형식을 지정 하지 않은 경우 PHP 드라이버를 자동으로 사용자에 대 한 SQL 형식을 결정 합니다.
 -   이 드라이버는 SSN 및 BirthDate 열에서 검색한 데이터의 암호를 투명하게 해독하므로 프로그램에서 인쇄한 모든 값은 일반 텍스트로 표시됩니다.
 
참고: 쿼리는 결정적 암호화 하는 경우에 암호화 된 열에서 같음 비교를 수행할 수 있습니다. 자세한 내용은 [결정적 또는 임의 암호화 선택](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)을 참조하세요.

SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>암호 텍스트 데이터 검색 예제

상시 암호화를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예제는 SQLSRV 및 PDO_SQLSRV 드라이버를 사용 하 여 암호화 된 열에서 암호화 된 이진 데이터 검색 보여 줍니다. 다음 사항을 note 합니다.
 -   연결 문자열에서는 Always Encrypted를 사용하지 않으므로 쿼리에서 SSN 및 BirthDate의 암호화된 값을 바이트 배열로 반환합니다(프로그램에서 값을 문자열로 변환).
 -   암호화된 열을 대상으로 하는 매개 변수가 없으면 상시 암호화를 사용하지 않고 암호화된 열에서 데이터를 검색하는 쿼리에 매개 변수가 있을 수 있습니다. 다음 쿼리는 LastName을 기준으로 필터링되며 데이터베이스에서 암호화되지 않습니다. 쿼리가 SSN 또는 BirthDate를 기준으로 필터링되면 쿼리가 실패합니다.
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>암호화된 열 쿼리 시 일반적인 문제 방지

이 섹션에서는 PHP 애플리케이션에서 암호화된 열을 쿼리할 때 발생하는 일반적인 오류 범주와 이를 방지하는 방법을 설명합니다.

#### <a name="unsupported-data-type-conversion-errors"></a>지원되지 않는 데이터 형식 변환 오류

상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 지원되는 형식 변환의 자세한 목록은 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. 데이터 형식 변환 오류를 방지하려면 다음을 수행합니다.
 -   사용 하 여 SQLSRV 드라이버를 사용 하는 경우 `sqlsrv_prepare` 고 `sqlsrv_execute` SQL 형식 열 크기 및 매개 변수의 소수 자릿수와 함께 자동으로 결정 됩니다.
 -   PDO_SQLSRV 드라이버를 사용 하 여 쿼리를 실행 하려면, 열 크기 및 매개 변수의 소수 자릿수를 사용 하 여 SQL 형식 결정도 자동으로 됩니다.
 -   사용 하 여 SQLSRV 드라이버를 사용 하는 경우 `sqlsrv_query` 쿼리를 실행 합니다.
  -   매개 변수의 SQL 형식을 동일 하거나 대상 열의 형식과 동일 하거나 열의 형식 변환이 SQL 유형에 서 지원 합니다.
  -   `decimal` 및 `numeric` SQL Server 데이터 형식의 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다.
  -   대상 열을 수정하는 쿼리에서 SQL Server 데이터 형식이 `datetime2`, `datetimeoffset` 또는 `time`인 열을 대상으로 하는 매개 변수의 정밀도가 대상 열의 정밀도보다 크지 않아야 합니다.
 -   PDO_SQLSRV 문 특성을 사용 하지 마세요 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 또는 `PDO::ATTR_EMULATE_PREPARES` 매개 변수가 있는 쿼리에서
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류

암호화 된 열을 대상으로 하는 모든 값을 서버로 전송 되기 전에 암호화 해야 합니다. 암호화된 열의 일반 텍스트 값으로 삽입, 수정 또는 필터링하면 오류가 발생합니다. 이러한 오류를 방지하려면 다음을 확인합니다.
 -   상시 암호화가 설정 (연결 문자열을 설정 합니다 `ColumnEncryption` 키워드를 `Enabled`).
 -   바인딩 매개 변수를 사용하여 암호화된 열을 대상으로 하는 데이터를 전송합니다. 다음 예제에서는 암호화 된 열 (SSN)에서 리터럴/상수 기준으로 잘못 필터링 하는 쿼리를 보여 줍니다.
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

Always Encrypted는 클라이언트 쪽 암호화 기술이므로 데이터베이스가 아닌 클라이언트 쪽에서 대부분의 성능 오버헤드가 발생합니다. 암호화 및 암호 해독 작업의 비용 외에 클라이언트 쪽 성능 오버헤드의 원인은 다음과 같습니다.
 -   쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복
 -   열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복

연결에 대한 Always Encrypted가 설정된 경우 기본적으로 ODBC 드라이버는 각 매개 변수화된 쿼리에 대해 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)을 호출하고 매개 변수 값 없이 쿼리 문을 SQL Server에 전달합니다. 이 저장된 프로시저 매개 변수를 암호화 해야 하 고 그렇다면 알아 쿼리 문을 분석 하 여, 드라이버를 암호화할 수 있도록 각 매개 변수에 대해 암호화 관련 정보를 반환 합니다.

SQL을 제공 하지 않고 준비 된 문을 입력, PHP 드라이버를 호출 하는 Always Encrypted가 설정 연결에서 매개 변수를 바인딩할 때 PHP 드라이버에는 사용자가 매개 변수를 바인딩할 수 있으므로 [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) 에 SQL 유형, 열 크기 및 소수 자릿수를 가져오려면 매개 변수입니다. 메타 데이터는 다음 호출 하는 데 사용 됩니다 [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)합니다. 이러한 여분의 `SQLDescribeParam` 호출 ODBC 드라이버에 이미 저장 된 정보를 클라이언트 쪽에서 데이터베이스에 대 한 추가 왕복 작업을 필요 하지 않습니다 때 `sys.sp_describe_parameter_encryption` 호출 되었습니다.

이전 동작 확인 높은 클라이언트 응용 프로그램 (및 응용 프로그램 개발자)에 대 한 투명도 수준을 암호화 된 열을 대상으로 하는 값은 드라이버에 전달할으로 어떤 쿼리가 암호화 된 열 액세스 알아야 할 필요 하지 않습니다 매개 변수입니다.

ODBC Driver for SQL Server와는 달리 문/쿼리 수준에서 상시 암호화를 사용 아직 지원 되지 않습니다는 PHP 드라이버. 

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

열 암호화 키 (CEK) 암호를 해독 하는 열 마스터 키 저장소에 대 한 호출의 수를 줄이려면 드라이버 메모리에 일반 텍스트 Cek를 캐시 합니다. 데이터베이스 메타 데이터에서 암호화 된 CEK (ECEK)를 받으면 ODBC 드라이버는 먼저 일반 텍스트 CEK에 해당 하는 캐시에 있는 암호화 된 키 값을 찾으려고 합니다. 드라이버는 해당 일반 텍스트 CEK 캐시에서 찾을 수 없는 경우에 CMK를 포함 하는 키 저장소를 호출 합니다.

참고: SQL Server 용 ODBC 드라이버에서 캐시의 항목을 2 시간 제한 시간이 지난 후 제거 됩니다. 이 동작을 지정 된 ECEK에 대 한는 또는 2 시간 마다 응용 프로그램의 수명 동안 한 번만 키 저장소를 연결 하는 드라이버에서 더 작은 의미 합니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업

를 암호화 하거나 데이터를 해독 하려면 드라이버를 대상 열에 대해 구성 된 CEK를 입수해 야 합니다. Cek는 데이터베이스 메타 데이터에 암호화 된 형식 (ECEKs)에 저장 됩니다. 각 CEK 암호화에 사용 된 해당 CMK에 있습니다. [데이터베이스 메타 데이터](../../t-sql/statements/create-column-master-key-transact-sql.md) 자체 CMK를 저장 하지 않는 키 저장소 CMK를 찾는 데 사용할 수 있는 정보와 키 저장소의 이름을 포함 합니다.

ECEK의 일반 텍스트 값을 가져오려면, 드라이버 먼저 CEK와 CMK는 해당 하는 방법에 대 한 메타 데이터를 가져오고이 정보를 사용 하 여 CMK를 포함 하는 키 저장소에 문의 하 고 암호 해독 된 ECEK에 요청 합니다. 드라이버는 키 저장소 공급자를 사용 하 여 키 저장소와 통신 합니다.

Microsoft Driver for SQL Server 용 PHP 5.3.0 Windows 인증서 저장소 공급자 및 Azure Key Vault 에서만 지원 됩니다. ODBC 드라이버 (사용자 지정 키 저장소 공급자)에서 지 원하는 다른 키 저장소 공급자가 아직 지원 되지 않습니다.

### <a name="using-the-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자 사용

라는 Windows 인증서 저장소에 대 한 기본 제공 열 마스터 키 저장소 공급자를 포함 하는 Windows의 SQL Server 용 ODBC 드라이버 `MSSQL_CERTIFICATE_STORE`합니다. (이 공급자는 macOS 또는 Linux에서 사용할 수 있습니다.) 이 공급자를 사용 하 여 CMK 클라이언트 컴퓨터에 로컬로 저장 되어 이며 응용 프로그램에서 추가 구성 없이 드라이버와 함께 사용 하는 데 필요한 합니다. 그러나 응용 프로그램 저장소에 인증서 및 개인 키에 액세스할 수 있어야 합니다. 자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

### <a name="using-azure-key-vault"></a>Azure Key Vault를 사용한 EKM

Azure Key Vault 암호화 키, 암호 및 Azure를 사용 하 여 다른 암호를 저장 하는 방법을 제공 하 고 Always Encrypted에 대 한 키를 저장 하기 위해 사용할 수 있습니다. ODBC Driver for SQL Server (버전 17 이상)는 Azure Key Vault에 대 한 기본 마스터 키 저장소 공급자를 포함합니다. Azure Key Vault 구성을 처리 하는 다음과 같은 연결 옵션: `KeyStoreAuthentication`, `KeyStorePrincipalId`, 및 `KeyStoreSecret`합니다. 
 -   `KeyStoreAuthentication` 두 개의 가능한 문자열 값 중 하나를 수행 합니다. `KeyVaultPassword` 및 `KeyVaultClientSecret`합니다. 이러한 값은 다른 두 키워드를 사용 하 여 어떤 종류의 인증 자격 증명 되는 제어 합니다.
 -   `KeyStorePrincipalId` Azure Key Vault에 액세스 하려는 계정에 대 한 식별자를 나타내는 문자열을 사용 합니다. 
     -   하는 경우 `KeyStoreAuthentication` 로 설정 된 `KeyVaultPassword`, 다음 `KeyStorePrincipalId` Azure active Directory 사용자의 이름 이어야 합니다.
     -   하는 경우 `KeyStoreAuthentication` 로 설정 된 `KeyVaultClientSecret`, 다음 `KeyStorePrincipalId` 는 응용 프로그램 클라이언트 ID 여야 합니다.
 -   `KeyStoreSecret` 자격 증명 비밀을 나타내는 문자열을 사용 합니다. 
     -   하는 경우 `KeyStoreAuthentication` 로 설정 된 `KeyVaultPassword`, 다음 `KeyStoreSecret` 사용자의 암호 여야 합니다. 
     -   하는 경우 `KeyStoreAuthentication` 로 설정 된 `KeyVaultClientSecret`, 다음 `KeyStoreSecret` 응용 프로그램 클라이언트 ID와 연결 된 응용 프로그램 암호 여야 합니다.

세 가지 옵션 모두 Azure Key Vault를 사용 하는 연결 문자열에 있어야 합니다. 또한 `ColumnEncryption` 으로 설정 되어 있어야 `Enabled`합니다. 하는 경우 `ColumnEncryption` 로 설정 된 `Disabled` Azure Key Vault 옵션이 있는지, 스크립트가 오류 없이 진행 하지만 지 않은 암호화 수행 됩니다.

다음 예제에서는 Azure Key Vault를 사용 하 여 SQL Server에 연결 하는 방법을 표시 합니다.

SQLSRV:

Azure Active Directory 계정을 사용합니다.
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreSecret"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
Azure 응용 프로그램 클라이언트 ID 및 암호를 사용합니다.
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreSecret"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV: Azure Active Directory 계정을 사용합니다.
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreSecret = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
Azure 응용 프로그램 클라이언트 ID 및 암호를 사용합니다.
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreSecret = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>상시 암호화를 사용 하는 경우 PHP 드라이버의 제한 사항

SQLSRV 및 PDO_SQLSRV:
 -   Linux/macOS Windows 인증서 저장소 공급자를 지원 하지 않습니다.
 -   매개 변수 강제 암호화
 -   문 수준에서 상시 암호화 사용 
 -   Linux 및 macOS (예: "en_US 상시 암호화 기능 및 UTF8 이외 로캘을 사용 하는 경우. ISO-8859-1 "), 암호화 된 char (n) 열에 데이터를 null 또는 빈 문자열을 삽입 코드 페이지 1252 시스템에 설치 되어 있지 않으면 작동 하지 않을 수 있습니다
 
SQLSRV에만 해당:
 -   사용 하 여 `sqlsrv_query` SQL 형식을 지정 하지 않고 바인딩 매개 변수
 -   사용 하 여 `sqlsrv_prepare` SQL 문의 일괄 처리에서 매개 변수 바인딩  
 
PDO_SQLSRV에만 해당:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` 매개 변수가 있는 쿼리에서 지정 하는 문 특성
 -   `PDO::ATTR_EMULATE_PREPARE` 매개 변수가 있는 쿼리에서 지정 하는 문 특성
 -   SQL 문의 일괄 처리에서 매개 변수 바인딩
 
PHP 드라이버에는 또한 SQL Server 및 데이터베이스에 대 한 ODBC 드라이버에 의해 적용 되는 제한을 상속 합니다. 참조 [상시 암호화를 사용 하는 경우 ODBC 드라이버의 제한 사항](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 하 고 [Always Encrypted 기능 세부 정보](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)합니다.  
  
## <a name="see-also"></a>참고 항목  
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
