---
title: 10진수 문자열 및 금액 값 형식 지정(PDO_SQLSRV 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 76c314159faf15e63bf77b17a8a45abf217b205c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265147"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>10진수 문자열 및 금액 값 형식 지정(PDO_SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

정확도를 유지 하기 위해 [decimal 또는 numeric 형식은](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) 항상 정확한 전체 자릿수 및 배율이 포함 된 문자열로 인출 됩니다. 값이 1 보다 작은 경우 앞에 0이 없습니다. Money 및 smallmoney 필드는 고정 소수 자릿수가 4 인 10 진수 필드 이므로 동일 합니다.

## <a name="add-leading-zeroes-if-missing"></a>누락 된 경우 선행 0 추가
5\.6.0 버전부터 connection 또는 statement 특성 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 을 사용 하면 10 진수 문자열의 서식을 지정할 수 있습니다. 이 특성은 부울 값 (true 또는 false)을 예상 하며 인출 된 결과에서 decimal 또는 numeric 값의 형식에만 영향을 줍니다. 즉,이 특성은 삽입 또는 업데이트와 같은 다른 작업에는 영향을 주지 않습니다.

기본적으로 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`는 **false**입니다. True로 설정 하면 1 보다 작은 10 진수 값에 대해 선행 0에서 10 진수 문자열이 추가 됩니다.

## <a name="configure-number-of-decimal-places"></a>소수 자릿수 구성
가 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` on으로 설정 되 면 다른 연결 또는 문 `PDO::SQLSRV_ATTR_DECIMAL_PLACES`특성인를 사용 하 여 money 및 smallmoney 데이터를 표시할 때 소수 자릿수를 구성할 수 있습니다. 이 값은 [0, 4] 범위의 정수 값을 허용 하 고, 반올림은 표시 될 때 발생할 수 있습니다. 그러나 기본 money 데이터는 동일 하 게 유지 됩니다.

문 특성은 항상 해당 하는 연결 설정을 재정의 합니다. 옵션 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 은**money 데이터** 에만영향을주며true로설정해야합니다.`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 그렇지 않으면 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 설정에 관계 없이 형식이 해제 됩니다.

> [!NOTE]
> Money 또는 smallmoney 필드에는 소수 자릿수 4가 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 있기 때문에를 음수로 설정 하거나 4 보다 큰 값은 무시 됩니다. 형식이 지정 된 money 데이터를 계산에 대 한 입력으로 사용 하지 않는 것이 좋습니다.

### <a name="to-set-the-connection-attributes"></a>연결 특성을 설정 하려면

-   연결 지점에서 특성 설정:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   연결 게시 특성 설정:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>예제-money 데이터 형식 지정
다음 예제에서는 [PDOStatement:: bindColumn](../../connect/php/pdostatement-bindcolumn.md)을 사용 하 여 money 데이터를 인출 하는 방법을 보여 줍니다.

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>예-연결 특성 재정의
다음 예에서는 연결 특성을 재정의 하는 방법을 보여 줍니다.

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>참고 항목
[10진수 문자열 및 금액 값 형식 지정(SQLSRV 드라이버)](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[데이터 검색](../../connect/php/retrieving-data.md)
