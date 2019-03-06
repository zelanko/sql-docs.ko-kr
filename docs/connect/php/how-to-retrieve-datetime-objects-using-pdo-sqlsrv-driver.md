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
manager: mbarwin
ms.openlocfilehash: 54e5b5c9c1ba59ed64db740fbbb1a643e7cb1b2c
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676539"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdosqlsrv-driver"></a>방법: PDO_SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 PHP DateTime 개체로 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

버전 5.6.0에 추가 하는이 기능을 때만 유효 PDO_SQLSRV 드라이버를 사용 하 여 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]입니다.

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>날짜 및 시간 형식을 DateTime 개체로 검색 하려면

PDO_SQLSRV를 사용 하는 경우 날짜 및 시간 형식 (**smalldatetime**를 **datetime**에 **날짜**를 **시간**, **datetime2**, 및 **datetimeoffset**) 기본적으로 문자열로 반환 됩니다. PDO::ATTR_STRINGIFY_FETCHES 아니고 PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 특성에 아무 효과가 있습니다. 날짜 및 시간 형식으로 검색 하기 위해 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 문이나 연결 특성을 설정 하는 개체를 `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` 하 **true** (것 **false** 기본적으로).

> [!NOTE]
> 이 연결 또는 문 특성에만 적용 됩니다 일반 가져오기 날짜 및 시간 형식을 DateTime 개체를 출력 매개 변수로 지정할 수 없습니다.

## <a name="example---use-the-connection-attribute"></a>예제-연결 특성을 사용 하 여
다음 예제에서는 오류 명확성을 위해 검사를 생략 합니다. 이 항목에 연결 특성을 설정 하는 방법을 보여 줍니다.

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

## <a name="example---use-the-statement-attribute"></a>예제-문 특성을 사용 하 여
이 예제에서는 문 특성을 설정 하는 방법을 보여 줍니다.

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

## <a name="example---use-the-statement-option"></a>예제-문 옵션을 사용 하 여
또는 문 특성 옵션으로 설정할 수 있습니다.

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

## <a name="example---retrieve-datetime-types-as-strings"></a>예제-날짜/시간 형식 문자열로 검색
다음 예제에서는 (실제로 필요 없는 기본적으로 false 이므로)는 그 반대를 수행 하는 방법을 보여 줍니다.

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