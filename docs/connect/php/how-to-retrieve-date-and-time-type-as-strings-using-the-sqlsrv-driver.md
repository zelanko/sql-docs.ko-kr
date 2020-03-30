---
title: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8c3fbd475d5f7038d36ba17a9578713c3ed1b53
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993535"
---
# <a name="how-to-retrieve-date-and-time-types-as-strings-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에 SQLSRV 드라이버를 사용하는 경우 연결 문자열 또는 문 수준에서 다음 옵션을 지정하여 날짜 및 시간 형식(**smalldatetime**, **datetime**, **date**, **time**, **datetime2** 및 **datetimeoffset**)을 문자열로 검색할 수 있습니다.

```
'ReturnDatesAsStrings'=>true
```

기본값은 **false**이며 **smalldatetime**, **datetime**, **date**, **time**, **datetime2** 및 **datetimeoffset** 형식이 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 개체로 반환됩니다. 문 수준에서 이 옵션이 설정되어 있는 경우 연결 수준 설정이 재정의됩니다.

기본적으로 PDO_SQLSRV 드라이버는 날짜 및 시간 형식을 문자열로 반환합니다. PHP DateTime 개체로 검색하려면 [방법: PDO_SQLSRV를 사용하여 날짜 및 시간 형식을 PHP Datetime 개체로 검색](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)을 참조하세요.

## <a name="example"></a>예제
다음 예제에서는 날짜 및 시간 형식을 문자열로 검색하기 위해 지정하는 구문을 보여 줍니다.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_close($conn);
?>
```

## <a name="example"></a>예제
다음 예제에서는 `"ReturnDatesAsStrings" => false`로 연결이 생성된 경우에도 문자열을 검색할 때 UTF-8을 지정하여 문자열로 날짜를 검색할 수 있음을 보여줍니다.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;

sqlsrv_close($conn);
?>
```

## <a name="example"></a>예제
다음 예제에서는 연결 문자열에서 UTF-8 및 `"ReturnDatesAsStrings" => true`를 지정하여 날짜를 문자열로 검색하는 방법을 보여줍니다.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8');
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;
sqlsrv_close($conn);
?>
```

## <a name="example"></a>예제
다음 예제에서는 날짜를 PHP 형식으로 검색하는 방법을 보여 줍니다. `'ReturnDatesAsStrings'=> false` 는 기본적으로 설정되어 있습니다.

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as a DateTime object, then convert to string using PHP's date_format function
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

$date_string = date_format($date, 'jS, F Y');
echo "Date = $date_string\n";

sqlsrv_close($conn);
?>
```

## <a name="example"></a>예제
문 수준의 ReturnDatesAsStrings 옵션은 해당하는 연결 옵션을 재정의합니다.

```php
<?php
$serverName = 'MyServer';
$connectionInfo = array('Database' => 'MyDatabase', 'ReturnDatesAsStrings' => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tableName = 'MyTable';
$options = array('ReturnDatesAsStrings' => true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}
sqlsrv_execute($stmt);

// Expect the fetched value to be a string
$field = sqlsrv_get_field($stmt, 0);
echo $field . PHP_EOL;

sqlsrv_close($conn);
?>
```

## <a name="see-also"></a>참고 항목
[데이터 검색](../../connect/php/retrieving-data.md)

[방법: PDO_SQLSRV를 사용하여 날짜 및 시간 형식을 PHP Datetime 개체로 검색](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)을 참조하세요.
