---
title: PDOStatement::bindParam
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDOStatement::bindParam 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65212058-2632-47a4-ba7d-2206883abf09
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6b8b1f838ce3351299e4069e80f692efb487df1
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646615"
---
# <a name="pdostatementbindparam"></a>PDOStatement::bindParam
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL 문의 명명된 표시 또는 물음표 자리 표시자에 매개 변수를 바인딩합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::bindParam($parameter, &$variable[, $data_type[, $length[, $driver_options]]]);  
```  
  
#### <a name="parameters"></a>매개 변수  
$*parameter*: (혼합) 매개 변수 식별자입니다. 명명된 자리 표시자를 사용하는 명령문의 경우 매개 변수 이름(:name)을 사용합니다. 물음표 구문을 사용하는 준비된 명령문의 경우 매개 변수의 1부터 시작하는 인덱스입니다.  
  
&$variable**: SQL 문 매개 변수에 바인딩할 PHP 변수의 (혼합) 이름입니다.  
  
$*data_type*: 선택적 (정수) PDO::PARAM_* 상수입니다. 기본값은 PDO::PARAM_STR입니다.  
  
$*length*: 데이터 형식의 선택적 (정수) 길이입니다. $*data_type*에서 PDO::PARAM_INT 또는 PDO::PARAM_BOOL을 사용할 때 기본 크기를 나타내기 위해 PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE를 지정할 수 있습니다.  
  
$*driver_options*: 선택적 (혼합) 드라이버 관련 옵션입니다. 예를 들어 PDO::SQLSRV_ENCODING_UTF8을 지정하여 UTF-8로 인코드된 문자열로 변수에 열을 바인딩할 수 있습니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 TRUE이고, 그렇지 않으면 FALSE입니다.  
  
## <a name="remarks"></a>설명  
varbinary, binary 또는 varbinary(max) 형식의 서버 열에 null 데이터를 바인딩할 때 $*driver_options*를 사용하여 이진 인코딩(PDO::SQLSRV_ENCODING_BINARY)을 지정해야 합니다. 인코딩 상수에 대한 자세한 내용은 [상수](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)를 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  

## <a name="example"></a>예제  
이 코드 샘플은 $contact가 매개 변수에 바인딩된 후 값을 변경하면 쿼리에 전달된 값을 변경한다는 것을 보여 줍니다.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindParam(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindParam(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```  
  
## <a name="example"></a>예제  
이 코드 샘플은 출력 매개 변수에 액세스하는 방법을 보여 줍니다.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$input1 = 'bb';  
  
$stmt = $conn->prepare("select ? = count(*) from Sys.tables");  
$stmt->bindParam(1, $input1, PDO::PARAM_STR, 10);  
$stmt->execute();  
echo $input1;  
?>  
```  
  
> [!NOTE]
> 출력 매개 변수를 bigint 형식에 바인딩할 때 값이 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)의 범위를 벗어나면 PDO::P ARAM_INT를 PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE와 함께 사용하는 경우 "값이 범위를 벗어남" 예외가 발생할 수 있습니다. 따라서 그 대신에 기본값인 PDO::PARAM_STR을 사용하고 결과 문자열의 크기(최대 21)를 제공합니다. 21은 음수 부호를 포함한 모든 bigint 값의 최대 자릿수입니다. 

## <a name="example"></a>예제  
이 코드 샘플은 입출력 매개 변수를 사용하는 방법을 보여 줍니다.  
  
```  
<?php  
   $database = "AdventureWorks";  
   $server = "(local)";  
   $dbh = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
   $dbh->query("IF OBJECT_ID('dbo.sp_ReverseString', 'P') IS NOT NULL DROP PROCEDURE dbo.sp_ReverseString");  
   $dbh->query("CREATE PROCEDURE dbo.sp_ReverseString @String as VARCHAR(2048) OUTPUT as SELECT @String = REVERSE(@String)");  
   $stmt = $dbh->prepare("EXEC dbo.sp_ReverseString ?");  
   $string = "123456789";  
   $stmt->bindParam(1, $string, PDO::PARAM_STR | PDO::PARAM_INPUT_OUTPUT, 2048);  
   $stmt->execute();  
   print $string;   // Expect 987654321  
?>  
```  

> [!NOTE]
> PHP에서는 [부동 소수점 숫자](https://php.net/manual/en/language.types.float.php)의 정밀도가 제한되어 있으므로 [decimal 또는 numeric 열](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)에 값을 바인딩할 때는 정밀도와 정확도를 보장하기 위해 문자열을 입력으로 사용하는 것이 좋습니다. bigint 열도 마찬가지이며, 값이 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) 범위를 벗어나는 경우 특히 그렇습니다.

## <a name="example"></a>예제  
이 코드 샘플에서는 10진수 값을 입력 매개 변수로 바인딩하는 방법을 보여 줍니다.  

```
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```


## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
