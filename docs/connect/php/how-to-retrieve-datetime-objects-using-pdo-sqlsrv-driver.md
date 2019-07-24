---
title: '방법: PDO_SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 PHP DateTime 개체로 검색| Microsoft Docs'
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 165e91cee3b0b4592f9b746f8b35b46bc73bce50
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264575"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdosqlsrv-driver"></a>방법: PDO_SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 PHP DateTime 개체로 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

버전 5.6.0에 추가 된이 기능은 용 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]PDO_SQLSRV 드라이버를 사용 하는 경우에만 유효 합니다.

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>날짜 및 시간 형식을 DateTime 개체로 검색 하려면

PDO_SQLSRV를 사용 하는 경우 날짜 및 시간 형식 (**smalldatetime**, **datetime**, **date**, **time**, **datetime2**및 **datetimeoffset**)은 기본적으로 문자열로 반환 됩니다. PDO:: ATTR_STRINGIFY_FETCHES 및 PDO:: SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 특성은 아무런 영향도 미치지 않습니다. 날짜 및 시간 형식을 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 개체로 검색 하려면 연결 또는 문 특성 `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` 을 **true** 로 설정 합니다 (기본적으로 **false** 임).

> [!NOTE]
> 이 연결 또는 문 특성은 날짜 및 시간 형식에 대 한 일반 인출에만 적용 됩니다. DateTime 개체는 출력 매개 변수로 지정할 수 없기 때문입니다.

## <a name="example---use-the-connection-attribute"></a>예-연결 특성 사용
다음 예에서는 명확 하 게 하기 위해 오류 검사를 생략 합니다. 이 항목에서는 연결 특성을 설정 하는 방법을 보여 줍니다.

```php
<?php
$server = 'myserver';
$databaseName = 'mydatabase';
$username = 'myusername';
$passwd = 'mypasword';
$tableName = 'mytable';

$conn = new PDO("sqlsrv:Server = $server; Database = $databaseName", $username, $passwd);

// To set the connection attribute
$conn->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = $conn->prepare($query);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_ASSOC);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-attribute"></a>예-statement 특성 사용
이 예에서는 문 특성을 설정 하는 방법을 보여 줍니다.

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");
$query = "SELECT DateTimeCol FROM myTable";
$stmt = $conn->prepare($query);
$stmt->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_NUM);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-option"></a>예-문 옵션 사용
또는 문 특성을 옵션으로 설정할 수 있습니다.

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");

$dateObj = null;
$query = "SELECT DateTimeCol FROM aTable";
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => true);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateObj, PDO::PARAM_LOB);
$row = $stmt->fetch(PDO::FETCH_BOUND);
var_dump($dateObj);

unset($stmt);
unset($conn);
?>
```

## <a name="example---retrieve-datetime-types-as-strings"></a>예제-datetime 형식을 문자열로 검색
다음 예에서는 반대를 얻는 방법을 보여 줍니다 .이는 기본적으로 false 이므로 반드시 필요한 것은 아닙니다.

```php
<?php
$database = "MyData";
$conn = new PDO("sqlsrv:server = (local); Database = $database");

$dateStr = null;
$query = 'SELECT DateTimeCol FROM table1';
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateStr);
$row = $stmt->fetch(PDO::FETCH_BOUND);
echo $dateStr . PHP_EOL;

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>참고 항목
[데이터 검색](../../connect/php/retrieving-data.md)

[SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)