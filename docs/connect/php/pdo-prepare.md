---
title: 'Pdo:: prepare | Microsoft Docs'
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 583ed80add549b5d90cff2aba24e25fb6e2050f9
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606403"
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
  
## <a name="return-value"></a>반환 값  
성공하면 PDOStatement 개체를 반환합니다. 실패하면 PDOException 개체를 반환하거나 PDO::ATTR_ERRMODE 값에 따라 false를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 실행 때까지 준비된 문을 평가하지 않습니다.  
  
다음 표에서는 가능한 *key_pair* 값을 나열합니다.  
  
|Key|설명|  
|-------|---------------|  
|PDO::ATTR_CURSOR|커서 동작을 지정합니다. 기본값은 PDO::CURSOR_FWDONLY입니다. PDO::CURSOR_SCROLL은 정적 커서입니다.<br /><br />`array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`)을 입력합니다.<br /><br />PDO::CURSOR_SCROLL을 사용하는 경우 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE을 사용할 수 있으며 아래 설명되어 있습니다.<br /><br />PDO_SQLSRV 드라이버의 결과 집합 및 커서에 대한 자세한 내용은 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.|  
|PDO::ATTR_EMULATE_PREPARES|기본적으로이 특성은 false,이 변경할 수 있는 `PDO::ATTR_EMULATE_PREPARES => true`합니다. 참조 [준비 에뮬레이트할](#emulate-prepare) 자세한 내용 및 예제에 대 한 합니다.|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8(기본값)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|True이면 직접 쿼리 실행을 지정합니다. False는 준비된 문을 실행합니다. PDO::SQLSRV_ATTR_DIRECT_QUERY에 대한 자세한 내용은 [PDO_SQLSRV 드라이버에서 직접 명령문 실행 및 준비된 명령문 실행](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)을 참조하세요.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|자세한 내용은 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)을 참조하세요.|  
  
PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL을 사용하는 경우 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE을 사용할 수 있습니다. 예:  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
다음 표는 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE에 대한 가능한 값을 보여 줍니다.  
  
|값|설명|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|클라이언트 쪽(버퍼됨) 정적 커서를 만듭니다. 클라이언트 쪽 커서에 대한 자세한 내용은 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.|  
|PDO::SQLSRV_CURSOR_DYNAMIC|서버 쪽(버퍼되지 않음) 동적 커서를 만들고 이를 통해 순서에 관계없이 행에 액세스할 수 있으며 데이터베이스에 변경 내용이 반영됩니다.|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|서버 쪽 키 집합 커서를 만듭니다. 행이 테이블에서 삭제되는 경우 키 집합 커서가 행 개수를 업데이트하지 않습니다(삭제된 행은 값 없이 반환됨).|  
|PDO::SQLSRV_CURSOR_STATIC|서버 쪽 정적 커서를 만들고 이를 통해 순서에 관계없이 행에 액세스할 수 있지만 데이터베이스에 변경 내용은 반영되지 않습니다.<br /><br />PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL은 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC을 암시합니다.|  
  
null로 설정하면 PDOStatement 개체를 닫을 수 있습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 매개 변수 표식 및 정방향 전용 커서를 사용하는 PDO::prepare 메서드를 사용하는 방법을 보여 줍니다.  
  
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
  
$stmt = null  
?>  
```  

## <a name="example"></a>예제  
이 예제에서는 클라이언트 쪽 커서를 사용하는 PDO::prepare 메서드를 사용하는 방법을 보여 줍니다. 서버 쪽 커서를 보여 주는 샘플은 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.  
  
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

<a name="emulate-prepare" />

## <a name="example"></a>예제 

Pdo:: prepare 메서드를 사용 하는 방법을 보여 주는이 예제 `PDO::ATTR_EMULATE_PREPARES` true로 설정 합니다. 

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

PDO_SQLSRV 드라이버에 의해 바인딩된 매개 변수를 사용 하 여 내부적으로 모든 자리 표시자를 바꿉니다 [PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md)합니다. 따라서 없습니다 자리 표시자를 사용 하 여 SQL 쿼리 문자열을 서버에 전송 됩니다. 이 예에서를 것이 좋습니다.

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

사용 하 여 `PDO::ATTR_EMULATE_PREPARES` 데이터베이스로 전송 되는 데이터는 false (기본값)로 설정 합니다.

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

서버 매개 변수를 바인딩하는 매개 변수가 있는 쿼리 기능을 사용 하 여 쿼리를 실행 하 고 있습니다. 사용 하 여 다른 한편으로 `PDO::ATTR_EMULATE_PREPARES` 를 true로 서버에 전송할 쿼리 집합은 기본적으로:

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

설정 `PDO::ATTR_EMULATE_PREPARES` 를 true로 SQL Server에서 몇 가지 제한 사항이 무시할 수 있습니다. 예를 들어, SQL Server는 몇 가지 TRANSACT-SQL 절에 명명 된 또는 위치 매개 변수를 지원 하지 않습니다. 또한 SQL Server의 한 제한은 바인딩 2100 매개 변수입니다.

> [!NOTE]
> True로 설정 준비 emulate 매개 변수가 있는 쿼리의 보안이 적용 되지 않습니다. 따라서 애플리케이션에서는 매개 변수에 바인딩되는 데이터에 악성 Transact-SQL 코드가 들어 있지 않은지 확인해야 합니다.

### <a name="encoding"></a>인코딩

사용자 (예를 들어, utf-8 또는 이진) 다른 인코딩 사용 하 여 매개 변수를 바인딩할 경우, 사용자는 PHP 스크립트에서 인코딩을 지정 명확 하 게 해야 합니다.

PDO_SQLSRV 드라이버에서 지정 된 인코딩은 먼저 확인 `PDO::bindParam()` (예를 들어 `$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`). 

찾을 수 없는 경우 드라이버 확인에 인코딩 설정 되어 있는지 `PDO::prepare()` 또는 `PDOStatement::setAttribute()`합니다. 그렇지 않으면 드라이버 사용에 지정 된 인코딩은 `PDO::__construct()` 또는 `PDO::setAttribute()`합니다.

### <a name="limitations"></a>제한 사항

알 수 있듯이 바인딩 드라이버에서 내부적으로 수행 됩니다. 유효한 쿼리를 매개 변수 없이 실행에 대 한 서버에 전송 됩니다. 몇 가지 제한 사항이 일반적인 경우에 비해, 매개 변수가 있는 쿼리 기능을 사용 하지 않는 경우 발생 합니다.

- 으로 바인딩되는 매개 변수에 대 한 작동 하지 않습니다 `PDO::PARAM_INPUT_OUTPUT`합니다.
    - 사용자가 지정 하는 경우 `PDO::PARAM_INPUT_OUTPUT` 에서 `PDO::bindParam()`, PDO 예외가 throw 됩니다.
- 출력 매개 변수로 바인딩되는 매개 변수는 작동 하지 않습니다.
    - 출력 매개 변수에 대 한 되며 사용자를 만들 때 준비 된 문을 자리 표시자를 포함 하는 (즉, 같은 자리 표시자 바로 뒤에 등호를가지고 있으므로, `SELECT ? = COUNT(*) FROM Table1`), PDO 예외가 throw 됩니다.
    - 준비 된 문을 자리 표시자를 사용 하 여 저장된 프로시저는 출력 매개 변수에 대 한 인수를 호출 하면 드라이버는 출력 매개 변수를 감지할 수 없으므로 예외가 throw 됩니다. 그러나 사용자가 제공 하는 출력 매개 변수에 대 한 변수는 그대로 유지 됩니다.
- 이진 인코딩된 매개 변수에 대 한 중복 된 자리 표시자 작동 하지 않습니다.

## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
