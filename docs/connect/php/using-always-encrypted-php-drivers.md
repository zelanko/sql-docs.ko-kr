---
title: SQL Server 용 PHP 드라이버와 함께 상시 암호화를 사용 하 여 | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: cc5ccc20d4a1a4324933ea64b9126f10df66dd26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>SQL Server 용 PHP 드라이버와 함께 상시 암호화 사용
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>에 적용할 수
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>소개

이 문서를 사용 하 여 PHP 응용 프로그램을 개발 하는 방법에 대해 설명 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 및 [SQL Server 용 PHP 드라이버](../../connect/php/Microsoft-php-driver-for-sql-server.md)합니다.

Always Encrypted를 사용하면 클라이언트 응용 프로그램이 중요한 데이터를 암호화하고 해당 데이터 또는 암호화 키를 SQL Server 또는 Azure SQL Database에 표시하지 않을 수 있습니다. 상시 암호화 지원 드라이버와 같은 SQL Server 용 ODBC 드라이버에서 투명 하 게 암호화 하 고 클라이언트 응용 프로그램의 중요 한 데이터를 해독 합니다. 이 드라이버는 중요 데이터베이스 열에 해당하는 쿼리 매개 변수를 자동으로 확인하고(Always Encrypted를 사용하여 보호) 데이터를 SQL Server 또는 Azure SQL Database로 전달하기 전에 이러한 매개 변수의 값을 암호화합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 [상시 암호화(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. SQL Server 용 PHP 드라이버는 ODBC Driver for SQL Server 중요 한 데이터 암호화를 사용 합니다.

## <a name="prerequisites"></a>필수 구성 요소

 -   데이터베이스에서 상시 암호화를 구성합니다. 이 구성에는 상시 암호화 키를 프로 비전 하 고 선택한 데이터베이스 열에 대 한 암호화를 설정 해야 합니다. 데이터베이스에 상시 암호화가 구성되지 않은 경우 [상시 암호화 시작](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)의 지침을 따르세요. 특히, 데이터베이스 열 마스터 키 (CMK), 열 암호화 키 (CEK), 및 해당 CEK를 사용 하 여 암호화 하는 하나 이상의 열을 포함 하는 테이블에 대 한 메타 데이터 정의 포함 해야 합니다.
 -   ODBC Driver for SQL Server 버전 17 이상인 개발 컴퓨터에 설치 되어 있는지 확인 합니다. 자세한 내용은 참조 [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)합니다.

## <a name="enabling-always-encrypted-in-a-php-application"></a>PHP 응용 프로그램에서 상시 암호화 설정

값을 설정 하 여 암호화 된 열 및 쿼리 결과의 암호 해독을 대상으로 하는 매개 변수를 암호화 하는 가장 쉬운 방법은는 `ColumnEncryption` 연결 문자열 키워드를 `Enabled`합니다. 다음은 SQLSRV 및 PDO_SQLSRV 드라이버에서 상시 암호화 사용의 예입니다.

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

암호화 또는 암호 해독을 위해; 하는 데 적합 하지 않은 상시 암호화 사용 또한 있는지 확인 해야 합니다.
 -   응용 프로그램에 데이터베이스에 상시 암호화 키에 대 한 메타 데이터에 액세스 하는 데 필요한 VIEW ANY COLUMN MASTER KEY DEFINITION 및 VIEW ANY COLUMN ENCRYPTION KEY DEFINITION 데이터베이스 권한이 있습니다. 자세한 내용은 참조 [데이터베이스 사용 권한](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)합니다.
 -   응용 프로그램에서 쿼리 된 암호화 된 열에 대 한 Cek를 보호 하는 CMK를 액세스할 수 있습니다. 이 요구 사항은 CMK를 저장 하는 키 저장소 공급자에 따라 달라 집니다. 자세한 내용은 참조 [열 마스터 키 저장소 작업](#working-with-column-master-key-stores)합니다.

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정

연결에서 항상 암호화를 사용 하면 표준 SQLSRV Api 사용할 수 있습니다 (참조 [SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)) 또는 PDO_SQLSRV Api (참조 [PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)) 데이터를 검색 또는 수정 암호화 된 데이터베이스 열에 있습니다. 응용 프로그램에 필요한 데이터베이스 권한이 하 고 열 마스터 키에 액세스할 수를 가정할 때 드라이버 암호화 암호화 된 열을 대상으로 투명 하 게 작동 하는 암호화 된 열에서 검색 된 데이터의 암호를 해독 하는 모든 쿼리 매개 변수는 열 암호화 되지 않은 경우 처럼 응용 프로그램입니다.

항상 암호화를 사용 하지 않는 경우 암호화 된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패 합니다. 쿼리에 암호화 된 열을 대상으로 하는 매개 변수 없이으로 암호화 된 열에서 데이터를 검색할 수 계속 합니다. 그러나 드라이버는 모든 암호 해독 하지 않으며 응용 프로그램 (바이트 배열)로 암호화 된 이진 데이터입니다.

다음 표에서 상시 암호화가 사용 여부에 따른 쿼리 동작을 요약:

| 쿼리 특성 | 항상 암호화가 설정 되 고 응용 프로그램 키와 키 메타 데이터에 액세스할 수 | 항상 암호화가 설정 되 고 응용 프로그램 키 또는 키 메타 데이터에 액세스할 수 없습니다 | 암호화 되지 않는지 항상 | | 암호화 된 열을 대상으로 하는 매개 변수입니다. | 매개 변수 값은 암호화 투명 하 게 됩니다. | 오류 | 오류 | | 에서 데이터를 검색할 암호화 된 열 없이 암호화 된 열을 대상으로 하는 매개 변수입니다. | 암호화 된 열의 결과가 투명 하 게 암호가 해독 됩니다. 응용 프로그램에는 일반 텍스트 열 값을 받습니다. | 오류 | 암호화 된 열의 결과가 암호 해독 되지 않습니다. 응용 프로그램으로 바이트 배열 암호화 된 값을 받습니다. |
 
다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 예제에서는 다음 스키마를 가진 테이블을 가정합니다. SSN 및 BirthDate 열은 암호화 됩니다.
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

다음 예에서는 환자 테이블에 행을 삽입 하려면 SQLSRV 및 PDO_SQLSRV 드라이버를 사용 하는 방법을 보여 줍니다. 다음 사항을 note:
 -   샘플 코드에는 암호화에 대한 내용이 없습니다. 드라이버는 자동으로 검색 하 고는 암호화 된 열을 대상 SSN 및 BirthDate 매개 변수의 값을 암호화 합니다. 이 메커니즘을 사용 하면 암호화 응용 프로그램입니다.
 -   데이터베이스 열을 포함 하는 암호화 된 열에 삽입 된 값은 바인딩된 매개 변수로 전달 됩니다. 동안 매개 변수를 사용 하 여는 (하지만 권장 SQL 주입 공격을 방지할 수 있으므로) 암호화 되지 않은 열에 값을 보낼 때 선택 사항, 암호화 된 열을 대상으로 하는 값에 필요 합니다. SSN 또는 BirthDate 열에 삽입 된 값이 쿼리 문에 포함 된 리터럴로 전달 된, 드라이버는 암호화 또는 쿼리에서 리터럴을 처리 하려고 시도 하지 않습니다 때문에 쿼리가 실패 합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.
 -   바인딩 매개 변수를 사용 하 여 값을 삽입할 때 대상 열의 데이터 형식을 동일 하거나 대상 열의 데이터 형식에 해당 변환을 사용할 수 있는 SQL 형식 데이터베이스에 전달 되어야 합니다. 이 요구 사항은 몇 가지 형식 변환을 원하는 상시 암호화 (세부 정보를 참조 하십시오. [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). 두 가지 PHP driver SQLSRV 및 PDO_SQLSRV, 각에 메뉴나 SQL 형식의 값을 결정 하는 메커니즘입니다. 따라서 사용자 SQL 형식을 명시적으로 제공 하지 않아도 됩니다.
  -   SQLSRV 드라이버에 대 한 사용자는 두 가지 옵션이 있습니다.
   -   확인 및 설정 적합 한 SQL 형식이 PHP driver에 의존 합니다. 이 경우 사용자 사용 해야 `sqlsrv_prepare` 및 `sqlsrv_execute` 매개 변수가 있는 쿼리를 실행 합니다.
   -   SQL 형식을 명시적으로 설정 합니다.
  -   PDO_SQLSRV 드라이버에 대 한 사용자 없는 SQL 형식의 매개 변수를 명시적으로 설정 하는 옵션입니다. 자동으로 PDO_SQLSRV 드라이버를 통해 사용자는 매개 변수를 바인딩할 때 SQL 형식을 결정 합니다.
 -   SQL 형식을 확인할 수는 드라이버의 경우 몇 가지 제한 사항이 적용 됩니다.
  -   SQLSRV 드라이버:
   -   사용자가 사용 해야만 사용자가 암호화 된 열에 대 한 SQL 유형을 결정 하는 드라이버, `sqlsrv_prepare` 및 `sqlsrv_execute`합니다.
   -   경우 `sqlsrv_query` 은 기본 설정에 사용자는 모든 매개 변수에 대 한 SQL 형식을 지정 하는 데 있습니다. 지정된 된 SQL 형식 문자열 형식에 대 한 문자열 길이 및 전체 자릿수 및 소수 형식에 포함 해야 합니다.
  -   PDO_SQLSRV 드라이버:
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

### <a name="plaintext-data-retrieval-example"></a>일반 텍스트 데이터 검색 예

다음 예에서는 암호화 된 값을 SQLSRV 및 PDO_SQLSRV 드라이버를 사용 하 여 암호화 된 열에서 일반 텍스트 데이터를 검색에 따라 데이터를 필터링을 보여 줍니다. 다음 사항을 note:
 -   전달할 바인딩 매개 변수를 사용 하 여 드라이버 암호화할 수 있도록 투명 하 게 해당 서버에 보내기 전에 필요한 SSN 열에서 필터링 할 WHERE 절에 사용 되는 값입니다.
 -   바인딩된 매개 변수를 사용 하 여 쿼리를 실행할 때 SQLSRV 드라이버를 사용 하는 경우 명시적으로 사용자 SQL 형식을 지정 하지 않은 경우 PHP 드라이버가 자동으로 사용자에 대 한 SQL 형식을 결정 합니다.
 -   프로그램에서 인쇄 하는 모든 값은 일반 텍스트로 되므로 드라이버 SSN 및 BirthDate 열에서 검색 된 데이터를 투명 하 게 해독입니다.
 
참고: 쿼리 같음 비교 암호화 된 열에 대해서만 실행할 수 암호화는 결정적입니다. 자세한 내용은 참조 [선택 하면 결정적 또는 임의 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)합니다.

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

### <a name="ciphertext-data-retrieval-example"></a>암호 텍스트 데이터 검색 예

상시 암호화를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예에서는 SQLSRV 및 PDO_SQLSRV 드라이버를 사용 하 여 암호화 된 열에서 암호화 된 이진 데이터를 검색 하는 방법을 보여 줍니다. 다음 사항을 note:
 -   연결 문자열에는 상시 암호화 사용 되지 않는 때 쿼리 (프로그램 값을 문자열로 변환) 하는 바이트 배열로 SSN 및 BirthDate의 암호화 된 값을 반환 합니다.
 -   암호화된 열을 대상으로 하는 매개 변수가 없으면 상시 암호화를 사용하지 않고 암호화된 열에서 데이터를 검색하는 쿼리에 매개 변수가 있을 수 있습니다. 데이터베이스에 암호화 되지 않은 lastname을 기준으로 다음 쿼리 필터를 지정 합니다. 쿼리가 SSN 또는 BirthDate 필터, 쿼리가 실패 합니다.
 
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

이 섹션에서는 PHP 응용 프로그램 및 방지 하는 방법에 대 한 몇 가지 지침에서 암호화 된 열을 쿼리할 때 일반적인 오류 범주를 설명 합니다.

#### <a name="unsupported-data-type-conversion-errors"></a>지원되지 않는 데이터 형식 변환 오류

상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 참조 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 자세한 목록은 지원 되는 형식 변환에 대 한 합니다. 데이터 형식 변환 오류를 방지하려면 다음을 수행합니다.
 -   사용 하 여 SQLSRV 드라이버를 사용 하는 경우 `sqlsrv_prepare` 및 `sqlsrv_execute` SQL 유형 열 크기 및 매개 변수의 소수 자릿수와 함께 자동으로 결정 됩니다.
 -   열 크기 및 매개 변수의 소수 자릿수를 사용 하 여 SQL 형식도 자동으로 결정 됩니다 PDO_SQLSRV 드라이버를 사용 하 여 쿼리를 실행를
 -   사용 하 여 SQLSRV 드라이버를 사용 하는 경우 `sqlsrv_query` 쿼리를 실행 합니다.
  -   매개 변수의 SQL 형식을 하거나 정확히 대상 열의 형식과 동일 되었거나 열 형식으로 변환 하는 SQL 형식에서 사용할 수 있습니다.
  -   전체 자릿수와 소수 자릿수의 열을 대상으로 하는 매개 변수는 `decimal` 및 `numeric` SQL Server 데이터 형식은 대상 열에 대해 구성 된 자릿수와 소수 자릿수와 같습니다.
  -   열을 대상으로 하는 매개 변수의 전체 자릿수 `datetime2`, `datetimeoffset`, 또는 `time` SQL Server 데이터 형식의 대상 열을 수정 하는 쿼리에서 대상 열에 대 한 전체 자릿수 보다 큽니다.
 -   PDO_SQLSRV 문 특성을 사용 하지 마십시오 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 또는 `PDO::ATTR_EMULATE_PREPARES` 에 매개 변수가 있는 쿼리
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화된 값 대신 일반 텍스트를 전달하여 발생하는 오류

암호화 된 열을 대상으로 하는 모든 값은 서버에 전송 되기 전에 암호화 해야 합니다. 삽입, 수정 또는 오류가 암호화 된 열에서 일반 텍스트 값으로 필터링 하려고 합니다. 이러한 오류를 방지 하려면 사항을 확인 합니다.
 -   암호화가 설정 되는 항상 (연결 문자열에 설정 된 `ColumnEncryption` 키워드를 `Enabled`).
 -   바인딩 매개 변수를 사용 하 여 암호화 된 열을 대상으로 하는 데이터를 보내려고 합니다. 다음 예제에서는 암호화 된 열 (SSN)에서 리터럴/상수를 기준으로 잘못 필터링 하는 쿼리를 보여 줍니다.
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

상시 암호화는 클라이언트 쪽 암호화 기술 이므로 데이터베이스에는 없는 클라이언트 쪽에서 대부분의 성능 오버 헤드가 발견 됩니다. 암호화 및 해독 작업의 비용 외에 클라이언트 쪽 성능 오버 헤드가 다른 원본 설정은:
 -   쿼리 매개 변수에 대 한 메타 데이터를 검색할 데이터베이스에 대 한 추가 왕복 작업
 -   열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대 한 메타 데이터를 검색 하는 왕복

상시 암호화를 연결에 사용 하는 경우 ODBC 드라이버는 기본적으로 호출 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) 각 매개 변수가 있는 쿼리에 대 한 모든 매개 변수 값) (없이 쿼리 문을 SQL Server에 전달 . 이 저장된 프로시저 매개 변수를 암호화 해야 하는 경우 그리고 있다면 확인 하려면 쿼리 문을 분석 하 여, 드라이버를 암호화할 수 있도록 각 매개 변수에 대해 암호화 관련 정보를 반환 합니다.

PHP 드라이버를 사용 하는 사용자는 매개 변수를 바인딩할 수 없으므로 SQL 제공 하지 않고 준비 된 문의 입력, 상시 암호화 지원 연결에서 매개 변수를 바인딩할 PHP 드라이버 호출 [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) 에 SQL 유형, 열 크기 및 소수 자릿수를 가져오는 매개 변수입니다. 메타 데이터는 다음 호출 하는 데 [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)합니다. 이러한 추가 `SQLDescribeParam` 호출 ODBC 드라이버는 이미에 저장 된 정보는 클라이언트 쪽 데이터베이스에 대 한 추가 라운드트립이 필요 하지 않습니다 때 `sys.sp_describe_parameter_encryption` 호출 되었습니다.

위의 동작 확인 높은 클라이언트 응용 프로그램 (및 응용 프로그램 개발자)에 대 한 투명도 수준을 암호화 된 열을 대상으로 하는 값에서 드라이버에 전달 됩니다으로 어떤 쿼리가 암호화 된 열 액세스 주의 해야 할 필요 하지 않습니다 매개 변수입니다.

ODBC Driver for SQL Server와는 달리 문/쿼리 수준에서 상시 암호화를 사용 아직 지원 되지 않습니다는 PHP 드라이버입니다. 

### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

열 암호화 키 (CEK) 암호를 해독 하는 열 마스터 키 저장소에 대 한 호출의 수를 줄이려면 드라이버 메모리에 일반 텍스트 Cek를 캐시 합니다. 데이터베이스 메타 데이터에서 암호화 된 CEK (ECEK)를 받은 후 ODBC 드라이버는 먼저 일반 텍스트 CEK에 해당 하는 캐시에 사용할 수 있는 암호화 된 키 값을 찾으려고 시도 합니다. 드라이버는 CMK를 캐시에 해당 일반 텍스트 CEK를 찾을 수 없는 경우에 포함 하는 키 저장소를 호출 합니다.

참고: SQL Server 용 ODBC 드라이버에서 캐시의 항목 2 시간, 시간 초과 이후 제거 됩니다. 이 동작은 드라이버 또는 2 시간 마다 응용 프로그램의 수명 동안 키 저장소를 한 번만 연결 주어진된 ECEK에 대 한 더 작은, 의미 합니다.

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업

데이터를 암호화 하거나 해독, 드라이버는 대상 열에 대해 구성 된 CEK를 가져올 해야 합니다. Cek는 데이터베이스 메타 데이터에 암호화 된 형식 (ECEKs)에 저장 됩니다. 각 CEK를 암호화 하기 위해 사용 된 해당 CMK에 있습니다. [데이터베이스 메타 데이터](../../t-sql/statements/create-column-master-key-transact-sql.md) 자체; CMK를 저장 하지 않는 키 저장소 CMK를 찾는 데 사용할 수 있는 정보와 키 저장소의 이름을 포함 합니다.

ECEK의 일반 텍스트 값을 가져오려면 드라이버 먼저 CEK 및 해당 해당 CMK를 둘 다에 대 한 메타 데이터를 가져오고이 정보를 사용 하 여 CMK를 포함 하는 키 저장소에 게 문의를 하 고는 ECEK 암호 해독 하도록 요청 합니다. 드라이버는 키 저장소 공급자를 사용 하 여 키 저장소와 통신 합니다.

Microsoft Driver 5.2.0 for PHP for SQL Server, Windows 인증서 저장소 공급자만 지원 됩니다. 두 명의 다른 키 저장소 공급자 (Azure 주요 자격 증명 모음 및 사용자 지정 키 저장소 공급자)는 ODBC 드라이버에서 지 원하는 아직 지원 되지 않습니다.

### <a name="using-the-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자를 사용 하 여

라는 Windows 인증서 저장소에 대 한 기본 제공 열 마스터 키 저장소 공급자를 포함 하는 Windows에서 SQL Server에 대 한 ODBC 드라이버 `MSSQL_CERTIFICATE_STORE`합니다. (이 공급자에서 사용할 수 없으면 macOS 또는 Linux.) 이 공급자와 클라이언트 컴퓨터에 CMK를 로컬로 저장 되며 응용 프로그램에서 추가 구성 없이 드라이버와 함께 사용할 필요가 있습니다. 그러나 응용 프로그램 저장소에 인증서와 해당 개인 키에 액세스할 수 있어야 합니다. 자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>PHP 드라이버 상시 암호화를 사용 하는 경우의 제한 사항

SQLSRV 및 PDO_SQLSRV:
 -   Linux/MacOS 지원
  -   Windows 인증서 저장소 공급자 및 즉 PHP 드라이버에서 현재 지 원하는 유일한 키 저장소 공급자에는 Linux/MacOS 지원 하지 않습니다.
 -   매개 변수 암호화를 강제 적용
 -   문 수준에서 상시 암호화 사용 
 
SQLSRV에만 해당:
 -   사용 하 여 `sqlsrv_query` SQL 형식을 지정 하지 않고 바인딩 매개 변수에 대 한
 -   사용 하 여 `sqlsrv_prepare` SQL 문의 일괄 처리에서 매개 변수 바인딩을 위한  
 
PDO_SQLSRV에만 해당:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` 매개 변수가 있는 쿼리에 지정 된 문 특성
 -   `PDO::ATTR_EMULATE_PREPARE` 매개 변수가 있는 쿼리에 지정 된 문 특성
 -   SQL 문의 일괄 처리에는 바인딩 매개 변수
 
PHP 드라이버에는 또한 SQL Server 및 데이터베이스에 대 한 ODBC 드라이버에 의해 적용 되는 제한을 상속 합니다. 참조 [상시 암호화를 사용 하는 경우 ODBC 드라이버의 제한 사항](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 및 [기능 정보 항상 암호화](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
