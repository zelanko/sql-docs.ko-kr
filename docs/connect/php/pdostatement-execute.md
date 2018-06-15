---
title: 'Pdostatement:: Execute | Microsoft Docs'
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e3f2be02678d909ee722045e6139f6d34b55e3
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308442"
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>매개 변수  
*$input*: (선택 사항) 매개 변수 표식에 대 한 값을 포함 하는 결합형 배열입니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>Remarks  
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
> 값을 바인딩하는 경우 입력으로 문자열을 사용 하는 것이 좋습니다.는 [10 진수 또는 숫자 열](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) PHP 정밀도 대 한 제한 된 대로 정밀도 정확도 진행 하려면 [부동 소수점 숫자](http://php.net/manual/en/language.types.float.php)합니다. 마찬가지 bigint 열에 값의 범위 밖에 있는 경우 특히는 [정수](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)합니다.

## <a name="see-also"></a>관련 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
