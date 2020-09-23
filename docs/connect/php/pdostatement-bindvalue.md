---
title: PDOStatement::bindValue
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDOStatement::bindValue 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13bc4ece-420e-4887-8809-bf0705ddf126
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebb895ac26aaff16ef4fb0d51a56243a9401e4d1
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645364"
---
# <a name="pdostatementbindvalue"></a>PDOStatement::bindValue
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL 문의 명명된 표시 또는 물음표 자리 표시자에 값을 바인딩합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::bindValue($parameter, $value[, $data_type]);  
```  
  
#### <a name="parameters"></a>매개 변수  
$*parameter*: (혼합) 매개 변수 식별자입니다. 명명된 자리 표시자를 사용하는 명령문의 경우 매개 변수 이름(:name)을 사용합니다. 물음표 구문을 사용하는 준비된 명령문의 경우 매개 변수의 1부터 시작하는 인덱스입니다.
  
$*value*: 매개 변수에 바인딩할 (혼합) 값입니다.  
  
$*data_type*: PDO::PARAM_* 상수로 표현되는 선택적(정수) 데이터 형식입니다. 기본값은 PDO::PARAM_STR입니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 TRUE이고, 그렇지 않으면 FALSE입니다.  
  
## <a name="remarks"></a>설명  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제는 $contact 값이 바인딩된 후 값을 변경하면 쿼리에 전달된 값을 변경한다는 것을 보여 줍니다.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindValue(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindValue(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```

> [!NOTE]
> PHP에서는 [부동 소수점 숫자](https://php.net/manual/en/language.types.float.php)의 정밀도가 제한되어 있으므로 [decimal 또는 numeric 열](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)에 값을 바인딩할 때는 정밀도와 정확도를 보장하기 위해 문자열을 입력으로 사용하는 것이 좋습니다. bigint 열도 마찬가지이며, 값이 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) 범위를 벗어나는 경우 특히 그렇습니다.

## <a name="example"></a>예제  
이 코드 샘플에서는 10진수 값을 입력 매개 변수로 바인딩하는 방법을 보여 줍니다.  

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
$stmt->bindValue(1, $input, PDO::PARAM_STR);
$stmt->execute();
```
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
