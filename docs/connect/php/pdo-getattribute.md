---
title: 'Pdo:: getattribute | Microsoft Docs'
ms.custom: 
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c81833ea-8b8a-459d-8f24-920098da994d
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56f361ca01d08db285ecd0f9d5afeae443935a92
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="pdogetattribute"></a>PDO::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

미리 정의된 PDO 또는 드라이버 특성의 값을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
mixed PDO::getAttribute ( $attribute )  
```  
  
#### <a name="parameters"></a>매개 변수  
*$attribute*: 지원되는 특성 중 하나입니다. 지원되는 특성의 목록에 대한 설명 섹션을 참조하세요.  
  
## <a name="return-value"></a>반환 값  
성공하면 연결 옵션, 미리 정의된 PDO 특성 또는 사용자 지정 드라이버 특성의 값을 반환하고, 실패하면 null을 반환합니다.  
  
## <a name="remarks"></a>주의  
다음 표에는 지원되는 특성 목록이 나와 있습니다.  
  
|Attribute|처리기|지원되는 값|Description|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|특정 사례에 열 이름이 있는지 여부를 지정합니다. PDO::CASE_LOWER는 열 이름을 소문자로 지정하고, PDO::CASE_NATURAL은 열 이름을 데이터베이스에서 반환된 대로 유지하며, PDO::CASE_UPPER는 열 이름을 대문자로 지정합니다.<br /><br />기본값은 PDO::CASE_NATURAL입니다.<br /><br />이 특성은 PDO::setAttribute를 사용하여 설정할 수도 있습니다.|  
|PDO::ATTR_CLIENT_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|문자열 배열|드라이버 및 관련 라이브러리의 버전을 설명합니다. 다음 요소로 배열을 반환 합니다: ODBC 버전 (*MajorVer*.* MinorVer*), [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Native Client DLL 이름과 버전, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 버전 (*MajorVer*.* MinorVer*.* BuildNumber*.* 수정 버전*)|  
|PDO::ATTR_DRIVER_NAME|PDO|문자열|항상 "sqlsrv"를 반환합니다.|  
|PDO::ATTR_DRIVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|문자열|나타냅니다는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 버전 (*MajorVer*.* MinorVer*.* BuildNumber*.* 수정 버전*)|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|드라이버에서 오류를 처리하는 방법을 지정합니다.<br /><br />PDO::ERRMODE_SILENT(기본값)에서는 오류 코드 및 정보를 설정합니다.<br /><br />PDO::ERRMODE_WARNING은 E_WARNING을 발생시킵니다.<br /><br />PDO::ERRMODE_EXCEPTION은 예외를 발생시킵니다.<br /><br />이 특성은 PDO::setAttribute를 사용하여 설정할 수도 있습니다.|  
|PDO::ATTR_ORACLE_NULLS|PDO|PDO 설명서를 참조하세요.|PDO 설명서를 참조하세요.|  
|PDO::ATTR_SERVER_INFO|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|3개 요소 배열|현재 데이터베이스, SQL Server 버전 및 SQL Server 인스턴스를 반환합니다.|  
|PDO::ATTR_SERVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|문자열|SQL Server 버전을 나타냅니다 (*주요*.* 사소한*.* BuildNumber*)|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|PDO 설명서를 참조하세요.|PDO 설명서를 참조하세요.|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1부터 PHP 메모리 제한까지입니다.|클라이언트 쪽 커서에 대한 결과 집합을 보유하는 버퍼의 크기를 구성합니다.<br /><br />기본값은 10, 240 기술 자료 (10MB).<br /><br />클라이언트 쪽 커서에 대 한 자세한 내용은 참조 [커서 유형 &#40; SQLSRV 드라이버 &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|직접 또는 준비된 쿼리 실행을 지정합니다. 자세한 내용은 [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)(PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행)를 참조하세요.|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM|드라이버에서 서버와 통신하는 데 사용되는 문자 집합 인코딩을 지정합니다.<br /><br />기본값은 PDO::SQLSRV_ENCODING_UTF8입니다.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 또는 false|(비트, 정수, smallint, tinyint, float 또는 real) 숫자 SQL 유형이 있는 열에서 숫자 인출을 처리합니다.<br /><br />연결 옵션 플래그 ATTR_STRINGIFY_FETCHES에 있으면 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE가 on으로 설정 하는 경우에 반환 값은 문자열입니다.<br /><br />바인딩할 열에 반환 되는 PDO 형식은 PDO_PARAM_INT 이면 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 꺼져 있는 경우에 정수 열에서 반환 값에는 int입니다.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|쿼리 시간 제한(초)을 설정합니다.<br /><br />기본값은 0이며, 드라이버가 결과를 무한정 기다린다는 것을 의미합니다.<br /><br />음수 값은 허용되지 않습니다.|  

  
PDO는 미리 정의된 몇 가지 특성을 처리하지만 다른 특성을 처리하려면 드라이버가 필요합니다. 모든 사용자 지정 특성 및 연결 옵션이 드라이버에 의해 처리 되며, 지원 되지 않는 특성 또는 연결 옵션 null을 반환 합니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 해당 값을 변경하기 전과 후의 PDO::ATTR_ERRMODE 특성 값을 보여 줍니다.  
  
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
  
// An example using PDO::ATTR_CLIENT_VERSION  
print_r($conn->getAttribute( PDO::ATTR_CLIENT_VERSION ));  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

