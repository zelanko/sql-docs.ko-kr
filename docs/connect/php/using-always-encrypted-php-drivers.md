---
title: SQL Server용 PHP 드라이버와 함께 Always Encrypted 사용 | Microsoft Docs
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-kaywon
ms.author: jroth
author: rothja
manager: v-mabarw
ms.openlocfilehash: 17bd2297a81ed8c4b9e62f80a8bffd7a4c87af34
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286367"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>SQL Server용 PHP 드라이버와 함께 Always Encrypted 사용
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>적용 가능 대상
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>소개

이 문서에서는 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 [SQL Server용 PHP 드라이버](../../connect/php/Microsoft-php-driver-for-sql-server.md)를 사용하여 PHP 애플리케이션을 개발하는 방법을 설명합니다.

Always Encrypted를 사용하면 클라이언트 애플리케이션이 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. ODBC Driver for SQL Server와 같은 Always Encrypted 사용 드라이버는 클라이언트 애플리케이션의 중요한 데이터를 투명하게 암호화하고 암호 해독합니다. 이 드라이버는 중요 데이터베이스 열에 해당하는 쿼리 매개 변수를 자동으로 확인하고(Always Encrypted를 사용하여 보호) 데이터를 SQL Server 또는 Azure SQL Database로 전달하기 전에 이러한 매개 변수의 값을 암호화합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. SQL Server용 PHP 드라이버는 ODBC Driver for SQL Server를 활용하여 중요한 데이터를 암호화합니다.

## <a name="prerequisites"></a>사전 요구 사항

 -   데이터베이스에서 상시 암호화를 구성합니다. 이 구성에는 Always Encrypted 키 프로비전 및 선택한 데이터베이스 열에 대한 암호화 설정이 포함됩니다. 데이터베이스에 상시 암호화가 구성되지 않은 경우 [상시 암호화 시작](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)의 지침을 따르세요. 특히, 데이터베이스에 CMK(열 마스터 키), CEK(열 암호화 키) 및 해당 CEK를 사용하여 암호화된 열을 하나 이상 포함하는 테이블에 대한 메타데이터 정의가 포함되어 있어야 합니다.
 -   ODBC Driver for SQL Server 버전 17 이상이 개발 컴퓨터에 설치되어 있어야 합니다. 자세한 내용은 [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)를 참조하세요.

## <a name="enabling-always-encrypted-in-a-php-application"></a>PHP 애플리케이션에서 Always Encrypted 사용

암호화된 열을 대상으로 하는 매개 변수 암호화를 설정하고 쿼리 결과의 암호를 해독하기에 가장 쉬운 방법은 `ColumnEncryption` 연결 문자열 키워드 값을 `Enabled`로 설정하는 것입니다. 다음은 SQLSRV 및 PDO_SQLSRV 드라이버에서 Always Encrypted를 사용하도록 설정하는 예제입니다.

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

