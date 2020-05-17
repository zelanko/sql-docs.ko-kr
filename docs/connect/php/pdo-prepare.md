---
title: PDO::prepare | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 902a1e986f79205dfd676c635ac54814382c2ec3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76941203"
---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

실행할 문을 준비합니다.

## <a name="syntax"></a>구문

```
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )
```

#### <a name="parameters"></a>매개 변수
$*statement*: SQL 문이 포함된 문자열입니다.

*key_pair*: 특성 이름 및 값이 포함된 배열입니다. 자세한 내용은 주의 섹션을 참조하십시오.

## <a name="return-value"></a>Return Value
성공하면 PDOStatement 개체를 반환합니다. 실패하면 `PDO::ATTR_ERRMODE` 값에 따라 PDOException 개체 또는 false를 반환합니다.

## <a name="remarks"></a>설명
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 실행 때까지 준비된 문을 평가하지 않습니다.

다음 표에서는 가능한 *key_pair* 값을 나열합니다.

|키|Description|
|-------|---------------|
|PDO::ATTR_CURSOR|커서 동작을 지정합니다. 기본값은 `PDO::CURSOR_FWDONLY`로, 스크롤할 수 없는 정방향 커서입니다. `PDO::CURSOR_SCROLL`은 스크롤 가능 커서입니다.<br /><br />`array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`)을 입력합니다.<br /><br />`PDO::CURSOR_SCROLL`로 설정하면, `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`을 사용하여 아래에 설명된 스크롤 가능 커서 형식을 설정할 수 있습니다.<br /><br />PDO_SQLSRV 드라이버의 결과 집합 및 커서에 대한 자세한 내용은 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.|
|PDO::ATTR_EMULATE_PREPARES|기본적으로 이 특성은 false이며, `PDO::ATTR_EMULATE_PREPARES => true`를 사용하여 변경할 수 있습니다. 자세한 내용과 예제는 [Emulate Prepare](#emulate-prepare)를 참조하세요.|
|PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE|스크롤 가능 커서 형식을 지정합니다. `PDO::ATTR_CURSOR`를 `PDO::CURSOR_SCROLL`로 설정한 경우에만 유효합니다. 이 특성에 사용할 수 있는 값은 아래를 참조하세요.|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|가져온 money 값의 서식을 지정할 때 사용할 소수 자릿수를 지정합니다. 이 옵션은 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`가 true인 경우에만 실행됩니다. 자세한 내용은 [10진수 문자열 및 Money 값 서식 지정(PDO_SQLSRV 드라이버)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)을 참조하세요.|
|PDO::SQLSRV_ATTR_DIRECT_QUERY|True이면 직접 쿼리 실행을 지정합니다. False는 준비된 문을 실행합니다. `PDO::SQLSRV_ATTR_DIRECT_QUERY`에 대한 자세한 내용은 [PDO_SQLSRV 드라이버의 직접 문 실행 및 준비된 문 실행](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)을 참조하세요.|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8(기본값)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|날짜 및 시간 형식을 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 개체로 검색할지를 지정합니다. 자세한 내용은 [방법: PDO_SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 PHP DateTime 개체로 검색](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)을 참조하세요.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|숫자 SQL 형식의 열에서 숫자 가져오기를 처리합니다. 자세한 내용은 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)을 참조하세요.|
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|해당하는 경우 10진수 문자열에 앞에 오는 0을 추가할지를 지정합니다. 이 옵션을 설정하면 money 형식의 서식 지정을 위한 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 옵션을 사용할 수 있습니다. 자세한 내용은 [10진수 문자열 및 Money 값 서식 지정(PDO_SQLSRV 드라이버)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)을 참조하세요.| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|자세한 내용은 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)을 참조하세요.|

`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`을 사용하는 경우 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`을 사용하여 커서 형식을 지정할 수 있습니다. 예를 들어 동적 커서를 설정하려면 PDO::prepare에 다음 배열을 전달합니다.
```
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));
```
다음 표에서는 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`에 사용할 수 있는 값을 보여 줍니다. 스크롤 가능 커서에 대한 자세한 내용은 [커서 형식 &#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)을 참조하세요.

|값|Description|
|---------|---------------|
|PDO::SQLSRV_CURSOR_BUFFERED|클라이언트 머신의 메모리에 결과 집합을 버퍼링하는 클라이언트 쪽(버퍼링됨) 정적 커서를 만듭니다.|
|PDO::SQLSRV_CURSOR_DYNAMIC|서버 쪽(버퍼되지 않음) 동적 커서를 만들고 이를 통해 순서에 관계없이 행에 액세스할 수 있으며 데이터베이스에 변경 내용이 반영됩니다.|
|PDO::SQLSRV_CURSOR_KEYSET|서버 쪽 키 집합 커서를 만듭니다. 행이 테이블에서 삭제되는 경우 키 집합 커서가 행 개수를 업데이트하지 않습니다(삭제된 행은 값 없이 반환됨).|
|PDO::SQLSRV_CURSOR_STATIC|서버 쪽 정적 커서를 만들고 이를 통해 순서에 관계없이 행에 액세스할 수 있지만 데이터베이스에 변경 내용은 반영되지 않습니다.<br /><br />`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`은 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC`을 의미합니다.|

`unset`을 호출하면 PDOStatement 개체를 닫을 수 있습니다.
```
unset($stmt);
```

## <a name="example"></a>예제
이 예제에서는 매개 변수 표식 및 정방향 전용 커서와 함께 PDO::prepare를 사용하는 방법을 보여 줍니다.

```
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$col1 = 'a';
$col2 = 'b';

$query = "insert into Table1(col1, col2) values(?, ?)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( $col1, $col2 ) );
print $stmt->rowCount();
echo "\n";

$query = "insert into Table1(col1, col2) values(:col1, :col2)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );
print $stmt->rowCount();

unset($stmt);
?>
```

## <a name="example"></a>예제
이 예제에서는 서버 쪽 정적 커서와 함께 PDO::prepare를 사용하는 방법을 보여 줍니다. 클라이언트 쪽 커서를 보여 주는 예제는 [커서 형식 &#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)을 참조하세요.

```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
$stmt->execute();

echo "\n";

while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){
   print "$row[Name]\n";
}
echo "\n..\n";

$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );
print "$row[Name]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );
print "$row[1]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );
print "$row[1]..\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );
print_r($row);
?>
```

## <a name="example"></a>예제
다음 두 코드 조각은 CHAR/VARCHAR 열을 대상으로 하는 데이터로 PDO::prepare를 사용하는 방법을 보여줍니다. PDO::prepare의 기본 인코딩은 UTF-8이므로 사용자는 `PDO::SQLSRV_ENCODING_SYSTEM` 옵션을 사용하여 암시적 전환을 방지할 수 있습니다.

**옵션 1**
```
$options = array(PDO::SQLSRV_ATTR_ENCODING => PDO::SQLSRV_ENCODING_SYSTEM);
$statement = $pdo->prepare(
  'SELECT *
   FROM myTable
   WHERE myVarcharColumn = :myVarcharValue',
  $options
);

$statement->bindValue(':myVarcharValue', 'my data', PDO::PARAM_STR);
```

**옵션 2**
```
$statement = $pdo->prepare(
  'SELECT *
   FROM myTable
   WHERE myVarcharColumn = :myVarcharValue'
);
$p = 'my data';
$statement->bindParam(':myVarcharValue', $p, PDO::PARAM_STR, 0, PDO::SQLSRV_ENCODING_SYSTEM);
```

<a name="emulate-prepare" />

## <a name="example"></a>예제

이 예제에서는 `PDO::ATTR_EMULATE_PREPARES`를 true로 설정하여 PDO::prepare를 사용하는 방법을 보여 줍니다.

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$database = "tempdb";
$conn = new PDO("sqlsrv:server = $serverName; Database = $database", $username, $password);

$pdo_options = array();
$pdo_options[PDO::ATTR_EMULATE_PREPARES] = true;
$pdo_options[PDO::SQLSRV_ATTR_ENCODING] = PDO::SQLSRV_ENCODING_UTF8;

$stmt = $conn->prepare("CREATE TABLE TEST([id] [int] IDENTITY(1,1) NOT NULL,
                                          [name] nvarchar(max))",
                                          $pdo_options);
$stmt->execute();

$prefix = '가각';
$name = '가각ácasa';
$name2 = '가각sample2';

$stmt = $conn->prepare("INSERT INTO TEST(name) VALUES(:p0)", $pdo_options);
$stmt->execute(['p0' => $name]);
unset($stmt);

$stmt = $conn->prepare("SELECT * FROM TEST WHERE NAME LIKE :p0", $pdo_options);
$stmt->execute(['p0' => "$prefix%"]);
foreach ($stmt as $row) {
    echo "\n" . 'FOUND: ' . $row['name'];
}

unset($stmt);
unset($conn);
?>
```

PDO_SQLSRV 드라이버는 내부적으로 모든 자리 표시자를 [PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md)으로 바인딩된 매개 변수로 바꿉니다. 따라서 자리 표시자가 없는 SQL 쿼리 문자열이 서버로 전송됩니다. 다음 예제를 살펴보세요.

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

`PDO::ATTR_EMULATE_PREPARES`가 false(기본값)로 설정된 경우 데이터베이스로 전송되는 데이터는 다음과 같습니다.

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

서버는 매개 변수가 있는 쿼리 기능을 매개 변수 바인딩에 사용하여 쿼리를 실행합니다. 반면, `PDO::ATTR_EMULATE_PREPARES`가 true로 설정된 경우 서버로 전송되는 쿼리는 기본적으로 다음과 같습니다.

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

`PDO::ATTR_EMULATE_PREPARES`를 true로 설정하면 SQL Server에서 몇 가지 제한 사항을 무시할 수 있습니다. 예를 들어 SQL Server는 일부 Transact-SQL 절에서 명명된 매개 변수 또는 위치 매개 변수를 지원하지 않습니다. 또한 SQL Server는 2100개 매개 변수만 바인딩할 수 있도록 제한됩니다.

> [!NOTE]
> emulate prepares를 true로 설정하면 매개 변수가 있는 쿼리의 보안이 적용되지 않습니다. 따라서 애플리케이션에서는 매개 변수에 바인딩되는 데이터에 악성 Transact-SQL 코드가 들어 있지 않은지 확인해야 합니다.

### <a name="encoding"></a>Encoding

사용자가 다른 인코딩(예: UTF-8 또는 이진)을 사용하여 매개 변수를 바인딩하려는 경우, PHP 스크립트에서 인코딩을 명확하게 지정해야 합니다.

PDO_SQLSRV 드라이버는 `PDO::bindParam()`에 지정된 인코딩(예: `$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`)을 먼저 확인합니다.

인코딩이 없으면, 드라이버는 `PDO::prepare()` 또는 `PDOStatement::setAttribute()`에 인코딩이 설정되어 있는지 확인합니다. 인코딩이 없으면, 드라이버는 `PDO::__construct()` 또는 `PDO::setAttribute()`에 지정된 인코딩을 사용합니다.

또한 버전 5.8.0부터는 true로 설정된 `PDO::ATTR_EMULATE_PREPARES`로 PDO::prepare를 사용할 때 사용자가 [PHP 7.2에 도입된 확장형 문자열 형식](https://wiki.php.net/rfc/extended-string-types-for-pdo)을 사용하여 `N` 접두사가 사용되도록 할 수 있습니다. 아래 코드 조각은 다양한 대안을 표시합니다.

> [!NOTE]
> 기본적으로 에뮬레이션 준비는 false로 설정되며 이 경우 확장형 PDO 문자열 제한은 무시됩니다.

**바인딩 시 드라이버 옵션 PDO::SQLSRV_ENCODING_UTF8 사용**

```
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true);
$stmt = $conn->prepare($sql, $options);
$stmt->bindParam(':value', $p, PDO::PARAM_STR, 0, PDO::SQLSRV_ENCODING_UTF8);
$stmt->execute();
```

**PDO::SQLSRV_ATTR_ENCODING 속성 사용**

```
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true, PDO::SQLSRV_ATTR_ENCODING => PDO::SQLSRV_ENCODING_UTF8);
$stmt = $conn->prepare($sql, $options);
$stmt->execute([':value' => $p]);
```

**PDO 상수 PDO::PARAM_STR_NATL 사용**
```
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true);
$stmt = $conn->prepare($sql, $options);
$stmt->bindParam(':value', $p, PDO::PARAM_STR | PDO::PARAM_STR_NATL);
$stmt->execute();
```

**기본 문자열 매개 변수 형식 PDO::PARAM_STR_NATL 설정**
```
$conn->setAttribute(PDO::ATTR_DEFAULT_STR_PARAM, PDO::PARAM_STR_NATL);
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true);
$stmt = $conn->prepare($sql, $options);
$stmt->execute([':value' => $p]);
```

### <a name="limitations"></a>제한 사항

바인딩은 드라이버에서 내부적으로 수행됩니다. 매개 변수 없이 유효한 쿼리가 서버로 전송되어 실행됩니다. 매개 변수가 있는 쿼리 기능을 사용하지 않으면, 일반적인 경우에 비해 몇 가지 제한 사항이 발생합니다.

- `PDO::PARAM_INPUT_OUTPUT`으로 바인딩된 매개 변수에 관해서는 실행되지 않습니다.
    - 사용자가 `PDO::PARAM_INPUT_OUTPUT`에 `PDO::bindParam()`을 지정하면 PDO 예외가 throw됩니다.
- 출력 매개 변수로 바인딩된 매개 변수에 관해서는 실행되지 않습니다.
    - 사용자가 출력 매개 변수용 자리 표시자(즉, `SELECT ? = COUNT(*) FROM Table1`과 같이 자리 표시자 바로 뒤에 등호가 있음)를 사용하여 준비된 문을 만들면 PDO 예외가 throw됩니다.
    - 준비된 문이 자리 표시자를 출력 매개 변수의 인수로 사용하여 저장 프로시저를 호출하는 경우에는 드라이버에서 출력 매개 변수를 감지할 수 없으므로 예외가 throw되지 않습니다. 그러나 사용자가 출력 매개 변수에 대해 제공한 변수가 변경되지 않고 그대로 유지됩니다.
- 이진 인코딩된 매개 변수에 대한 중복 자리 표시자는 실행되지 않습니다.

## <a name="see-also"></a>참고 항목
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)

