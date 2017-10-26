---
title: "방법: Multiple Active Resultsets (MARS) 사용 안 함 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 641b6ed54cf668aee1218b05fda1a5c3c792d409
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>방법: MARS(Multiple Active Resultsets)를 사용하지 않도록 설정
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

MARS(Multiple Active Result Sets)를 사용하지 않도록 설정된 SQL Server 데이터 원본에 연결해야 하는 경우 MultipleActiveResultSets 연결 옵션을 사용하여 MARS를 사용하거나 사용하지 않도록 설정할 수 있습니다.  
  
## <a name="procedure"></a>절차  
  
#### <a name="to-disable-mars-support"></a>MARS 지원을 사용하지 않도록 설정하려면  
  
-   다음 연결 옵션을 사용합니다.  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    응용 프로그램이 열려 있는 활성 결과 집합이 있는 연결에서 쿼리를 실행하려는 경우 두 번째 쿼리 시도는 다음과 같은 오류 정보를 반환합니다.  
  
    결과가 보류 중인 문이 있기 때문에 이 연결에서 이 작업을 처리할 수 없습니다.  다른 쿼리에 대해 연결을 사용할 수 있도록 모든 결과를 페치하거나 문을 취소 또는 해제합니다. MultipleActiveResultSets 연결 옵션에 대한 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
  
## <a name="example"></a>예제  
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
  
## <a name="example"></a>예제  
PDO_SQLSRV 드라이버를 사용 하 여 MARS 지원을 사용 하지 않도록 설정 하는 방법을 보여 주는 다음 예제는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
[서버에 연결](../../connect/php/connecting-to-the-server.md)  
  

