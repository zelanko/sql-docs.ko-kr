---
title: 'Pdo:: setattribute | Microsoft Docs'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66d64917b83e23739ad35e8629b028904a300060
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707691"
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
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|드라이버에서 오류를 보고 하는 방법을 지정 합니다.<br /><br />PDO::ERRMODE_SILENT(기본값)에서는 오류 코드 및 정보를 설정합니다.<br /><br />PDO::ERRMODE_WARNING은 E_WARNING을 발생시킵니다.<br /><br />PDO::ERRMODE_EXCEPTION은 예외를 발생시킵니다.<br /><br />PDO::setAttribute를 사용하면 이 특성을 설정할 수 있습니다.|  
|PDO::ATTR_ORACLE_NULLS|PDO|PDO 설명서를 참조하세요.|Null이 반환되는 방법을 지정합니다.<br /><br />PDO::NULL_NATURAL은 변환되지 않습니다.<br /><br />PDO::NULL_EMPTY_STRING은 빈 문자열을 null로 변환합니다.<br /><br />PDO::NULL_TO_STRING은 null을 빈 문자열로 변환합니다.|  
|PDO::ATTR_STATEMENT_CLASS|PDO|PDO 설명서를 참조하세요.|PDOStatement에서 파생된 사용자 제공 문 클래스를 설정합니다.<br /><br />`array(string classname, array(mixed constructor_args))`가 필요합니다.<br /><br />자세한 내용은 PDO 설명서를 참조하세요.|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|true 또는 false|데이터를 검색할 때 숫자 값을 문자열로 변환합니다.|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1부터 PHP 메모리 제한까지입니다.|클라이언트 쪽 커서를 사용할 때 결과 집합을 보유하는 버퍼의 크기를 설정합니다.<br /><br />기본값은 10240KB을 php.ini 파일에서 지정 하지 않으면.<br /><br />0과 음수는 허용되지 않습니다.<br /><br />클라이언트 쪽 커서를 만드는 쿼리에 대한 자세한 내용은 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|직접 또는 준비된 쿼리 실행을 지정합니다. 자세한 내용은 [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)(PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행)를 참조하세요.|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM.|드라이버에서 서버와 통신하는 데 사용되는 문자 집합 인코딩을 설정합니다.<br /><br />PDO::SQLSRV_ENCODING_BINARY는 지원되지 않습니다.<br /><br />기본값은 PDO::SQLSRV_ENCODING_UTF8입니다.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 또는 false|열에서 숫자 인출 (비트, 정수, smallint, tinyint, float 또는 real) 숫자 SQL 형식으로 처리합니다.<br /><br />연결 옵션 플래그 ATTR_STRINGIFY_FETCHES 켜져 있으면 반환 값은 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 켜져 있는 경우에 문자열입니다.<br /><br />바인딩할 열에 반환 되는 PDO 형식은 PDO_PARAM_INT 경우 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 꺼져 있는 경우에 정수 열에서 반환 값에는 int입니다.|  
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

[PDO](http://php.net/manual/book.pdo.php)  
  
