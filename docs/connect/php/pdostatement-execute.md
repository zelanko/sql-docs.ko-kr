---
title: PDOStatement::execute | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d6918a70217e7b98100bdc514edf65622e30b1a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909079"
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>매개 변수  
*$input*: (선택 사항) 매개 변수 표식에 대한 값이 포함된 결합형 배열입니다.  
  
## <a name="return-value"></a>Return Value  
성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>설명  
PDOStatement::execute와 함께 실행되는 문은 먼저 [PDO::prepare](../../connect/php/pdo-prepare.md)를 사용하여 준비해야 합니다. 직접 문 또는 준비된 문 실행을 지정하는 방법에 대한 자세한 내용은 [PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) 을 참조하세요.  
  
입력 매개 변수 배열의 모든 값은 PDO::PARAM_STR 값으로 처리됩니다.  
  
준비된 문에 매개 변수 표식이 있으면 PDOStatement::bindParam을 호출하여 PHP 변수를 매개 변수 표식에 바인딩하거나 입력 전용 매개 변수 값 배열을 전달해야 합니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
$stmt->execute();  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
  
echo "\n";  
$param = "Owner";  
$query = "select * from Person.ContactType where name = ?";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
?>  
```  
  
> [!NOTE]
> PHP에서는 [부동 소수점 숫자](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)의 정밀도가 제한되어 있으므로 [decimal 또는 numeric 열](https://php.net/manual/en/language.types.float.php)에 값을 바인딩할 때는 정밀도와 정확도를 보장하기 위해 문자열을 입력으로 사용하는 것이 좋습니다. bigint 열도 마찬가지이며, 값이 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) 범위를 벗어나는 경우 특히 그렇습니다.

## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
