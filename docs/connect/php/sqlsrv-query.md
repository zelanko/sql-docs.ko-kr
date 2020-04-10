---
title: sqlsrv_query | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab8c3912c33280738c8bebc012686490d7c55926
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928557"
---
# <a name="sqlsrv_query"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

문을 준비하고 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_query(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>매개 변수  
*$conn*: 준비된 문과 연결된 연결 리소스입니다.  
  
*$tsql*: 준비된 명령문에 해당하는 Transact-SQL 식입니다.  
  
*$params* [선택 사항]: 매개 변수가 있는 쿼리의 매개 변수에 해당하는 값의 **배열**입니다. 배열의 각 요소는 다음 중 하나일 수 있습니다.
  
-   리터럴 값입니다.  
  
-   PHP 변수입니다.  
  
-   다음 구조체를 가진 **배열** 입니다.  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    배열의 각 요소에 대한 설명이 다음 표에 나와 있습니다.  
  
    |요소|Description|  
    |-----------|---------------|  
    |*$value*|리터럴 값, PHP 변수 또는 PHP by-reference 변수입니다.|  
    |*$direction*[선택 사항]|매개 변수 방향을 나타내기 위해 사용되는 다음 **SQLSRV_PARAM_\*** 상수 중 하나입니다. **SQLSRV_PARAM_IN**, **SQLSRV_PARAM_OUT**, **SQLSRV_PARAM_INOUT**. 기본값은 **SQLSRV_PARAM_IN**입니다.<br /><br />PHP 상수에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요.|  
    |*$phpType*[선택 사항]|반환된 값의 PHP 데이터 형식을 지정하는 **SQLSRV_PHPTYPE_\*** 상수입니다.<br /><br />PHP 상수에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요.|  
    |*$sqlType*[선택 사항]|입력 값의 SQL Server 데이터 형식을 지정하는 **SQLSRV_SQLTYPE_\*** 상수입니다.<br /><br />PHP 상수에 대한 자세한 내용은 [상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요.|  
  
*$options* [선택 사항]: 쿼리 속성을 설정하는 결합형 배열입니다. [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md#properties)에서도 지원하는 동일한 키 목록입니다.
  
## <a name="return-value"></a>Return Value  
문 리소스입니다. 명령문을 만들 수 없거나 실행할 수 없는 경우 **false**가 반환됩니다.  
  
## <a name="remarks"></a>설명  
**sqlsrv_query** 함수는 일회성 쿼리에 적합하며 특수한 환경이 적용되지 않는 한 쿼리를 실행하는 기본 선택이어야 합니다. 이 함수는 최소한의 코드 작성으로 쿼리를 실행하기 위한 간소한 메서드를 제공합니다. **sqlsrv_query** 함수는 명령문 준비와 명령문 실행을 수행하므로 매개 변수가 있는 쿼리를 실행하는 데 사용할 수 있습니다.  
  
자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)을 참조하세요.  
  
## <a name="example"></a>예제  
다음 예제에서는 단일 행이 AdventureWorks 데이터베이스의 *Sales.SalesOrderDetail* 테이블에 삽입됩니다. 이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
> [!NOTE]  
> 다음 예제에서는 일회성 명령문 실행을 위해 INSERT 문을 사용하여 **sqlsrv_query**의 사용을 보여 주지만 이 개념은 모든 Transact-SQL 문에 적용됩니다.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if ($stmt) {  
    echo "Row successfully inserted.\n";  
} else {  
    echo "Row insertion failed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>예제  
다음 예제에서는 AdventureWorks 데이터베이스의 *Sales.SalesOrderDetail* 테이블에서 필드를 업데이트합니다. 이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = (?)   
         WHERE SalesOrderDetailID = (?)";  
  
/* Assign literal parameter values. */  
$params = array(5, 10);  
  
/* Execute the query. */  
if (sqlsrv_query($conn, $tsql, $params)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Error in statement execution.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> PHP에서는 [부동 소수점 숫자](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)의 정밀도가 제한되어 있으므로 [decimal 또는 numeric 열](https://php.net/manual/en/language.types.float.php)에 값을 바인딩할 때는 정밀도와 정확도를 보장하기 위해 문자열을 입력으로 사용하는 것이 좋습니다. bigint 열도 마찬가지이며, 값이 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) 범위를 벗어나는 경우 특히 그렇습니다.

## <a name="example"></a>예제  
이 코드 샘플에서는 10진수 값을 입력 매개 변수로 바인딩하는 방법을 보여 줍니다.  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
     echo "Could not connect.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="example"></a>예제
이 코드 샘플에서는 [sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) 형식의 테이블을 만들고 삽입된 데이터를 가져오는 방법을 보여 줍니다.

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$options = array("Database"=>$dbName, "UID"=>$uid, "PWD"=>$pwd);
$conn = sqlsrv_connect($server, $options);
if($conn === false) {
    die(print_r(sqlsrv_errors(), true));
}

$tableName = 'testTable';
$query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $query);

if(sqlsrv_fetch($stmt) === false) {
    die(print_r(sqlsrv_errors(), true));
}

$col1 = sqlsrv_get_field($stmt, 0);
echo "First field:  $col1 \n";

$col2 = sqlsrv_get_field($stmt, 1);
echo "Second field:  $col2 \n";

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```

예상 출력은 다음과 같습니다.

```
First field:  1
Second field:  test_data
```

## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[방법: 매개 변수가 있는 쿼리 수행](../../connect/php/how-to-perform-parameterized-queries.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  

[방법: 데이터를 스트림으로 전송](../../connect/php/how-to-send-data-as-a-stream.md)  

[방향 매개 변수 사용](../../connect/php/using-directional-parameters.md)  

  
