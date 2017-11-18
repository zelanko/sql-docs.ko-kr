---
title: "방법: SQL Server 인증을 사용 하 여 연결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8d4305d3b6dd25f3a06cda56db8e69fcd5d09972
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-connect-using-sql-server-authentication"></a>방법: SQL Server 인증을 사용하여 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

SQL Server에 연결할 때 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 가 SQL Server 인증을 지원합니다.  
  
Windows 인증이 불가능한 경우에만 SQL Server 인증을 사용해야 합니다. Windows 인증과 연결하는 방법에 대한 자세한 내용은 [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md)을 참조하세요.  
  
SQL Server 인증을 사용하여 SQL Server에 연결할 때 다음 사항을 고려해야 합니다.  
  
-   SQL Server 혼합 모드 인증이 서버에서 사용하도록 설정되어 있어야 합니다.  
  
-   사용자 ID와 암호 (*UID* 및 *PWD* SQLSRV 드라이버에서 연결 특성) 연결을 설정 하려고 할 때 설정 해야 합니다. 사용자 ID 및 암호가 유효한 SQL Server 사용자 및 암호에 매핑되어야 합니다.  
  
> [!NOTE]  
> 닫는 중괄호(})가 포함된 암호는 두 번째 닫는 중괄호로 이스케이프되어야 합니다. 예를 들어 SQL Server 암호가 "pass}word"인 경우 *PWD* 연결 특성의 값이 "pass}}word"로 설정되어야 합니다.  
  
SQL Server 인증을 사용하여 SQL Server에 연결할 때 다음 예방 조치를 수행해야 합니다.  
  
-   네트워크를 통해 웹 서버에서 데이터베이스로 전달된 자격 증명을 보호(암호화)합니다. 자격 증명은 SQL Server 2005부터 기본적으로 암호화됩니다. 추가 보안을 위해 서버에 전달된 모든 데이터를 암호화하기 위해 암호화 연결 특성을 "설정"으로 설정합니다.  
  
> [!NOTE]  
> 암호화 연결 특성을 "설정"으로 설정하면 데이터 암호화에서 계산이 많아질 수 있기 때문에 성능이 저하될 수 있습니다.  
  
-   PHP 스크립트에서 일반 텍스트로 연결 특성 *UID* 및 *PWD* 에 대한 값을 포함하지 마세요. 이러한 값은 적절하게 제한된 권한을 사용하여 응용 프로그램과 관련된 디렉터리에 저장되어야 합니다.  
  
-   *sa* 계정을 사용하지 마세요. 응용 프로그램을 원하는 권한을 가진 데이터베이스 사용자에게 매핑하고 강력한 암호를 사용합니다.  
  
> [!NOTE]  
> 연결을 설정할 때 사용자 ID 및 암호 외에 연결 특성을 설정할 수 있습니다. 지원되는 연결 특성의 전체 목록은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
  
## <a name="example"></a>예제  
다음 예제에서는 SQL Server 인증이 포함된 SQLSRV 드라이버를 사용하여 SQL Server의 로컬 인스턴스에 연결합니다. 필요한 값 *UID* 및 *PWD* 응용 프로그램별 텍스트 파일에서 연결 특성 가져옵니다 *uid.txt* 및 *pwd.txt*에 *C:\AppData* 디렉터리입니다. 연결이 설정된 후 사용자 로그인을 확인하기 위해 서버가 쿼리됩니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 브라우저에서 예제를 실행할 때 브라우저에 기록됩니다.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>예제  
이 샘플에서는 PDO_SQLSRV 드라이버를 사용하여 SQL Server 인증과 연결하는 방법을 보여 줍니다.  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
      $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
   }  
  
   catch( PDOException $e ) {  
      die( "Error connecting to SQL Server" );   
   }  
  
   echo "Connected to SQL Server\n";  
  
   $query = 'select * from Person.ContactType';   
   $stmt = $conn->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
      print_r( $row );   
   }  
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
[SUSER_SNAME (Transact SQL)](http://go.microsoft.com/fwlink/?LinkId=106382)  
[방법: SQL Server 로그인 만들기](http://go.microsoft.com/fwlink/?LinkId=106325)  
[방법: 데이터베이스 사용자 만들기](http://go.microsoft.com/fwlink/?LinkId=106327)  
[사용자, 역할 및 로그인 관리](http://go.microsoft.com/fwlink/?LinkId=106329)  
[사용자와 스키마 분리](http://go.microsoft.com/fwlink/?LinkId=106330)  
[Grant 개체 사용 권한 (Transact SQL)](http://go.microsoft.com/fwlink/?LinkId=106332)  
  

