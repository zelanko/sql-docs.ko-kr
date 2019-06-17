---
title: 'Pdostatement:: Bindcolumn | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: de72eb899274502e6a99e160e4911b5e4bf275b8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761957"
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

결과 집합의 열에 변수를 바인딩합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*column*: 결과 집합의 (혼합) 열 번호(인덱스 1부터 시작) 또는 열 이름입니다.  
  
&$*param*: 열이 바인딩될 (혼합) PHP 변수 이름입니다.  
  
$*type*: PDO::PARAM_* 상수로 표현된 매개 변수의 선택적 데이터 형식입니다.  
  
$*maxLen*: Microsoft Drivers for PHP for SQL Server에서 사용되지 않는 선택적 정수입니다.  
  
$*driverdata*: 드라이버의 선택적 혼합 매개 변수입니다. 예를 들어 PDO::SQLSRV_ENCODING_UTF8을 지정하여 UTF-8로 인코드된 문자열로 변수에 열을 바인딩할 수 있습니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 TRUE이고, 그렇지 않으면 FALSE입니다.  
  
## <a name="remarks"></a>Remarks  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 변수를 결과 집합의 열에 바인딩하는 방법을 보여 줍니다.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
