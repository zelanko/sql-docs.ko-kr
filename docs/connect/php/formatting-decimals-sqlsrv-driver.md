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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265140"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>10진수 문자열 및 금액 값 형식 지정(SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

정확도를 유지 하기 위해 [decimal 또는 numeric 형식은](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) 항상 정확한 전체 자릿수 및 배율이 포함 된 문자열로 인출 됩니다. 값이 1 보다 작은 경우 앞에 0이 없습니다. Money 및 smallmoney 필드는 고정 소수 자릿수가 4 인 10 진수 필드 이므로 동일 합니다.

## <a name="add-leading-zeroes-if-missing"></a>누락 된 경우 선행 0 추가
버전 5.6.0부터 옵션이 `FormatDecimals` sqlsrv 연결 및 문 수준에 추가 되어 사용자가 10 진수 문자열의 서식을 지정할 수 있습니다. 이 옵션은 부울 값 (true 또는 false)을 예상 하며 인출 된 결과에서 decimal 또는 numeric 값의 형식에만 영향을 줍니다. 즉, 옵션은 `FormatDecimals` 삽입 또는 업데이트와 같은 다른 작업에는 영향을 주지 않습니다.

기본적으로 `FormatDecimals`는 **false**입니다. True로 설정 하면 1 보다 작은 10 진수 값에 대해 선행 0에서 10 진수 문자열이 추가 됩니다.

## <a name="configure-number-of-decimal-places"></a>소수 자릿수 구성
가 `FormatDecimals` 설정 된 경우 다른 `DecimalPlaces`옵션인를 사용 하 여 money 및 smallmoney 데이터를 표시할 때 소수 자릿수를 구성할 수 있습니다. 이 값은 [0, 4] 범위의 정수 값을 허용 하 고, 반올림은 표시 될 때 발생할 수 있습니다. 그러나 기본 money 데이터는 동일 하 게 유지 됩니다.

두 옵션 모두 연결 또는 문 수준으로 설정할 수 있으며, 문 설정은 항상 해당 하는 연결 설정을 재정의 합니다. 옵션은 `DecimalPlaces` `DecimalPlaces` money데이터**에만**영향을주므로에대해true로설정해야`FormatDecimals` 합니다. 그렇지 않으면 `DecimalPlaces` 설정에 관계 없이 형식이 해제 됩니다.

> [!NOTE]
> Money 또는 smallmoney 필드에는 소수 자릿수 4가 `DecimalPlaces` 있으므로 값을 음수로 설정 하거나 4 보다 큰 값을 설정 하는 것은 무시 됩니다. 형식이 지정 된 money 데이터를 계산에 대 한 입력으로 사용 하지 않는 것이 좋습니다.

## <a name="example---a-simple-fetch"></a>예-간단한 인출
다음 예에서는 간단한 인출에서 새 옵션을 사용 하는 방법을 보여 줍니다.

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

## <a name="example---format-the-output-parameter"></a>예-output 매개 변수 형식 지정
Decimal 또는 numeric 필드가 [output 매개 변수로](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)반환 되는 경우 반환 되는 값은 일반 varchar 문자열로 간주 됩니다. 그러나 SQLSRV_SQLTYPE_DECIMAL 또는 SQLSRV_SQLTYPE_NUMERIC를 지정 하면 숫자 문자열 값에 대해 앞 `FormatDecimals` 에 오는 0이 없는 것을 확인 하기 위해을 true로 설정할 수 있습니다. 자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 출력 매개 변수 검색](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)을 참조하세요.

다음 예에서는 decimal (8, 4) 값을 반환 하는 저장 프로시저의 출력 매개 변수 형식을 지정 하는 방법을 보여 줍니다.

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
