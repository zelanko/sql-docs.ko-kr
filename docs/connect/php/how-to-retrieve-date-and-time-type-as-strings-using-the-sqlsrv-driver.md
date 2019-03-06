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
manager: craigg
ms.openlocfilehash: 4b83978f35dadff86e231b93b836c7ffdd1e0f08
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676051"
---
# <a name="how-to-retrieve-date-and-time-types-as-strings-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQLSRV 드라이버를 사용 하는 경우는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], 날짜 및 시간 형식을 검색할 수 있습니다 (**smalldatetime**, **datetime**를 **날짜**, **시간**하십시오 **datetime2**, 및 **datetimeoffset**) 연결 문자열 또는 문 수준에서 다음 옵션을 지정 하 여 문자열로:

```
'ReturnDatesAsStrings'=>true
```

기본값은 **false**이며 **smalldatetime**, **datetime**, **date**, **time**, **datetime2** 및 **datetimeoffset** 형식이 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 개체로 반환됩니다. 이 옵션을 문 수준에서 설정 하는 경우에 연결 수준 설정 보다 우선 합니다.

PDO_SQLSRV 드라이버 기본적으로 날짜 및 시간 형식 문자열로 반환합니다. PHP DateTime 개체로 검색, 참조 [방법: 검색 날짜 및 시간 형식을 PHP Datetime 개체를 사용 하 여 PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)

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
문 수준에서 ReturnDatesAsStrings 옵션에 해당 하는 연결 옵션을 재정의합니다.

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

[방법: PDO_SQLSRV를 사용하여 날짜 및 시간 형식을 PHP Datetime 개체로 검색](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)
