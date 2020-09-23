---
title: PDO::quote
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDO::quote 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9ddc48-42f8-4edf-aa8b-b0fc66706161
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cc39e175c46317428836af6562abc9af3d02dd9
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645564"
---
# <a name="pdoquote"></a>PDO::quote
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

기본 SQL Server 데이터베이스에 필요한 입력 문자열을 따옴표로 묶어 쿼리에서 사용할 문자열을 처리합니다. PDO::quote는 SQL Server에 적절한 따옴표 스타일을 사용하여 입력 문자열 내에서 특수 문자를 이스케이프합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
string PDO::quote( $string[, $parameter_type ] )  
```  
  
#### <a name="parameters"></a>매개 변수  
$*문자열*: 따옴표로 묶을 문자열입니다.  
  
$*parameter_type*: 데이터 형식을 나타내는 선택적 (정수) 기호입니다.  기본값은 PDO::PARAM_STR입니다.  

[유니코드 및 비유니코드 문자열 바인딩](https://wiki.php.net/rfc/extended-string-types-for-pdo)에 대한 지원을 추가하기 위해 새 PDO 상수를 PHP 7.2에 도입하였습니다. 유니코드 문자열은 N을 접두사로 하여 따옴표로 묶을 수 있습니다(예: ‘문자열’ 대신 N‘문자열’).

1. PDO::PARAM_STR_NATL - 유니코드 문자열의 새 형식으로서 PDO::PARAM_STR에 대한 비트 OR로 적용됩니다.
1. PDO::PARAM_STR_CHAR - 유니코드가 아닌 문자열의 새 형식으로서 PDO::PARAM_STR에 대한 비트 OR로 적용됩니다.
1. PDO::ATTR_DEFAULT_STR_PARAM - PDO::PARAM_STR_NATL 또는 PDO::PARAM_STR_CHAR로 설정하여 PDO::PARAM_STR에 대한 비트 OR로 값을 지정합니다.

5.8.0 버전부터 이러한 상수를 PDO::quote와 함께 사용할 수 있습니다.
  
## <a name="return-value"></a>반환 값  
SQL 문에 전달할 수 있는 따옴표로 묶은 문자열이고, 실패하면 false입니다.  
  
## <a name="remarks"></a>설명  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
  
```  
<?php  
$database = "test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = 'a \' g';  
$param2 = $conn->quote( $param );  
  
$query = "INSERT INTO Table1 VALUES( ?, '1' )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
$query = "INSERT INTO Table1 VALUES( ?, ? )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param, $param2));  
?>  
```  
  
## <a name="example"></a>예제  

다음 스크립트는 확장 문자열 형식이 PHP 7.2+를 사용하는 PDO::quote()에 미치는 영향에 관한 몇 가지 예를 보여 줍니다.

```
<?php
$database = "test";
$server = "(local)";
$db = new PDO("sqlsrv:server=$server; Database=$database", "", "");

$db->quote('über', PDO::PARAM_STR | PDO::PARAM_STR_NATL); // N'über'
$db->quote('foo'); // 'foo'

$db->setAttribute(PDO::ATTR_DEFAULT_STR_PARAM, PDO::PARAM_STR_NATL);
$db->quote('über'); // N'über'
$db->quote('foo', PDO::PARAM_STR | PDO::PARAM_STR_CHAR); // 'foo'
?>
```
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
