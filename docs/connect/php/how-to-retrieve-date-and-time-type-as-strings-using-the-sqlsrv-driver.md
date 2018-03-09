---
title: "검색할 날짜 및 시간 형식을 문자열로 SQLSRV 드라이버를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43517dce78fe7303c1b4e687b4d3e786fc627a20
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 기능은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 버전 1.1에서 추가되었으며 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에 대해 SQLSRV 드라이버를 사용할 때만 유효합니다. PDO_SQLSRV 드라이버에서 ReturnDatesAsStrings 연결 옵션을 사용하면 오류가 발생합니다.  
  
날짜 및 시간 형식을 검색할 수 있습니다 (**datetime**, **날짜**, **시간**, **datetime2**, 및 **datetimeoffset**) 연결 문자열에서 옵션을 지정 하 여 문자열로 합니다.  
  
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
다음 예제에서는 연결 된 경우에 문자열을 검색할 때 u t F-8을 지정 하 여 문자열로 날짜를 검색할 수 있습니다 `"ReturnDatesAsStrings" => false`합니다.  
  
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
다음 예제에서는 u t F-8을 지정 하 여 문자열로 날짜를 검색 하는 방법을 보여 줍니다. 및 `"ReturnDatesAsStrings" => true` 연결 문자열에 있습니다.  
  
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
  
