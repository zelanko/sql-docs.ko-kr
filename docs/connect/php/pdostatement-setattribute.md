---
title: PDOStatement::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46b6c9be6566b3b4857f58d779838356fe3b689e
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774980"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

미리 정의된 PDO 특성 또는 사용자 지정 드라이버 특성의 특성 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*attribute*: PDO::ATTR_* 또는 PDO::SQLSRV_ATTR_\* 상수 중 하나인 정수입니다. 사용 가능한 특성의 목록에 대한 설명 부분을 참조하세요.  
  
$*value*: 지정된 $*attribute*에 대해 설정할 (혼합) 값입니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 TRUE이고, 그렇지 않으면 FALSE입니다.  
  
## <a name="remarks"></a>Remarks  
다음 표에는 사용 가능한 특성 목록이 나와 있습니다.  
  
|attribute|값|설명|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1부터 PHP 메모리 제한까지입니다.|클라이언트 쪽 커서에 대한 결과 집합을 보유하는 버퍼의 크기를 구성합니다.<br /><br />기본값은 10240KB(10MB)입니다.<br /><br />클라이언트 쪽 커서에 대한 자세한 내용은 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|0과 4(포함) 사이의 정수|가져온 money 값의 서식을 지정할 때 사용할 소수 자릿수를 지정합니다.<br /><br />음의 정수 또는 4보다 큰 값은 무시됩니다.<br /><br />이 옵션은 PDO::SQLSRV_ATTR_FORMAT_DECIMALS가 true인 경우에만 실행됩니다.<br /><br />연결 수준에서 이 옵션을 설정할 수도 있습니다. 연결 수준에서 설정하면, 이 옵션이 연결 수준 옵션을 재정의합니다.<br /><br />자세한 내용은 [10진수 문자열 및 Money 값 서식 지정(PDO_SQLSRV 드라이버)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)을 참조하세요.|
|PDO::SQLSRV_ATTR_ENCODING|정수<br /><br />PDO::SQLSRV_ENCODING_UTF8(기본값)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|드라이버에서 서버와 통신하는 데 사용되는 문자 집합 인코딩을 설정합니다.|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true 또는 false|날짜 및 시간 형식을 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 개체로 검색할지를 지정합니다. false로 유지하면, 기본적으로 문자열로 반환됩니다.<br /><br />연결 수준에서 이 옵션을 설정할 수도 있습니다. 연결 수준에서 설정하면, 이 옵션이 연결 수준 옵션을 재정의합니다.<br /><br />자세한 내용은 [방법: PDO_SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 PHP DateTime 개체로 검색](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)을 참조하세요.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true 또는 false|숫자 SQL 형식(bit, integer, smallint, tinyint, float, real)의 열에서 숫자 가져오기를 처리합니다.<br /><br />연결 옵션 플래그 ATTR_STRINGIFY_FETCHES를 켜면, SQLSRV_ATTR_FETCHES_NUMERIC_TYPE이 켜져 있더라도 반환 값이 문자열입니다.<br /><br />바인딩 열에 반환된 PDO 형식이 PDO_PARAM_INT이면, SQLSRV_ATTR_FETCHES_NUMERIC_TYPE이 꺼져 있더라도 정수 열의 반환 값이 int입니다.|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true 또는 false|해당하는 경우 10진수 문자열에 앞에 오는 0을 추가할지를 지정합니다. 이 옵션을 설정하면 money 형식의 서식 지정을 위한 PDO::SQLSRV_ATTR_DECIMAL_PLACES 옵션을 사용할 수 있습니다. false로 유지하면, 1 미만의 값에서 앞에 오는 0을 생략하고 정확한 전체 자릿수를 반환하는 기본 동작이 사용됩니다.<br /><br />연결 수준에서 이 옵션을 설정할 수도 있습니다. 연결 수준에서 설정하면, 이 옵션이 연결 수준 옵션을 재정의합니다.<br /><br />자세한 내용은 [10진수 문자열 및 Money 값 서식 지정(PDO_SQLSRV 드라이버)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)을 참조하세요.| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|정수|쿼리 시간 제한(초)을 설정합니다.<br /><br />기본적으로 드라이버가 결과를 무한정 기다립니다. 음수 값은 허용되지 않습니다.<br /><br />0은 "시간 제한 없음"을 의미합니다.|  
  
## <a name="example"></a>예제  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
