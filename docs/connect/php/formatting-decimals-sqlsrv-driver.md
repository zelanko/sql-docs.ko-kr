---
title: 10진수 문자열 및 금액 값 형식 지정(SQLSRV 드라이버) | Microsoft Docs
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
ms.openlocfilehash: 4a5ac641a98077c09bb38a5fc8fbd3fb1a4bf73d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68265140"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>10진수 문자열 및 금액 값 형식 지정(SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

정확도를 유지하기 위해 [decimal 또는 numeric 형식](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)은 항상 정확한 전체 자릿수 및 소수 자릿수가 포함된 문자열로 페치됩니다. 값이 1보다 작은 경우 선행 0이 없습니다. money 및 smallmoney 필드도 마찬가지입니다. 이들 필드는 고정 소수 자릿수가 4인 10진수 필드이기 때문입니다.

## <a name="add-leading-zeroes-if-missing"></a>누락된 경우 선행 0 추가
버전 5.6.0부터 사용자가 10진수 문자열의 서식을 지정할 수 있는 sqlsrv 연결 및 문 수준에 `FormatDecimals` 옵션이 추가됩니다. 이 옵션은 부울 값(true 또는 false)을 예상하며 페치된 결과에서 10진수 또는 숫자 값의 서식 지정에만 영향을 줍니다. 즉, `FormatDecimals` 옵션은 삽입 또는 업데이트와 같은 다른 작업에는 영향을 주지 않습니다.

기본적으로 `FormatDecimals`는 **false**입니다. true로 설정하면 1보다 작은 10진수 값에 대해 선행 0이 10진수 문자열에 추가됩니다.

## <a name="configure-number-of-decimal-places"></a>소수 자릿수 구성
`FormatDecimals`가 설정된 상태에서 다른 옵션인 `DecimalPlaces`를 사용하여 money 및 smallmoney 데이터를 표시할 때 소수 자릿수를 구성할 수 있습니다. 이 값은 [0, 4] 범위의 정수 값을 허용하고, 표시될 때 반올림이 발생할 수 있습니다. 그러나 기본 money 데이터는 동일하게 유지됩니다.

두 옵션 모두 연결 또는 문 수준으로 설정할 수 있으며, 문 설정은 항상 해당하는 연결 설정을 재정의합니다. `DecimalPlaces` 옵션은 **money 데이터**에만 영향을 미치며 `FormatDecimals`를 true로 설정해야 `DecimalPlaces`가 적용됩니다. 그렇지 않으면 `DecimalPlaces` 설정에 관계없이 서식이 해제됩니다.

> [!NOTE]
> money 또는 smallmoney 필드에는 소수 자릿수 4가 있기 때문에 `DecimalPlaces` 값을 음수로 설정하거나 4보다 큰 값을 설정하는 것은 무시됩니다. 서식 있는 money 데이터를 계산에 대한 입력으로 사용하지 않는 것이 좋습니다.

## <a name="example---a-simple-fetch"></a>예제 - 단순한 페치
다음 예제에서는 단순한 페치에서 새 옵션을 사용하는 방법을 보여 줍니다.

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>예제 - 출력 매개 변수 서식 지정
10진수 또는 숫자 필드가 [출력 매개 변수](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)로 반환되는 경우 반환되는 값은 일반 varchar 문자열로 간주됩니다. 그러나 SQLSRV_SQLTYPE_DECIMAL 또는 SQLSRV_SQLTYPE_NUMERIC이 지정된 경우에는 `FormatDecimals`를 true로 설정하여 숫자 문자열 값에 대해 선행 0이 누락되지 않도록 할 수 있습니다. 자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 출력 매개 변수 검색](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)을 참조하세요.

다음 예제에서는 decimal(8, 4) 값을 반환하는 저장 프로시저의 출력 매개 변수 서식을 지정하는 방법을 보여 줍니다.

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>참고 항목
[10진수 문자열 및 금액 값 형식 지정(PDO_SQLSRV 드라이버)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[데이터 검색](../../connect/php/retrieving-data.md)
