---
title: 'Pdostatement:: Setattribute | Microsoft Docs'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19990702bee03a89fdf83aa35ae0a11d679f8c70
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

미리 정의된 PDO 특성 또는 사용자 지정 드라이버 특성의 특성 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*특성*::: ATTR_ * 또는 pdo:: SQLSRV_ATTR_ 중 하나는 정수\* 상수입니다. 사용 가능한 특성의 목록에 대한 설명 부분을 참조하세요.  
  
$*값*:에 지정 된 $ 설정할 (혼합된) 값*특성*합니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 TRUE이고, 그렇지 않으면 FALSE입니다.  
  
## <a name="remarks"></a>주의  
다음 표에는 사용 가능한 특성 목록이 나와 있습니다.  
  
|attribute|값|Description|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1부터 PHP 메모리 제한까지입니다.|클라이언트 쪽 커서에 대한 결과 집합을 보유하는 버퍼의 크기를 구성합니다.<br /><br />기본값은 10, 240 기술 자료 (10MB).<br /><br />클라이언트 쪽 커서에 대 한 자세한 내용은 참조 [커서 유형 &#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)합니다.|  
|PDO::SQLSRV_ATTR_ENCODING|정수<br /><br />PDO::SQLSRV_ENCODING_UTF8(기본값)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|드라이버에서 서버와 통신하는 데 사용되는 문자 집합 인코딩을 설정합니다.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true 또는 false|(비트, 정수, smallint, tinyint, float 또는 real) 숫자 SQL 유형이 있는 열에서 숫자 인출을 처리합니다.<br /><br />ATTR_STRINGIFY_FETCHES 연결 옵션 플래그를 설정 하면 반환 값은 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE에 있을 경우에 문자열입니다.<br /><br />바인딩할 열에 반환 되는 PDO 형식은 PDO_PARAM_INT 이면 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 꺼져 있는 경우에 정수 열에서 반환 값에는 int입니다.|  
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
  
## <a name="see-also"></a>관련 항목:  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