Always Encrypted를 사용하도록 설정해도 암호화 또는 암호 해독에 실패할 수 있습니다. 다음 사항도 확인해야 합니다.
 -   애플리케이션에는 VIEW ANY COLUMN MASTER KEY DEFINITION 및 VIEW ANY COLUMN ENCRYPTION KEY DEFINITION 데이터베이스 권한이 있으며 데이터베이스에서 Always Encrypted 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 [데이터베이스 사용 권한](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)을 참조하세요.
 -   애플리케이션은 쿼리된 암호화된 열의 CEK를 보호하는 CMK에 액세스할 수 있습니다. 이 요구 사항은 CMK를 저장하는 키 저장소 공급자에 따라 달라집니다. 자세한 내용은 [열 마스터 키 저장소 작업](#working-with-column-master-key-stores)을 참조하세요.

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정

연결에 Always Encrypted를 사용하도록 설정하면 표준 SQLSRV API([SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md) 참조) 또는 PDO_SQLSRV API([PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md) 참조)를 사용하여 암호화된 데이터베이스 열의 데이터를 검색하거나 수정할 수 있습니다. 애플리케이션에 필요한 데이터베이스 사용 권한이 있고 열 마스터 키에 액세스할 수 있다고 가정할 경우, 드라이버는 암호화된 열을 대상으로 하는 쿼리 매개 변수를 모두 암호화하고 암호화된 열에서 검색된 데이터의 암호를 해독하여 열이 암호화되지 않은 것처럼 애플리케이션에 투명하게 동작합니다.

Always Encrypted를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없는 경우 암호화된 열에서 데이터를 검색할 수 있습니다. 그러나 드라이버에서 암호 해독을 시도하지 않고, 애플리케이션이 암호화된 이진 데이터를 바이트 배열로 수신합니다.

다음 표에서는 Always Encrypted 사용 여부에 따른 쿼리 동작을 요약합니다.

|쿼리 특성|상시 암호화가 설정되고 애플리케이션에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 애플리케이션에서 키 또는 키 메타데이터에 액세스할 수 없는 경우|상시 암호화를 사용하지 않는 경우|
|---|---|---|---|
|암호화된 열을 대상으로 하는 매개 변수입니다.|매개 변수 값이 투명하게 암호화됩니다.|Error|Error|
|암호화된 열을 대상으로 하는 매개 변수 없이 암호화된 열에서 데이터를 검색합니다.|암호화된 열의 결과가 투명하게 암호 해독됩니다. 애플리케이션이 일반 텍스트 열 값을 받습니다. |Error|암호화된 열의 결과가 암호 해독되지 않습니다. 애플리케이션에서 암호화된 값을 바이트 배열로 수신합니다.|
 
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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>데이터 삽입 예제

다음 예제에서는 SQLSRV 및 PDO_SQLSRV 드라이버를 사용하여 Patient 테이블에 행을 삽입하는 방법을 보여 줍니다. 다음 사항에 유의하세요.
 -   샘플 코드에는 암호화에 대한 내용이 없습니다. 드라이버에서 암호화된 열을 대상으로 하는 SSN 및 BirthDate 매개 변수의 값을 자동으로 검색하고 암호화합니다. 이 메커니즘을 통해 애플리케이션에 투명하게 암호화할 수 있습니다.
 -   암호화된 열을 포함하여 데이터베이스 열에 삽입된 값은 바인딩된 매개 변수로 전달됩니다. 매개 변수를 사용하여 암호화되지 않은 열에 값을 전달하는 것은 선택 사항이지만(그러나 SQL 삽입을 방지할 수 있으므로 매우 권장됨) 암호화된 열을 대상으로 하는 값에 필요합니다. SSN 또는 BirthDate 열에 삽입된 값을 쿼리 문에 포함된 리터럴로 전달하면, 드라이버에서 쿼리의 리터럴을 암호화하거나 다른 방식으로 처리하지 않기 때문에 쿼리가 실패합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.
 -   bind 매개 변수를 사용하여 값을 삽입할 때 대상 열의 데이터 형식과 동일하거나 대상 열의 데이터 형식으로 변환이 지원되는 SQL 형식이 데이터베이스에 전달되어야 합니다. 이 요구 사항은 Always Encrypted에서 몇 가지 형식 변환을 지원하기 때문입니다. 자세한 내용은 [Always Encrypted(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. 두 PHP 드라이버 SQLSRV 및 PDO_SQLSRV에는 사용자가 값의 SQL 형식을 결정하는 데 도움이 되는 메커니즘이 있습니다. 따라서 사용자는 SQL 형식을 명시적으로 제공할 필요가 없습니다.
  -   SQLSRV 드라이버의 경우 사용자에게 두 가지 옵션이 있습니다.
   -   PHP 드라이버를 사용하여 올바른 SQL 형식을 결정하고 설정합니다. 이 경우 사용자는 `sqlsrv_prepare` 및 `sqlsrv_execute`를 사용하여 매개 변수가 있는 쿼리를 실행해야 합니다.
   -   SQL 형식을 명시적으로 설정합니다.
  -   PDO_SQLSRV 드라이버의 경우 사용자에게 매개 변수의 SQL 형식을 명시적으로 설정할 수 있는 옵션이 없습니다. PDO_SQLSRV 드라이버는 기본적으로 사용자가 매개 변수를 바인딩할 때 SQL 형식을 결정하는 데 도움을 줍니다.
 -   드라이버가 SQL 형식을 결정하는 데 몇 가지 제한 사항이 적용됩니다.
  -   SQLSRV 드라이버
   -   암호화된 열에 대한 SQL 형식을 결정하려면 `sqlsrv_prepare` 및 `sqlsrv_execute`를 사용해야 합니다.
   -   `sqlsrv_query`를 선호하는 경우 사용자는 모든 매개 변수에 대해 SQL 형식을 지정해야 합니다. 지정된 SQL 형식은 문자열 형식에 대한 문자열 길이와 decimal 형식의 소수 자릿수 및 전체 자릿수를 포함해야 합니다.
  -   PDO_SQLSRV 드라이버
   -   매개 변수가 있는 쿼리에서는 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 문 특성을 지원하지 않습니다.
   -   매개 변수가 있는 쿼리에서는 `PDO::ATTR_EMULATE_PREPARES` 문 특성을 지원하지 않습니다.
   
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

PDO_SQLSRV 드라이버 및 [PDO::prepare](../../connect/php/pdo-prepare.md):
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

다음 예제에서는 암호화된 값에 따라 데이터를 필터링하고 SQLSRV 및 PDO_SQLSRV 드라이버를 사용하여 암호화된 열에서 일반 텍스트 데이터를 검색하는 방법을 보여 줍니다. 다음 사항에 유의하세요.
 -   해당 드라이버가 서버로 전달하기 전에 투명하게 암호화할 수 있도록 바인딩 매개 변수를 사용하여 SSN 열에서 필터링하기 위해 WHERE 절에 사용되는 값을 전달해야 합니다.
 -   바인딩된 매개 변수를 사용하여 쿼리를 실행하는 경우 사용자가 SQLSRV 드라이버를 사용할 때 명시적으로 SQL 형식을 지정하지 않으면 PHP 드라이버가 사용자 대신 자동으로 SQL 형식을 결정합니다.
 -   이 드라이버는 SSN 및 BirthDate 열에서 검색한 데이터의 암호를 투명하게 해독하므로 프로그램에서 인쇄한 모든 값은 일반 텍스트로 표시됩니다.
 
참고: 암호화가 결정적인 경우에만 쿼리에서 암호화된 열에 대해 동등 비교를 수행할 수 있습니다. 자세한 내용은 [결정적 또는 임의 암호화 선택](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)을 참조하세요.

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

다음 예제에서는 SQLSRV 및 PDO_SQLSRV 드라이버를 사용하여 암호화된 열에서 암호화된 이진 데이터를 검색하는 방법을 보여 줍니다. 다음 사항에 유의하세요.
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
 -   `sqlsrv_prepare` 및 `sqlsrv_execute`에서 SQLSRV 드라이버를 사용하는 경우 SQL 형식이 매개 변수의 열 크기 및 소수 자릿수와 함께 자동으로 결정됩니다.
 -   PDO_SQLSRV 드라이버를 사용하여 쿼리를 실행하는 경우 SQL 형식이 매개 변수의 열 크기 및 소수 자릿수와 함께 자동으로 결정됩니다.
 -   `sqlsrv_query`에서 SQLSRV 드라이버를 사용하여 쿼리를 실행하는 경우:
  -   매개 변수의 SQL 형식이 대상 열의 형식과 정확히 같거나, SQL 형식에 열 형식으로의 변환이 지원되어야 합니다.
  -   `decimal` 및 `numeric` SQL Server 데이터 형식의 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다.
  -   대상 열을 수정하는 쿼리에서 SQL Server 데이터 형식이 `datetime2`, `datetimeoffset` 또는 `time`인 열을 대상으로 하는 매개 변수의 정밀도가 대상 열의 정밀도보다 크지 않아야 합니다.
 -   매개 변수가 있는 쿼리에 PDO_SQLSRV 문 특성 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 또는 `PDO::ATTR_EMULATE_PREPARES`를 사용하지 마세요.
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류

암호화된 열을 대상으로 하는 값은 서버로 전송하기 전에 암호화해야 합니다. 암호화된 열의 일반 텍스트 값으로 삽입, 수정 또는 필터링하면 오류가 발생합니다. 이러한 오류를 방지하려면 다음을 확인합니다.
 -   Always Encrypted가 사용하도록 설정되었습니다(연결 문자열에서 `ColumnEncryption` 키워드를 `Enabled`로 설정).
 -   바인딩 매개 변수를 사용하여 암호화된 열을 대상으로 하는 데이터를 전송합니다. 다음 예제에서는 암호화된 열(SSN)에서 리터럴/상수를 기준으로 잘못 필터링하는 쿼리를 보여 줍니다.
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

Always Encrypted는 클라이언트 쪽 암호화 기술이므로 데이터베이스가 아닌 클라이언트 쪽에서 대부분의 성능 오버헤드가 발생합니다. 암호화 및 암호 해독 작업의 비용 외에 클라이언트 쪽 성능 오버헤드의 원인은 다음과 같습니다.
 -   쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복
 -   열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복

연결에 대한 Always Encrypted가 설정된 경우 기본적으로 ODBC 드라이버는 각 매개 변수화된 쿼리에 대해 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)을 호출하고 매개 변수 값 없이 쿼리 문을 SQL Server에 전달합니다. 이 저장 프로시저는 쿼리 문을 분석하여 암호화해야 하는 매개 변수가 있는지 확인하고, 있을 경우 드라이버에서 매개 변수를 암호화할 수 있도록 각 매개 변수에 대한 암호화 관련 정보를 반환합니다.

PHP 드라이버를 사용하면 사용자가 SQL 형식을 제공하지 않고 준비된 문의 매개 변수를 바인딩할 수 있으므로 Always Encrypted가 사용 설정된 연결에서 매개 변수를 바인딩할 때 PHP 드라이버는 매개 변수에 대해 [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md)을 호출하여 SQL 형식, 열 크기 및 소수 자릿수를 가져옵니다. 그러면 메타데이터가 [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)를 호출하는 데 사용됩니다. `sys.sp_describe_parameter_encryption`를 호출할 때 ODBC 드라이버에서 클라이언트 쪽에 정보를 이미 저장했으므로 이러한 추가 `SQLDescribeParam` 호출에는 데이터베이스에 대한 추가 왕복이 필요하지 않습니다.

위의 동작은 클라이언트 애플리케이션에 대한 높은 수준의 투명성을 보장하며 암호화된 열을 대상으로 하는 값이 매개 변수로 드라이버에 전달되는 한 애플리케이션 개발자는 어떤 쿼리가 암호화된 열에 액세스하는지 유의하지 않아도 됩니다.

ODBC Driver for SQL Server와 달리, 문/쿼리 수준에서 Always Encrypted를 사용하도록 설정하는 것은 PHP 드라이버에서 아직 지원되지 않습니다. 

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

CEK(열 암호화 키)의 암호 해독을 위한 열 마스터 키 저장소 호출 수를 줄이기 위해 드라이버는 일반 텍스트 CEK를 메모리에 캐시합니다. 데이터베이스 메타데이터에서 ECEK(암호화된 CEK)를 받은 후 ODBC 드라이버는 먼저 캐시에 있는 암호화된 키 값에 해당하는 일반 텍스트 CEK를 찾으려고 합니다. 캐시에서 해당하는 일반 텍스트 CEK를 찾을 수 없는 경우에만 드라이버에서 CMK가 포함된 키 저장소를 호출합니다.

참고: ODBC Driver for SQL Server에서는 2시간 제한이 경과하면 캐시에서 항목이 제거됩니다. 즉, 드라이버는 지정된 ECEK에 대해 애플리케이션 수명이나 2시간마다 중 더 짧은 시간에 한 번만 키 저장소에 연결합니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업

데이터를 암호화하거나 암호를 해독하려면 드라이버가 대상 열에 대해 구성된 CEK를 가져와야 합니다. CEK는 데이터베이스 메타데이터에 암호화된 형태(ECEK)로 저장됩니다. 각 CEK를 암호화하는 데 사용된 해당 CMK가 있습니다. [데이터베이스 메타데이터](../../t-sql/statements/create-column-master-key-transact-sql.md)는 CMK 자체를 저장하는 것이 아니라 키 저장소의 이름 및 키 저장소에서 CMK를 찾는 데 사용할 수 있는 정보만 포함합니다.

ECEK의 일반 텍스트 값을 가져오기 위해 드라이버는 먼저 CEK와 해당 CMK에 대한 메타데이터를 가져온 다음, 이 정보를 사용하여 CMK가 포함된 키 저장소에 연결하고 ECEK의 암호를 해독하도록 요청합니다. 드라이버는 키 저장소 공급자를 사용하여 키 저장소와 통신합니다.

Microsoft Driver 5.3.0 for PHP for SQL Server의 경우 Windows 인증서 저장소 공급자 및 Azure Key Vault만 지원됩니다. ODBC 드라이버에서 지원하는 다른 키 저장소 공급자(사용자 지정 키 저장소 공급자)는 아직 지원되지 않습니다.

### <a name="using-the-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자 사용

Windows의 ODBC Driver for SQL Server에는 `MSSQL_CERTIFICATE_STORE`라는 Windows 인증서 저장소용 기본 제공 열 마스터 키 저장소 공급자가 포함되어 있습니다. macOS 또는 Linux에서는 이 공급자를 사용할 수 없습니다. 이 공급자를 사용하면 CMK가 클라이언트 머신에 로컬로 저장되며, 드라이버에서 CMK를 사용하는 데 필요한 애플리케이션의 추가 구성이 없습니다. 그러나 애플리케이션에서 인증서 및 저장소에 있는 해당 프라이빗 키에 액세스할 수 있어야 합니다. 자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

### <a name="using-azure-key-vault"></a>Azure Key Vault 사용

Azure Key Vault는 Azure를 사용하여 암호화 키, 암호 및 기타 암호를 저장하는 방법을 제공하며 Always Encrypted용 키를 저장하는 데 사용할 수 있습니다. ODBC Driver for SQL Server(버전 17 이상)에는 Azure Key Vault에 대한 기본 제공 마스터 키 저장소 공급자가 포함되어 있습니다. `KeyStoreAuthentication`, `KeyStorePrincipalId` 및 `KeyStoreSecret` 연결 옵션이 Azure Key Vault 구성을 처리합니다. 
 -   `KeyStoreAuthentication`은 두 개의 문자열 값 `KeyVaultPassword` 및 `KeyVaultClientSecret` 중 하나를 사용할 수 있습니다. 이러한 값은 다른 두 키워드에 사용되는 인증 자격 증명의 종류를 제어합니다.
 -   `KeyStorePrincipalId`는 Azure Key Vault에 액세스하려는 계정에 대한 식별자를 나타내는 문자열을 사용합니다. 
     -   `KeyStoreAuthentication`이 `KeyVaultPassword`로 설정된 경우 `KeyStorePrincipalId`는 Azure ActiveDirectory 사용자의 이름이어야 합니다.
     -   `KeyStoreAuthentication`이 `KeyVaultClientSecret`으로 설정된 경우 `KeyStorePrincipalId`는 애플리케이션 클라이언트 ID여야 합니다.
 -   `KeyStoreSecret`은 자격 증명 비밀을 나타내는 문자열을 사용합니다. 
     -   `KeyStoreAuthentication`이 `KeyVaultPassword`로 설정된 경우 `KeyStoreSecret`은 사용자의 암호여야 합니다. 
     -   `KeyStoreAuthentication`이 `KeyVaultClientSecret`으로 설정된 경우 `KeyStoreSecret`은 애플리케이션 클라이언트 ID와 연결된 애플리케이션 비밀이어야 합니다.

Azure Key Vault를 사용하려면 연결 문자열에 세 가지 옵션이 모두 있어야 합니다. 또한 `ColumnEncryption`이 `Enabled`로 설정되어야 합니다. `ColumnEncryption`을 `Disabled`로 설정했지만 Azure Key Vault 옵션이 있는 경우 스크립트는 오류 없이 계속되지만 암호화가 수행되지 않습니다.

다음 예제에서는 Azure Key Vault를 사용하여 SQL Server에 연결하는 방법을 보여 줍니다.

SQLSRV:

Azure Active Directory 계정 사용:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreSecret"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
Azure 애플리케이션 클라이언트 ID 및 암호 사용:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreSecret"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV: Azure Active Directory 계정 사용:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreSecret = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
Azure 애플리케이션 클라이언트 ID 및 암호 사용:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreSecret = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Always Encrypted를 사용할 때 PHP 드라이버의 제한 사항

SQLSRV 및 PDO_SQLSRV:
 -   Linux/macOS는 Windows 인증서 저장소 공급자를 지원하지 않습니다.
 -   매개 변수 강제 암호화
 -   문 수준에서 Always Encrypted 사용 
 -   Linux 및 macOS에서 Always Encrypted 기능 및 비 UTF8 로캘을 사용하는 경우(예: "en_US.ISO-8859-1"), 코드 페이지 1252가 시스템에 설치되지 않은 경우 null 데이터 또는 빈 문자열을 암호화된 char(n) 열에 삽입하지 못할 수 있습니다.
 
SQLSRV만 해당:
 -   SQL 형식을 지정하지 않고 바인딩 매개 변수에 `sqlsrv_query` 사용
 -   SQL 문 일괄 처리에서 매개 변수를 바인딩하는 데 `sqlsrv_prepare` 사용  
 
PDO_SQLSRV만 해당:
 -   매개 변수가 있는 쿼리에 지정된 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 문 특성
 -   매개 변수가 있는 쿼리에 지정된 `PDO::ATTR_EMULATE_PREPARE` 문 특성
 -   SQL 문 일괄 처리에서 매개 변수 바인딩
 
PHP 드라이버는 ODBC Driver for SQL Server 및 데이터베이스에서 적용하는 제한 사항도 상속합니다. [Always Encrypted를 사용하는 경우 ODBC 드라이버의 제한 사항](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 및 [Always Encrypted 기능 세부 정보](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
