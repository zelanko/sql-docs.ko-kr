---
title: '방법: MARS(Multiple Active Rresultsets)를 사용하지 않도록 설정'
description: Microsoft Drivers for PHP for SQL Server를 사용할 때 MARS(Multiple Active Resultsets) 지원을 사용하지 않도록 설정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11ca08618f0b8d7675e8ec74ec259d4225d44aba
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92080622"
---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>방법: MARS(Multiple Active Resultsets)를 사용하지 않도록 설정
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

MARS(Multiple Active Result Sets)를 사용하지 않도록 설정된 SQL Server 데이터 원본에 연결해야 하는 경우 MultipleActiveResultSets 연결 옵션을 사용하여 MARS를 사용하거나 사용하지 않도록 설정할 수 있습니다.  
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-disable-mars-support"></a>MARS 지원을 사용하지 않도록 설정하려면  
  
-   다음 연결 옵션을 사용합니다.  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    애플리케이션이 열려 있는 활성 결과 집합이 있는 연결에서 쿼리를 실행하려는 경우 두 번째 쿼리 시도는 다음과 같은 오류 정보를 반환합니다.  
  
    결과가 보류 중인 문이 있기 때문에 이 연결에서 이 작업을 처리할 수 없습니다.  다른 쿼리에 대해 연결을 사용할 수 있도록 모든 결과를 페치하거나 문을 취소 또는 해제합니다. MultipleActiveResultSets 연결 옵션에 대한 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
  
## <a name="sqlsrv-example"></a>SQLSRV 예제  
다음 예제에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 SQLSRV 드라이버를 사용하여 MARS 지원을 사용하지 않도록 설정하는 방법을 보여 줍니다.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="pdo_sqlsrv-example"></a>PDO_SQLSRV 예제  
다음 예제에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 PDO_SQLSRV 드라이버를 사용하여 MARS 지원을 사용하지 않도록 설정하는 방법을 보여 줍니다.  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[서버에 연결](../../connect/php/connecting-to-the-server.md)  
  
