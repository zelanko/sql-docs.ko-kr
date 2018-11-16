---
title: PDOStatement::bindValue | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13bc4ece-420e-4887-8809-bf0705ddf126
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7ae069a5bb485f4b74a11b066f5871aba2f30ec
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606283"
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
  
## <a name="remarks"></a>Remarks  
  
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
> 값을 바인딩하는 경우 입력으로 문자열을 사용 하는 것이 좋습니다.는 [소수 또는 숫자 열](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) PHP에 대 한 전체 자릿수를 제한적으로 되도록 정밀도 정확도 [부동 소수점 숫자](https://php.net/manual/en/language.types.float.php)합니다. 값의 범위 밖에 있는 경우 특히 bigint 열에도 마찬가지는 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)합니다.

## <a name="example"></a>예제  
이 코드 샘플에는 입력된 매개 변수로 10 진수 값을 바인딩하는 방법을 보여 줍니다.  

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
  
