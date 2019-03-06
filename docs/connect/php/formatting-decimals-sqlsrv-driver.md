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
manager: mbarwin
ms.openlocfilehash: 76b6d27acedcfe2ec462a764559237a1a2218f78
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676544"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>10진수 문자열 및 금액 값 형식 지정(SQLSRV 드라이버)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

정확도 유지 하기 위해 [10 진수 또는 숫자 형식](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) 정확한 전체 자릿수 및 확장을 사용 하 여 문자열로 항상 페치됩니다. 모든 값이 1 보다 작은 경우 앞에 오는 0이 없습니다. 패턴은 4 같음 고정 소수 10 진수 필드는 그대로 money 및 smallmoney 필드와 같습니다.

## <a name="add-leading-zeroes-if-missing"></a>누락 된 경우 앞에 오는 0을 추가 합니다.
버전 5.6.0, 옵션부터 `FormatDecimals` 추가할 sqlsrv 연결 및 문 수준 10 진수 문자열을 서식을 적용할 수 있습니다. 이 옵션은 부울 값 (true 또는 false) 및 인출된 결과에서 소수 또는 숫자 값의 서식 지정에 적용 합니다. 즉,는 `FormatDecimals` 옵션은 삽입 또는 업데이트 등과 같은 다른 작업에 영향을 주지 않습니다.

기본적으로 `FormatDecimals`는 **false**입니다. 이면 10 진수 문자열에 선행 0 true로 설정은 1 보다 작은 10 진수 값에 대 한 추가 됩니다.

## <a name="configure-number-of-decimal-places"></a>소수 자릿수를 구성 합니다.
사용 하 여 `FormatDecimals` 켜지 면 또 다른 옵션 `DecimalPlaces`, money 및 smallmoney 데이터를 표시할 때 소수 자릿수의 수를 구성할 수 있습니다. 정수 값의 범위를 받아들이는지 [0, 4], 표시 될 때 반올림 발생할 수 있습니다. 그러나 기본 비용 데이터를 그대로 유지 됩니다.

두 옵션 모두 연결 또는 문 수준에서 설정할 수 있습니다 하 고 항상 설정 하는 문을 해당 연결 설정을 재정의 합니다. `DecimalPlaces` 옵션 **만** money 데이터에 영향을 줍니다 및 `FormatDecimals` 로 설정 되어야 합니다 마찬가지 `DecimalPlaces` 적용 합니다. 그렇지 않은 경우 서식 지정 꺼져에 관계 없이 `DecimalPlaces` 설정 합니다.

> [!NOTE]
> 비용 또는 smallmoney 필드 확장 4가 설정 `DecimalPlaces` 값을 임의의 음수 또는 4를 무시할지 보다 큰 값입니다. 하지 서식이 지정 된 비용 데이터 계산에 대 한 입력으로 사용 하는 것이 좋습니다.

## <a name="example---a-simple-fetch"></a>예제-간단한 페치
다음 예제에서는 간단한 인출에서 새 옵션을 사용 하는 방법을 보여 줍니다.

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

## <a name="example---format-the-output-parameter"></a>예제-출력 매개 변수 형식
10 진수 또는 숫자 필드를로 반환 되 면 합니다 [출력 매개 변수](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), 반환 된 값을 일반 varchar 문자열로 간주 됩니다. 그러나 SQLSRV_SQLTYPE_DECIMAL 또는 SQLSRV_SQLTYPE_NUMERIC 중 하나를 지정 하는 경우 설정할 수 있습니다 `FormatDecimals` 누락 앞에 0이 숫자 문자열 값이 true입니다. 자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 출력 매개 변수 검색](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)을 참조하세요.

다음 예제에서는 decimal(8,4) 값을 반환 하는 저장된 프로시저의 출력 매개 변수 형식을 지정 하는 방법을 보여 줍니다.

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
