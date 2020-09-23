---
title: 10진수 문자열 및 금액 값 서식 지정(PDO_SQLSRV 드라이버)
description: PDO_SQLSRV 드라이버를 사용할 때 PDO::SQLSRV_ATTR_FORMAT_DECIMALS 및 SQLSRV_ATTR_DECIMAL_PLACES 특성을 사용하여 10진수 또는 금액 값의 서식을 지정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae61b239fca2a923645b9de963309c62a3919b3d
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680658"
---
# <a name="formatting-decimal-strings-and-money-values-pdo_sqlsrv-driver"></a>10진수 문자열 및 금액 값 형식 지정(PDO_SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

정확도를 유지하기 위해 [decimal 또는 numeric 형식](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)은 항상 정확한 전체 자릿수 및 소수 자릿수가 포함된 문자열로 페치됩니다. 값이 1보다 작은 경우 선행 0이 없습니다. money 및 smallmoney 필드도 마찬가지입니다. 이들 필드는 고정 소수 자릿수가 4인 10진수 필드이기 때문입니다.

## <a name="add-leading-zeroes-if-missing"></a>누락된 경우 선행 0 추가
버전 5.6.0부터 사용자가 연결 또는 문 특성 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`에서 10진수 문자열의 서식을 지정할 수 있습니다. 이 특성은 부울 값(true 또는 false)을 예상하며 페치된 결과에서 10진수 또는 숫자 값의 서식 지정에만 영향을 줍니다. 즉, 이 특성은 삽입 또는 업데이트와 같은 다른 작업에는 영향을 주지 않습니다.

기본적으로 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`는 **false**입니다. true로 설정하면 1보다 작은 10진수 값에 대해 선행 0이 10진수 문자열에 추가됩니다.

## <a name="configure-number-of-decimal-places"></a>소수 자릿수 구성
`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 설정된 경우 다른 연결 또는 문 특성 `PDO::SQLSRV_ATTR_DECIMAL_PLACES`를 사용하여 money 및 smallmoney 데이터를 표시할 때 소수 자릿수를 구성할 수 있습니다. 이 값은 [0, 4] 범위의 정수 값을 허용하고, 표시될 때 반올림이 발생할 수 있습니다. 그러나 기본 money 데이터는 동일하게 유지됩니다.

문 특성은 항상 해당하는 연결 설정을 재정의합니다. `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 옵션은 **money 데이터**에만 영향을 미치며 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`를 true로 설정해야 합니다. 그렇지 않으면 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 설정에 관계없이 서식이 해제됩니다.

> [!NOTE]
> money 또는 smallmoney 필드에는 소수 자릿수 4가 있기 때문에 `PDO::SQLSRV_ATTR_DECIMAL_PLACES`를 음수로 설정하거나 4보다 큰 값을 설정하는 것은 무시됩니다. 서식 있는 money 데이터를 계산에 대한 입력으로 사용하지 않는 것이 좋습니다.

### <a name="to-set-the-connection-attributes"></a>연결 특성을 설정하려면

-   연결 지점에서 특성 설정:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   연결 후 특성 설정:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>예제 - money 데이터 서식 지정
다음 예제에서는 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md)을 사용하여 money 데이터를 페치하는 방법을 보여 줍니다.

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

## <a name="example---override-connection-attributes"></a>예제 - 연결 특성 재정의
다음 예제에서는 연결 특성을 재정의하는 방법을 보여 줍니다.

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
