---
title: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29e36f2246556da7a43c3b8335f7a4e3479ae63c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686991"
---
# <a name="how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 기능은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 버전 1.1에서 추가되었으며 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에 대해 SQLSRV 드라이버를 사용할 때만 유효합니다. PDO_SQLSRV 드라이버에서 ReturnDatesAsStrings 연결 옵션을 사용하면 오류가 발생합니다.  
  
연결 문자열에서 옵션을 지정하여 날짜 및 시간 형식(**datetime**, **date**, **time**, **datetime2** 및 **datetimeoffset**)을 문자열로 검색할 수 있습니다.  
  
### <a name="to-retrieve-date-and-time-types-as-strings"></a>날짜 및 시간 형식을 문자열로 검색하려면  
  
-   다음 연결 옵션을 사용합니다.  
  
    ```  
    'ReturnDatesAsStrings'=>true  
    ```  
  
    기본값은 **false**이며 **datetime**, **Date**, **Time**, **DateTime2**및 **DateTimeOffset** 형식이 PHP **Datetime** 형식으로 반환됩니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 날짜 및 시간 형식을 문자열로 검색하기 위해 지정하는 구문을 보여 줍니다.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>예제  
다음 예제에서는 `"ReturnDatesAsStrings" => false`로 연결이 생성된 경우에도 문자열을 검색할 때 UTF-8을 지정하여 문자열로 날짜를 검색할 수 있음을 보여줍니다.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));  
  
if( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
echo $date;  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>예제  
다음 예제에서는 연결 문자열에서 UTF-8 및 `"ReturnDatesAsStrings" => true`를 지정하여 날짜를 문자열로 검색하는 방법을 보여줍니다.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8' );  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0 );  
  
if ( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
echo $date;  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>예제  
다음 예제에서는 날짜를 PHP 형식으로 검색하는 방법을 보여 줍니다. `'ReturnDatesAsStrings'=> false` 는 기본적으로 설정되어 있습니다.  
  
```  
<?php  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "SELECT VersionDate FROM AWBuildVersion";  
  
$stmt = sqlsrv_query( $conn, $tsql);  
  
if ( $stmt === false ) {  
   echo "Error in statement preparation/execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_fetch( $stmt );  
  
// retrieve date as string  
$date = sqlsrv_get_field( $stmt, 0 );  
  
if ( $date === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$date_string = date_format( $date, 'jS, F Y' );  
echo "Date = $date_string\n";  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[데이터 검색](../../connect/php/retrieving-data.md)  
  
