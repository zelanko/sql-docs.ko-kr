---
title: 'Pdostatement:: Bindparam | Microsoft Docs'
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 65212058-2632-47a4-ba7d-2206883abf09
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 683ee4dcfd797f49ccd297f0a88f8fc607ea7aae
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308325"
---
# <a name="pdostatementbindparam"></a>PDOStatement::bindParam
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL 문의 명명된 표시 또는 물음표 자리 표시자에 매개 변수를 바인딩합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::bindParam($parameter, &$variable[, $data_type[, $length[, $driver_options]]]);  
```  
  
#### <a name="parameters"></a>매개 변수  
$*매개 변수*: (혼합된) 매개 변수 식별자입니다. 명명 된 자리 표시자를 사용 하 여 문을 사용 하 여 매개 변수 이름 (: name). 물음표 구문을 사용 하 여 준비 된 문의 경우이 매개 변수의 1부터 시작 인덱스입니다.  
  
&$*변수*: SQL 문 매개 변수에 바인딩할 PHP 변수의 (혼합된) 이름입니다.  
  
$*data_type*: 선택적 (정수) pdo:: PARAM_ * 상수입니다. 기본값은 PDO::PARAM_STR입니다.  
  
$*길이*: 데이터 형식에서 선택적 (정수) 길이입니다. $에서 Param_int 또는 PDO::PARAM_BOOL를 사용할 때 기본 크기를 나타내기 위해 PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE를 지정할 수 있습니다*data_type*합니다.  
  
$*driver_options*: 선택적 (혼합된) 드라이버 관련 옵션입니다. 예를 들어 PDO::SQLSRV_ENCODING_UTF8을 지정하여 UTF-8로 인코드된 문자열로 변수에 열을 바인딩할 수 있습니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 TRUE이고, 그렇지 않으면 FALSE입니다.  
  
## <a name="remarks"></a>Remarks  
이진 인코딩 (pdo:: SQLSRV_ENCODING_BINARY) $를 사용 하 여 지정 해야 형식 varbinary, binary 또는 varbinary (max)의 서버 열에 null 데이터를 바인딩할 때*driver_options*합니다. 인코딩 상수에 대 한 자세한 내용은 참조 [상수](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)합니다.  
  
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
> 값의 범위 밖에 있는 될 수 있습니다 하는 경우 출력 매개 변수는 bigint 형식에 바인딩할 때는 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), "값 범위를 벗어났습니다" 예외가 발생할 수 있습니다 PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE PARAM_INT 사용 합니다. 따라서 기본 pdo:: PARAM_STR를 대신 사용 하 고은 최대 21 결과 문자열의 크기를 제공 합니다. 숫자를 bigint 값의 음수 기호를 포함 하 여 최대 수입니다. 

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
> 값을 바인딩하는 경우 입력으로 문자열을 사용 하는 것이 좋습니다.는 [10 진수 또는 숫자 열](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) PHP 정밀도 대 한 제한 된 대로 정밀도 정확도 진행 하려면 [부동 소수점 숫자](http://php.net/manual/en/language.types.float.php)합니다. 마찬가지 bigint 열에 값의 범위 밖에 있는 경우 특히는 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)합니다.

## <a name="example"></a>예제  
이 코드 예제에는 10 진수 값을 입력된 매개 변수로 바인딩하는 방법을 보여 줍니다.  

```
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  

// Assume TestTable exists with a decimal field 
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```


## <a name="see-also"></a>관련 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
