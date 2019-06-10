---
title: PDO::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5402742793877d8e022eff4d207c49cf31f42256
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761803"
---
# <a name="pdosetattribute"></a>PDO::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

미리 정의된 PDO 특성 또는 사용자 지정 드라이버 특성을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```
bool PDO::setAttribute ( $attribute, $value );  
```  
  
#### <a name="parameters"></a>매개 변수  
*$attribute*: 설정할 특성입니다. 지원되는 특성의 목록은 설명 섹션을 참조하세요.  
  
*$value*: 값(혼합 형식)입니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>Remarks  
  
|attribute|처리기|지원되는 값|설명|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|열 이름의 대/소문자를 지정합니다.<br /><br />PDO::CASE_LOWER를 사용하면 열 이름이 소문자가 됩니다.<br /><br />PDO::CASE_NATURAL(기본값)은 데이터베이스에서 반환된 열 이름을 표시합니다.<br /><br />PDO::CASE_UPPER를 사용하면 열 이름이 대문자가 됩니다.<br /><br />PDO::setAttribute를 사용하면 이 특성을 설정할 수 있습니다.|  
|PDO::ATTR_DEFAULT_FETCH_MODE|PDO|PDO 설명서를 참조하세요.|PDO 설명서를 참조하세요.|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|드라이버에서 오류를 보고하는 방법을 지정합니다.<br /><br />PDO::ERRMODE_SILENT(기본값)에서는 오류 코드 및 정보를 설정합니다.<br /><br />PDO::ERRMODE_WARNING은 E_WARNING을 발생시킵니다.<br /><br />PDO::ERRMODE_EXCEPTION은 예외를 발생시킵니다.<br /><br />PDO::setAttribute를 사용하면 이 특성을 설정할 수 있습니다.|  
|PDO::ATTR_ORACLE_NULLS|PDO|PDO 설명서를 참조하세요.|Null이 반환되는 방법을 지정합니다.<br /><br />PDO::NULL_NATURAL은 변환되지 않습니다.<br /><br />PDO::NULL_EMPTY_STRING은 빈 문자열을 null로 변환합니다.<br /><br />PDO::NULL_TO_STRING은 null을 빈 문자열로 변환합니다.|  
|PDO::ATTR_STATEMENT_CLASS|PDO|PDO 설명서를 참조하세요.|PDOStatement에서 파생된 사용자 제공 문 클래스를 설정합니다.<br /><br />`array(string classname, array(mixed constructor_args))`가 필요합니다.<br /><br />자세한 내용은 PDO 설명서를 참조하세요.|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|true 또는 false|데이터를 검색할 때 숫자 값을 문자열로 변환합니다.|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1부터 PHP 메모리 제한까지입니다.|클라이언트 쪽 커서를 사용할 때 결과 집합을 보유하는 버퍼의 크기를 설정합니다.<br /><br />php.ini 파일에 지정하지 않으면, 기본값은 10240KB입니다.<br /><br />0과 음수는 허용되지 않습니다.<br /><br />클라이언트 쪽 커서를 만드는 쿼리에 대한 자세한 내용은 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|0과 4(포함) 사이의 정수|가져온 money 값의 서식을 지정할 때 사용할 소수 자릿수를 지정합니다.<br /><br />음의 정수 또는 4보다 큰 값은 무시됩니다.<br /><br />이 옵션은 PDO::SQLSRV_ATTR_FORMAT_DECIMALS가 true인 경우에만 실행됩니다.<br /><br />문 수준에서 이 옵션을 설정할 수도 있습니다. 문 수준에서 설정하면, 문 수준 옵션이 이 옵션을 재정의합니다.<br /><br />자세한 내용은 [10진수 문자열 및 Money 값 서식 지정(PDO_SQLSRV 드라이버)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)을 참조하세요.|
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 또는 false|직접 또는 준비된 쿼리 실행을 지정합니다. 자세한 내용은 [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)(PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행)를 참조하세요.|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM.|드라이버에서 서버와 통신하는 데 사용되는 문자 집합 인코딩을 설정합니다.<br /><br />PDO::SQLSRV_ENCODING_BINARY는 지원되지 않습니다.<br /><br />기본값은 PDO::SQLSRV_ENCODING_UTF8입니다.|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 또는 false|날짜 및 시간 형식을 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 개체로 검색할지를 지정합니다. false로 유지하면, 기본적으로 문자열로 반환됩니다.<br /><br />문 수준에서 이 옵션을 설정할 수도 있습니다. 문 수준에서 설정하면, 문 수준 옵션이 이 옵션을 재정의합니다.<br /><br />자세한 내용은 [방법: PDO_SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 PHP DateTime 개체로 검색](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)을 참조하세요.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 또는 false|숫자 SQL 형식(bit, integer, smallint, tinyint, float, real)의 열에서 숫자 가져오기를 처리합니다.<br /><br />연결 옵션 플래그 ATTR_STRINGIFY_FETCHES를 켜면, SQLSRV_ATTR_FETCHES_NUMERIC_TYPE이 켜져 있더라도 반환 값이 문자열입니다.<br /><br />바인딩 열에 반환된 PDO 형식이 PDO_PARAM_INT이면, SQLSRV_ATTR_FETCHES_NUMERIC_TYPE이 꺼져 있더라도 정수 열의 반환 값이 int입니다.|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 또는 false|해당하는 경우 10진수 문자열에 앞에 오는 0을 추가할지를 지정합니다. 이 옵션을 설정하면 money 형식의 서식 지정을 위한 PDO::SQLSRV_ATTR_DECIMAL_PLACES 옵션을 사용할 수 있습니다. false로 유지하면, 1 미만의 값에서 앞에 오는 0을 생략하고 정확한 전체 자릿수를 반환하는 기본 동작이 사용됩니다.<br /><br />문 수준에서 이 옵션을 설정할 수도 있습니다. 문 수준에서 설정하면, 문 수준 옵션이 이 옵션을 재정의합니다.<br /><br />자세한 내용은 [10진수 문자열 및 Money 값 서식 지정(PDO_SQLSRV 드라이버)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)을 참조하세요.| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|쿼리 시간 제한(초)을 설정합니다.<br /><br />기본값은 0이며, 드라이버가 결과를 무한정 기다린다는 것을 의미합니다.<br /><br />음수 값은 허용되지 않습니다.|  
  
PDO는 미리 정의된 몇 가지 특성을 처리하지만 다른 특성을 처리하려면 드라이버가 필요합니다. 모든 사용자 지정 특성 및 연결 옵션이 드라이버에 의해 처리됩니다. 지원되지 않는 특성, 연결 옵션 또는 지원되지 않는 값이 PDO::ATTR_ERRMODE의 설정에 따라 보고됩니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 샘플은 PDO::ATTR_ERRMODE 특성을 설정하는 방법을 보여 줍니다.  
  
```  
<?php  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
  
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
