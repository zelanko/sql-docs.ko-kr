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
manager: mbarwin
ms.openlocfilehash: 35626c192c3d74ad0201cee3c5e97adbce92a3aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669698"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>10진수 문자열 및 금액 값 형식 지정(PDO_SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

정확도 유지 하기 위해 [10 진수 또는 숫자 형식](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) 정확한 전체 자릿수 및 확장을 사용 하 여 문자열로 항상 페치됩니다. 모든 값이 1 보다 작은 경우 앞에 오는 0이 없습니다. 패턴은 4 같음 고정 소수 10 진수 필드는 그대로 money 및 smallmoney 필드와 같습니다.

## <a name="add-leading-zeroes-if-missing"></a>누락 된 경우 앞에 오는 0을 추가 합니다.
버전 5.6.0, 연결 또는 문 특성을 사용 하 여 시작 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 10 진수 문자열을 서식을 적용할 수 있습니다. 이 특성은 부울 값 (true 또는 false) 및 인출된 결과의 소수 또는 숫자 값의 서식 지정에 적용 합니다. 즉,이 특성에 삽입 또는 업데이트 등과 같은 다른 작업에 영향을 주지 않습니다.

기본적으로 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`는 **false**입니다. 이면 10 진수 문자열에 선행 0 true로 설정은 1 보다 작은 10 진수 값에 대 한 추가 됩니다.

## <a name="configure-number-of-decimal-places"></a>소수 자릿수를 구성 합니다.
사용 하 여 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 켜지 면 다른 연결 또는 명령문 특성 `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, money 및 smallmoney 데이터를 표시할 때 소수 자릿수의 수를 구성할 수 있습니다. 정수 값의 범위를 받아들이는지 [0, 4], 표시 될 때 반올림 발생할 수 있습니다. 그러나 기본 비용 데이터를 그대로 유지 됩니다.

문 특성에는 항상 해당 연결 설정을 재정의 합니다. 합니다 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 옵션 **만** money 데이터에 영향을 줍니다 및 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 설정 해야 true로 합니다. 그렇지 않은 경우 서식 지정 꺼져에 관계 없이 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 설정 합니다.

> [!NOTE]
> 비용 또는 smallmoney 필드 확장 4가 설정 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 임의의 음수 또는 4를 무시할지 보다 큰 값입니다. 하지 서식이 지정 된 비용 데이터 계산에 대 한 입력으로 사용 하는 것이 좋습니다.

### <a name="to-set-the-connection-attributes"></a>연결 속성을 설정 하려면

-   연결 지점에서 특성을 설정 합니다.

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Post 연결 특성을 설정 합니다.

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>예제-money 데이터 형식
다음 예제에서는 사용 하 여 비용 데이터를 인출 하는 방법을 보여 줍니다 [pdostatement:: Bindcolumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>예제-재정의 연결 특성
다음 예제에는 연결 특성을 재정의 하는 방법을 보여 줍니다.

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
